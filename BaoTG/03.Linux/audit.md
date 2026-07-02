# TÌM HIỂU VỀ AUDITD
## KHÁI NIỆM
- auditd (Linux Audit Daemon) chính là "camera giám sát" tối cao của hệ điều hành Linux. Nó là một dịch vụ chạy ngầm ở tầng hệ thống, có nhiệm vụ theo dõi, ghi lại một cách chi tiết và không thể chối cãi mọi hành vi can thiệp vào Nhân Linux (Kernel).

- Khác với các file log thông thường như syslog hay journald (vốn chỉ ghi lại thông báo từ các phần mềm), auditd bắt lấy các System Calls (Lời gọi hệ thống). Điều này có nghĩa là cho dù một user cố tình che giấu hành vi bằng cách xóa lịch sử gõ lệnh (history -c), mọi hành động đọc, ghi file hay chạy phần mềm của họ vẫn bị auditd tóm gọn.

## CÁCH THỨC HOẠT ĐỘNG CỦA AUDITD
- Hệ thống auditd được chia làm hai không gian làm việc rõ rệt:
+ Tầng Nhân (Kernel Space): Nơi đây chứa các bộ lọc (như audit_filter). Khi có bất kỳ một hành động nào xảy ra (ví dụ: mở file, đổi IP, gọi lệnh sudo), Kernel sẽ kiểm tra xem hành động đó có nằm trong danh sách cần theo dõi hay không. Nếu có, nó sẽ đẩy dữ liệu qua một hàng đợi (Netlink socket) để gửi lên tầng trên.
+ Tầng Người dùng (User Space): auditd daemon sẽ túc trực để hứng dữ liệu từ Kernel gửi lên, sau đó ghi trực tiếp vào file log tại đường dẫn `/var/log/audit/audit.log`.