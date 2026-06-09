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

