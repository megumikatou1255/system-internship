# TỔNG QUAN VỀ LINUX
## I. LINUX LÀ GÌ ?
### 1. Khái niệm.
- Linux là một hệ điều hành mã nguồn mở dựa trên nhân (kernel) Linux do Linus Torvalds phát triển từ năm 1991. Hệ điều hành Linux không chỉ là nhân mà còn bao gồm nhiều phần mềm khác nhau tạo nên một hệ thống hoàn chỉnh.
- Linux được sử dụng rộng rãi trên máy chủ, đám mây, thiết bị nhúng và cả máy tính cá nhân. Ưu điểm chính của Linux bao gồm tính ổn định cao, bảo mật tốt và khả năng tùy biến mạnh.

### 2. Kiến trúc thành phần Linux.
Linux có kiến trúc phân lớp rõ ràng giữa không gian nhân (kernel space) và không gian người dùng (user space). Mỗi thành phần đảm nhiệm một vai trò riêng nhưng phối hợp chặt chẽ để tạo ra hệ điều hành hoàn chỉnh.

- **Nhân Linux (Linux Kernel)**:
  + Là lõi của hệ điều hành, quản lý phần cứng, tài nguyên và bảo mật.
  + **Quản lý tiến trình**: tạo và hủy tiến trình, chuyển đổi ngữ cảnh, lập lịch CPU bằng các thuật toán như CFS, O(1), và real-time.
  + **Quản lý bộ nhớ**: phân trang ảo, ánh xạ bộ nhớ, quản lý bộ nhớ dùng chung, swap và bảo vệ vùng nhớ.
  + **Quản lý thiết bị**: thông qua driver để điều khiển ổ đĩa, mạng, USB, GPU, âm thanh, cảm biến.
  + **Hệ thống tập tin**: sử dụng VFS (Virtual File System) để hỗ trợ nhiều hệ thống tập tin khác nhau như ext4, XFS, Btrfs, VFAT, NTFS.
  + **Mạng**: triển khai ngăn xếp TCP/IP, socket, firewall và các giao thức khác.
  + **Dịch vụ nội bộ**: IPC (Inter-Process Communication), cgroups, namespaces, audit, và đồng bộ hóa.

- **Không gian người dùng (User Space)**:
  + **Shell và terminal**:
    - Shell (Bash, Zsh, Fish) là giao diện dòng lệnh chính để người dùng nhập và thực thi lệnh.
    - Terminal emulator cho phép hiển thị và tương tác với shell.
  + **Tiện ích hệ thống (System Utilities)**:
    - Các công cụ cơ bản như `ls`, `cp`, `mv`, `ps`, `top`, `systemctl`, `ip`, `chmod`, `chown`.
    - Những tiện ích này giúp quản lý tệp, tiến trình, dịch vụ, mạng và cấu hình hệ thống.
  + **Daemon và service**:
    - Tiến trình chạy ngầm để cung cấp dịch vụ như web server, database, logging, cron.
    - Được quản lý bởi init system và khởi động cùng hệ thống.
  + **Ứng dụng người dùng**:
    - Trình duyệt, bộ office, phần mềm lập trình, ứng dụng đa phương tiện.
    - Chạy trên user space và sử dụng API hệ thống để truy cập tài nguyên.

- **Thư viện hệ thống (System Libraries)**:
  - Thư viện chuẩn `glibc`, `musl` hoặc `uclibc` cung cấp các hàm chuẩn C như `printf`, `open`, `read`, `write`.
  - Các thư viện bổ sung như `libm`, `libpthread`, `libdl`, `libssl` hỗ trợ toán học, đa luồng, nạp động và bảo mật.
  - Thư viện đóng vai trò là cầu nối giữa ứng dụng và kernel bằng cách thực hiện các `system call`.

- **Init System và quản lý dịch vụ**:
  - Init system là chương trình đầu tiên được khởi chạy sau khi kernel nạp xong.
  - Các hệ thống init phổ biến: `systemd`, `SysV init`, `Upstart`, `OpenRC`.
  - Chức năng: khởi tạo môi trường người dùng, khởi động/dừng dịch vụ, quản lý runlevel/target, và xử lý tắt/mở lại.

- **Hệ thống tập tin và cấu trúc thư mục**:
  - Linux dùng cấu trúc phân cấp bắt đầu từ `/`.
  - Các thư mục ảo như `/proc`, `/sys`, `/dev` cung cấp thông tin hệ thống và thiết bị.
  - Cơ chế mount cho phép gắn kết phân vùng và thiết bị vào cây thư mục thống nhất.

- **Quản lý người dùng và quyền**:
  - Linux dùng UID/GID để định danh người dùng và nhóm.
  - Quyền truy cập gồm `read`, `write`, `execute` cho chủ sở hữu, nhóm và người dùng khác.
  - Còn có ACL, SELinux/AppArmor để kiểm soát bảo mật tinh vi.

