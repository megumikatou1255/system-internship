# TÌM HIỂU VỀ TẤT CẢ GIAI ĐOẠN CỦA QUÁ TRÌNH KHỞI ĐỘNG WINDOW.
- Tài liệu này giải thích rất kỹ quy trình khởi động của hệ điều hành Linux từ khi bạn nhấn nút nguồn cho đến khi màn hình đăng nhập (Login Prompt) xuất hiện. Mặc dù đây là kiến trúc chung của Linux, một vài tệp tin cấu hình và câu lệnh cụ thể trong bài có thể hơi thiên về các dòng Red Hat (RHEL/CentOS).

## I. KHỞI TẠO BIOS (BIOS INITIALIZATION)
BIOS (Basic Input Output System) là một chương trình phần sụn (firmware) được lưu trữ trên một chip chip xử lý nhỏ trên bo mạch chủ. Đây là chương trình đầu tiên giành quyền kiểm soát máy tính ngay khi bạn nhấn nút bật nguồn.
+ **Hành động cốt lõi**: BIOS thực hiện một bài kiểm tra toàn bộ các linh kiện phần cứng và thiết bị ngoại vi kết nối với máy tính, quá trình này gọi là POST (Power On Self Test - Tự kiểm tra khi bật nguồn).
+ **Tìm kiếm thiết bị boot**: Sau khi POST chạy thành công, BIOS sẽ tìm kiếm một thiết bị có khả năng khởi động (bootable device) dựa trên danh sách thứ tự ưu tiên được cấu hình sẵn trong cài đặt (như Ổ cứng SSD/HDD, USB, CD-ROM, hoặc qua Mạng).
+ **Đọc Boot Sector**: BIOS tìm đến Boot sector (Phân khu khởi động) - chính là phân khu vật lý đầu tiên (Sector 0) trên thiết bị lưu trữ để đọc mã lệnh khởi động máy.

## II. GIAI ĐOẠN MBR (MASTER BOOT RECORD)
- MBR là một khu vực lưu trữ cực kỳ quan trọng, nằm ở sector đầu tiên của đĩa khởi động (ví dụ /dev/sda), với kích thước chuẩn xác là 512 bytes.
- Thành phần bên trong 512 bytes của MBR được chia thành 3 phần:
    + Mã khởi động chính (Primary boot loader): 446 bytes.
    + Bảng phân vùng (Partition table): 64 bytes (chứa thông tin của tối đa 4 phân vùng chính - Primary partition).
    + Chữ ký kiểm tra hợp lệ (Magic number / Validation signature): 2 bytes.
    + Hành động cốt lõi: MBR chứa thông tin về trình quản lý khởi động (Boot Loader) của hệ điều hành. MBR sẽ tải mã nguồn của Boot Loader (ví dụ GRUB) vào bộ nhớ RAM và giao lại quyền điều khiển cho nó.

## III. TRÌNH QUẢN LÝ KHỞI ĐỘNG GRUB (GRUB BOOTLOADER)
- GRUB (Grand Unified Bootloader) là chương trình chịu trách nhiệm hiển thị menu lựa chọn hệ điều hành và tải Nhân (Kernel) của Linux vào bộ nhớ. Nếu máy bạn cài song song nhiều hệ điều hành (Dual-boot), giao diện menu chọn OS chính là do GRUB quản lý.
    + GRUB tìm cấu hình hệ điều hành tại tệp tin: /boot/grub/grub.conf hoặc /boot/grub2/grub.cfg.
    + Hành động cốt lõi: Sau khi bạn chọn hệ điều hành (hoặc hết thời gian chờ tự động), GRUB sẽ tải tệp tin cấu hình Kernel Image (như vmlinuz-xxx) và hệ thống tệp tạm thời initrd (Initial RAM Disk) vào bộ nhớ RAM, sau đó chuyển giao toàn quyền điều hành cho Kernel.
