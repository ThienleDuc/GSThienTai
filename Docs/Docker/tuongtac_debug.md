# Xem log container
docker logs <container-id>

# Xem log và theo dõi real-time (follow)
docker logs -f <container-id>

# Xem 50 dòng log cuối
docker logs --tail 50 <container-id>

# Xem log kèm timestamp
docker logs -t <container-id>

# Vào shell bên trong container đang chạy
docker exec -it <container-id> bash
# (nếu image dùng Alpine, thử /bin/sh)
docker exec -it <container-id> sh

# Xem thống kê tài nguyên (CPU, RAM, I/O) real-time
docker stats

# Xem tiến trình bên trong container
docker top <container-id>

# Copy file từ host vào container
docker cp <file-path> <container-id>:<path-in-container>

# Copy file từ container ra host
docker cp <container-id>:<path-in-container> <file-path>