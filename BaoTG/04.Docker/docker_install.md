# CÁCH CÀI ĐẶT DOCKER
## CÀI ĐẶT TRÊN WINDOWS
- Để cài đặt Docker trên Windows, ta có thể tải file cài đặt trực tiếp trên trang chủ tại link
https://docs.docker.com/desktop/setup/install/windows-install/

## CÀI ĐẶT TRÊN UBUNTU SERVER 24.04
- Để cài đặt Docker trên Ubuntu, ta sẽ tiến hành thực hiện các bước sau đây
**Bước 1: Cập nhật hệ thống và cài đặt các gói phụ trợ**
```console
sudo apt update && sudo apt upgrade -y
sudo apt install -y ca-certificates curl gnupg
```
+ `ca-certificates`: Cung cấp danh sách các chứng chỉ số tin cậy. Giúp máy ảo Ubuntu xác thực được chứng chỉ SSL/TLS khi tải file bảo mật qua HTTPS từ trang chủ Docker.
+ `curl`: Công cụ dòng lệnh dùng để tải dữ liệu/file từ các máy chủ qua giao thức HTTP/HTTPS.
+ `gnupg (GnuPG)`: Công cụ mã hóa và quản lý khóa OpenPGP. Nó được dùng ở bước tiếp theo để giải mã và xác thực chữ ký số của Docker.

**Bước 2: Thêm GPG Key chính thức của Docker**
`sudo install -m 0755 -d /etc/apt/keyrings` Tạo ra thư mục lưu trữ khóa bảo mật /etc/apt/keyrings với quyền 0755 (Owner có quyền Đọc/Ghi/Chạy, người khác chỉ có quyền Đọc/Chạy).
`sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc` Tải về Khóa công khai (Public GPG Key) chính thức của Docker và lưu thành file docker.asc.
`sudo chmod a+r /etc/apt/keyrings/docker.asc` Phân quyền cho phép tất cả các người dùng và dịch vụ hệ thống trên máy tính có thể đọc file khóa này.

*Giải thích:* Để đảm bảo tính an toàn chống tấn công độc hại (Man-in-the-middle / Supply chain attack). Khi cài bất kỳ gói phần mềm nào từ Docker, trình quản lý gói apt sẽ dùng khóa GPG này để kiểm tra chữ ký số. Nếu gói phần mềm bị ai đó chỉnh sửa hay chèn mã độc trên đường truyền, apt sẽ từ chối cài đặt ngay lập tức.

**Bước 3: Thêm repo của Docker vào APT**
``` bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
Tác dụng:
+ Tạo ra một file cấu hình nguồn tải phần mềm mới có tên là /etc/apt/sources.list.d/docker.list.
arch=$(dpkg --print-architecture): Tự động nhận diện kiến trúc CPU của máy bạn (ví dụ: amd64 cho PC/Server x86, hoặc arm64 cho chip Apple Silicon/Raspberry Pi).
+ signed-by=/etc/apt/keyrings/docker.asc: Ép trình quản lý apt bắt buộc phải kiểm tra gói tải về bằng đúng file khóa GPG đã tạo ở Bước 2.
+ $VERSION_CODENAME: Tự động lấy tên mã của phiên bản Ubuntu hiện tại (ví dụ: Ubuntu 24.04 sẽ là noble, Ubuntu 22.04 sẽ là jammy).
Kết quả: Đoạn lệnh này ghi vào file một đường dẫn kho tải có dạng:
deb [arch=amd64 signed-by=...] [https://download.docker.com/linux/ubuntu](https://download.docker.com/linux/ubuntu) noble stable

**Bước 4: Cài đặt các gói thành phần của Docker**
```console
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
- Tác dụng
+ *docker-ce (Community Edition):* Trái tim của Docker (Docker Engine / dockerd). Dịch vụ chạy ngầm quản lý mạng, container, volume, image.
+ *docker-ce-cli:* Công cụ dòng lệnh (Command Line Interface) cung cấp lệnh docker ... để bạn gõ và tương tác với Docker Engine.
+ *containerd.io:* Core ảo hóa thực sự bên dưới. Đây là Runtime quản lý vòng đời container chuẩn OCI (Open Container Initiative) mà Docker (và cả Kubernetes) sử dụng để trực tiếp gọi lệnh tới nhân (Kernel) Linux.
+ *docker-buildx-plugin:* Công cụ nâng cấp giúp đóng gói (build) Image nhanh hơn, hỗ trợ biên dịch Image đa kiến trúc CPU (chạy được trên cả x86 và ARM).
+ *docker-compose-plugin:* Tích hợp sẵn công cụ Docker Compose (dùng lệnh docker compose thay vì docker-compose cũ) để quản lý chạy nhiều container qua file .yml.

- Sau khi đã cài đặt xong, chúng ta cần kiểm tra Docker đã chạy chưa
```console
sudo systemctl status docker
```
Nếu chưa chạy thì sử dụng lệnh
```console
sudo systemctl enable docker
```