# TÌM HIỂU VỀ KVM STORAGE
## CÁC ĐỊNH DẠNG Ổ ĐĨA TRONG KVM
### RAW
RAW là định dạng mặc định đơn giản nhất. Nó lưu trữ dữ liệu dưới dạng chuỗi bit thô, hoàn toàn không chứa cấu trúc metadata hay định dạng đặc biệt nào của trình ảo hóa.
- **Đặc điểm:**
    + Cấp phát tĩnh (Thick Provisioning): Nếu bạn tạo đĩa ảo 50GB, một tập tin 50GB sẽ được tạo ra lập tức trên đĩa thật của Host.
    + Cấu trúc tối giản: File RAW hiển thị đúng như một ổ đĩa vật lý thật trên hệ thống.

- **Ưu điểm:**
    + Hiệu năng cao nhất: Bỏ qua các bước xử lý metadata trung gian, tốc độ đọc/ghi (I/O) gần như tiệm cận 100% so với ổ đĩa vật lý thật.
    + Tính tương thích tuyệt đối: Có thể đọc và mở bằng bất kỳ phần mềm ảo hóa hay công cụ xử lý đĩa nào (VMware, VirtualBox, Hyper-V, KVM).
    + Dễ phục hồi dữ liệu: Nếu file đĩa bị hỏng, việc trích xuất lại dữ liệu thô dễ dàng hơn rất nhiều so với các định dạng đĩa phức tạp.

- **Nhược điểm:**
    + Lãng phí dung lượng: Chiếm toàn bộ dung lượng đã cấp phát ngay từ đầu, bất kể máy ảo có sử dụng hết hay không.
    + Thiếu tính năng nâng cao: Không hỗ trợ tạo Snapshot nội bộ (Internal Snapshot), không hỗ trợ nén (Compression) hay mã hóa (Encryption) trực tiếp trên file đĩa.

### QCOW2 (QEMU COPY-ON-WRITE v2)
QCOW2 là định dạng thế hệ thứ hai được phát triển riêng và tối ưu hóa hoàn toàn cho hệ sinh thái KVM / QEMU.

Đặc điểm:
Cấp phát linh hoạt (Thin Provisioning): Khi bạn tạo đĩa 50GB, file ban đầu chỉ chiếm vài Megabyte và sẽ tự động nới rộng dung lượng khi máy ảo ghi thêm dữ liệu.

Cơ chế Copy-On-Write (CoW): Cho phép tạo ra các đĩa ảo dựa trên một đĩa gốc (Base Image), chỉ lưu lại các dữ liệu thay đổi.

Ưu điểm:
Tiết kiệm không gian lưu trữ: Giúp tối ưu hóa dung lượng ổ đĩa vật lý của máy chủ.

Hỗ trợ Snapshot mạnh mẽ: Tạo, quản lý và khôi phục các điểm sao lưu (Snapshot) của máy ảo cực kỳ nhanh chóng.

Tích hợp sẵn Nén & Mã hóa: Hỗ trợ nén dữ liệu (zlib/zstd) và mã hóa cấp đĩa (AES) giúp tăng cường bảo mật.

Hỗ trợ Backing File: Dễ dàng nhân bản (Clone) hàng loạt máy ảo từ một file hệ điều hành mẫu chung (Golden Image).

Nhược điểm:
Hiệu năng I/O thấp hơn RAW: Do phải xử lý lớp metadata để tra cứu vị trí dữ liệu và tốn tài nguyên cấp phát đĩa động.

Nguy cơ phân mảnh dữ liệu (Fragmentation): Do file liên tục nở rộng và ghi ngắt quãng trên đĩa thật, dẫn đến việc đọc/ghi lâu ngày bị chậm đi.

## VMDK (VIRTUAL MACHINE DISK)
VMDK là định dạng chuẩn được phát triển bởi VMware, được KVM/QEMU hỗ trợ đọc/ghi thông qua công cụ qemu-img.

