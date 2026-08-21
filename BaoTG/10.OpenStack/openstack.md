# TÌM HIỂU VỀ OPENSTACK
## OPENSTACK LÀ GÌ ?
- OpenStack là một platform điện toán đám mây nguồn mở hỗ trợ cả public clouds và private clouds. Nó cung cấp giải pháp xây dựng hạ tầng điện toán đám mây đơn giản, có khả năng mở rộng và nhiều tính năng phong phú. Được bắt đầu bởi NASA và Rackspace, Openstack sẽ cung cấp và phân phối nền tảng lưu trữ và điện toán đám mây.

![openstack](./images/openstack_2.png)

- Tóm lại, để trả lời câu hỏi Openstack là gì. Hiểu đơn giản, thì OpenStack chính là một hệ thống mã nguồn mở ảo hay còn gọi là một hệ điều hành ảo cho phép người dùng có thể nghiên cứu, chỉnh sửa, quản lý thông tin của mình một cách phù hợp, hiệu quả theo nhu cầu của họ.

## CÁC TÍNH NĂNG CỦA OPENSTACK
OpenStack sở hữu một bộ tính năng nổi bật, giúp doanh nghiệp vận hành hạ tầng cloud theo mô hình tự động và linh hoạt. Cụ thể:
**Kiến trúc module linh hoạt**
- OpenStack được xây dựng theo kiến trúc module với nhiều project độc lập như Nova, Neutron, Swift, Cinder, Keystone và Glance. Doanh nghiệp có thể triển khai toàn bộ hệ thống hoặc chỉ lựa chọn những thành phần phù hợp với nhu cầu sử dụng.
- Nhờ cách thiết kế này, OpenStack có thể đáp ứng nhiều quy mô triển khai khác nhau, từ môi trường thử nghiệm nhỏ cho đến hệ thống cloud lớn trong doanh nghiệp.
**Hỗ trợ đa người thuê**
- OpenStack hỗ trợ mô hình multi-tenancy, cho phép nhiều nhóm người dùng cùng sử dụng chung một hạ tầng vật lý nhưng vẫn được tách biệt về tài nguyên, mạng, máy ảo và lưu trữ.
- Tính năng này đặc biệt phù hợp với doanh nghiệp có nhiều phòng ban, nhiều nhóm kỹ thuật hoặc nhiều dự án cần vận hành song song trên cùng một nền tảng cloud.
**Mã nguồn mở và dễ tùy chỉnh**
- Là nền tảng mã nguồn mở, OpenStack cho phép doanh nghiệp sử dụng, tùy chỉnh và mở rộng theo nhu cầu riêng. Đây là lợi thế lớn đối với các tổ chức muốn chủ động về công nghệ và hạn chế phụ thuộc vào một nhà cung cấp cloud duy nhất.
- Bên cạnh đó, OpenStack cũng có thể tích hợp với nhiều công cụ trong hệ sinh thái DevOps, giám sát, bảo mật và tự động hóa hạ tầng.
**Kiến trúc phân tán**
- Các dịch vụ trong OpenStack có thể được triển khai trên nhiều máy chủ khác nhau. Nhờ đó, hệ thống có thể mở rộng theo chiều ngang, tăng khả năng sẵn sàng và giảm ảnh hưởng khi một node gặp sự cố.
- Đây là yếu tố quan trọng đối với các hệ thống cloud cần phục vụ nhiều người dùng, xử lý khối lượng tài nguyên lớn hoặc yêu cầu tính ổn định cao.
**Điều khiển thông qua API**
- Hầu hết thao tác trong OpenStack đều có thể được thực hiện thông qua API. Điều này giúp quản trị viên dễ dàng tích hợp OpenStack với các công cụ tự động hóa như Ansible, Terraform hoặc các quy trình Infrastructure as Code.
- Thay vì xử lý thủ công từng tác vụ, đội ngũ kỹ thuật có thể tự động hóa việc tạo máy ảo, cấp phát mạng, cấu hình lưu trữ và quản lý tài nguyên theo các kịch bản đã định sẵn.
**Dashboard quản trị trực quan**
- OpenStack cung cấp Horizon, một dashboard quản trị dựa trên giao diện web. Thông qua Horizon, người dùng có thể tạo máy ảo, quản lý volume, cấu hình mạng, theo dõi tài nguyên và thực hiện nhiều tác vụ quản trị cơ bản.
- Nhờ có giao diện trực quan, việc sử dụng OpenStack trở nên dễ tiếp cận hơn, đặc biệt với những người dùng không muốn phụ thuộc hoàn toàn vào dòng lệnh.
**Gom tài nguyên thành pool chung**
- OpenStack có khả năng gom các tài nguyên rời rạc trong trung tâm dữ liệu thành một pool tài nguyên chung. Khi người dùng yêu cầu tạo máy ảo hoặc cấp phát lưu trữ, hệ thống sẽ tự động điều phối tài nguyên phù hợp.
- Cơ chế này giúp doanh nghiệp sử dụng tài nguyên hiệu quả hơn, đồng thời hạn chế tình trạng lãng phí phần cứng trong quá trình vận hành.

