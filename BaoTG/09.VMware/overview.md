# TÌM HIỂU TỔNG QUAN VỀ CÁC CÔNG NGHỆ CẦN HỌC ĐỂ VẬN HÀNH MORPHEUS
## Lộ trình
### Mức 1: Nền tảng cốt lõi (Bắt buộc phải vững)
Đây là các kỹ năng cơ sở để hiểu và vận hành hệ thống trước khi tự động hóa:
- **Quản trị Linux nâng cao (RHEL):**
    - Quản trị dịch vụ (systemd), cấu hình mạng tĩnh/động, phân quyền, quản lý tiến trình.
    - Kỹ năng xử lý sự cố qua file log (/var/log/messages, /var/log/morpheus/).
- **Kỹ thuật đóng gói Image (Image Baking & Templates):**
    - Nhiệm vụ : Đóng gói và import image cho Jump Host, Checkpoint, F5, vDBF, ELK, Zabbix.
    - Công nghệ: Chuyển đổi và tối ưu template trên VMware (.ova, .ovf, VM Template) và OpenStack Glance (qcow2, raw).
    - Công cụ chuẩn hóa: cloud-init (trên Linux) và Sysprep (trên Windows) để máy ảo tự nhận hostname, user, SSH key khi sinh ra từ image.
- **Mạng & Cân bằng tải cơ bản đến trung cấp:**
    - Khái niệm mạng phân đoạn: VLAN, VXLAN, Subnet, Routing, NAT.
    - Hiểu kiến trúc vận hành của Firewall (Stateful Inspection, Access Rules) và Load Balancer (Pool, Node, VIP, Virtual Server, cơ chế High Availability Active/Standby).
### Mức 2: Hạ tầng Ảo hóa & Đám mây (Southbound Infrastructure)
Danh sách công việc ghi rõ yêu cầu tích hợp đồng thời cả VMware VCF và Red Hat OpenStack:
- **VMware Cloud Foundation (VCF):**
    - Quản trị cụm vSphere / vCenter.
    - VMware NSX: Hiểu cơ chế định tuyến phân tán (Tier-0 / Tier-1 Gateway), phân đoạn mạng (Segments), tích hợp API để Morpheus có thể gọi lệnh tự tạo mạng.
- **Red Hat OpenStack Platform (RHOSP):**
    - Keystone: Quản lý Identity và Project (tương ứng với Tenant/VPC).
    - Nova: Quản lý tài nguyên tính toán (Compute/Flavor).
    - Neutron: Cấu hình mạng ảo (Network, Subnet, Router, Security Groups, Floating IP).
    - Cinder & Swift/Ceph: Quản lý Block Storage, File Storage và Object Storage.
- **Lưu trữ chuyên dụng (File & Object Storage):**
    - Nhiệm vụ : Tích hợp quy trình cấp phát File Storage và Object Storage.
    - Công nghệ: Giao thức NFS/SMB (cho File Storage), giao thức S3 API / Ceph RadosGW / Swift (cho Object Storage).
### Mức 3: Tự động hóa & Khung làm việc trên Morpheus (Core Workflow)
Phần lớn đầu việc yêu cầu "Viết workflow", "Tự động khởi tạo", "Tự động config IP/rule":
- **Scripting & Tự động hóa:**
    - Bash Shell & PowerShell: Viết script cài đặt agent tự động (cho vAV, vDLP, vEDR, Zabbix) ngay khi máy ảo vừa boot.
    - Ansible: Viết Playbook cấu hình dịch vụ, đẩy cấu hình rule mạng, triển khai phần mềm sau khi máy ảo được tạo (Post-provisioning tasks).
    - Python: Dùng thư viện requests để tương tác trực tiếp với REST API của các thiết bị mạng/bảo mật.
- **Morpheus Engine & Automation Tools:**
    - Morpheus Tasks & Workflows: Phối hợp các bước Provisioning, Teardown, Startup.
    - Morpheus Layouts & Blueprints: Thiết kế mẫu kiến trúc triển khai HA cho vFW và vLB.  
    - Morpheus Cypher & Context Variables: Quản lý biến bảo mật (passwords, tokens) truyền vào trong quá trình chạy workflow.
- **API của các thiết bị mạng & bảo mật:**
    - Checkpoint Management API: Viết lệnh tạo Object, Policy Rule, cài đặt policy tự động.
    - F5 BIG-IP iControl REST API: Viết lệnh tạo VIP, gán Pool member, cấu hình Health Check tự động.
### Mức 4: Tích hợp Hệ sinh thái Vận hành, Giám sát & An toàn thông tin
Các dịch vụ dùng chung bắt buộc phải tích hợp vào quy trình vận hành:
- **Giám sát & Quản lý Log:**
    - Zabbix: Cơ chế Zabbix Agent, Zabbix Proxy, cách dùng API của Zabbix để tự động đăng ký host (Auto-registration) khi Morpheus sinh ra máy ảo mới.
    - Elasticsearch / Logstash / Kibana (vELK): Đóng gói cụm SIEM, cấu hình Filebeat/Logstash để thu thập log tập trung.
- **Bảo mật & Giám sát Endpoint:**
    - PAM (Privileged Access Management): Hiểu cơ chế phân quyền tài khoản đặc quyền, cấu hình Jump Host và gọi API của hệ thống PAM để tự động thêm máy chủ Jump vào quản lý.
    - Security Endpoints (vAV, vDLP, vEDR): Quản lý cài đặt agent ở mức silent (chạy ngầm không giao diện), xác thực license key tự động khi tạo máy ảo.
- **Sao lưu dữ liệu doanh nghiệp (Veritas NetBackup):**
    - Nhiệm vụ : Phát triển module tích hợp Morpheus với Veritas, viết workflow cấp phát.
    - Công nghệ: NetBackup REST API (tạo backup policy, thêm client vào policy, kích hoạt snapshot/backup, truy vấn trạng thái job khôi phục).
### Mức 5: Lập trình tích hợp & Tùy biến cấp cao (Advanced CMP)
Nhóm công việc này yêu cầu kỹ năng lập trình phần mềm để mở rộng chính Morpheus:
- **Xác thực tập trung & Phân quyền (SSO / IAM):**
    - Nhiệm vụ : Viết luồng tích hợp SSO với TTDL.
    - Công nghệ: Giao thức SAML 2.0 và OpenID Connect (OIDC) / OAuth2 (thường tích hợp qua Keycloak, Microsoft Entra ID hoặc ADFS).
- **Phát triển Plugin cho Morpheus (Morpheus Plugin Development):**
    - Nhiệm vụ : Viết plugin chuyển ngữ tiếng Việt, phát triển module tích hợp Veritas/Storage.
    - Công nghệ: Java / Groovy và Morpheus Java Core SDK. Cần hiểu cấu trúc một plugin Morpheus (Custom UI Tab, Custom Backup Provider, Custom Task Type, Localization bundles).
- **Quy trình Quản lý Dịch vụ CNTT (ITSM):**
    - Nắm vững chu trình ITIL: Service Request, Change Request, Incident Management để ánh xạ luồng phê duyệt (Approval Policies) trên Morpheus đúng với quy trình thực tế của đơn vị.   