**Mối quan hệ giữa không gian nhân và không gian người dùng**
- Ứng dụng trong user space không thể truy cập trực tiếp phần cứng hoặc bộ nhớ kernel.
- Khi cần tài nguyên, ứng dụng gọi `system call` như `open()`, `read()`, `write()`, `fork()`, `execve()`.
- Kernel nhận yêu cầu này, thực hiện công việc và trả kết quả về user space.
- Mô hình này bảo vệ hệ thống khỏi lỗi và hành vi độc hại của ứng dụng.

**Một vài thành phần hỗ trợ quan trọng**
- **VFS (Virtual File System)**: cung cấp giao diện chung cho nhiều hệ thống tập tin khác nhau.
- **Loadable Kernel Modules (LKM)**: cho phép nạp tính năng và driver vào kernel khi hệ thống đang chạy.
- **Cgroups**: nhóm tiến trình để kiểm soát tài nguyên CPU, bộ nhớ, I/O.
- **Namespaces**: cách ly tiến trình, cho phép tạo container như Docker.

## II. CẤU TRÚC FILE, FOLDER TRONG LINUX.
### 1. Root - thư mục gốc (`/`).
- Root filesystem (`/`) là thư mục gốc của toàn bộ hệ thống tập tin Linux. Tất cả các thư mục và tập tin khác đều nằm dưới `/` theo cấu trúc phân cấp.

- Các đặc điểm chính của root filesystem:
+ **Cấu trúc phân cấp duy nhất**: tất cả các phân vùng, thiết bị đều được gắn (mount) dưới thư mục `/`.
+ **Tiêu chuẩn FHS (Filesystem Hierarchy Standard)**: Linux tuân theo tiêu chuẩn FHS để đảm bảo tính nhất quán giữa các bản phân phối.
+ **Phân tách quyền hạn**: Root filesystem thường chứa các thư mục hệ thống cốt lõi như `/bin`, `/etc`, `/lib`.
+ **Bảo vệ**: các tập tin và thư mục có quyền truy cập hạn chế để bảo vệ tính toàn vẹn hệ thống.

Ý nghĩa của việc dùng cấu trúc thư mục duy nhất:
+ Quản lý tài nguyên thống nhất.
+ Dễ dàng mở rộng bằng cách gắn các phân vùng mới.
+ Giúp người quản trị định vị tệp và dịch vụ dễ dàng hơn.

### 2. Các thư mục quan trọng trong hệ thống Linux.
- **/bin**: chứa các lệnh/tiện ích cơ bản cần thiết để khởi động và sửa chữa hệ thống, như `ls`, `cp`, `mv`, `cat`, `grep`, `sed`, `awk`.
  - Những tiện ích ở đây được sử dụng bởi tất cả người dùng.
  - `/bin` thường là link tới `/usr/bin` trong các bản phân phối hiện đại.

- **/sbin**: chứa các lệnh hệ thống (system binaries) dành cho quản trị viên, như `ifconfig`, `route`, `iptables`, `mount`, `shutdown`, `reboot`.
  - Thường chỉ root mới có quyền thực thi các lệnh này.
  - `/sbin` thường link tới `/usr/sbin`.

- **/etc**: chứa các tập tin cấu hình của hệ thống và ứng dụng.
  - `/etc/passwd`: thông tin người dùng.
  - `/etc/shadow`: mật khẩu được mã hóa.
  - `/etc/group`: thông tin nhóm người dùng.
  - `/etc/sudoers`: cấu hình cho lệnh sudo.
  - `/etc/fstab`: cấu hình tự động gắn phân vùng khi khởi động.
  - `/etc/hostname`, `/etc/hosts`: cấu hình mạng.
  - `/etc/systemd/system/`: cấu hình dịch vụ systemd.

- **/home**: chứa thư mục người dùng cá nhân.
  - Mỗi người dùng có một thư mục con, ví dụ `/home/username`.
  - Người dùng có toàn quyền đối với thư mục của mình.
  - Thông thường `/home` nằm trên phân vùng riêng để bảo vệ dữ liệu người dùng.

- **/lib** và **/lib64**: chứa các thư viện hệ thống cần thiết cho các tiện ích ở `/bin` và `/sbin`.
  - Gồm `libc.so.6` (GNU C Library), `libm.so.6` (math library), v.v.
  - `/lib64` chứa thư viện 64-bit trên hệ thống 64-bit.

- **/media**: điểm gắn kết cho các thiết bị di động như USB, CD, DVD.
  - Người dùng thông thường có quyền truy cập các thiết bị ở đây.

- **/mnt**: điểm gắn kết tạm thời cho các phân vùng hoặc thiết bị khác.
  - Người quản trị sử dụng để gắn phân vùng hoặc chia sẻ mạng.

- **/boot**: chứa kernel, initrd (initial ramdisk) và các tập tin cấu hình bootloader (GRUB, LILO).
  - Khi máy khởi động, bootloader đọc các tập tin ở đây để nạp kernel.
  - Thường là một phân vùng riêng để tránh lỗi khi cập nhật kernel.

- **/opt**: chứa các phần mềm thứ ba được cài đặt thêm, không phải từ package manager.
  - Ví dụ: `/opt/google/chrome`, `/opt/vagrant`.

- **/root**: thư mục home của người dùng root (quản trị viên).
  - Khác với `/home` dùng cho người dùng thông thường.

