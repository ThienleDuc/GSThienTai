# Xem trạng thái file (đỏ = chưa stage, xanh = đã stage)
git status

# Xem trạng thái dạng ngắn gọn
git status -s

# Stage một file
git add <file>

# Stage tất cả thay đổi (bao gồm file mới, sửa, xóa)
git add .

# Chỉ stage các file đã được track (không thêm file mới)
git add -u

# Bỏ stage một file (giữ nguyên thay đổi trong working directory)
git reset <file>

# Xem thay đổi chưa stage
git diff

# Xem thay đổi đã stage
git diff --staged