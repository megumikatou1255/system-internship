# TÌM HIỂU DHCP
## I. DHCP LÀ GÌ ?
### 1. KHÁI NIỆM DHCP
- DHCP được viết tắt từ cụm từ Dynamic Host Configuration Protocol (có nghĩa là Giao thức cấu hình máy chủ). DHCP có nhiệm vụ giúp quản lý nhanh, tự động và tập trung việc phân phối địa chỉ IP bên trong một mạng. Ngoài ra DHCP còn giúp đưa thông tin đến các thiết bị hợp lý hơn cũng như việc cấu hình subnet mask hay cổng mặc định.
![Khái niệm DHCP](./images/khai_niem.png)

### 2. CHỨC NĂNG CỦA DHCP
- *Cấp IP tự động*: Tự động gán địa chỉ IP duy nhất cho từng thiết bị, tránh lỗi trùng lặp IP trong mạng.
- *Phân phối thông số mạng*: Cung cấp thông tin về Subnet Mask (mạng con), Gateway (cổng mặc định) và máy chủ DNS để thiết bị hiểu và giao tiếp được với internet.
- *Tiết kiệm thời gian*: Quản trị viên không cần phải cấu hình IP bằng tay cho từng máy, giúp việc thêm/bớt thiết bị cực kỳ dễ dàng

### 3. DHCP GỒM NHỮNG THÀNH PHẦN NÀO
![Thành phần](./images/thanh_phan.png)
- **DHCP Client**
DHCP Client là thiết bị yêu cầu và nhận thông tin cấu hình mạng từ DHCP Server. Các thiết bị như máy tính, điện thoại, hoặc máy in đóng vai trò làm DHCP Client khi cần kết nối mạng. Chúng gửi yêu cầu để nhận địa chỉ IP và các thông số mạng như Subnet Mask, Gateway, và DNS Server. Sau khi nhận được thông tin từ DHCP Server, DHCP Client sử dụng các thông số này để kết nối và giao tiếp trong mạng.

- **DHCP Server**
DHCP Server là máy chủ hoặc thiết bị chịu trách nhiệm cấp phát địa chỉ IP và thông số mạng cho các DHCP Client. Nó lưu trữ một dải địa chỉ IP để phân phối, đồng thời quản lý thông tin thuê địa chỉ IP (DHCP Lease). Ngoài ra, DHCP Server cung cấp các thông tin mạng quan trọng như Subnet Mask, Gateway, và DNS Server, đảm bảo các thiết bị trong mạng có thể kết nối và giao tiếp một cách hiệu quả.

- **DHCP Relay agents**
DHCP Relay Agents là các thiết bị trung gian, đảm nhiệm vai trò chuyển tiếp gói tin DHCP giữa Client và Server khi chúng không nằm trong cùng một mạng (khác Subnet). Relay Agent nhận các gói tin từ DHCP Client trong mạng con và chuyển tiếp chúng đến DHCP Server. Sau khi Server phản hồi, Relay Agent gửi lại thông tin cho Client. Thành phần này rất hữu ích trong các hệ thống mạng lớn, nơi DHCP Server không được triển khai trong từng mạng con.

- **DHCP Lease**
DHCP Lease là khoảng thời gian mà DHCP Server cấp phát địa chỉ IP cho một thiết bị cụ thể. Thời gian thuê này được quản lý để tối ưu hóa việc sử dụng tài nguyên địa chỉ IP trong mạng. Khi thời gian thuê sắp hết, DHCP Client có thể yêu cầu gia hạn để tiếp tục sử dụng địa chỉ IP đó. Nếu không có yêu cầu gia hạn, địa chỉ IP sẽ được giải phóng và tái sử dụng cho thiết bị khác, giúp đảm bảo việc quản lý IP hiệu quả.