- **/tmp**: chứa tập tin tạm thời được tạo bởi các ứng dụng và người dùng.
  - Tập tin ở đây thường bị xóa khi khởi động lại hệ thống.
  - Mỗi người dùng có quyền ghi vào `/tmp`.

- **/usr**: chứa các chương trình người dùng, thư viện, tài liệu (sẽ chi tiết ở phần 3).

- **/var**: chứa dữ liệu biến đổi như log, cache, spool (sẽ chi tiết ở phần 4).

### 3. Các thư mục quan trọng trong `/usr`.
`/usr` chứa các chương trình, thư viện, tài liệu và dữ liệu dành cho người dùng, không bao gồm các tập tin cấu hình hệ thống cốt lõi.

- **/usr/bin**: chứa hầu hết các lệnh và tiện ích dành cho người dùng.
  - Ví dụ: `python`, `gcc`, `git`, `vim`, `wget`, `curl`, `node`, `java`.
  - Là nơi chính chứa các ứng dụng được cài đặt qua package manager.

- **/usr/sbin**: chứa các lệnh quản trị hệ thống không cần thiết để khởi động.
  - Ví dụ: `useradd`, `userdel`, `groupadd`, `usermod`, `parted`, `mkfs`.

- **/usr/lib** và **/usr/lib64**: chứa thư viện chia sẻ cho các chương trình ở `/usr/bin` và `/usr/sbin`.
  - Ví dụ: `libc.so`, `libssl.so`, `libcrypto.so`.

- **/usr/local**: chứa các chương trình được cài đặt thủ công (không qua package manager).
  - Cấu trúc tương tự `/usr`: `/usr/local/bin`, `/usr/local/lib`, `/usr/local/include`.
  - Được dùng để tránh xung đột với gói được quản lý bởi hệ thống.

- **/usr/share**: chứa dữ liệu độc lập với hệ thống (kiến trúc).
  - `/usr/share/doc`: tài liệu và man page của các gói.
  - `/usr/share/man`: trang manual cho các lệnh.
  - `/usr/share/icons`, `/usr/share/pixmaps`: hình ảnh và icon cho giao diện đồ họa.
  - `/usr/share/locale`: dữ liệu bản địa hóa (ngôn ngữ, mã hóa).

### 4. Các thư mục quan trọng trong `/var`.
`/var` chứa các tập tin dữ liệu biến đổi như log, cache, mail queue, những tập tin thay đổi thường xuyên trong quá trình hoạt động của hệ thống.

- **/var/log**: chứa các tập tin log của hệ thống và các ứng dụng.
  - `/var/log/syslog` hoặc `/var/log/messages`: log chung của hệ thống.
  - `/var/log/auth.log`: log xác thực người dùng.
  - `/var/log/kernel.log`: log của kernel.
  - `/var/log/apache2/`, `/var/log/nginx/`: log của web server.
  - `/var/log/mysql/`: log của database MySQL.
  - Việc kiểm tra log rất quan trọng trong việc tìm ra sự cố hệ thống.

- **/var/spool**: chứa dữ liệu chờ xử lý cho các dịch vụ.
  - `/var/spool/mail`: thư được gửi tới người dùng cục bộ.
  - `/var/spool/cron`: tập tin cron job của từng người dùng.
  - `/var/spool/cups`: hàng đợi in của CUPS (Common Unix Printing System).

- **/var/cache**: chứa dữ liệu cache của các ứng dụng.
  - `/var/cache/apt`: cache các gói apt đã tải về.
  - `/var/cache/dnf`: cache các gói dnf.
  - Dữ liệu ở đây có thể an toàn xóa khi cần lấy lại dung lượng.

- **/var/run** hoặc **/run**: chứa các tập tin PID (Process ID) và socket của các dịch vụ đang chạy.
  - `/var/run/systemd/`: socket của systemd.
  - `/var/run/sshd.pid`: tập tin PID của SSH daemon.
  - Các tập tin ở đây thường được xóa khi khởi động lại hệ thống.

- **/var/tmp**: chứa tập tin tạm thời lâu dài, không bị xóa khi khởi động lại (khác `/tmp`).
  - Một số ứng dụng dùng `/var/tmp` để lưu trữ tập tin tạm thời lớn.

- **/var/www**: chứa các tập tin web cho máy chủ HTTP.
  - `/var/www/html`: các trang web HTML mặc định.

### 5. Một số thư mục đặc biệt khác.
- **/proc**: hệ thống tập tin ảo cung cấp thông tin về các tiến trình và thông tin hệ thống.
  - `/proc/cpuinfo`: thông tin CPU.
  - `/proc/meminfo`: thông tin bộ nhớ.
  - `/proc/[PID]`: thông tin về tiến trình có ID là `[PID]`.
  - `/proc/[PID]/status`: trạng thái chi tiết của tiến trình.
  - Tất cả tập tin ở đây không thực sự tồn tại trên đĩa cứng, chúng được sinh ra động bởi kernel.

- **/sys**: hệ thống tập tin ảo cung cấp thông tin và kiểm soát thiết bị và module kernel.
  - `/sys/class/`: thông tin về các lớp thiết bị (usb, net, block, etc).
  - `/sys/devices/`: cây phân cấp các thiết bị hệ thống.
  - `/sys/module/`: thông tin về các module kernel được nạp.