## IV. GIAI ĐOẠN NẠP NHÂN HỆ ĐIỀU HÀNH (KERNEL STAGE)
- Nhân (Kernel) chính là trái tim của hệ điều hành Linux. Khi được nạp vào RAM, việc đầu tiên nó làm là tự giải nén chính nó và thiết lập môi trường hệ thống.
    + Hành động cốt lõi: Kernel tiến hành cấu hình lại toàn bộ các thiết bị phần cứng ở mức chuyên sâu, gắn kết (mount) phân vùng gốc (/) của ổ cứng dưới chế độ Chỉ đọc (Read-only) để kiểm tra tính toàn vẹn hệ thống một cách an toàn.
    + Khởi chạy tiến trình đầu tiên: Sau khi chuẩn bị xong xuôi môi trường, Kernel sẽ tìm kiếm và kích hoạt tệp tin thực thi đầu tiên của hệ thống. Đây là tổ tiên của tất cả các tiến trình sau này, mang mã định danh PID = 1.

## V. HỆ THỐNG KHỞI TẠO INIT/SYSTEMD (INIT/SYSTEMD STAGE)
Kể từ khi systemd (hoặc init cũ) giành quyền điều khiển với tư cách là **PID 1**, nó sẽ phụ trách việc dựng toàn bộ các dịch vụ phần mềm chạy ngầm trên máy tính.

- Đối với hệ thống chạy init cũ (SysVinit): Nó sẽ đọc tệp cấu hình /etc/inittab để xác định Runlevel (mức độ vận hành). Có 7 Runlevel từ 0 đến 6 (ví dụ Runlevel 3 là giao diện dòng lệnh thuần túy có mạng, Runlevel 5 là giao diện đồ họa GUI).
- Đối với hệ thống chạy systemd hiện đại: systemd không dùng khái niệm Runlevel nữa mà thay bằng các Target Units (được cấu hình qua các tệp tin trong /lib/systemd/system/ và /etc/systemd/system/).
    + Nó thực hiện khởi động song song các dịch vụ thông qua các cơ chế kích hoạt Socket và D-Bus để tăng tốc độ boot.
    + Nó liên kết các dịch vụ mặc định phụ thuộc vào nhau qua sơ đồ logic (ví dụ dịch vụ mạng phải chạy thành công trước khi dịch vụ SSH được phép mở cổng).
    + Mục tiêu cuối cùng là nạp thành công mục tiêu multi-user.target (đối với giao diện dòng lệnh Terminal của Ubuntu Server) hoặc graphical.target (đối với bản có giao diện đồ họa).

## VI. GIAI ĐOẠN RUNLEVEL SCRIPTS/LOGIN PROMPT (MÀN HÌNH ĐĂNG NHẬP)
- Đây là bước cuối cùng của quy trình.
    + Hệ thống khởi chạy các đoạn Script cấu hình môi trường cuối cùng tùy thuộc vào Target/Runlevel được chọn (ví dụ: gán địa chỉ IP tĩnh hoặc chạy DHCP nhận IP từ Router, kích hoạt dịch vụ OpenSSH Server để chờ kết nối bên ngoài).
    + Giao diện đăng nhập hiện ra: Hệ thống kích hoạt chương trình mingetty hoặc gdm để hiển thị dòng chữ login: trên màn hình Terminal (hoặc giao diện nhập mật khẩu đồ họa).
    + Khi bạn nhập đúng Username và Password, Linux sẽ mở ra một tiến trình Shell (ví dụ /bin/bash) cho phép bạn chính thức gõ lệnh làm việc.

# TÓM TẮT QUÁ TRÌNH BOOTING
## Giai đoạn 1: Tiếp nhận nguồn điện (Power-On)
Khi bạn nhấn nút nguồn trên thùng máy:
+ Bộ nguồn (PSU) sẽ chuyển đổi dòng điện xoay chiều thành điện một chiều và cấp phát cho bo mạch chủ (Motherboard), CPU, RAM, ổ cứng...
+ Khi dòng điện ổn định, bộ nguồn sẽ gửi một tín hiệu có tên là Power Good đến bo mạch chủ để báo rằng: "Điện đã an toàn, hệ thống có thể chạy".
+ Ngay khi nhận được tín hiệu này, chip hẹn giờ trên bo mạch chủ sẽ ngừng gửi tín hiệu Reset đến CPU, cho phép CPU chính thức "tỉnh giấc".

