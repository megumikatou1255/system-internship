# THỰC HÀNH LAB
## MÔ TẢ
- Lab: tạo tunnel vxlan giữa 2 máy (IP vxlan tùy chọn), ping thông nhau, bắt và phân tích gói trên interface underlay

## THỰC HÀNH
**Giai đoạn 1: Phân tích**
Phân tích sơ đồ lab như sau:
VM 1 : Ip underlay 192.168.100.20, IP VXLAN 10.0.0.1/24
VM2 : Ip underlay 1921.68.100.30, IP VXLAn 10.0.0.2/24
VNI (virtual network identifier) : 100 (đây là ID của tunnel giữa 2 máy)
Port service : 4789
**Giai đoạn 2: Tạo interface vxlan0 nối từ máy 1 sang máy 2**
- Ở màn hình terminal ta sẽ sử dụng câu lệnh
`sudo ip link add vxlan0 type vxlan id 100 remote 192.168.100.30 local 192.168.100.20 dev ens33 dstport 4789`
+ tạo card mạng ảo có tên là `vxlan0`
+ loại vxlan
+ id tunnel: 100
+ trỏ sang máy 2 có địa chỉ IP là 192.168.100.30
+ chạy trên card vật lý ens33
+ cổng dịch vụ tiêu chuẩn của vxlan 4789
- Sau khi nối từ máy 1 sang máy 2 xong, ta sẽ tiến hành đặt IP Overlay cho máy 1:
`sudo ip addr add 10.0.0.1/24 dev vxlan0`
- Bật interface vxlan0 đã khởi tạo
`sudo ip link set vxlan0 up`

**Giai đoạn 3: Tạo interface vxlan0 nối từ máy 2 sang máy 1**
- Ở màn hình terminal ta sẽ sử dụng câu lệnh
`sudo ip link add vxlan0 type vxlan id 100 remote 192.168.100.30 local 192.168.100.20 dev ens33 dstport 4789`
+ tạo card mạng ảo có tên là `vxlan0`
+ loại vxlan
+ id tunnel: 100
+ trỏ sang máy 1 có địa chỉ IP là 192.168.100.20
+ chạy trên card vật lý ens33
+ cổng dịch vụ tiêu chuẩn của vxlan 4789
- Sau khi nối từ máy 2 sang máy 1 xong, ta sẽ tiến hành đặt IP Overlay cho máy 2:
`sudo ip addr add 10.0.0.2/24 dev vxlan0`
- Bật interface vxlan0 đã khởi tạo
`sudo ip link set vxlan0 up`

**Giai đoạn 4: Mở firewall trên cả 2 máy ảo**
- Vì khi bật tường lửa, mặc định firewall sẽ chặn các gói tin đi đến cổng UDP 4789. Cho nên ta cần phải cập nhật rule trên cả 2 máy để cho phép 2 máy có thể gửi gói tin đến nhau
`sudo ufw allow 4789/udp`
`sudo ufw reload`

**Giai đoạn 5: tiến hành ping từ máy 1 -> 2, 2 -> 1 và bắt gói tin để kiểm tra**
- Để phân tích được quá trình đóng gói (encapsulation) của vxlan, ta sẽ phải bắt gói tin trên card vật lý (underlay) là ens33. Trên VM2, ta sẽ sử dụng câu lệnh sau để bắt gói tin khi đi qua cổng 4789
`sudo tcpdump -i ens33 port 4789 -vv -XX`
+ ở đây ta sẽ sử dụng công cụ tcpdump để bắt gói tin
+ card mạng ens33
+ cổng 4789
+ `vv`: hiển thị thông tin chi tiết của gói tin
+ `XX`: hiển thị toàn bộ thông tin dưới dạng mã hex và ascii để xem dữ liệu thô
