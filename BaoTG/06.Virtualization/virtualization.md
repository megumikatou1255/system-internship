# TÌM HIỂU VỀ ẢO HÓA (VIRTUALIATION)
## KHÁI NIỆM
- Ảo hóa là một công nghệ cho phép tạo ra các phiên bản ảo của các tài nguyên vật lý như máy chủ, hệ thống lưu trữ hoặc mạng máy tính. Thay vì truy cập trực tiếp vào phần cứng, người dùng làm việc thông qua các tài nguyên “ảo” được tạo ra bằng phần mềm. Điều này giúp tối ưu hóa việc sử dụng phần cứng, cải thiện hiệu suất và nâng cao khả năng quản lý hệ thống.
![](./images/virtualization_1.png)
## TẠI SAO PHẢI DÙNG ẢO HÓA
- Ảo hóa đang ngày càng trở thành yếu tố then chốt trong quản lý hạ tầng công nghệ nhờ vào những lợi ích vượt trội mà nó mang lại cho doanh nghiệp. Khi áp dụng công nghệ này, doanh nghiệp có thể tối ưu hóa việc sử dụng tài nguyên hệ thống, giảm chi phí đầu tư và vận hành, đồng thời nâng cao tính linh hoạt trong quản lý cơ sở hạ tầng CNTT.

- Thông qua ảo hóa, các máy chủ vật lý được khai thác hiệu quả hơn, giúp giảm nhu cầu đầu tư phần cứng mới mà vẫn đảm bảo hiệu suất hoạt động. Ngoài ra, khả năng mở rộng hệ thống trở nên đơn giản và nhanh chóng, đáp ứng tốt các yêu cầu thay đổi trong môi trường kinh doanh hiện đại, nơi mà sự linh hoạt và tốc độ là yếu tố sống còn.

- Một điểm nổi bật khác của ảo hóa là khả năng hỗ trợ doanh nghiệp chuyển đổi sang mô hình hạ tầng như một dịch vụ (IaaS - Infrastructure as a Service). Nhờ đó, doanh nghiệp, đặc biệt là các startup, có thể triển khai hệ thống hạ tầng mà không cần đầu tư lớn vào máy chủ vật lý hay phần cứng. Họ chỉ cần thuê tài nguyên máy chủ ảo từ nhà cung cấp dịch vụ đám mây và chỉ trả chi phí cho những gì đã sử dụng, giúp tiết kiệm tối đa ngân sách.

## LỢI ÍCH CỦA ẢO HÓA
### Tiết kiệm năng lượng, thân thiện với môi trường
- Ảo hóa giúp giảm đáng kể số lượng máy chủ vật lý cần thiết để vận hành hệ thống CNTT. Thay vì sử dụng nhiều thiết bị tiêu tốn điện năng và chi phí bảo trì, doanh nghiệp chỉ cần một số ít máy chủ vật lý để chạy nhiều máy ảo. Điều này không chỉ giúp tiết kiệm chi phí vận hành mà còn góp phần làm giảm lượng khí thải CO₂ từ các trung tâm dữ liệu, mang lại lợi ích thiết thực cho cả doanh nghiệp và môi trường.

### Tăng hiệu suất hoạt động của máy chủ
- Thông qua việc phân bổ tài nguyên linh hoạt như CPU và RAM, ảo hóa giúp các ứng dụng chạy nhanh và ổn định hơn. Trong các tác vụ đòi hỏi hiệu suất cao, chẳng hạn như xử lý dữ liệu lớn hoặc vận hành các nền tảng thương mại điện tử - máy ảo có thể được tùy chỉnh để đáp ứng tối ưu nhu cầu sử dụng. Điều này giúp giảm độ trễ, nâng cao tốc độ xử lý và đảm bảo hệ thống hoạt động mượt mà.

### Tăng thời gian hoạt động (uptime)
- Một ưu điểm nổi bật của ảo hóa là khả năng duy trì dịch vụ liên tục. Nếu một máy chủ vật lý gặp sự cố, các máy ảo có thể nhanh chóng được chuyển sang máy chủ khác mà không gây gián đoạn hoạt động. Quá trình chuyển đổi này diễn ra gần như tức thì và hoàn toàn tự động, giúp hệ thống duy trì trạng thái hoạt động 24/7, điều đặc biệt quan trọng đối với các doanh nghiệp cung cấp dịch vụ trực tuyến.