## Giai đoạn 2: CPU tìm đến BIOS/UEFI
+ Khi vừa thức dậy, CPU hoàn toàn "mất trí nhớ" và không biết hệ điều hành nằm ở đâu. Nó được lập trình cứng để luôn tìm đến một địa chỉ ô nhớ duy nhất tại thời điểm khởi đầu: 0xFFFFFFF0h (nằm ở cuối thanh RAM ảo).
+ Địa chỉ này thực chất là một đường tắt (jump) dẫn thẳng đến con chip ROM BIOS/UEFI trên bo mạch chủ.
+ CPU bắt đầu đọc và thực thi các lệnh điều khiển được lưu trong BIOS/UEFI.

## Giai đoạn 3: Kiểm tra phần cứng (POST - Power-On Self-Test)
+ Đây là giai đoạn "khám sức khỏe tổng quát" của máy tính do BIOS/UEFI đảm nhận.
+ BIOS sẽ kiểm tra các linh kiện cốt lõi: CPU, bộ đếm thời gian, chip đồ họa (VGA), các thanh RAM, bàn phím, ổ cứng...
+ Kiểm tra kiểu boot: Ở giai đoạn này, BIOS sẽ ngó qua ô nhớ 0000:0472h (như chúng ta đã thảo luận trước đó). Nếu là Cold Boot, nó kiểm tra kỹ toàn bộ RAM; nếu là Warm Boot, nó sẽ lướt nhanh qua để tiết kiệm thời gian.
+ Nếu phát hiện lỗi nặng (ví dụ: lỏng RAM, hỏng card màn hình), máy sẽ dừng lại và phát ra các tiếng Bíp (Beep codes) hoặc nháy đèn LED để báo hiệu. Nếu mọi thứ ổn thỏa, máy sẽ phát 1 tiếng bíp ngắn (ở các dòng máy cũ) và chuyển sang bước tiếp theo.

## Giai đoạn 4: Tìm kiếm thiết bị khởi động (Boot Loader Phase)
+ Sau khi phần cứng ổn định, BIOS/UEFI sẽ tìm nơi lưu trữ hệ điều hành dựa trên danh sách ưu tiên cấu hình trong cài đặt (Boot Priority - ví dụ: Ưu tiên USB trước, rồi đến Ổ cứng SSD).
+ Lúc này, quy trình sẽ rẽ làm 2 nhánh tùy thuộc vào bo mạch chủ của bạn dùng chuẩn cũ hay mới:

### Nhánh 1: Nếu dùng chuẩn cũ (BIOS/MBR)
+ BIOS tìm đến phân vùng đầu tiên (Sector 0) của ổ cứng, tức là MBR (Master Boot Record).
+ BIOS tải 512 bytes dữ liệu của MBR này vào RAM tại địa chỉ huyền thoại 0000:7C00h.
+ CPU thực thi đoạn mã tại 7C00h. Đoạn mã MBR này rất nhỏ, nhiệm vụ duy nhất của nó là quét bảng phân vùng (Partition Table) để tìm phân vùng nào đang được đánh dấu là "Active" (chứa hệ điều hành) rồi kích hoạt trình khởi động nâng cao hơn (như bootmgr của Windows hoặc GRUB của Linux).

### Nhánh 2: Nếu dùng chuẩn mới (UEFI/GPT)
+ UEFI không tìm MBR và không dùng địa chỉ 7C00h.
+ Nó có khả năng đọc trực tiếp các định dạng phân vùng (thường là FAT32). Nó sẽ tìm một phân vùng đặc biệt gọi là EFI System Partition (ESP).
+ Tại đây, UEFI sẽ chạy thẳng các file khởi động có đuôi .efi (ví dụ: bootmgfw.efi của Windows) được lưu trong ổ cứng. Cách này nhanh và an toàn hơn MBR rất nhiều.

## Giai đoạn 5: Tải Core Hệ điều hành (Kernel Loading)
+ Lúc này, các trình khởi động (bootmgr hoặc GRUB) sẽ tiến hành thu thập thông tin phần cứng mà BIOS/UEFI bàn giao lại.
+ Nó bắt đầu tải các file cốt lõi của Hệ điều hành (Kernel - Nhân hệ điều hành) và các driver phần cứng cơ bản vào RAM.
+ Trình khởi động chính thức nhường toàn quyền kiểm soát máy tính cho Kernel.
+ Kernel khởi chạy các tiến trình chạy ngầm (Services), trình quản lý hiển thị (Display Manager), và cuối cùng là đẩy bạn ra màn hình đăng nhập (Login Screen) hoặc Màn hình Desktop.