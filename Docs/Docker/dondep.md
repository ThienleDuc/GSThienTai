# Xóa tất cả container đã dừng
docker container prune

# Xóa tất cả image không dùng (dangling)
docker image prune

# Xóa tất cả volume không dùng (CẨN THẬN: có thể mất dữ liệu)
docker volume prune

# Xóa tất cả network không dùng
docker network prune

# Dọn dẹp TẤT CẢ tài nguyên không dùng (container, image, network, build cache)
docker system prune

# Dọn dẹp bao gồm cả volume (nguy hiểm hơn)
docker system prune --volumes