### Cải thiện khả năng khôi phục sau thảm họa (Disaster Recovery)
- Ảo hóa cho phép sao lưu và phục hồi hệ thống một cách nhanh chóng, dễ dàng. Doanh nghiệp có thể tạo bản sao đầy đủ của máy ảo và khôi phục trong vòng vài phút khi có sự cố xảy ra. Việc sao lưu liên tục còn giúp hạn chế tối đa nguy cơ mất dữ liệu, đồng thời đảm bảo hoạt động của hệ thống ngay cả trong các tình huống khẩn cấp như thiên tai hoặc hỏng hóc phần cứng.

## CÁCH THỨC HOẠT ĐỘNG CỦA ẢO HÓA
- Ảo hóa vận hành nhờ vào một phần mềm trung gian gọi là Hypervisor – thành phần đóng vai trò như "người quản lý tài nguyên" giữa phần cứng vật lý và các máy ảo (Virtual Machines – VM).

### Hypervisor
- Hypervisor (trình giám sát máy ảo) là nền tảng cốt lõi trong công nghệ ảo hóa, giúp tạo và quản lý các máy ảo, đồng thời phân bổ tài nguyên phần cứng từ máy chủ vật lý (như CPU, RAM, ổ cứng) cho các máy ảo. Có hai loại Hypervisor phổ biến:
![hypervisor type](./images/hypervisor_1.png)

#### Hypervisor type 1 (Native/Bare-metal)
- Chạy trực tiếp trên phần cứng mà không cần hệ điều hành trung gian. Đây là lựa chọn tối ưu cho doanh nghiệp lớn nhờ vào hiệu suất cao, độ ổn định tốt và khả năng quản lý tài nguyên hiệu quả.

#### Hypervisor type 2 (Hosted)
- Cài đặt và chạy trên hệ điều hành hiện có. Loại này phù hợp với môi trường nhỏ, phòng lab hoặc người dùng cá nhân do dễ sử dụng và triển khai nhanh chóng.

### Phân bổ tài nguyên linh hoạt
- Khi Hypervisor được triển khai, nó sẽ chia sẻ tài nguyên vật lý giữa các máy ảo. Mỗi VM hoạt động như một máy tính riêng biệt với hệ điều hành và ứng dụng riêng, nhưng vẫn dùng chung tài nguyên phần cứng. Hypervisor giám sát và phân bổ tài nguyên một cách hợp lý, đảm bảo hệ thống hoạt động ổn định và hiệu quả.
![](./images/hypervisor_2.png)

### Chạy nhiều hệ điều hành cùng lúc
- Một điểm mạnh của ảo hóa là khả năng chạy nhiều hệ điều hành khác nhau trên cùng một máy chủ vật lý. Nhờ đó, doanh nghiệp có thể vận hành các ứng dụng yêu cầu môi trường hệ điều hành riêng biệt mà không cần đầu tư thêm phần cứng, từ đó tăng tính linh hoạt và tiết kiệm chi phí.

### Máy ảo - hệ thống độc lập trong môi trường chia sẻ
- Mỗi máy ảo có thể được cấu hình theo nhu cầu cụ thể, với mức tài nguyên riêng (CPU, RAM, ổ cứng), tương tự như một máy tính thật sự. Các VM có thể di chuyển giữa các máy chủ vật lý mà không gây gián đoạn dịch vụ, mang lại sự linh hoạt trong quản lý và bảo trì hệ thống.

### Tối ưu hóa tài nguyên
- Hypervisor không chỉ phân bổ mà còn giám sát và tối ưu việc sử dụng tài nguyên. Nếu một VM không sử dụng hết phần tài nguyên được cấp, Hypervisor có thể tái phân bổ cho các VM khác đang cần, giúp hệ thống vận hành hiệu quả hơn và tránh lãng phí.

