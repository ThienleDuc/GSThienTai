# Xem log đầy đủ
git log

# Xem log gọn (mỗi commit một dòng)
git log --oneline

# Xem log kèm đồ thị nhánh
git log --graph --oneline --all

# Xem 5 commit gần nhất
git log -n 5

# Xem ai đã sửa từng dòng trong file
git blame <file>

# Xem chi tiết một commit
git show <commit-hash>

# Xem lịch sử thao tác (kể cả commit đã "mất") - dùng để cứu commit
git reflog