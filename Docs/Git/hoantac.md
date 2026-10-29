# Bỏ thay đổi trong working directory (chưa stage) của một file
git restore <file>

# Bỏ stage (đưa file từ staging về working directory)
git restore --staged <file>

# Undo commit gần nhất nhưng GIỮ thay đổi trong working directory
git reset --soft HEAD~1

# Undo commit và bỏ stage, giữ thay đổi trong working directory (mặc định)
git reset --mixed HEAD~1

# Undo commit và XÓA LUÔN thay đổi (nguy hiểm)
git reset --hard HEAD~1

# Tạo commit mới đảo ngược commit cũ (an toàn với nhánh đã push)
git revert <commit-hash>