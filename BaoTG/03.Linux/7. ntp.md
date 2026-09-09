# TÌM HIỂU VỀ NTP VÀ CÁCH CẤU HÌNH NTP TRÊN UBUNTU SERVER 24.04

## 1. KHÁI NIỆM
- NTP (Network Time Protocol) là giao thức hoạt động ở tầng Ứng dụng (Application Layer) trong mô hình TCP/IP (sử dụng cổng UDP 123), được thiết kế để đồng bộ hóa đồng hồ của các máy tính trong mạng theo một nguồn thời gian chuẩn xác.

- NTP hoạt động theo mô hình Phân cấp (Stratum) dạng cây:
+ Stratum 0: Là các thiết bị phần cứng đo thời gian tuyệt đối và chính xác nhất như đồng hồ nguyên tử (Atomic Clock), đồng hồ GPS, hoặc đồng hồ vô tuyến. Các thiết bị này không kết nối trực tiếp qua mạng.
+ Stratum 1: Là các máy chủ kết nối trực tiếp với thiết bị Stratum 0. Đây là những cỗ máy cung cấp thời gian trực tiếp cho mạng Internet.
+ Stratum 2: Là các máy chủ đồng bộ thời gian từ máy chủ Stratum 1 qua kết nối mạng (Hầu hết các máy chủ Ubuntu sẽ đồng bộ từ các pool ở cấp độ Stratum 2 này).
+ Stratum 3, 4...: Cấp độ càng xa Stratum 0 thì độ trễ mạng tích lũy càng lớn, nhưng độ lệch thường chỉ tính bằng mili-giây.

## 2. MỤC ĐÍCH CỦA NTP
Trong môi trường máy tính cá nhân, thời gian lệch vài phút có thể không sao. Nhưng đối với một máy chủ (Server), đặc biệt là với công việc của một Software Tester hay quản trị hệ thống, thời gian bị lệch dù chỉ vài giây cũng có thể gây ra những thảm họa sau:
- **Đảm bảo tính chính xác của file log (Liên quan đến hệ thống)**

- **Xác thực và bảo mật**
Các chứng chỉ bảo mật HTTPS (SSL/TLS) luôn có thời hạn kích hoạt và hết hạn cụ thể. Nếu đồng hồ trên Ubuntu Server bị sai lệch (ví dụ: lùi về quá khứ hoặc chạy trước tương lai), trình duyệt sẽ báo lỗi kết nối không an toàn, hoặc các phiên thiết lập SSH Key/Token Token sẽ bị từ chối do hết hạn (Expired).

- **Đồng bộ hóa Cơ sở dữ liệu**
Khi chạy các hệ thống dữ liệu lớn cần phân tán (Replication) hoặc đồng bộ giữa nhiều máy chủ, Database dựa vào mốc thời gian chính xác từng mili-giây để quyết định xem dữ liệu nào được ghi trước, dữ liệu nào ghi sau. Lệch thời gian sẽ làm hỏng tính toàn vẹn của dữ liệu (Data Integrity).

- **Chạy các tác vụ tự động**
Các kịch bản kiểm thử tự động (Automation Test scripts), tác vụ sao lưu dữ liệu (Backup) thường được lên lịch chạy vào lúc thấp điểm (ví dụ: 2 giờ sáng). Nếu không có NTP, các tác vụ này có thể chạy sai giờ, gây ảnh hưởng đến hiệu năng của hệ thống lúc người dùng đang truy cập đông.

## 3. PHƯƠNG THỨC HOẠT ĐỘNG
![NTP](./images/ntp_1.png)
- Để tính toán được độ lệch thời gian và bù trừ độ trễ mạng, NTP Client và NTP Server thực hiện một quy trình trao đổi gói tin gồm 4 mốc thời gian quan trọng:
* Client gửi yêu cầu: Client ghi lại mốc thời gian $T_1$ (thời điểm gói tin rời máy Client).
* Server nhận yêu cầu: Server nhận được gói tin và ghi lại mốc thời gian $T_2$.
* Server phản hồi: Sau khi xử lý, Server gửi gói tin trả về và ghi lại mốc thời gian $T_3$ (thời điểm gói tin rời Server).
* Client nhận phản hồi: Client nhận được gói tin từ Server và ghi lại mốc thời gian $T_4$.
- Dựa trên 4 chỉ số này, thuật toán NTP sẽ tính ra 2 giá trị cốt lõi:
+ Độ trễ đường truyền vòng về (Round-trip delay - $d$):$$d = (T_4 - T_1) - (T_3 - T_2)$$
+ Độ lệch thời gian giữa Client và Server (Offset - $t$):$$t = \frac{(T_2 - T_1) + (T_3 - T_4)}{2}$$
Sau khi tính được $t$, Client sẽ điều chỉnh lại đồng hồ của mình để khớp với Server.