- **/dev**: chứa các tập tin thiết bị (device files).
  - `/dev/sda`, `/dev/sdb`: ổ đĩa cứng.
  - `/dev/sda1`, `/dev/sda2`: phân vùng trên ổ đĩa.
  - `/dev/null`: thiết bị null (loại bỏ dữ liệu ghi vào).
  - `/dev/zero`: thiết bị cung cấp byte 0 vô hạn.
  - `/dev/tty`: terminal hiện tại.
  - `/dev/pts/`: pseudo-terminal cho SSH, terminal ảo.
  - Linux sử dụng udev để quản lý các tập tin thiết bị động.

- **/lost+found**: thư mục được tạo bởi fsck (file system check) để lưu trữ các tập tin bị hỏng hoặc bắt gặp.
  - Thường trống nếu hệ thống hoạt động ổn định.

- **/.dockerenv** hoặc **/.containerenv**: tập tin đánh dấu cho biết hệ thống đang chạy trong container.
  - Ứng dụng có thể kiểm tra sự tồn tại của tập tin này để phát hiện container.

## III. ĐẶC ĐIỂM LINUX.
### 1. Ưu điểm.
- **Mã nguồn mở**:
  - Mã nguồn của Linux có sẵn để mọi người xem, sửa đổi và phân phối.
  - Cộng đồng các lập trình viên toàn thế giới có thể đóng góp, phát hiện và sửa lỗi bảo mật.
  - Giúp Linux có độ bảo mật cao vì lỗi được phát hiện nhanh chóng.

- **Miễn phí**:
  - Hầu hết các bản phân phối Linux đều miễn phí, tiết kiệm chi phí so với các hệ điều hành thương mại như Windows, macOS.
  - Không cần trả phí giấy phép để sử dụng Linux.

- **Tính ổn định cao**:
  - Linux có thể chạy không lỗi trong hàng năm hoặc thậm chí hàng chục năm mà không cần khởi động lại.
  - Rất phù hợp cho các máy chủ chạy dịch vụ quan trọng.
  - Kernel Linux liên tục được tối ưu hóa để có hiệu năng tối đa.

- **Bảo mật cao**:
  - Linux sử dụng mô hình quyền người dùng/nhóm (user/group permissions) để kiểm soát truy cập.
  - Cơ chế file descriptor, SELinux, AppArmor giúp cô lập các tiến trình.
  - Tường lửa (iptables, firewalld, nftables) giúp bảo vệ mạng.
  - Được sử dụng rộng rãi trong các tổ chức yêu cầu bảo mật cao như chính phủ, quân sự, ngân hàng.

- **Tính tương thích (Portability)**:
  - Linux chạy trên mọi nền tảng phần cứng từ máy chủ siêu cấp, máy tính để bàn, máy tính xách tay, đến các thiết bị nhúng như router, camera, điện thoại thông minh.
  - Kernel Linux có thể được biên dịch cho nhiều kiến trúc CPU khác nhau.

- **Hiệu năng cao**:
  - Linux có chi phí quản lý hệ thống thấp, sử dụng tài nguyên hệ thống hiệu quả.
  - Cho phép chạy nhiều ứng dụng đồng thời mà không giảm hiệu năng đáng kể.
  - Thích hợp cho các máy chủ chịu tải cao.

- **Hỗ trợ đa nhiệm và đa người dùng**:
  - Nhiều người dùng có thể đăng nhập và làm việc trên cùng một máy tính mà không ảnh hưởng đến nhau.
  - Nhiều chương trình có thể chạy cùng lúc (multitasking).
  - CPU được chia sẻ công bằng giữa các tiến trình.

- **Linh hoạt và có thể tùy biến**:
  - Có thể tùy chỉnh kernel để phù hợp với nhu cầu cụ thể.
  - Có thể gỡ bỏ các tính năng không cần thiết để giảm kích thước và tăng hiệu năng.
  - Cấu trúc phân lớp giúp dễ dàng thêm hoặc xóa chức năng.

- **Hỗ trợ cộng đồng mạnh**:
  - Có rất nhiều tài liệu, hướng dẫn, diễn đàn trực tuyến.
  - Cộng đồng các nhà phát triển và người dùng sẵn lòng giúp đỡ.
  - Có nhiều tổ chức như Linux Foundation hỗ trợ phát triển.

- **Hỗ trợ các công cụ phát triển mạnh**:
  - GCC, Clang, Python, Node.js, Java, Go và nhiều ngôn ngữ lập trình khác được hỗ trợ tốt.
  - Git, Docker, Kubernetes và các công cụ hiện đại được phát triển chủ yếu cho Linux.

- **Khả năng mở rộng**:
  - Loadable Kernel Modules cho phép thêm tính năng mới mà không cần khởi động lại hệ thống.
  - Dễ dàng mở rộng tài nguyên phần cứng như thêm ổ đĩa, bộ nhớ, CPU.

