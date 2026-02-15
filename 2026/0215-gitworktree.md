# 0215-gitworktree

`.git/objects/` 里存的是 **Git 的全部版本历史本体**\
—— 不是“diff”，不是“版本号”，而是 **完整的不可变内容对象（content-addressed objects）**

Git 只有 4 种对象：

| 类型     | 存什么  | 类比   |
| ------ | ---- | ---- |
| blob   | 文件内容 | 文件快照 |
| tree   | 目录结构 | 文件系统 |
| commit | 一次提交 | 版本节点 |
| tag    | 标签   | 书签   |

***

### 1️⃣ blob — 文件内容

最底层对象：纯字节数据

例：文件 `a.txt`

```
hello world
```

Git 会计算哈希：

```
SHA1("blob 12\0hello world\n") → 3b18e5...
```

然后存储为：

```
.git/objects/3b/18e5...
```

特点：

* 不包含文件名
* 不包含路径
* 不包含时间
* 只包含内容

👉 同内容文件在整个仓库只存一份（去重）

***

### 2️⃣ tree — 目录结构

tree 描述“这个提交里有哪些文件”

```
src/
  main.c
  util.c
README.md
```

tree 内部记录：

```
100644 blob a1b2c3 main.c
100644 blob d4e5f6 util.c
040000 tree 9a9b9c src
100644 blob ffffff README.md
```

所以：

> blob = 内容\
> tree = 文件名 + 层级关系

***

### 3️⃣ commit — 提交节点

commit 指向一个 tree + 父提交 + 元数据

内容类似：

```
tree 9f1c2e...
parent 2ab41c...
author Alice <a@b.com> 1700000000
committer Alice <a@b.com> 1700000000

fix memory leak
```

所以 commit 不是“改了什么”\
而是：

> 在时间轴上指向某个完整文件系统状态（tree）

Git 历史其实是一张 DAG：

```
A --- B --- C --- D   (main)
       \
        E --- F       (feature)
```

***

### 4️⃣ tag — 标签

给 commit 起名字

```
tag v1.0
object a1b2c3...
type commit
```

***

### 对象关系总结

```
commit
  ↓
tree
  ↓
tree
  ↓
blob
```

也就是：

> Git 保存的是一棵棵“完整文件系统快照”，而不是补丁

***

### 为什么 worktree 能共享 objects

因为这些对象全部是：

**不可变 + 内容寻址**

同一个 commit 在任何目录都表示完全相同的状态\
所以多个工作目录直接共用 `.git/objects`

***

### 看一个真实对象

你可以运行：

```
git cat-file -p HEAD
```

查看 commit

```
git cat-file -p <tree-hash>
```

查看目录

```
git cat-file -p <blob-hash>
```

查看文件内容

***

### 一句话

`.git/objects` 存的就是：

> 整个仓库从诞生到现在的所有文件内容 + 每个时刻的完整文件系统结构 + 历史关系图

工作区文件只是“把某个 commit 解压出来的结果”。
