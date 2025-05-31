## ✅ 一、Git 冲突的常见场景

### 🔹 1. **合并冲突（merge conflict）**

> 当你执行 `git merge` 时，如果你和别人**修改了同一个文件的同一行内容**，Git 无法自动判断要保留哪一份，就会产生冲突。

比如：

```
bash复制编辑git checkout main
git pull
git merge feature-branch
```

------

### 🔹 2. **变基冲突（rebase conflict）**

> 当你使用 `git rebase` 把当前分支的提交“挪动”到另一个分支后面，如果存在相同位置的修改，也会产生冲突。

```
bash


复制编辑
git rebase main
```

------

### 🔹 3. **拉取远程冲突**

> 当你执行 `git pull`（默认是 fetch + merge），如果你本地改动和远程仓库的修改冲突，也会导致合并失败。

```
bash


复制编辑
git pull origin main
```

------

### 🔹 4. **Cherry-pick 或 Stash pop 冲突**

> 这类操作本质上也会把提交套用在当前分支上，也可能冲突。

## ✅ 二、冲突后的 Git 会做什么？

Git 会在**冲突的文件中插入标记**，比如：

```
diff复制编辑<<<<<<< HEAD
本地修改
=======
远程或目标分支的修改
>>>>>>> main
```

你需要手动修改这些内容，保留正确的部分，然后重新提交。

------

## ✅ 三、解决 Git 冲突的步骤（标准流程）

```
bash复制编辑# 1. 查看冲突状态
git status

# 2. 打开发生冲突的文件，手动解决冲突（删除 <<<<<<< 和 >>>>>>>）

# 3. 将已解决的文件标记为已解决
git add <filename>

# 4. 继续合并或变基
# 合并时：
git commit
# Rebase 时：
git rebase --continue

# 如果不想合并了：
git merge --abort 或 git rebase --abort
```

------

## ✅ 四、冲突处理建议（加分点）

- **使用工具辅助**：如 VS Code、WebStorm、GitKraken 提供图形化的冲突解决界面。
- **提前避免冲突**：
  - 频繁 `pull`，减少分歧；
  - 尽量细化分支、避免多人同时改动同一文件；
- **保持沟通**：协作开发中，及时沟通比硬合并更重要。

------

## ✅ 五、一句话总结（面试收尾）：

> Git 冲突本质上是对同一内容的不同修改导致无法自动合并，一般在 merge、rebase 或 pull 过程中出现。关键是**理解发生的原因**，然后**手动干预并继续流程**。