### 2. Nhược điểm.
- **Độ khó cao cho người mới**:
  - Linux yêu cầu kiến thức dòng lệnh (command line) để sử dụng hiệu quả.
  - Giao diện người dùng (GUI) trên Linux không bằng Windows hoặc macOS trong mặt thân thiện.
  - Đường cong học tập cao đối với người dùng thông thường.

- **Hỗ trợ phần cứng hạn chế**:
  - Một số nhà sản xuất phần cứng không viết driver cho Linux, đặc biệt là GPU của NVIDIA và AMD.
  - Máy in, scanner, card âm thanh đôi khi không tương thích hoàn toàn với Linux.
  - Có thể mất thời gian để tìm driver phù hợp.

- **Hỗ trợ phần mềm thương mại hạn chế**:
  - Nhiều phần mềm thương mại được thiết kế chỉ cho Windows hoặc macOS.
  - Phần mềm Office, Photoshop, 3DS Max không có phiên bản native cho Linux.
  - Mặc dù có các công cụ thay thế (LibreOffice, GIMP, Blender) nhưng không luôn tương thích 100%.

- **Hỗ trợ game hạn chế**:
  - Phần lớn game AAA được phát triển cho Windows.
  - Proton (compatibility layer) giúp chạy game Windows trên Linux nhưng có hiệu năng kém hơn.
  - Không phải tất cả game đều tương thích với Proton.

- **Sự phân mảnh (Fragmentation)**:
  - Có quá nhiều bản phân phối Linux khác nhau (Debian, Ubuntu, Fedora, RHEL, Arch, v.v.).
  - Mỗi bản phân phối có cách quản lý gói, cấu hình khác nhau.
  - Điều này khiến khó khăn cho người dùng khi chuyển đổi giữa các bản phân phối.

- **Thiếu hỗ trợ chính thức cho một số lĩnh vực**:
  - Mặc dù Linux được sử dụng trong các máy chủ, nhưng Windows vẫn chiếm ưu thế trong các doanh nghiệp nhỏ.
  - Một số phần mềm chuyên ngành chỉ có trên Windows.

- **Không có hỗ trợ kỹ thuật tập trung**:
  - Mặc dù có cộng đồng, nhưng không có một "công ty" chính thức hỗ trợ Linux.
  - RedHat, Canonical, SUSE cung cấp hỗ trợ thương mại nhưng phải trả phí.
  - Hỗ trợ cộng đồng có thể chậm hoặc không đáp ứng.

- **Yêu cầu quản lý cao**:
  - Linux yêu cầu người quản trị có kiến thức sâu để cấu hình và bảo trì.
  - Không có giao diện GUI duy nhất, mỗi bản phân phối có cách quản lý khác nhau.
  - Phải cập nhật hệ thống, patch bảo mật định kỳ.

- **Hệ sinh thái máy tính để bàn yếu**:
  - Linux không bao giờ thành công trên máy tính để bàn cá nhân (chỉ ~2% thị phần).
  - Driver GPU, âm thanh, wifi không luôn hoạt động tốt.
  - Giao diện không thống nhất giữa các ứng dụng.

- **Thiếu chuẩn hóa**:
  - Cách các bản phân phối tổ chức thư mục, đặt tên dịch vụ, quản lý gói khác nhau.
  - Điều này khiến khó khăn khi viết kịch bản tự động hoặc hướng dẫn dùng chung.

- **Hiệu năng I/O đôi khi không ổn định**:
  - Đối với các ứng dụng yêu cầu truy cập đĩa ngẫu nhiên cao, hiệu năng có thể gặp vấn đề.
  - Cơ chế swap có thể làm chậm hệ thống nếu bộ nhớ không đủ.

## IV. DISTRO LINUX LÀ GÌ ? PHÂN LOẠI DISTRO LINUX.
### 1. Khái niệm Distro Linux.
- **Distro** là viết tắt của "distribution" (bản phân phối).
- Một bản phân phối Linux là tập hợp của nhân Linux, các gói phần mềm hệ thống, thư viện, trình cài đặt và các công cụ quản lý được đóng gói lại để người dùng có thể cài đặt và sử dụng.
- Mỗi distro có thể tùy biến khác nhau về giao diện, quản lý gói, init system, cấu hình mặc định và mục tiêu sử dụng.
- Linux kernel chỉ là một phần trong toàn bộ distro; phần quan trọng còn lại là các tiện ích GNU, trình quản lý gói, và phần mềm tích hợp.

### 2. Thành phần chính của một bản phân phối Linux.
- **Kernel**:
  - Nhân Linux là lõi của hệ điều hành, chịu trách nhiệm quản lý phần cứng.
  - Mỗi distro có thể dùng phiên bản kernel khác nhau hoặc kernel tùy chỉnh.

- **System libraries**:
  - Thư viện như `glibc` hoặc `musl` cung cấp API cho ứng dụng.
  - Thư viện chuẩn giúp phần mềm tương thích với hệ thống.

- **System utilities**:
  - Các công cụ căn bản của GNU như `bash`, `coreutils`, `findutils`, `grep`.
  - Các tiện ích giúp quản lý tệp, xử lý văn bản, hệ thống và mạng.

- **Init system**:
  - Chịu trách nhiệm khởi động và quản lý dịch vụ.
  - Ví dụ: `systemd`, `SysV init`, `Upstart`, `OpenRC`, `runit`.