### Di chuyển và khôi phục dễ dàng
- Một tính năng nổi bật là live migration - cho phép di chuyển máy ảo giữa các máy chủ vật lý mà không gián đoạn dịch vụ. Điều này rất hữu ích khi cần bảo trì hoặc nâng cấp hệ thống mà không gây ảnh hưởng đến người dùng. Nếu máy chủ gặp sự cố, các VM có thể được chuyển ngay sang máy khác để duy trì hoạt động liên tục và giảm thiểu thời gian chết.

## CÁC LOẠI ẢO HÓA
![](./images/hypervisor_3.png)

### Ảo hóa máy chủ/phần cứng (Hardware / Server Virtualization)
- Đây là hình thức ảo hóa phổ biến nhất, nơi phần mềm Hypervisor được cài đặt trực tiếp hoặc gián tiếp lên máy chủ vật lý để tạo ra và quản lý các Máy ảo (Virtual Machines - VMs). Mỗi VM hoạt động độc lập với hệ điều hành và tài nguyên ảo riêng (CPU, RAM, ổ đĩa, NIC).
![](./images/hypervisor_4.png)

### Ảo hóa hệ điều hành (Operating system Virtualization)
- Thay vì dùng Hypervisor để giả lập lại toàn bộ phần cứng, loại ảo hóa này tạo ra các môi trường ảo độc lập (thường gọi là Containers) chạy trực tiếp trên cùng một Kernel của Hệ điều hành gốc (Host OS).
- Đặc điểm: Cực kỳ nhẹ, khởi động tức thì và tiết kiệm tài nguyên do dùng chung hệ điều hành mẹ.

Ví dụ: Docker containers, Linux Containers (LXC), Solaris Zones.

### Ảo hóa lưu trữ (Storage Virtualization)
- Quá trình trừu tượng hóa và hợp nhất nhiều thiết bị lưu trữ vật lý (như mảng ổ cứng SAN, NAS) từ các máy chủ khác nhau thành một vùng lưu trữ logic duy nhất (Storage Pool).
- Đặc điểm: Giúp việc phân bổ, sao lưu (snapshot), nhân bản và quản lý dung lượng ổ đĩa trở nên linh hoạt hơn mà không bị giới hạn bởi thiết bị phần cứng đơn lẻ.
- Ví dụ: Software-Defined Storage (SDS), SAN/NAS Virtualization, VMware vSAN, Ceph.
![](./images/hypervisor_5.png)

### Ảo hóa mạng (Nework Virtualization)
- Kết hợp cả thiết bị phần cứng (Switch, Router) lẫn phần mềm để mô phỏng một hạ tầng mạng hoàn chỉnh bằng phần mềm (Software-Defined Networking - SDN).
- Đặc điểm: Cho phép chia dải băng thông, tạo các mạng LAN ảo (VLAN), Switch ảo, Firewall ảo để nối các máy ảo với nhau hoàn toàn trên môi trường phần mềm.
- Ví dụ: Virtual Private Network (VPN), VLANs, VMware NSX, Cisco ACI.
![](./images/hypervisor_6.png)

### Ảo hóa máy tính (Desktop Virtualization)
- Tách biệt môi trường máy tính người dùng (màn hình, hệ điều hành, dữ liệu cá nhân) khỏi thiết bị vật lý. Toàn bộ trải nghiệm desktop được xử lý trên các máy ảo đặt tại Trung tâm dữ liệu (Data Center).
- Đặc điểm: Người dùng có thể truy cập vào máy tính làm việc của mình từ bất kỳ đâu thông qua các thiết bị như Thin Client, laptop, hay thiết bị di động.
- Ví dụ: Virtual Desktop Infrastructure (VDI), VMware Horizon, Remote Desktop Services (RDS).
![](./images/hypervisor_7.png)

### Ảo hóa ứng dụng (Application Virtualization)
- Đóng gói một ứng dụng cùng với các thư viện/dependencies cần thiết của nó để chạy cách ly hoàn toàn khỏi hệ điều hành nền bên dưới.
- Đặc điểm: Ứng dụng chạy trong một lớp ảo hóa độc lập, giúp tránh xung đột phần mềm (như cài 2 phiên bản ứng dụng khác nhau trên cùng 1 máy) mà không cần cài đặt trực tiếp vào OS.
- Ví dụ: Microsoft App-V, VMware ThinApp, Citrix XenApp.
![](./images/hypervisor_8.png)

