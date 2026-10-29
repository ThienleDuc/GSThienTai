# Merge nhánh khác vào nhánh hiện tại
git merge <branch-name>

# Merge không fast-forward (tạo merge commit, giữ lịch sử rõ ràng)
git merge --no-ff <branch-name>

# Hủy merge khi đang có conflict
git merge --abort

# Tiếp tục merge sau khi đã giải quyết conflict
git merge --continue

# Rebase nhánh hiện tại lên nhánh main (làm phẳng lịch sử)
git rebase main

# Rebase tương tác 3 commit gần nhất (squash, reorder, sửa message)
git rebase -i HEAD~3