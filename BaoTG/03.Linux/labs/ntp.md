## 4. CÁCH CẤU HÌNH NTP TRÊN UBUNTU SERVER 24.04
- Đầu tiên ta cần cập nhật package và tiến hành cài đặt NTP

- sử dụng câu lệnh
`sudo apt update`
`sudo apt install ntp`

- Sau khi cài đặt xong, ta sẽ tiến hành xác nhận xem NTP đã được cài đặt chưa bằng câu lệnh `ntpd -V` (lưu ý option `-V` phải viết hoa)
![NTP](../images/ntp_2.png)

Ta có thể thấy đã cài đặt thành công NTP phiên bản 1.2.2
**Lưu ý**: tại sao lại là ntpsec, hiện nay `ntpsec` (NTP Security) đã thay thế hoàn toàn `ntp` ngày xưa vì `ntpsec` là phiên bản bảo trì nâng cấp, loại bỏ các dòng code thừa thãi cũng như vá lại toàn bộ lỗ hổng bảo mật và tối ưu hóa lại tốc độ xử lý

- Tiếp theo, ta sẽ cần cấu hình lại nguồn lấy giờ trong file cấu hình, để làm được điều này ta sử dụng câu lệnh
`sudo nano /etc/ntpsec/ntp_conf`
![NTP](../images/ntp_3.png)
+ Ta cần chỉnh sửa lại server khu vực Việt Nam/Asia để lấy giờ nhanh và chính xác. Truy cập `https://www.ntppool.org/zone/vn` để lấy được thông tin server của Server Việt Nam
![NTP](../images/ntp_4.png)

- Tiến hành copy và dán vào file `ntp.conf`

- Chọn múi giờ chuẩn khu vực TP.Hồ Chí Minh/khu vực Asia
`sudo timedatectl set-timezone Asia/Ho_Chi_Minh`

- Mở tường lửa cho phép giao thức NTP hoạt động
`sudo ufw allow 123/udp`

- Khởi động lại dịch vụ `ntpsec` để áp dụng cấu hình
`sudo systemctl restart ntpsec`

- CHo phép dịch vụ NTP tự động khởi chạy cùng hệ thống
`sudo systemctl enable ntpsec`

- Kiểm tra dịch vụ NTP đã hoạt động hay chưa và các cấu hình khác
+ `sudo systemctl status ntpsec`
+ `timedatectl`

![NTP](../images/ntp_5.png)
![NTP](../images/ntp_6.png)