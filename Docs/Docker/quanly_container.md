# Liệt kê container đang chạy
docker ps

# Liệt kê TẤT CẢ container (kể cả đã dừng)
docker ps -a

# Chạy container từ image (foreground)
docker run <image-name>

# Chạy container nền (detached)
docker run -d <image-name>

# Chạy container với tên cụ thể
docker run --name <container-name> <image-name>

# Map port host:container
docker run -p 8080:80 <image-name>

# Chạy container tương tác với shell (bash)
docker run -it <image-name> bash

# Chạy container và tự xóa khi dừng
docker run --rm <image-name>

# Khởi động container đã tạo
docker start <container-id>

# Dừng container
docker stop <container-id>

# Khởi động lại container
docker restart <container-id>

# Xóa container (phải dừng trước)
docker rm <container-id>

# Xóa container đang chạy (cưỡng bức)
docker rm -f <container-id>

# Đổi tên container
docker rename <old-name> <new-name>