# TÌM HIỂU VỀ AUDITD
## KHÁI NIỆM
- auditd (Linux Audit Daemon) chính là "camera giám sát" tối cao của hệ điều hành Linux. Nó là một dịch vụ chạy ngầm ở tầng hệ thống, có nhiệm vụ theo dõi, ghi lại một cách chi tiết và không thể chối cãi mọi hành vi can thiệp vào Nhân Linux (Kernel).

- Khác với các file log thông thường như syslog hay journald (vốn chỉ ghi lại thông báo từ các phần mềm), auditd bắt lấy các System Calls (Lời gọi hệ thống). Điều này có nghĩa là cho dù một user cố tình che giấu hành vi bằng cách xóa lịch sử gõ lệnh (history -c), mọi hành động đọc, ghi file hay chạy phần mềm của họ vẫn bị auditd tóm gọn.

## CHỨC NĂNG CỦA AUDITD
- Linux Audit đóng vai trò trung tâm trong việc bảo vệ và giám sát hệ thống nhờ khả năng kiểm soát và ghi nhận toàn bộ hoạt động nội bộ – từ người dùng cho đến tiến trình. Không giống các phần mềm giám sát bên ngoài, hệ thống Audit hoạt động độc lập, không cần tải thêm chương trình, giúp đảm bảo tính tự chủ và an toàn. Nhờ khả năng theo dõi mọi hành vi xảy ra trên hệ thống, Linux Audit trở thành công cụ đắc lực trong việc:
+ Phát hiện các nguy cơ tiềm ẩn hoặc hành vi bất thường trong hệ thống.
+ Hỗ trợ phân tích và điều tra khi có sự cố bảo mật xảy ra (forensics).
+ Hoạt động như một hệ thống phát hiện xâm nhập (IDS), hoặc kết hợp cùng các IDS khác để nâng cao hiệu quả bảo mật.

## CÁCH THỨC HOẠT ĐỘNG CỦA AUDITD
- Hệ thống auditd được chia làm hai không gian làm việc rõ rệt:
+ Tầng Nhân (Kernel Space): Nơi đây chứa các bộ lọc (như audit_filter). Khi có bất kỳ một hành động nào xảy ra (ví dụ: mở file, đổi IP, gọi lệnh sudo), Kernel sẽ kiểm tra xem hành động đó có nằm trong danh sách cần theo dõi hay không. Nếu có, nó sẽ đẩy dữ liệu qua một hàng đợi (Netlink socket) để gửi lên tầng trên.
+ Tầng Người dùng (User Space): auditd daemon sẽ túc trực để hứng dữ liệu từ Kernel gửi lên, sau đó ghi trực tiếp vào file log tại đường dẫn `/var/log/audit/audit.log`.


