# Tìm hiểu mô hình OSI
## I Mô hình OSI là gì ?
### 1. Khái niệm.
![OSI Model](./images/osi_model.png)

- Mô hình OSI là gì? Mô hình OSI (Open Systems Interconnection) là một khung làm việc cơ bản giúp hiểu và mô tả cách một hệ thống mạng hoạt động. Được phát triển bởi Tổ chức Tiêu chuẩn Hóa Quốc tế (ISO), mô hình OSI đã trở thành một nguồn kiến thức cơ bản quan trọng trong lĩnh vực mạng và truyền thông.
- Mô hình OSI chia nhỏ quá trình truyền thông mạng thành 7 tầng (layer). Mỗi tầng đảm nhiệm một chức năng cụ thể. Các chức năng này tương tác theo thứ tự từ trên xuống dưới. Các tầng trong mô hình OSI gồm: Physical, Data Link, Network, Transport, Session, Presentation và Application. Mô hình OSI đưa ra các giao thức, tiêu chuẩn cho mỗi tầng để đảm bảo các thiết bị mạng khác nhau có thể giao tiếp, kết nối với nhau.
### 2. Vai trò của mô hình OSI
>Mô hình OSI không phải là một thiết bị hay phần mềm cụ thể, mà là một khung tham chiếu với các vai trò chính:
+ **Chuẩn hóa**: Giúp các nhà sản xuất phần cứng và phần mềm tạo ra các sản phẩm có thể làm việc cùng nhau (tính tương thích).

+ **Chia nhỏ quy trình phức tạp**: Chia việc truyền tin khổng lồ thành 7 tầng nhỏ hơn, giúp việc học tập, thiết kế và quản trị mạng trở nên dễ dàng hơn.

+ **Giao diện rõ ràng**: Xác định rõ ràng các dịch vụ mà một tầng cung cấp cho tầng trên nó và cách các tầng tương tác.

+ **Hỗ trợ khắc phục sự cố (Troubleshooting)**: Giúp kỹ thuật viên khoanh vùng lỗi. (Ví dụ: Nếu dây cáp đứt, họ biết lỗi ở Tầng 1; nếu sai địa chỉ IP, họ biết lỗi ở Tầng 3).
### Ưu/ nhược điểm của mô hình OSI
> Ưu điểm
- **Tính linh hoạt**: Bạn có thể thay đổi công nghệ ở một tầng mà không ảnh hưởng đến các tầng khác. Ví dụ: Bạn thay thế cáp đồng (Tầng 1) bằng cáp quang, nhưng ứng dụng web (Tầng 7) của bạn vẫn hoạt động bình thường.

- **Dễ dàng phát triển sản phẩm**: Các nhà phát triển chỉ cần tập trung vào tầng mà sản phẩm của họ hoạt động thay vì phải thiết kế lại toàn bộ hệ thống từ đầu đến cuối.

- **Tính giảng dạy cao**: Đây là công cụ tốt nhất để đào tạo về mạng, giúp người mới bắt đầu hình dung được dòng chảy dữ liệu một cách logic.

- **Giảm thiểu sự phức tạp**: Bằng cách chia nhỏ các chức năng mạng, mô hình này giúp giảm bớt sự chồng chéo và nhầm lẫn trong thiết kế hệ thống.

> Nhược điểm
- **Tính lý thuyết thuần túy**: OSI là mô hình tham chiếu, không phải mô hình thực thi. Trong thực tế, các tầng thường bị gộp lại (như mô hình TCP/IP chỉ có 4 hoặc 5 tầng).

- **Sự trùng lặp chức năng**: Một số chức năng xuất hiện ở nhiều tầng gây lãng phí tài nguyên. Ví dụ: Việc kiểm soát lỗi (Error Control) xuất hiện ở cả Tầng 2 (Data Link) và Tầng 4 (Transport).

- **Độ trễ hệ thống**: Vì dữ liệu phải đi qua tất cả 7 tầng (thêm Header ở máy gửi và gỡ Header ở máy nhận), quá trình này đôi khi gây tốn tài nguyên CPU và làm chậm tốc độ truyền tin.