- **Package manager**:
  - Quản lý cài đặt, cập nhật và gỡ bỏ phần mềm.
  - Ví dụ: `apt` (Debian/Ubuntu), `yum`/`dnf` (Fedora/RHEL), `pacman` (Arch), `zypper` (openSUSE).

- **Desktop environment và GUI**:
  - Một số distro cung cấp giao diện đồ họa đầy đủ như GNOME, KDE Plasma, XFCE, Cinnamon.
  - Một số distro chỉ cài đặt môi trường dòng lệnh (server hoặc minimal).

- **Installer**:
  - Trình cài đặt giúp người dùng thiết lập hệ thống.
  - Ví dụ: `Ubiquity` (Ubuntu), `Calamares`, `Anaconda` (Fedora/RHEL), `Arch Install Script`.

- **Repository**:
  - Kho lưu trữ phần mềm do distro cung cấp.
  - Giúp cài đặt gói chính thức và cập nhật bảo mật một cách đồng nhất.

- **Configuration files**:
  - Các tệp cấu hình nằm trong `/etc` và các thư mục cấu hình khác.
  - Distro thường cài sẵn cấu hình mặc định để phù hợp mục tiêu sử dụng.

### 3. Phân loại distro Linux.
- **Theo mục đích sử dụng**:
  + **Server**: tập trung vào hiệu năng, ổn định và bảo mật. Ví dụ: RHEL, CentOS Stream, Ubuntu Server, Debian.
  + **Desktop**: tập trung vào trải nghiệm người dùng, giao diện đồ họa và phần mềm đa phương tiện. Ví dụ: Ubuntu Desktop, Linux Mint, Fedora Workstation.
  + **Security / Penetration testing**: tích hợp các công cụ bảo mật và tấn công. Ví dụ: Kali Linux, Parrot OS.
  + **Embedded / IoT**: tối ưu cho thiết bị nhúng, kích thước nhỏ. Ví dụ: Raspberry Pi OS, Yocto, Buildroot.

- **Theo quản lý gói (package manager)**:
  + `deb`/`apt`: Debian, Ubuntu, Linux Mint.
  + `rpm`/`dnf`/`yum`/`zypper`: Fedora, RHEL, CentOS, openSUSE.
  + `pacman`: Arch Linux, Manjaro.
  + `xbps`: Void Linux.
  + `pkgsrc`: NetBSD, SmartOS.

- **Theo cách tiếp cận**:
  + **Rollng release**: cập nhật liên tục, không có phiên bản cố định. Ví dụ: Arch Linux, openSUSE Tumbleweed, Manjaro.
  + **Fixed release**: phát hành theo chu kỳ, mỗi phiên bản ổn định trong thời gian nhất định. Ví dụ: Ubuntu LTS, Debian Stable, Fedora.

- **Theo mức độ thân thiện người dùng**:
  + **Distro thân thiện**: cài đặt dễ dàng, hỗ trợ GUI mạnh. Ví dụ: Ubuntu, Linux Mint, Zorin OS.
  + **Distro cho người dùng cao cấp**: yêu cầu cấu hình hoặc thao tác dòng lệnh nhiều. Ví dụ: Arch Linux, Gentoo, Slackware.

- **Theo nguồn gốc**:
  + **Distro gốc**: phát triển độc lập, không dựa trên distro khác. Ví dụ: Debian, Arch Linux, Gentoo, openSUSE.
  + **Distro dẫn xuất**: dựa trên distro khác và tùy chỉnh thêm. Ví dụ: Ubuntu (dựa trên Debian), Linux Mint (dựa trên Ubuntu), Manjaro (dựa trên Arch).

## V. USER VÀ GROUP.
### 1. Thế nào là User trong Linux ?
- **User** trong Linux là một tài khoản đại diện cho một người hoặc một dịch vụ.
- Mỗi user có một **UID** (User ID) duy nhất.
- User được dùng để xác thực khi đăng nhập và để phân quyền truy cập tài nguyên.
- User được định nghĩa trong các tập tin như `/etc/passwd` và `/etc/shadow`.
- Một số thuộc tính của user:
  + **Username**: tên đăng nhập.
  + **UID**: số định danh user.
  + **GID chính**: nhóm chính của user.
  + **Home directory**: thư mục cá nhân, ví dụ `/home/tan`.
  + **Shell**: chương trình shell mặc định, ví dụ `/bin/bash`.

### 2. Các loại user trong Linux.
- **Root user**:
  + Là user đặc quyền cao nhất trong Linux.
  + UID = 0.
  + Có quyền thực thi mọi lệnh và truy cập mọi tập tin.
  + Dùng để cài đặt phần mềm, thay đổi cấu hình hệ thống, quản lý dịch vụ.

- **User bình thường (regular user)**:
  + Có quyền hạn giới hạn.
  + Không thể thực hiện các tác vụ yêu cầu quyền root trừ khi dùng `sudo`.
  + Được dùng để làm việc hàng ngày, bảo vệ hệ thống khỏi thay đổi không mong muốn.

