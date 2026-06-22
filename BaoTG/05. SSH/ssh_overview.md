# TỔNG QUAN VỀ SSH
## 1. KHÁI NIỆM.
- SSH, hay Secure Shell, là một giao thức mạng cho phép một máy tính kết nối an toàn với một máy tính khác qua mạng không bảo mật như internet, bằng việc có một thỏa thuận chung về cách thức liên lạc. SSH là một giao thức application layer, là layer thứ 7 của mô hình OSI.
## 2. KHI NÀO NÊN SỬ DỤNG SSH.
Nên sử dụng SSH trong tất cả các trường hợp cần tương tác với máy tính/máy chủ từ xa thông qua mạng Internet hoặc mạng nội bộ:
+ Quản trị Máy chủ từ xa: Khi bạn thuê VPS trên Cloud (AWS, Azure, DigitalOcean) hoặc dựng máy ảo VMware, bạn không thể ngồi trước màn hình vật lý của chúng. SSH là cách duy nhất để bạn bốc terminal của chúng về máy mình để gõ lệnh.
+ Thay thế các giao thức kém an toàn: Bắt buộc phải dùng SSH thay thế cho Telnet, Rsh, rlogin khi quản lý các thiết bị mạng như Switch, Router Cisco.
+ Quản lý mã nguồn với Git: Khi bạn đẩy code (git push) lên GitHub hoặc GitLab, giao thức SSH Key thường được dùng để định danh tài khoản của bạn một cách tự động và bảo mật mà không cần nhập đi nhập lại mật khẩu.

# 3. CÁC CHỨC NĂNG CHÍNH CỦA SSH.
|                   Chức năng chính                   |                                                            Mô tả chi tiết                                                           |                                          Ứng dụng thực tế                                          |
|:---------------------------------------------------:|:-----------------------------------------------------------------------------------------------------------------------------------:|:--------------------------------------------------------------------------------------------------:|
| Quản lý từ xa (Remote Command Execution)            | Cho phép đăng nhập và thực thi mọi câu lệnh trên máy chủ từ xa giống như đang ngồi trực tiếp trước máy đó.                          | Chạy lệnh cấu hình NTP, cài phần mềm, khởi động lại dịch vụ qua Terminal.                          |
| Truyền file an toàn (Secure File Transfer)          | Sử dụng các giao thức con chạy trên nền SSH là SFTP hoặc SCP để gửi/nhận file được mã hóa giữa các máy.                             | Kéo thả file mã nguồn, file script .sh từ Windows lên Ubuntu bằng MobaXterm/FileZilla.             |
| Xác thực an toàn (Authentication)                   | Hỗ trợ nhiều cơ chế xác thực từ cơ bản (mật khẩu) cho đến nâng cao (SSH Key Pair, xác thực 2 lớp - 2FA).                            | Sử dụng cặp khóa id_rsa và id_rsa.pub để đăng nhập không cần mật khẩu.                             |
| Đường hầm bảo mật (SSH Tunneling / Port Forwarding) | Tạo ra một đường hầm mã hóa để bọc các giao thức không an toàn khác bên trong nó, giúp dữ liệu của ứng dụng đó đi qua mạng an toàn. | Truy cập vào một Database (MySQL/PostgreSQL) đang bị chặn cổng trong mạng nội bộ của công ty.      |
| Chạy ứng dụng đồ họa (X11 Forwarding)               | Cho phép truyền giao diện đồ họa (GUI) của một ứng dụng chạy từ máy Linux từ xa hiển thị lên màn hình máy Windows của bạn.          | Mở một trình duyệt hoặc một công cụ cài đặt có giao diện trên Ubuntu Server hiển thị trên Windows. |