- **Phân tầng không đồng đều**: Một số tầng rất "bận rộn" và quan trọng (như Tầng 2, 3, 4), trong khi một số tầng khác lại khá ít việc (như Tầng 5 - Session và Tầng 6 - Presentation).
## II. Các lớp trong mô hình OSI
- Mô hình bao gồm 7 tầng riêng biệt nhưng chúng liên kết chặt chẽ với nhau, mỗi tầng đều có nhiệm vụ gửi/nhận dữ liệu từ tầng kề trên hoặc kề dưới nó. Tại thiết bị gửi, dữ liệu xuất phát từ tầng ứng dụng (Application layer), lần lượt được chuyển tiếp và xử lý qua mỗi tầng, cho tới tầng vật lý (Physical layer); bên nhận thu được dữ liệu từ tầng vật lý, chuyển tiếp và xử lý lần lượt qua các tầng, cho tới tầng ứng dụng, thiết bị nhận đón tiếp dữ liệu tại đây.
![OSI Layer](./images/osi_layer.png)

- Có thể hình dung việc gửi và nhận dữ liệu dựa trên mô hình OSI giống như quá trình gửi và nhận thư: dữ liệu là nội dung thư, được ghi vào giấy, cho vào phong bì thư, đóng phong bì, dán tem, cho vào hòm thư, người đưa thư chuyển thư trong hòm tới hòm thư đích, bên nhận sẽ thực hiện ngược lại các bước này, cuối cùng đọc được nội dung thư. Mỗi bước đều lấy dữ liệu từ bước trước và xử lý thêm một thao tác, dữ liệu cũng được chuyển đổi từ hình trạng này tới hình trạng khác. Trong mô hình OSI cũng vậy, tương ứng với mỗi tầng, dữ liệu được thể hiện ở một hình thái khác nhau:
![OSI Data](./images/osi_data.png)

### 1. Application Layer (Tầng ứng dụng)
- Khái niệm: Là tầng cao nhất, giao tiếp trực tiếp với người dùng qua các phần mềm.
- Chức năng:
    + Cung cấp các dịch vụ mạng cho người dùng (duyệt web, gửi email, truyền file).
    + Xác định tính sẵn sàng của đối tác liên lạc.
- Giao thức tiêu biểu: HTTP, FTP, SMTP, DNS.

### 2. Presentation Layer (Tầng trình diễn)
- Khái niệm: Đóng vai trò như một "phiên dịch viên" cho dữ liệu.
- Chức năng:
    + Định dạng dữ liệu để tầng ứng dụng có thể hiểu được (như chuyển từ ASCII sang EBCDIC).
    + Mã hóa (Encryption) và giải mã dữ liệu để bảo mật.
    + Nén dữ liệu để giảm dung lượng khi truyền đi.

### 3. Session Layer (Tầng phiên)
- Khái niệm: Thiết lập và quản lý các "cuộc hội thoại" giữa hai ứng dụng trên hai máy khác nhau.
- Chức năng:
    + Mở, duy trì và đóng các phiên giao dịch.
    + Tạo các điểm kiểm tra (Checkpoints) để nếu kết nối bị ngắt, dữ liệu có thể tiếp tục truyền từ điểm kiểm tra gần nhất thay vì gửi lại từ đầu.

### 4. Transport Layer (Tầng vận chuyển)
- Khái niệm: Chịu trách nhiệm truyền tải dữ liệu "đầu cuối đến đầu cuối" (End-to-End) giữa hai máy tính.
- Chức năng:
    + Phân đoạn dữ liệu lớn thành các đoạn nhỏ và đánh số thứ tự để máy nhận có thể ghép lại.
    + Kiểm soát luồng (Flow control) để tránh làm nghẽn máy nhận.
    + Cung cấp các giao thức tin cậy (TCP) hoặc không tin cậy (UDP).
- Đơn vị dữ liệu: Segment (TCP) hoặc Datagram (UDP).

### 5. Network Layer (Tầng mạng)
- Khái niệm: Quản lý việc định tuyến dữ liệu giữa các mạng khác nhau trên toàn thế giới.
- Chức năng:
    + Định địa chỉ logic (Địa chỉ IP).
    + Xác định đường đi tốt nhất (Routing) để gói tin đến được đích.
- Đơn vị dữ liệu: Packet.

### 6. Data Link Layer (Tầng liên kết dữ liệu)
- Khái niệm: Đảm bảo việc truyền dữ liệu giữa hai thiết bị kết nối trực tiếp trong cùng một mạng LAN.
- Chức năng:
    + Đóng gói các bit thành các khung hình (Frame).
    + Sử dụng địa chỉ vật lý (MAC Address) để định danh thiết bị.
    + Kiểm tra và sửa lỗi cơ bản xảy ra ở tầng vật lý.
