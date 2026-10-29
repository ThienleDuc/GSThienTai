# Khởi động môi trường dev (DB, cache, ...)
docker compose up -d postgres redis

# Kiểm tra service đã lên chưa
docker compose ps

# Xem log nếu có lỗi
docker compose logs -f postgres

# Vào DB để kiểm tra
docker compose exec postgres psql -U postgres

# Dừng môi trường khi hết giờ
docker compose down