## ƯU NHƯỢC ĐIỂM CỦA OPENSTACK
### Ưu Điểm:
- Tiết kiệm chi phí: OpensTack mà phần mềm mã nguồn mở được phát hành miễn phí theo giấy phép Apache 2.0.
- Độ tin cậy cao: OpenStack gồm có nhiều mô đun cho phép các doanh nghiệp xây dựng và vận hành đám mây riêng hoặc công cộng 
với nhiều khả năng như mở rộng lưu trữ, nâng cao hiệu suất, bảo mật dữ liệu và quy mô sử dụng lớn.
- Nhà cung cấp trung lập: không có bất kỳ hạn chế nào bởi OpenStack là một phần mềm mã nguồn mở.
### Nhược Điểm:
- Việc triển khai OpenStack đòi hỏi nhiều kỹ năng gây tốn thời gian và chi phí.
- Gây khó khăn trong việc hỗ trợ quản lý chất lượng các dự án ngoài cộng đồng mã nguồn mở.
- Ngừng hỗ trợ các phiên bản thành phần cũ khi có phiên bản mới thay thế.

## CÁC THÀNH PHẦN CỦA OPENSTACK
- OpenStack hoạt động theo kiến trúc module, bao gồm 6 thành phần chính đảm nhiệm mọi chức năng, từ tính toán, kết nối mạng và lưu trữ để phục vụ các yêu cầu VM theo nhu cầu sử dụng của người dùng. Ngoài ra, trong OpenStack sẽ có rất nhiều thành phần phụ khác hỗ trợ các tính năng bổ sung, bao gồm bảng điều khiển, Containers, quản lý bảo mật, đo từ xa và Bare Metal Provisioning. 
- Để đơn giản hóa việc sử dụng tất cả các thành phần này, nhiều doanh nghiệp thường sử dụng OpenStack Charms để việc thiết lập và vận hành OpenStack được diễn ra hoàn toàn tự động. Dưới đây, cùng tìm hiểu kỹ hơn về từng thành phần trong OpenStack:

![architecture](./images/openstack_1.png)

### Nova
- Nova là phần khá quan trọng trong hệ thống OpenStack, là nơi cung cấp nguồn lực về tính toán, thực hiện quản lý máy ảo và tự động hóa việc triển khai các chu kỳ lưu trữ trong môi trường đám mây.
- Trong cấu trúc Nova được phân làm nhiều phân nhánh khác nhau để hỗ trợ thực hiện các công việc chung: Nova API cung cấp giao diện lập trình tính toán, Nova Scheduler quyết định nơi triển khai máy ảo, Nova Database là nơi lưu trữ thông tin.

![nova](./images/openstack_3.png)

### Glance
- Chịu trách nhiệm quản lý và cung cấp các hình ảnh (images) cho máy ảo (instances) trong môi trường đám mây, Glance là nơi cho phép thực hiện các thao tác tạo, đọc, cập nhật và xóa hình ảnh trên Openstack.
- Các chức năng này làm việc dưới sự hỗ trợ của các thành phần Glance API, Glance Registry, Glance Store và Glance Database.
- Khi người dùng tiến hành thực hiện thao tác chỉnh sửa hình ảnh từ máy chủ, Glance API sẽ nhận diện thông tin và xử lý, API kiểm tra tên, định dạng và kích thước trong Glance Registry thông qua việc theo dõi quản lý thông tin từ Glance Database và cuối cùng sẽ được lưu trữ tại Glance Store.

![glance](./images/openstack_4.png)

### Neutron
- Cũng như các thành phần khác trong Openstack Neutron đảm bảo việc kết nối giữa máy ảo và mạng vật lý linh hoạt hơn, bằng việc quản lý cấu hình mạng và các dịch vụ mạng khác nhau trong hệ thống OpenStack.
- Hệ thống API Neutron tiếp nhận các hoạt động cập nhật hay xóa tài nguyên mạng, Neutron Plugin tương tác với các tài nguyên mạng như Virtual Network, Load Balancer, VPN, và các plugin khác, trong khi đó Neutron Database sẽ theo dõi tiến trình này và Neutron Agent là bộ phận trung tâm quản lý kết nối mạng cho máy ảo, xử lý thông tin mạng từ Compute Nodes hoặc Network Nodes.