Đặc điểm:
Được thiết kế để chạy mượt mà trên hệ sinh thái VMware vSphere / ESXi / Workstation.

Hỗ trợ cả hai chế độ cấp phát: Cấp phát trước (Thick) hoặc Cấp phát động (Thin), cũng như chia nhỏ file đĩa thành các file 2GB.

Ưu điểm:
Tính linh hoạt cao: Dễ dàng di chuyển (Migrate) máy ảo qua lại giữa môi trường VMware và KVM.

Hỗ trợ đầy đủ các tính năng nâng cao khi chạy trong môi trường VMware gốc.

Nhược điểm:
Hiệu năng không tối ưu trên KVM: Khi chạy VMDK trên KVM, KVM phải chuyển đổi lệnh qua lớp giả lập của QEMU, làm suy giảm hiệu năng I/O.

Không tận dụng được trọn vẹn các tính năng quản lý snapshot hay clone mượt mà như QCOW2 trên KVM.

## VHD/VHDX (VIRTUAL HARD DISK)
VHD và thế hệ mới VHDX là định dạng đĩa ảo độc quyền do Microsoft phát triển dành cho Hyper-V và Windows Server.

Đặc điểm:
VHDX hỗ trợ dung lượng ổ đĩa lên tới 64TB và có khả năng chống hỏng dữ liệu khi mất điện ngột ngột nhờ cơ chế ghi Log.

Ưu điểm:
Dễ dàng chuyển đổi và di chuyển các máy ảo chạy từ Windows Hyper-V sang hệ thống KVM.

Nhược điểm:
KVM chỉ hỗ trợ VHD/VHDX ở mức cơ bản (phục vụ mục đích convert/migrate). Không nên dùng VHDX làm định dạng chạy chính thức lâu dài trên KVM.

## SO SÁNH RAW VÀ QCOW2
| Tiêu chí                   | RAW                                                                                                                              | QCOW2                                                                                                                                     |   |   |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|---|---|
| Bản chất                   | File đĩa thô, lưu dữ liệu trực tiếp dưới dạng chuỗi bit không qua xử lý cấu trúc.                                                | File đĩa thông minh của QEMU, lưu dữ liệu theo cấu trúc bảng và quản lý metadata.                                                         |   |   |
| Cấp phát dung lượng        | Thick Provisioning: Chiếm đúng dung lượng đã khai báo trên ổ thật ngay khi khởi tạo (Ví dụ: tạo đĩa 30GB -> file chiếm đủ 30GB). | Thin Provisioning: Tự nở rộng dung lượng thực tế theo lượng dữ liệu máy ảo ghi vào (Ví dụ: tạo đĩa 30GB -> file ban đầu chỉ nặng vài MB). |   |   |
| Hiệu năng Đọc/Ghi (I/O)    | Cao nhất (Gần 100% so với máy thật): Không tốn chi phí xử lý metadata hay cấp phát block mới.                                    | Khá - Tốt (~90-95%): Thấp hơn RAW một chút do overhead quản lý metadata và việc mở rộng file ngắt quãng.                                  |   |   |
| Tính năng Snapshot         | Không hỗ trợ tính năng tạo Snapshot nội bộ (Internal Snapshot).                                                                  | Hỗ trợ rất mạnh: Cho phép tạo, quản lý và khôi phục Snapshot cực kỳ nhanh chóng.                                                          |   |   |
| Nén & Mã hóa               | Không hỗ trợ nén hoặc mã hóa trực tiếp trên file đĩa.                                                                            | Có hỗ trợ: Tích hợp nén dữ liệu (zlib/zstd) và mã hóa cấp đĩa (AES).                                                                      |   |   |
| Tính năng Nhân bản (Clone) | Tốn thời gian do phải copy toàn bộ khối đĩa dung lượng thực.                                                                     | Rất nhanh: Hỗ trợ tính năng CoW (Copy-On-Write) để tạo đĩa con (Linked Clone) từ đĩa gốc.                                                 |   |   |
| Tương thích & Phục hồi     | Rất cao: Dễ dàng đọc/mở trên mọi phần mềm ảo hóa khác; dễ phục hồi dữ liệu khi đĩa lỗi.                                          | Chuyên biệt: Tối ưu cho KVM/QEMU; nếu bị hỏng file metadata sẽ khó phục hồi hơn RAW.                                                      |   |   |
| Trường hợp sử dụng         | Các máy chủ Database lớn (MySQL, PostgreSQL, Oracle), hệ thống High-I/O không cần Snapshot.                                      | Mặc định cho hầu hết máy ảo: Web Server, App Server, Lab/Testing, môi trường Cloud.                                                       |   |   |

