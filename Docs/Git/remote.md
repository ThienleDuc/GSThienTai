# Xem remote hiện tại
git remote -v

# Thêm remote
git remote add origin <repository-url>

# Đổi URL remote
git remote set-url origin <new-url>

# Fetch (lấy thay đổi về nhưng KHÔNG merge)
git fetch origin

# Pull (fetch + merge)
git pull origin <branch-name>

# Pull với rebase (lịch sử thẳng, không tạo merge commit)
git pull --rebase

# Push nhánh lên remote
git push origin <branch-name>

# Push lần đầu và set upstream (các lần sau chỉ cần git push)
git push -u origin <branch-name>