![neutron](./images/openstack_5.png)

### Cinder
Cinder là nơi lưu trữ, chịu trách nhiệm chính về việc cung cấp, quản lý và kết thúc các thiết bị khối liên tục (Persistent Block Devices - PBD). Chúng có thể được tích hợp vào các phiên bản khởi chạy của OpenStack để hỗ trợ việc lưu trữ các PBD.

### Swift
- Swift trong Openstack là nơi lưu trữ và quản lý dữ liệu metadata khối lượng lớn, được chia nhỏ ra thành Swift Proxy Server, Swift Storage Nodes và Swift Rings.
- Tại đây Swift Proxy Server xác thực yêu cầu từ người dùng, sau đó chuyển tiếp thông tin đến các Storage Nodes, còn Swift Rings xác định vị trí của đối tượng (Object) trên các Storage Nodes, giúp xác định nơi dữ liệu được lưu trữ (Container).

### Keystone
Keystone là thành phần giúp nhận dạng, cung cấp các tính năng về xác thực và ủy quyền cho người dùng để nhiều người thuê dịch vụ. Doanh nghiệp có thể dễ dàng tích hợp Keystone với các hệ thống nhận dạng của bên thứ ba, ví dụ như Active Directory hoặc là các giao thức truy cập gọn nhẹ (Lightweight Directory Access Protocol - LDAP).

## PHÂN BIỆT OPENSTACK, VMWARE VÀ KVM
- OpenStack, VMware và KVM đều liên quan đến điện toán đám mây và ảo hóa, nhưng mỗi công nghệ đảm nhiệm một vai trò khác nhau trong kiến trúc hạ tầng. Bảng dưới đây sẽ giúp làm rõ sự khác biệt giữa ba nền tảng này.

|      Tiêu chí     |                                  OpenStack                                  |                            VMware                            |                            KVM                           |
|:-----------------:|:---------------------------------------------------------------------------:|:------------------------------------------------------------:|:--------------------------------------------------------:|
| Bản chất          | Nền tảng quản lý cloud mã nguồn mở                                          | Hệ sinh thái ảo hóa và cloud thương mại                      | Công nghệ ảo hóa cấp hypervisor                          |
| Vai trò chính     | Quản lý compute, storage, networking, identity và API                       | Quản lý ảo hóa, hạ tầng doanh nghiệp và cloud                | Chạy máy ảo trên nền Linux                               |
| Mã nguồn          | Mã nguồn mở                                                                 | Độc quyền thương mại                                         | Mã nguồn mở                                              |
| Phạm vi sử dụng   | Private cloud, public cloud, hạ tầng IaaS                                   | Ảo hóa doanh nghiệp, data center, cloud hybrid               | Lớp ảo hóa cho máy chủ Linux                             |
| Mức độ quản lý    | Quản lý hạ tầng cloud nhiều thành phần                                      | Quản lý ảo hóa và hạ tầng theo hệ sinh thái VMware           | Không phải nền tảng quản lý cloud hoàn chỉnh             |
| Chi phí bản quyền | Không tốn phí bản quyền phần mềm gốc, nhưng tốn chi phí triển khai/vận hành | Thường có chi phí bản quyền cao                              | Không tốn phí bản quyền                                  |
| Đối tượng phù hợp | Doanh nghiệp có đội ngũ kỹ thuật mạnh, cần cloud tùy biến                   | Doanh nghiệp cần nền tảng ổn định, hỗ trợ thương mại rõ ràng | Admin/Linux engineer cần hypervisor mạnh, gọn, linh hoạt |

- Tóm lại, KVM, VMware và OpenStack nằm ở ba lớp khác nhau trong hệ sinh thái cloud. Việc lựa chọn OpenStack, VMware hay KVM phụ thuộc vào mục tiêu triển khai và năng lực vận hành của từng hệ thống. 

- OpenStack phù hợp với các tổ chức muốn tự chủ về hạ tầng cloud, cần khả năng tùy chỉnh sâu và hạn chế phụ thuộc vào một nhà cung cấp duy nhất. VMware là lựa chọn đáng cân nhắc khi ưu tiên sự ổn định, hệ sinh thái hoàn thiện và hỗ trợ thương mại rõ ràng. Trong khi đó, KVM phù hợp với những hệ thống cần một lớp ảo hóa nhẹ, hiệu quả và tối ưu chi phí trên nền tảng Linux.

## CÁCH OPENSTACK HOẠT ĐỘNG
