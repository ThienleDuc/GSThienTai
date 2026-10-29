# 1. Cập nhật nhánh chính
git checkout main
git pull origin main

# 2. Tạo nhánh feature
git switch -c feature/ten-task

# 3. Code...

# 4. Stage và commit
git add .
git commit -m "feat: mo ta ngan gon"

# 5. Push nhánh lên remote
git push -u origin feature/ten-task