# CÀI ĐẶT OPENSTACK SỬ DỤNG CÔNG CỤ DEVSTACK

## THỰC HÀNH



- Khi quá trình cài đặt đã diễn ra thành công, tiến hành kiểm tra các service của openstack đang chạy trên máy bằng câu lệnh
```bash
sudo systemctl list-units --type=service "devstack@*"
```

![install](./images/1.png)

- Khi màn hình hiển thị ra như trên nghĩa là quá trình cài đặt đã thành công, bây giờ sẽ cùng phân tích các service kia là gì và có chức năng như thế nào nhé

**Keystone (Dịch vụ định danh)**
- Cách nhận biết: Chứa từ khóa keystone nguyên bản.
- Service trong danh sách:
    + devstack@keystone.service: Dịch vụ định danh trung tâm.

**Cinder (Dịch vụ lưu trữ khối)**
- Cách nhận biết: Bắt đầu bằng chữ c (viết tắt của Cinder).
- Các service trong danh sách:
    + devstack@c-api.service: Cinder API (tiếp nhận yêu cầu ổ đĩa).
    + devstack@c-sch.service: Cinder Scheduler (chọn node lưu trữ).
    + devstack@c-vol.service: Cinder Volume (tiến trình quản lý ổ đĩa thực tế).

**Glance (Dịch vụ hình ảnh)**
- Cách nhận biết: Bắt đầu bằng chữ g (viết tắt của Glance).
- Service trong danh sách:
    + devstack@g-api.service: Glance API (quản lý và cung cấp image hệ điều hành).

**Nova (Dịch vụ tính toán)**
- Cách nhận biết: Bắt đầu bằng chữ n (viết tắt của Nova).
- Các service trong danh sách:
    + devstack@n-api.service: Nova API.
    + devstack@n-api-meta.service: Nova Metadata API.
    + devstack@n-sch.service: Nova Scheduler (chọn máy chủ đặt máy ảo).
    + devstack@n-cond-cell1.service & n-super-cond.service: Nova Conductor (giao tiếp cơ sở dữ liệu).
    + devstack@n-cpu.service: Nova Compute (tiến trình quản lý KVM/máy ảo trên node).
    + devstack@n-novnc-cell1.service: Nova noVNC Proxy (truy cập màn hình console máy ảo).

**Neutron (Dịch vụ mạng)**
- Cách nhận biết: Bắt đầu bằng chữ q (bắt nguồn từ tên cũ của Neutron là Quantum).
- Các service trong danh sách:
    + devstack@q-svc.service: Neutron Server (dịch vụ mạng cốt lõi).
    + devstack@q-ovn-metadata-agent.service: OVN Metadata Agent (hỗ trợ phân giải metadata mạng tích hợp OVN).

**Các service bổ trợ khác:**
+ devstack@etcd.service: Hệ thống cơ sở dữ liệu khóa-giá trị phân tán (thường được OVN sử dụng để đồng bộ trạng thái).
+ devstack@placement-api.service: Dịch vụ Placement (theo dõi tài nguyên CPU/RAM của Nova để scheduler phân bổ chính xác).
+ devstack@dstat.service: Công cụ giám sát hiệu năng hệ thống (CPU, RAM, Disk) đi kèm của DevStack.