- **DHCP Binding**
DHCP Binding là bản ghi lưu trữ trong DHCP Server, chứa thông tin ánh xạ giữa địa chỉ IP được cấp và địa chỉ MAC của thiết bị nhận. Đây là cơ chế giúp DHCP Server ghi lại các thông tin cấp phát, đảm bảo tính nhất quán và minh bạch trong quản lý mạng. Ngoài ra, DHCP Binding cũng hỗ trợ cấp phát địa chỉ IP cố định (Reservation) dựa trên địa chỉ MAC của thiết bị, rất hữu ích cho các thiết bị cần sử dụng một IP cụ thể, chẳng hạn như máy in hoặc máy chủ trong mạng.

### 4. CÁC THÔNG ĐIỆP CỦA DHCP.
![Các thông điệp trong DHCP](./images/thong_diep.png)
- **DHCP Discover**
DHCP Discover là thông điệp đầu tiên do DHCP Client gửi đi dưới dạng broadcast để tìm kiếm DHCP Server khả dụng trong mạng. Đây là tín hiệu “xin chào” từ Client để yêu cầu Server cung cấp địa chỉ IP và các thông số mạng khác. Do Client chưa có địa chỉ IP, gói tin được gửi đến địa chỉ broadcast (255.255.255.255). Thông điệp này khởi đầu quá trình cấp phát IP trong giao thức DHCP.

- **DHCP Offer**
DHCP Offer là thông điệp phản hồi từ DHCP Server gửi đến Client sau khi nhận được gói DHCP Discover. Thông điệp này chứa một địa chỉ IP khả dụng cùng các thông số mạng như Subnet Mask, Gateway, và DNS Server. Đây là bước “đề nghị” của Server để Client lựa chọn. Nếu trong mạng có nhiều DHCP Server, Client có thể nhận được nhiều gói DHCP Offer từ các Server khác nhau.

- **DHCP Request**
DHCP Request là thông điệp Client gửi đến Server để xác nhận việc chấp nhận địa chỉ IP được cung cấp trong DHCP Offer. Thông điệp này thể hiện ý định của Client muốn sử dụng địa chỉ IP cụ thể từ một Server. Nếu Client nhận được nhiều gói DHCP Offer, nó sẽ chỉ chọn một và gửi DHCP Request đến Server đã cung cấp địa chỉ được chọn.

- **DHCP Acknowledge**
DHCP Acknowledge là thông điệp từ DHCP Server xác nhận việc cấp phát địa chỉ IP và hoàn tất quá trình cấu hình mạng. Khi nhận được gói tin này, Client chính thức sở hữu địa chỉ IP cùng các thông số mạng. Server cũng cung cấp thêm thông tin như thời gian thuê địa chỉ IP (Lease Time) để Client sử dụng.

- **DHCP Nak (Negative Acknowledge)**
DHCP Nak là thông điệp từ DHCP Server gửi đến Client để từ chối yêu cầu cấp phát địa chỉ IP. Điều này xảy ra khi yêu cầu của Client không hợp lệ, như khi Client yêu cầu một địa chỉ IP đã hết hạn hoặc không thuộc phạm vi cấp phát của Server. Thông điệp này buộc Client phải bắt đầu lại quá trình cấp phát bằng việc gửi gói DHCP Discover mới.

- **DHCP Decline**
DHCP Decline là thông điệp từ Client gửi đến Server để từ chối sử dụng địa chỉ IP mà Server đã cấp phát. Thông điệp này được gửi đi khi Client phát hiện địa chỉ IP không hợp lệ, ví dụ như xảy ra xung đột địa chỉ IP trong mạng. Sau khi từ chối, Client sẽ gửi lại gói DHCP Discover để yêu cầu một địa chỉ IP khác.

- **DHCP Release**
DHCP Release là thông điệp từ Client gửi đến Server để thông báo rằng địa chỉ IP không còn được sử dụng. Thông điệp này giúp giải phóng địa chỉ IP, cho phép DHCP Server tái sử dụng nó cho các thiết bị khác. Thông điệp này thường được gửi khi Client ngắt kết nối khỏi mạng hoặc tắt thiết bị.