## CÁC MỨC ĐỘ ẢO HÓA
### Full Virtualization (Ảo hóa toàn phần)
- Cơ chế: Hypervisor giả lập hoàn toàn 100% phần cứng vật lý. Dùng kỹ thuật Binary Translation (dịch mã nhị phân): khi Guest OS thực thi các lệnh đặc quyền (Ring 0 privileges), Hypervisor sẽ chặn lại, quét mã, dịch sang tập lệnh an toàn rồi mới gửi xuống CPU thật.
- Tình trạng Guest OS: Không bị chỉnh sửa (Unmodified OS). Hệ điều hành khách hoàn toàn không biết mình đang nằm trong môi trường ảo hóa.
- Đánh giá:
    + Ưu điểm: Tương thích cực cao, cài đặt được mọi OS mà không cần can thiệp mã nguồn.
    + Nhược điểm: Hiệu năng thấp nhất do tốn nhiều overhead cho việc quét và dịch tập lệnh liên tục bằng phần mềm.
- Ví dụ: VMware Workstation thế hệ đầu, VirtualBox (khi chạy ở chế độ không hỗ trợ phần cứng).

### Paravirtualization (Bán ảo hóa)
- Cơ chế: Loại bỏ hoàn toàn lớp dịch mã nhị phân phức tạp. Mã nguồn Kernel của Guest OS được chỉnh sửa để thay thế các lệnh đặc quyền bằng các lời gọi hàm trực tiếp xuống Hypervisor (gọi là Hypercall).
- Tình trạng Guest OS: Bắt buộc phải chỉnh sửa Kernel. OS biết rõ mình đang chạy trên một Hypervisor.
- Đánh giá:
    + Ưu điểm: Hiệu năng cao hơn nhiều so với Full Virtualization, độ trễ I/O (mạng, ổ đĩa) thấp.
    + Nhược điểm: Không thể chạy được các hệ điều hành đóng mã nguồn (như Windows) trừ khi có các driver paravirtualized riêng (ví dụ: virtio).
- Ví dụ: Xen (chế độ PV), KVM khi cài bộ driver virtio cho ổ cứng và cạc mạng.

### Hardware-Assisted Virtualization (Ảo hóa hỗ trợ phần cứng)
- Cơ chế: Tận dụng trực tiếp các tập lệnh ảo hóa được xây dựng sẵn bên trong CPU vật lý (Intel VT-x hoặc AMD-V). CPU cung cấp thêm các chế độ thực thi mới (Root mode cho Hypervisor và Non-Root mode cho Guest OS), cho phép Guest OS chạy các lệnh Ring 0 trực tiếp trên phần cứng mà không cần Binary Translation hay Hypercall.
- Tình trạng Guest OS: Không bị chỉnh sửa.
- Đánh giá:
    + Ưu điểm: Kết hợp hoàn hảo ưu điểm của 2 loại trên: Giữ nguyên 100% tính tương thích của Full Virtualization và đạt hiệu năng tiệm cận máy thật (Bare-metal).
    + Nhược điểm: Bắt buộc phần cứng CPU của máy chủ phải hỗ trợ và bật tính năng VT-x/AMD-V trong BIOS.

- Ví dụ: KVM, VMware ESXi, Microsoft Hyper-V, Proxmox VE. (Đây là tiêu chuẩn mặc định của hầu hết máy chủ hiện đại).

