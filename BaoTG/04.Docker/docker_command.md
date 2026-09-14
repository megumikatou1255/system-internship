# DOCKER COMMAND HAY DÙNG
1. Quản lý Image (Hình ảnh Docker)
docker pull <image_name>:<tag>: Tải một Docker image từ Docker Hub về máy.

docker images: Liệt kê tất cả các image đang có trên máy tính của bạn.

docker rmi <image_id>: Xóa một hoặc nhiều image không còn sử dụng.

docker build -t <image_name> .: Xây dựng một Docker image từ tệp Dockerfile trong thư mục hiện tại.

2. Quản lý Container (Môi trường chạy)
docker run -d -p <host_port>:<container_port> --name <name> <image_name>: Tạo và chạy một container mới ở chế độ nền (-d), ánh xạ cổng (-p) và đặt tên (--name).

docker ps: Liệt kê các container đang chạy.

docker ps -a: Liệt kê tất cả các container (cả đang chạy và đã dừng).

docker stop <container_id/name>: Dừng một container đang chạy một cách an toàn.

docker start <container_id/name>: Khởi động lại một container đã dừng.

docker restart <container_id/name>: Khởi động lại container.

docker rm <container_id/name>: Xóa một container đã dừng (thêm -f để xóa cả container đang chạy).

3. Gỡ lỗi và Theo dõi Container
docker logs -f <container_id/name>: Xem nhật ký (logs) hoạt động của container theo thời gian thực (-f).

docker exec -it <container_id/name> bash (hoặc sh): Truy cập vào bên trong terminal của container đang chạy.

docker stats: Theo dõi mức sử dụng tài nguyên (CPU, RAM, Network) của các container.

4. Quản lý Volume và Network (Lưu trữ và Mạng)
docker volume ls: Liệt kê các volume dữ liệu.

docker volume create <volume_name>: Tạo một volume mới để lưu trữ dữ liệu bền vững.

docker network ls: Liệt kê các mạng Docker đang có.

5. Docker Compose (Quản lý nhiều container)
docker compose up -d: Khởi chạy toàn bộ hệ thống các service được định nghĩa trong file docker-compose.yml ở chế độ nền.

docker compose down: Dừng và xoá toàn bộ container, network được tạo bởi Docker Compose.

docker compose logs -f: Xem logs của tất cả các service trong file compose.