- **System user / Service account**:
  + Dùng cho các dịch vụ hệ thống như `www-data`, `mysql`, `postgres`.
  + Không phải user để đăng nhập bình thường.
  + Thường có shell `/usr/sbin/nologin` hoặc `/bin/false`.

### 3. Ngữ cảnh phân loại.
- **User theo mục đích**:
  + **Người dùng hệ thống**: root và các user dịch vụ.
  + **Người dùng tương tác**: người dùng thực sự đăng nhập và sử dụng máy.

- **User theo quyền**:
  + **User toàn quyền**: root.
  + **User hạn chế**: regular user và service account.

- **User theo nhóm**:
  + Mỗi user có một nhóm chính.
  + Có thể thuộc nhiều nhóm phụ để mở rộng quyền hạn.

### 4. Group là gì ?
- **Group** trong Linux là tập hợp các user.
- Mỗi group có một **GID** (Group ID).
- Group giúp quản lý quyền truy cập theo nhóm thay vì từng user.
- Group được định nghĩa trong `/etc/group`.
- Ví dụ:
  + group `sudo`: cho phép user dùng `sudo`.
  + group `www-data`: cho phép user truy cập tài nguyên web server.

### 5. Mối quan hệ giữa User và Group trong quản lý quyền.
- Mỗi tập tin hoặc thư mục trong Linux có ba bộ quyền:
  + **Owner**: chủ sở hữu file.
  + **Group**: nhóm thứ hai.
  + **Others**: mọi người còn lại.
- Các quyền cơ bản:
  + `r` = read (đọc)
  + `w` = write (ghi)
  + `x` = execute (thực thi)
- Quản lý quyền dựa trên user và group giúp:
  + Giới hạn ai được đọc, ghi hoặc thực thi tập tin.
  + Chia sẻ tài nguyên giữa các thành viên nhóm.
  + Tăng tính bảo mật và kiểm soát truy cập.

### 6. Quản lý User và Group.
- **Xem thông tin user**:
  + `id username` — hiển thị UID, GID và các nhóm của user.
  + `whoami` — hiển thị user hiện tại.
  + `getent passwd username` — lấy thông tin user từ hệ thống.

- **Tạo user**:
  + `useradd username` — tạo user mới.
  + `adduser username` — tương tự `useradd` nhưng thường tương tác hơn (Ubuntu/Debian).
  + `useradd -m -s /bin/bash username` — tạo user với thư mục home và shell Bash.

- **Xóa user**:
  + `userdel username` — xóa user.
  + `userdel -r username` — xóa user và thư mục home.

- **Thay đổi thông tin user**:
  + `usermod -aG group username` — thêm user vào nhóm.
  + `usermod -g group username` — đổi nhóm chính của user.
  + `usermod -l newname oldname` — đổi tên user.
  + `chfn username` — sửa thông tin người dùng.

- **Thay đổi mật khẩu**:
  + `passwd username` — thay đổi mật khẩu cho user.

- **Tạo và quản lý group**:
  + `groupadd groupname` — tạo nhóm mới.
  + `groupdel groupname` — xóa nhóm.
  + `gpasswd -a username groupname` — thêm user vào nhóm.
  + `gpasswd -d username groupname` — xóa user khỏi nhóm.

### 7. Xem phân quyền của một file/folder.

- `ls -l filename` — hiển thị quyền, chủ sở hữu và nhóm của file.
  + Ví dụ: `-rwxr-xr-- 1 tan tan 4096 Apr 10 12:00 script.sh`
  + Trong đó:
    * `rwx` là quyền của owner.
    * `r-x` là quyền của group.
    * `r--` là quyền của others.

- `stat filename` — xem thông tin chi tiết về file, bao gồm UID/GID và quyền.

- `chmod` — thay đổi quyền của file hoặc thư mục.
  + `chmod 755 file` — owner đọc/ghi/thực thi, group và others đọc/ thực thi.
  + `chmod u+rwx,g+rx,o+r file` — dùng biểu thức ký tự để thay đổi quyền.

- `chown` — thay đổi owner và group của file.
  + `chown tan:tan file` — đổi owner và group thành user `tan`.
  + `chown root:www-data /var/www/html` — đổi owner thành root và group thành www-data.

- `chgrp` — thay đổi group của file.
  + `chgrp www-data /var/www/html`.

- `getfacl` / `setfacl` — quản lý ACL (Access Control List) cho quyền truy cập linh hoạt hơn.
  + `getfacl file` — xem ACL.
  + `setfacl -m u:tan:rwx file` — thêm quyền cho user tan.

## VI. GIẤY PHÉP NGUỒN MỞ TRONG LINUX.
Giấy phép nguồn mở (Open Source License) xác định cách sử dụng, sửa đổi, và phân phối phần mềm. Linux và phần lớn các ứng dụng trên Linux đều sử dụng giấy phép nguồn mở, cho phép người dùng truy cập, sửa đổi và phân phối mã nguồn.
### 1. Khái niệm về giấy phép mã nguồn mở.