## CÁCH CHUYỂN ĐỔI TỪ ĐỊNH DẠNG RAW -> QCOW2 VÀ NGƯỢC LẠI
Để chuyển đổi qua lại giữa hai định dạng này, KVM cung cấp công cụ qemu-img.
*Lưu ý quan trọng: Phải tắt máy ảo hoàn toàn trước khi tiến hành chuyển đổi để tránh hỏng dữ liệu (data corruption).*

### RAW -> QCOW2
- Để tiết kiệm dung lượng lưu trữ trên Host và sử dụng tính năng Snapshot, sử dụng câu lệnh:
``` bash
qemu-img convert -f raw -O qcow2 /duong/dan/disk.raw /duong/dan/disk.qcow2
```
- Bổ sung tính năng Nén dữ liệu khi chuyển đổi (file .qcow2 thu được sẽ nhỏ hơn nữa):
``` bash
qemu-img convert -c -f raw -O qcow2 /duong/dan/disk.raw /duong/dan/disk_compressed.qcow2
```

### QCOW2 -> RAW
- Để tối ưu hóa hiệu năng I/O cho máy ảo, sử dụng câu lệnh:
``` bash
qemu-img convert -f qcow2 -O raw /duong/dan/disk.qcow2 /duong/dan/disk.raw
```

**Lưu ý**: Sau khi chuyển đổi xong, bạn cần cập nhật lại đường dẫn tập tin và định dạng đĩa trong cấu hình XML của máy ảo qua lệnh `virsh edit <ten_may_ao>`

## CÁC CÂU LỆNH THƯỜNG DÙNG
### Kiểm tra thông tin tập tin đĩa ảo
- Xem chi tiết định dạng, dung lượng ảo (virtual size), dung lượng thực tế (disk size) và thông tin snapshot:
``` bash
qemu-img info /duong/dan/disk.qcow2
# hoặc
qemu-img info /duong/dan/disk.raw
```

### Tạo file đĩa ảo mới
- Tạo đĩa QCOW2 20GB:
``` bash
qemu-img create -f qcow2 /duong/dan/new_disk.qcow2 20G
```

- Tạo đĩa RAW 20GB
``` bash
qemu-img create -f qcow2 /duong/dan/new_disk.qcow2 20G
```

### Mở rộng (Tăng dung lượng) ổ đĩa ảo
- Tăng dung lượng ảo thêm 10GB:
```bash
qemu-img resize /duong/dan/disk.qcow2 +10G
# hoặc
qemu-img resize /duong/dan/disk.raw +10G
```

### Các câu lệnh thao tác Snapshot (Chỉ dành cho QCOW2)
- Tạo Snapshot:
``` bash
qemu-img snapshot -c snapshot_demo /duong/dan/disk.qcow2
```
- Xem danh sách Snapshot trong file đĩa
``` bash
qemu-img snapshot -l /duong/dan/disk.qcow2
```
- Khôi phục máy ảo về 1 Snapshot cụ thể:
``` bash
qemu-img snapshot -a snapshot_demo /duong/dan/disk.qcow2
```
- Xóa Snapshot
``` bash
qemu-img snapshot -d snapshot_demo /duong/dan/disk.qcow2
```

### Kiểm tra và sửa lỗi file đĩa QCOW2
``` bash
qemu-img check /duong/dan/disk.qcow2
```