### 5. SƠ ĐỒ HOẠT ĐỘNG DHCP
- Đối với cách thức hoạt động của DHCP thì khá dễ hiểu, khi một thiết bị truy cập mạng yêu cầu địa chỉ IP từ một router thì ngay sau đó router sẽ gán cho một địa chỉ IP khả dụng cho phép thiết bị có thể giao tiếp trên mạng dễ dàng. Trong đó, router hoạt động như một máy chủ DHCP đối với các mô hình nhỏ hay hộ gia đình. Còn đối với các mạng lớn hơn thì router không thể quản lý được nên đóng vai trò là một máy chủ chuyên dụng để cấp địa chỉ IP.
- Cách thức hoạt động còn có thể hiểu theo một khía cạnh khác, khi một thiết bị muốn kết nối mạng thì nó sẽ gửi một yêu cầu đến máy chủ (gọi là DHCP DISCOVER). Sau khi có yêu cầu đến máy chủ thì ngay tại đó máy chủ sẽ tìm một địa chỉ IP khả dụng với thiết bị đó và cung cấp địa chỉ IP và gói DHCP OFFER.
- Ngay sau khi nhận được địa chỉ IP, thiết bị đó sẽ phản hồi lại máy chủ với gói tin DHCP REQUEST. Và đây là lúc chấp nhận yêu cầu thì máy chủ sẽ gửi tin báo nhận (ACK) để xác nhận rằng thiết bị đó đã có điạ chỉ IP và xác định được thời gian sử dụng địa chỉ IP vừa đucợ cấp đến khi có địa chỉ IP mới.

## II. ĐẶC ĐIỂM DHCP
### 1. ƯU ĐIỂM
+ _Cấu hình đáng tin cậy_: Cấu hình địa chỉ IP theo cách thủ công có thể dẫn đến sai sót. Ví dụ: nếu bạn nhập sai số hoặc gán cùng một số cho hai thiết bị, cả hai thiết bị sẽ không thể kết nối với mạng. Tự động hoá quy trình gán IP của DHCP sẽ giúp giảm những lỗi đó.
+ _Ít công việc hơn cho quản trị viên mạng_: Quản trị viên mạng sẽ mất rất nhiều thời gian và tài nguyên để định cấu hình địa chỉ IP theo cách thủ công trong những mạng lớn. DHCP sẽ giúp mọi thứ hoạt động hiệu quả hơn.
+ _Sửa đổi trong thời gian thực_: Quản trị viên có thể thực hiện những thay đổi đối với tùy chọn DHCP trong mạng ngay cả khi máy chủ DHCP đang chạy và cấp phát địa chỉ IP.
+ _Miễn phí_: Đối với hầu hết hệ thống mạng, việc triển khai DHCP là hoàn toàn miễn phí.
+ _Hỗ trợ nhiều thiết bị trên một mạng_: DHCP cho phép bạn kết nối và lướt web trên bất kỳ thiết bị nào bạn chọn mà vẫn có trải nghiệm liền mạch.

### 2. NHƯỢC ĐIỂM
+ _Bảo mật_: Máy chủ DHCP không có cách nào để xác thực những máy khách yêu cầu địa chỉ IP. Vì vậy, khách hàng có thể truy cập vào những địa chỉ IP trái phép bằng cách giả vờ là một khách hàng khác.
+ _Ảnh hưởng đến máy khách khi gặp lỗi_: Nếu một mạng chỉ có một máy chủ DHCP và nó bị lỗi, máy khách sẽ không thể truy cập vào web cho đến khi lỗi DHCP được khắc phục.
+ _Cần tác nhân chuyển tiếp cần thiết_: Máy chủ DHCP phải có tác nhân chuyển tiếp để có thể giao tiếp với mạng vì dữ liệu DHCP không thể truyền qua bộ định tuyến.
+ _Không có IP tĩnh_: Không thể sử dụng những máy tính được kết nối với mạng có triển khai DHCP làm máy chủ vì địa chỉ IP của chúng luôn thay đổi.
+ _Theo dõi hoạt động trên Internet_: Việc theo dõi hoạt động trên Internet sẽ trở nên khó khăn hơn với DHCP vì cùng một thiết bị có thể có hai địa chỉ IP trở lên trong một khoảng thời gian nhất định.