## 4. CÁC CÔNG CỤ NTP PHỔ BIẾN HIỆN NAY
Tùy thuộc vào hệ điều hành và nhu cầu, người ta sử dụng các phần mềm NTP Client/Server khác nhau:
+ NTPd (Classic NTP): Bản phần mềm truyền thống lâu đời nhất, tính năng rất đầy đủ nhưng xử lý độ lệch thời gian lớn khá chậm và tốn tài nguyên hơn.
+ Chrony: Công cụ hiện đại, mặc định trên RHEL/CentOS và rất phổ biến trên Ubuntu. Chrony đồng bộ thời gian nhanh hơn, xử lý độ lệch rất tốt và cực kỳ tối ưu cho các máy ảo (VM) hoặc máy tính thường xuyên bị mất kết nối mạng.
+ systemd-timesyncd: Một dịch vụ siêu nhẹ được tích hợp sẵn trong các bản Ubuntu/Debian hiện đại. Nó chỉ làm nhiệm vụ của một NTP Client (chỉ nhận giờ về, không thể biến máy thành NTP Server phát giờ cho máy khác).

## 5. PHÂN BIỆT NTP VÀ SNTP
- Bạn có thể sẽ bắt gặp khái niệm SNTP (Simple Network Time Protocol).
+ Về cơ bản, SNTP sử dụng cùng một cấu trúc gói tin và cổng UDP 123 giống như NTP.
+ Tuy nhiên, SNTP bỏ qua các thuật toán phức tạp về tối ưu hóa độ trễ đường truyền. Nó phù hợp cho các thiết bị phần cứng có cấu hình yếu như Router nhỏ, Camera IP, thiết bị IoT - nơi không yêu cầu độ chính xác tuyệt đối từng mili-giây.

## 6. CẤU TRÚC GÓI TIN NTP (NTP HEADER)
Trong tài liệu kỹ thuật, việc mô tả cấu trúc gói tin là bắt buộc để lập trình viên hoặc kỹ sư hệ thống hiểu cách dữ liệu được truyền tải. Một gói tin NTP thô ở tầng vận chuyển (UDP) có kích thước cố định là 48 byte ở phần header (chưa tính phần mở rộng tùy chọn) với cấu trúc các trường như sau:
| Trường                     | Kích thước      | Mô tả chi tiết chức năng                                                                                                       |
|----------------------------|-----------------|--------------------------------------------------------------------------------------------------------------------------------|
| LI (Leap Indicator)        | 2 bit           | Cảnh báo giây nhuận. Hệ thống dùng trường này để thông báo xem có chèn thêm hoặc bớt 1 giây vào cuối tháng hiện tại hay không. |
| VN (Version Number)        | 3 bit           | Phiên bản của giao thức NTP (Phiên bản hiện tại phổ biến là NTPv4).                                                            |
| Mode                       | 3 bit           | Chế độ hoạt động (Ví dụ: 3 là Client, 4 là Server, 5 là Broadcast).                                                            |
| Stratum                    | 8 bit (1 Byte)  | Cấp độ phân cấp của máy chủ trong mạng lưới thời gian (Từ 0 đến 16).                                                           |
| Poll                       | 8 bit (1 Byte)  | Khoảng thời gian tối đa giữa các lần gửi gói tin liên tiếp (tính bằng lũy thừa của 2, ví dụ: $2^6 = 64$ giây).                 |
| Precision                  | 8 bit (1 Byte)  | Độ chính xác của đồng hồ trên hệ thống cục bộ (tính bằng lũy thừa của 2).                                                      |
| Root Delay                 | 32 bit (4 Byte) | Tổng độ trễ vòng về (Round-trip delay) từ máy chủ này đến nguồn thời gian gốc Stratum 0.                                       |
| Root Dispersion            | 32 bit (4 Byte) | Độ phân tán tối đa (sai số tích lũy) đối với nguồn thời gian gốc.                                                              |
| Reference ID               | 32 bit (4 Byte) | Mã định danh nguồn thời gian cụ thể (Ví dụ: Chuỗi chữ "GPS", "ATOM" hoặc địa chỉ IP của máy chủ cấp trên).                     |
| Reference Timestamp        | 64 bit (8 Byte) | Mốc thời gian hệ thống được đồng bộ lần cuối cùng.                                                                             |
| Origin Timestamp ($T_1$)   | 64 bit (8 Byte) | Mốc thời gian lúc gói tin yêu cầu rời phía Client.                                                                             |
| Receive Timestamp ($T_2$)  | 64 bit (8 Byte) | Mốc thời gian lúc gói tin yêu cầu đến phía Server.                                                                             |
| Transmit Timestamp ($T_3$) | 64 bit (8 Byte) | Mốc thời gian lúc gói tin phản hồi rời phía Server.                                                                            |

## 7. CÁC CHẾ ĐỘ HOẠT ĐỘNG (NTP MODES)
NTP hỗ trợ nhiều mô hình triển khai mạng khác nhau, bạn có thể đưa vào phần kiến trúc (Architecture) của Document:
- Client/Server Mode (Chế độ phổ biến nhất): Client chủ động gửi gói tin yêu cầu đến Server và chờ Server phản hồi. Phù hợp cho cấu hình mạng thông thường.
- Symmetric Mode (Chế độ đối xứng - Peer to Peer): Hai máy chủ NTP ngang hàng (ví dụ: hai máy chủ trong một cụm Cluster) đồng bộ qua lại với nhau để làm nguồn dự phòng, đảm bảo tính sẵn sàng cao (High Availability).
- Broadcast/Multicast Mode: Server định kỳ phát gói tin thời gian ra toàn bộ mạng LAN mà không cần chờ Client yêu cầu. Rất tiết kiệm băng thông nhưng độ chính xác thấp hơn do không tính toán được độ trễ đường truyền riêng của từng máy.