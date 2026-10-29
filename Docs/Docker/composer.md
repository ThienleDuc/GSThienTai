# Khởi động tất cả service (foreground, hiển thị log)
docker compose up

# Khởi động nền (detached)
docker compose up -d

# Khởi động và force rebuild image trước
docker compose up -d --build

# Dừng và xóa container + network (giữ volume)
docker compose down

# Dừng và xóa container + network + volume (MẤT DỮ LIỆU!)
docker compose down -v

# Dừng container nhưng KHÔNG xóa
docker compose stop

# Khởi động lại các service đã dừng
docker compose start

# Khởi động lại một service cụ thể
docker compose restart <service-name>

# Xem trạng thái các service
docker compose ps

# Xem log tất cả service
docker compose logs

# Xem log và follow một service cụ thể
docker compose logs -f <service-name>

# Vào shell trong container của service
docker compose exec <service-name> bash

# Chạy một lệnh trong container mới (không ảnh hưởng container đang chạy)
docker compose run --rm <service-name> <command>

# Build lại image của service
docker compose build <service-name>

# Build không dùng cache
docker compose build --no-cache <service-name>

# Scale service (ví dụ chạy 3 instance web)
docker compose up -d --scale web=3

# Xem cấu hình cuối cùng sau khi merge (hữu ích để debug)
docker compose config

# Chỉ định file compose khác
docker compose -f <file-path> up -d