- Đơn vị dữ liệu: Frame.

### 7. Physical Layer (Tầng vật lý)
- Khái niệm: Là tầng thấp nhất, làm việc trực tiếp với các thiết bị phần cứng và phương tiện truyền dẫn (cáp, sóng).
- Chức năng:
    + Chuyển đổi dữ liệu thành các xung điện, tín hiệu ánh sáng hoặc sóng vô tuyến (dòng bit 0 và 1).
    + Định nghĩa các tiêu chuẩn về điện, cơ học như hình dáng đầu cắm (RJ45), loại cáp.
- Đơn vị dữ liệu: Bit.

## III. Quy trình hoạt động của mô hình OSI
- Quy trình hoạt động của mô hình OSI dựa trên hai nguyên tắc cốt lõi: Đóng gói dữ liệu (Encapsulation) tại máy gửi và Mở gói dữ liệu (De-encapsulation) tại máy nhận. Dữ liệu sẽ đi xuyên suốt qua 7 tầng để đến được đích.

### Giai đoạn 1: Tại máy gửi (Quá trình Đóng gói)
Dữ liệu sẽ đi từ tầng cao nhất xuống tầng thấp nhất. Tại mỗi tầng (trừ tầng Vật lý), một mẩu thông tin điều khiển gọi là Header (tiêu đề) sẽ được dán thêm vào.
- Bước 1 (Application): Người dùng tạo ra dữ liệu (ví dụ: soạn tin nhắn). Tầng này xác định dịch vụ mạng phù hợp.
- Bước 2 (Presentation): Dữ liệu được chuyển đổi định dạng, nén hoặc mã hóa để đảm bảo máy nhận có thể hiểu được.
- Bước 3 (Session): Thiết lập một phiên giao dịch giữa máy gửi và máy nhận để đảm bảo luồng thông tin không bị gián đoạn.
- Bước 4 (Transport): Dữ liệu lớn được chia nhỏ thành các Segment. Tầng này thêm Header chứa số cổng (Port) và số thứ tự để máy nhận có thể ghép lại đúng cách.
- Bước 5 (Network): Segment được đóng vào Packet. Tầng này thêm địa chỉ IP nguồn và IP đích để xác định đường đi trên Internet.
- Bước 6 (Data Link): Packet được đóng vào Frame. Tầng này thêm địa chỉ vật lý (MAC Address) để truyền tải giữa các thiết bị trong cùng một mạng nội bộ.
- Bước 7 (Physical): Frame được chuyển đổi thành các dòng bit (0 và 1) và truyền đi qua dây cáp, sóng Wi-Fi hoặc cáp quang.

![OSI Progress](./images/osi_progress.png)

### Giai đoạn 2: Truyền dẫn trên môi trường mạng
- Dữ liệu dưới dạng tín hiệu vật lý sẽ di chuyển qua các thiết bị trung gian như Switch và Router.
- Router (hoạt động ở tầng 3) sẽ mở gói tin để xem địa chỉ IP đích, sau đó lại đóng gói lại để đẩy sang mạng tiếp theo cho đến khi tới đích.

### Giai đoạn 3: Tại máy nhận (Quá trình Mở gói)
Quá trình này diễn ra ngược lại hoàn toàn so với máy gửi (đi từ tầng 1 lên tầng 7). Mỗi tầng sẽ gỡ bỏ Header mà tầng tương ứng ở máy gửi đã thêm vào.
- Bước 8 (Physical): Nhận tín hiệu và chuyển đổi ngược lại thành các bit nhị phân.
- Bước 9 (Data Link): Kiểm tra địa chỉ MAC. Nếu đúng là gửi cho mình, máy sẽ gỡ bỏ Header tầng 2 để lấy Packet.
- Bước 10 (Network): Kiểm tra địa chỉ IP. Nếu đúng IP của máy, nó gỡ bỏ Header tầng 3 để lấy Segment.
- Bước 11 (Transport): Kiểm tra số thứ tự để ghép lại dữ liệu gốc. Gỡ bỏ Header tầng 4 để lấy dữ liệu ban đầu.
- Bước 12 (Session): Xác định dữ liệu này thuộc về phiên làm việc nào đang mở.
- Bước 13 (Presentation): Giải mã, giải nén dữ liệu về định dạng nguyên bản.
- Bước 14 (Application): Hiển thị nội dung tin nhắn hoặc website lên màn hình cho người dùng.