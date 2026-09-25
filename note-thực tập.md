*********************************************OPENSTACK****************************************************
** Lý thuyết:
- Các service của OpenStack: OpenStack chạy những service gì trên Linux, kiểm tra service hoạt động thế nào? khi cần check log thì check ở đâu?
- Tìm hiểu về OVN network: cơ chế network giữa các máy ảo như nào, bắt log như nào, cấu hình policy như nào.
- Storage: thử triển khai ceph storage để lưu máy ảo

s** LAB:
- làm 1 con ntp server để con talos trỏ vào

** CHỈNH SỬA, BỔ SUNG

- chuyển backend glance
-tại sao lại có  glance-uwsgi.ini, nó bật service lên như thế nào
- xem queue như nào
- tìm hiểu data plane của neutron, ovs (chỉ ovs) và ovn khác nhau cái gì, nếu chỉ có ovs thì phải có những thành phần nào, l2 và l3 làm gì, nếu khi có ovn thì tại sao không cần l2 l3 agent
- khi tạo router thì ovs và ovn xuất hiện them cái gì

- cấu hình l2/l3 agent như thế nào khi tạo network thì sẽ xuất hiện gì dưới network namespace -> done
- ui của queue -> done
- tìm hiểu network trên openstack tương đương cái gì, router tương đương cái gì -> done
- network node để làm gì, trên ovn có cần hay không, gateway node làm cái gì, ovs có cần gateway node không -> done		

****************************************MORPHEUS*************************************************
> Giai đoạn 1: Nền tảng & Kiến trúc CMP (Tuần 1)	
- Mục tiêu:
    + Hiểu vai trò của Morpheus trong mối quan hệ với hạ tầng sẵn có (vCenter, NSX).	
- Nội dung tìm hiểu: 
    + Khái niệm CMP (Cloud Management Platform) vs Hypervisor thông thường.
    + Mô hình phân quyền đa khách hàng: Tenant, Group, Role, User.
    + Kiến trúc kết nối giữa Morpheus và vCenter (vcenter-new), NSX Manager (labnsx-wld01.ndc.bca).
- Thực hành:
    + Khảo sát các menu chính trên giao diện: Operations, Provisioning, Infrastructure, Administration.
    + Tạo một Sub-tenant/Group thử nghiệm và phân quyền tài khoản người dùng hạn chế.

> Giai đoạn 2: Hạ tầng Mạng & Lưu trữ (Tuần 2)
- Mục tiêu:
    + Nắm vững cách trừu tượng hóa tài nguyên mạng và IPAM.	
- Nội dung tìm hiểu:
    + Kiến trúc mạng: Segments, Routers (Tier-0/Tier-1), Network Groups.
    + Cơ chế quản lý địa chỉ IP: IP Pools, Static Pools, DHCP Profiles.
    + Bảo mật mạng vi phân đoạn: Security Groups, Tags/Labels, Firewall Rules.
- Thực hành:
    + Tạo 1 NSX Segment mới gắn với Router Tier-1.
    + Tạo 1 dải IP Pool tĩnh với Gateway và Subnet Mask hoàn chỉnh.
    + Cấu hình Security Group dùng Tag động trên NSX Integration.

> Giai đoạn 3: Đóng gói Tài nguyên & Cấp phát (Tuần 3)	
- Mục tiêu:
    + Xây dựng quy trình tự phục vụ (Self-service Provisioning) cho Dev/Ops.	
- Nội dung tìm hiểu:
    + Các đối tượng đóng gói: Virtual Images (Template/ISO), Service Plans (CPU/RAM/Disk), Node Types, Layouts.
    + Khái niệm Instance vs App (Topology đa máy chủ).
    + Tùy biến cấu hình lúc khởi tạo bằng Cloud-init và biến môi trường.
- Thực hành
    + Đăng ký một bản OS Template từ vCenter vào thư viện Virtual Images.
    + Tạo các Service Plan mẫu (Small: 1vCPU/2GB, Medium: 2vCPU/4GB).
    + Đóng gói hoàn chỉnh một Instance Type (ví dụ: Ubuntu 22.04 Nginx).
    + Chạy thử nghiệm quy trình tạo máy ảo tự động hoàn toàn từ Catalog.

> Giai đoạn 4: Vận hành Vòng đời & Tự động hóa Day-2 (Tuần 4)
- Mục tiêu:
Quản trị, giám sát và tối ưu hóa hệ thống sau khi triển khai.	
- Nội dung tìm hiểu:
    + Day-2 Operations: Snapshot, Scale-up (đổi Plan), Restart, Console.
    + Automation Tasks & Workflows: Chạy bash script, Ansible playbook sau khi dựng máy.
    + Policies: Giới hạn hạn mức (Quota), lịch tắt mở máy tự động, thời gian hết hạn (Lifecycle/Expiration).
- Thực hành:
    + Viết một Task chạy script Bash cài đặt dịch vụ tự động sau khi VM boot xong.
    + Gán chính sách Lease Policy: Tự động tắt máy sau 7 ngày nếu không gia hạn.
    + Thực hiện snapshot, nâng cấp RAM trực tiếp trên Morpheus và xóa thu hồi IP về Pool.




https://www.youtube.com/watch?v=dtjDmhgTfLU&t=4s

**Lời anh Kiên dạy**
triển khai -> mở mạng, bind port -> vận hành: logging, monitoring -> backup -> update (bảo mật, an toàn)