### OS-Level Virtualization (Containerization - Ảo hóa cấp Hệ điều hành)
- Cơ chế: Bỏ qua toàn bộ lớp Hypervisor và máy ảo. Tất cả các môi trường ảo (Container) dùng chung duy nhất một Kernel của máy chủ mẹ (Host OS). Sự cô lập được thực hiện nhờ các tính năng cốt lõi của Linux Kernel như Namespaces (cách ly tầm nhìn tiến trình, mạng, mount point) và cgroups (giới hạn tài nguyên CPU, RAM).
- Tình trạng Guest OS: Không có Guest OS, chỉ chứa User Space (ứng dụng và các thư viện phụ thuộc).
- Đánh giá:
    + Ưu điểm: Khởi động tức thì (mili-giây), tốn cực kỳ ít tài nguyên RAM/CPU, mật độ đóng gói ứng dụng cao gấp nhiều lần VM.
    + Nhược điểm: Mức độ cách ly an toàn kém hơn VM (nếu Kernel bị khai thác lỗi, toàn bộ container trên host đều bị ảnh hưởng); không thể chạy OS khác nhân (ví dụ: không thể chạy Container Windows trên Host Linux).
- Ví dụ: Docker, containerd, LXC/LXD, Podman.

## TẦNG ĐẶC QUYỀN (PRIVILEGE RING)
![privilege rings](./images/privilege_ring.png)
Phần cứng CPU x86 được thiết kế với 4 mức đặc quyền, đánh số từ Ring 0 đến Ring 3:
- Ring 0 (Kernel Mode - Mức cao nhất):
    + Có toàn quyền truy cập trực tiếp vào mọi tài nguyên phần cứng (CPU, bộ nhớ RAM, thiết bị I/O).
    + Chạy Nhân hệ điều hành (OS Kernel) và các Driver thiết bị.
    + Mọi lệnh đặc quyền (privileged instructions) như quản lý bảng phân trang RAM, tắt/mở ngắt (interrupts) đều chỉ được thực thi tại đây.
- Ring 1 & Ring 2:
    + Được thiết kế cho các dịch vụ hệ điều hành hoặc driver có mức đặc quyền trung gian, nhưng trên thực tế, các hệ điều hành hiện đại (Linux, Windows, macOS) gần như không sử dụng hai tầng này để đơn giản hóa kiến trúc và tối ưu hiệu năng.
- Ring 3 (User Mode - Mức thấp nhất):
    + Bị giới hạn quyền truy cập phần cứng. Các ứng dụng thông thường (Web browser, Text Editor, Docker daemon...) chạy tại đây.
    + Muốn can thiệp vào tài nguyên hệ thống (như ghi file hoặc mở kết nối mạng), ứng dụng bắt buộc phải gửi một System Call (lời gọi hệ thống) lên Ring 0 để Kernel xử lý hộ.

## Mối quan hệ giữa ảo hóa và điện toán đám mây
- Ảo hóa và điện toán đám mây có mối quan hệ mật thiết và bổ trợ lẫn nhau. Trong đó, ảo hóa đóng vai trò là nền tảng công nghệ cốt lõi giúp điện toán đám mây hoạt động linh hoạt, hiệu quả và tối ưu.
- Thông qua ảo hóa, các tài nguyên phần cứng như máy chủ, lưu trữ và mạng được chia sẻ và chuyển đổi thành các môi trường ảo. Điều này cho phép các nhà cung cấp dịch vụ đám mây dễ dàng phân phối tài nguyên theo nhu cầu mà không phụ thuộc vào cấu trúc phần cứng vật lý phức tạp.
- Vai trò cụ thể của ảo hóa trong điện toán đám mây:
    + Ảo hóa máy chủ: Tạo ra nhiều máy ảo (VM) trên một máy chủ vật lý duy nhất, giúp tối ưu hóa hiệu suất và linh hoạt trong việc phân bổ tài nguyên trong môi trường đám mây.
    + Ảo hóa lưu trữ: Kết hợp nhiều thiết bị lưu trữ thành không gian lưu trữ ảo thống nhất, giúp mở rộng dung lượng, tăng tính bảo mật và đơn giản hóa quản lý dữ liệu.
- Nhờ sự hỗ trợ từ công nghệ ảo hóa, các dịch vụ đám mây có thể cung cấp tài nguyên tính toán, lưu trữ và mạng theo mô hình "trả theo nhu cầu", cho phép doanh nghiệp truy cập và sử dụng mọi lúc, mọi nơi mà không cần đầu tư vào hạ tầng vật lý đắt đỏ.