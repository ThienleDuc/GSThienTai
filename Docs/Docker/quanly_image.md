# Tải image từ registry (Docker Hub)
docker pull <image-name>:<tag>
# Ví dụ:
docker pull nginx:1.25

# Liệt kê image local
docker images

# Build image từ Dockerfile trong thư mục hiện tại
docker build -t <image-name>:<tag> .

# Build với file Dockerfile chỉ định
docker build -f <dockerfile-path> -t <image-name>:<tag> .

# Xóa image
docker rmi <image-id>

# Xóa image không dùng (dangling)
docker image prune

# Xem lịch sử các layer của image
docker history <image-name>