- **Định nghĩa**: Giấy phép mã nguồn mở là một hợp đồng pháp lý mô tả các quyền và trách nhiệm của người phát triển và người sử dụng phần mềm.
- **Các nguyên tắc cơ bản**:
  + **Tự do sử dụng**: người dùng có quyền sử dụng phần mềm cho bất kỳ mục đích nào (thương mại hoặc phi thương mại).
  + **Tự do nghiên cứu**: người dùng có quyền xem và hiểu mã nguồn của phần mềm.
  + **Tự do sửa đổi**: người dùng có quyền sửa đổi mã nguồn để phù hợp với nhu cầu của mình.
  + **Tự do phân phối**: người dùng có quyền chia sẻ hoặc phân phối phần mềm gốc hoặc đã sửa đổi.

- **Tổ chức quản lý**:
  + **OSI (Open Source Initiative)**: tổ chức xác định tiêu chuẩn cho giấy phép nguồn mở.
  + **FSF (Free Software Foundation)**: tổ chức do Richard Stallman thành lập, quản lý giấy phép GNU.

### 2. Các giấy phép mã nguồn mở phổ biến.
**GNU General Public License (GPL)**
- **Phiên bản chính**: GPLv2, GPLv3
- **Đặc điểm**:
  + Giấy phép copyleft mạnh nhất, yêu cầu bất kỳ phần mềm nào sử dụng code GPL phải cũng được phát hành dưới GPL.
  + Nếu sửa đổi phần mềm GPL, phiên bản sửa đổi cũng phải là GPL.
  + Cho phép sử dụng cho mục đích thương mại nhưng phải công khai mã nguồn.
  + Yêu cầu cung cấp một bản sao của giấy phép cùng phần mềm.

- **Sử dụng**:
  + Linux kernel, GNU tools (gcc, gdb, bash, coreutils).
  + Rất phổ biến trong các dự án lớn.

- **Ưu điểm**: đảm bảo phần mềm luôn mở, khuyến khích đóng góp cộng đồng.
- **Nhược điểm**: có thể hạn chế các công ty thương mại sử dụng hoặc tích hợp vào sản phẩm của mình.

**MIT License**
- **Đặc điểm**:
  + Một trong những giấy phép permissive đơn giản nhất.
  + Cho phép sử dụng, sửa đổi, phân phối, thậm chí trong phần mềm thương mại.
  + Không yêu cầu công khai mã nguồn của phần mềm đã sửa đổi.
  + Chỉ yêu cầu ghi nhận tác giả gốc.

- **Sử dụng**:
  + Node.js, Rails, jQuery, Dotnet Core.
  + Rất phổ biến trong các dự án web và ứng dụng hiện đại.

- **Ưu điểm**: linh hoạt, không hạn chế sử dụng thương mại, đơn giản.
- **Nhược điểm**: có thể bị "lợi dụng" bởi các công ty có mục đích lợi nhuận cao.

**Apache License 2.0**
- **Đặc điểm**:
  + Giấy phép permissive, cho phép sử dụng thương mại, sửa đổi và phân phối tự do.
  + Không yêu cầu công khai mã nguồn đã sửa đổi.
  + Cung cấp bảo vệ pháp lý rõ ràng về bằng sáng chế.
  + Chi tiết hơn MIT, bao gồm điều khoản về bằng sáng chế và trách nhiệm.

- **Sử dụng**:
  + Apache Web Server, Hadoop, Spark, Kafka, Android.
  + Được sử dụng bởi nhiều công ty lớn.

- **Ưu điểm**: cung cấp bảo vệ pháp lý tốt, tương thích với GPL v3.
- **Nhược điểm**: dài hơn MIT, có thể phức tạp hơn cho các dự án nhỏ.

**BSD License (2-Clause và 3-Clause)**
- **Đặc điểm**:
  + Giấy phép permissive tương tự MIT nhưng có thêm một số điều khoản.
  + 2-Clause BSD (Simplified BSD): gần giống MIT, chỉ yêu cầu ghi nhận tác giả.
  + 3-Clause BSD (New BSD): thêm điều khoản không sử dụng tên của người sáng tạo để quảng cáo phần mềm đã sửa đổi.

- **Sử dụng**:
  + Flask, Bottle, NumPy.
  + Phổ biến trong các dự án Python.

- **Ưu điểm**: đơn giản, linh hoạt, cho phép sử dụng thương mại.
- **Nhược điểm**: không yêu cầu công khai sửa đổi nên có thể mất dấu hiệu cộng đồng.

**GNU Affero General Public License (AGPL)**

- **Đặc điểm**:
  + Giấy phép copyleft dựa trên GPL nhưng bổ sung yêu cầu quan trọng.
  + Nếu phần mềm AGPL được sử dụng qua mạng (ví dụ: dịch vụ web), mã nguồn đã sửa đổi cũng phải được công khai.
  + Ngăn chặn các công ty sử dụng phần mềm AGPL mà không công khai sửa đổi của mình.

- **Sử dụng**:
  + MongoDB, Mastodon, Nextcloud (tuỳ chọn).
  + Ít phổ biến hơn GPL nhưng ngày càng tăng.

- **Ưu điểm**: đảm bảo tính công khai ngay cả với dịch vụ web.
- **Nhược điểm**: chặt chẽ nhất, có thể hạn chế sử dụng.