# THỰC HÀNH CÀI MỘT SCRIPT ĐƯỢC QUẢN LÝ BẰNG SYSTEMD
- Đầu tiên tạo một Script đơn giản in ra lời chào 10 lần, sử dụng câu lệnh để tạo một file script
`sudo nano /usr/local/bin/helloworld.sh`

- Lúc này ta sẽ thêm câu lệnh vào trong file để in ra lời chào 10 lần
![systemd](../images/systemd_2.png)

#!/bin/bash
for i in {1..10}
do
    echo "Hello world ! $i"
    sleep 3
done
+ Câu lệnh đầu tiên dùng để khai báo cho hệ thống biết sẽ sử dụng phần mềm nào để chạy các câu lệnh ở dưới
+ vòng lặp sẽ in ra `Hello world !` 10 lần và mỗi lần in ra sẽ cách nhau 3 giây
+ sau khi thực hiện xong thì sẽ dừng lại

- Nhấn Ctrl + O để lưu file, và Ctrl + X để thoát cấu hình

- Bây giờ ta cần cấp quyền thực thi để systemd có quyền gọi đến file này
`sudo chmod +x /usr/local/bin/helloworld.sh`
+ chmod (chang mode) dùng để thêm quyền thực thi (`+x`, dấu cộng ở đây có nghĩa là thêm vào, x - execute - thực thi) cho file helloworld.sh

- Việc cần làm bây giờ là thêm một service nằm dưới quyền quản lý của `systemd`, ta sẽ sử dụng câu lệnh
`sudo nano /etc/systemd/system/helloworld.service`
![systemd](../images/systemd_3.png)
Trong file này ta sẽ cấu hình một vài thông tin quan trọng như sau:
+ Mô tả để khi đọc log ta biết service này sẽ làm gì (dòng 2)
+ thể loại `oneshot` chỉ chạy một lần rồi ngắt (dòng 4)
+ đường dẫn đến file script để thực thi (dòng 4)

- Bây giờ ta cần lưu file cấu hình, Ctrl + O để lưu file và Ctrl + X để thoát

- Cuối cùng, ta sẽ cho systemd nạp cấu hình mới bằng câu lệnh
`sudo systemctl daemon-reload`
Việc này là cần thiết vì khi bạn thêm một file mới trong thư mục /etc/systemd/system thì systemd sẽ không biết đến sự tồn tại của file đó, lúc này ta phải sử dụng câu lệnh trên để systemd quét lại thư mục

- Để có thể chạy được script, ta sẽ sử dụng câu lệnh sau `sudo systemctl start helloworld.service`, lúc này màn hình sẽ không hiển thị gì và con trỏ sẽ đứng im một lúc. Sau khi hoàn thành ta sẽ có thể gõ được những câu lệnh khác. Vậy làm sao để kiểm tra script đã thực hiện thành công hay chưa ?

- Bây giờ ta sẽ sử dụng câu lệnh `sudo journalctl -u helloworld` để kiểm tra log của hệ thống
![systemd](../images/systemd_4.png)

- Vậy là script đã chạy thành công
