# TẠO MỘT MÁY ẢO
## MÔ TẢ
- Tạo một máy ảo Ubuntu Server 24.04 bằng KVM và tìm hiểu chi tiết về máy ảo được tạo

## THỰC HÀNH
### Bước 1: Tải file ISO Ubuntu Server 24.04 trên trang chủ của Ubuntu, dùng lệnh wget để tải trực tiếp vào thư mục lưu trữ ISO (ví dụ /var/lib/libvirt/images/):
``` bash
cd /var/lib/libvirt/images/
sudo wget https://releases.ubuntu.com/24.04/ubuntu-24.04-live-server-amd64.iso
```

### Bước 2: Tiến hành cài đặt máy ảo
- Nếu thao tác qua giao diện dòng lệnh SSH (không có màn hình đồ họa GUI), hãy dùng tham số --graphics none kết hợp --extra-args 'console=ttyS0,115200n8 serial' để cài đặt qua giao diện dòng lệnh (Text installer).

```bash
sudo virt-install \
  --name ubuntu24-vm \
  --ram 2048 \
  --vcpus 2 \
  --disk path=/var/lib/libvirt/images/ubuntu24-vm.qcow2,size=20,format=qcow2 \
  --os-variant ubuntu24.04 \
  --network network=default,model=virtio \
  --graphics none \
  --location /var/lib/libvirt/images/ubuntu-24.04-live-server-amd64.iso \
  --extra-args 'console=ttyS0,115200n8 serial'
```

- *Giải thích các thông số*
    + `--name`: Tên của máy ảo (ở đây đặt là ubuntu24-vm).
    + `--ram`: Dung lượng RAM cấp cho máy ảo (tính bằng MB, ví dụ 2048 là 2GB).
    + `--vcpus`: Số lượng nhân CPU ảo cấp cho máy ảo (2 core).
    + `--disk`: Đường dẫn tạo file đĩa ảo dung lượng 20GB định dạng qcow2.
    + `--os-variant`: Khai báo hệ điều hành để KVM tối ưu (ubuntu24.04).
    + `--network`: Cấu hình mạng dùng chế độ NAT mặc định và tối ưu card virtio.
    + `--location`: Đường dẫn tới file ISO Ubuntu 24.04 vừa tải.

### Bước 3: Tiến hành cài đặt bên trong máy ảo
- Ngay sau khi chạy lệnh trên, màn hình console sẽ chuyển trực tiếp sang giao diện cài đặt Ubuntu Server 24.04 (Subiquity installer).
    + Bạn thực hiện các bước chọn ngôn ngữ, cấu hình bàn phím, kết nối mạng và phân vùng ổ đĩa giống như khi cài đặt trên máy tính thật.
    + Sau khi quá trình cài đặt hoàn tất và máy ảo yêu cầu Reboot, máy ảo sẽ tự động khởi động lại vào hệ điều hành mới.

### Bước 4: Quản lý và thao tác máy ảo sau khi cài xong
- Xem danh sách máy ảo đang chạy hoặc đã tắt:
```bash
virsh list --all
```
- Khởi động máy ảo:
```bash
virsh start ten_may_ao
```
- Khởi động lại máy ảo
```bash
virsh reboot ten-may-ao
```
- Truy cập vào màn hình console của máy ảo
```bash
virsh console ten_may_ao
```
Để thoát khỏi màn hình console và quay về máy chủ host, sử dụng tổ hợp `Ctrl + ]`
- Tắt máy ảo
```bash
virsh destroy ten_may_ao
```
hoặc nếu đang SSH vào máy ảo thì sử dụng câu lệnh `sudo shutdown now`

- Xóa hoàn toàn máy ảo nếu không sử dụng nữa
```bash
virsh destroy ten_may_ao
virsh undefine ten_may_ao --remove-all-storage
```
