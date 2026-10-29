# Cất tạm thay đổi chưa commit
git stash

# Xem danh sách stash
git stash list

# Áp dụng stash gần nhất (giữ stash trong list)
git stash apply

# Áp dụng stash cụ thể
git stash apply stash@{0}

# Áp dụng stash và xóa khỏi list
git stash pop