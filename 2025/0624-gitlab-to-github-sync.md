# 0624-gitlab to github sync

好的，我们来 **一步一步详细讲解**如何通过 **GitLab 的 CI/CD 自动将代码同步到 GitHub**：

***

### 🎯目标

当你在 GitLab 仓库中 push 新代码时，GitLab CI/CD 会自动将最新代码推送（mirror）到 GitHub 仓库，实现两个仓库的同步。

***

### 🧱一、准备工作

#### ✅ 1. 在 GitHub 上创建一个空仓库

比如你在 GitHub 上建了：

```
https://github.com/yourusername/your-repo.git
```

> 不要加 README、LICENSE 或其他文件，保持仓库“空”。

***

#### ✅ 2. 在 GitHub 获取一个 Access Token

用于在 GitLab 的 CI/CD 脚本中自动化 push：

1. 打开 [GitHub Token 创建页面](https://github.com/settings/tokens)
2. 点击 **Generate new token (classic)**（或使用 fine-grained token，注意权限）
3. 勾选：
   * `repo`（包括 repo:status, repo\_deployment 等）
4. 创建后复制这个 Token（例如：`ghp_abc1234567890xyz`）

***

#### ✅ 3. 在 GitLab 项目中设置 CI/CD 环境变量

进入 GitLab 项目 → **Settings → CI / CD → Variables**，添加以下三项：

| Key               | Value                                           | Notes                        |
| ----------------- | ----------------------------------------------- | ---------------------------- |
| `GITHUB_REPO`     | `https://github.com/yourusername/your-repo.git` | 目标仓库地址                       |
| `GITHUB_USERNAME` | 你的 GitHub 用户名                                   | 如：yourusername               |
| `GITHUB_TOKEN`    | 你刚刚生成的 GitHub Access Token                      | 建议设置为 `Masked` 和 `Protected` |

***

### ⚙️二、配置 `.gitlab-ci.yml`

在 GitLab 项目的根目录添加或编辑 `.gitlab-ci.yml` 文件，内容如下：

```yaml
stages:
  - sync

sync_to_github:
  stage: sync
  only:
    - main  # 你可以改成你自己的主分支名，如 master
  script:
    # 设置 git 用户信息
    - git config --global user.email "ci-bot@example.com"
    - git config --global user.name "GitLab CI"

    # 克隆当前 GitLab 仓库（mirror 克隆会保留所有分支、标签等）
    - git clone --mirror "$CI_REPOSITORY_URL" mirror_repo.git
    - cd mirror_repo.git

    # 添加 GitHub 作为新的远程仓库
    - git remote add github "https://${GITHUB_USERNAME}:${GITHUB_TOKEN}@github.com/yourusername/your-repo.git"

    # 将所有分支/标签强制推送到 GitHub
    - git push --mirror github
```

***

### 🧪三、验证是否生效

1. 确保你已经 push `.gitlab-ci.yml` 到 GitLab
2. Push 任意一次代码到 `main` 分支
3. 去 GitLab → **CI/CD → Pipelines** 查看运行状态
4. 成功后，去 GitHub 检查代码是否被同步

***

### 📌 四、注意事项

#### 🚫 不建议直接写 token 到 `.gitlab-ci.yml`

* 这是安全漏洞，应通过 GitLab 的 CI/CD Variables 管理
* 用 `${GITHUB_TOKEN}` 在脚本中引用变量

#### 🧩 `--mirror` 和 `--all` 的区别

* `--mirror`：同步所有内容（包括 remote-tracking branches, refs/pull 等），会**覆盖 GitHub**
*   如果只想同步代码主分支，可以改成：

    ```bash
    git push github main
    ```

***

### 🧱五、进阶：使用 SSH 而非 Token（可选）

如果你不想使用 HTTPS+Token，也可以用 SSH Key：

1. 在 GitLab 生成一对 SSH 密钥
2. 把公钥添加到 GitHub 仓库的 `Deploy Keys`
3. 私钥作为 GitLab 的 `CI/CD Variable`（设为 `SSH_PRIVATE_KEY`）
4. 在 `.gitlab-ci.yml` 中用 `ssh-agent` 加载私钥进行同步

***

### ✅ 六、同步效果总结

你会看到：

* 每次你 push 到 GitLab 主分支，CI/CD 就自动跑一次
* 代码同步到 GitHub，保留了所有分支、tag、提交记录
* 不需要手动去 GitHub 操作，实现双端仓库同步备份

***

