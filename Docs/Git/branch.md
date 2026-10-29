# Liệt kê nhánh local
git branch

# Liệt kê cả nhánh remote
git branch -a

# Tạo nhánh mới (chưa chuyển)
git branch <branch-name>

# Chuyển nhánh (cách cũ)
git checkout <branch-name>

# Chuyển nhánh (cách mới, khuyến nghị từ Git 2.23+)
git switch <branch-name>

# Tạo và chuyển ngay sang nhánh mới
git checkout -b <branch-name>
# hoặc
git switch -c <branch-name>

# Xóa nhánh đã merge (an toàn)
git branch -d <branch-name>

# Xóa nhánh chưa merge (cưỡng bức)
git branch -D <branch-name>

# Đổi tên nhánh hiện tại
git branch -m <new-name>