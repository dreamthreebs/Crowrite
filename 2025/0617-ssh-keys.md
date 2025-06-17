# 0617-ssh keys

好的，下面是从 **零开始**，一步步配置 SSH 密钥免密登录远程服务器的完整流程，适用于 macOS（包括 Warp 终端）连接 Linux 服务器的常见场景。

***

### 🎯 目标

你要实现的是：

> ✅ 本地不输密码，直接 `ssh user@server` 登录远程服务器。

***

### 🪜 操作流程（从无到有）

#### ✅ 第一步：生成 SSH 密钥对（在本地 macOS 上）

在 Warp 或终端中运行：

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

一路按回车，系统会默认生成文件：

* 私钥：`~/.ssh/id_rsa`（请勿泄露）
* 公钥：`~/.ssh/id_rsa.pub`（可以给别人）

📌 如果提示覆盖已有密钥，请确认是否继续，或给出其他名字如 `id_rsa_serverA`。

***

#### ✅ 第二步：把公钥复制到远程服务器

推荐方法（如果支持）：

```bash
ssh-copy-id username@server_ip
```

如果没有 `ssh-copy-id`，用手动方式：

```bash
cat ~/.ssh/id_rsa.pub | ssh username@server_ip 'mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys'
```

✅ 这样，服务器就“记住”你的公钥了。

***

#### ✅ 第三步：测试是否免密成功

在本地执行：

```bash
ssh username@server_ip
```

如果能直接登录，不再要求输入服务器密码，说明配置成功。

***

#### ✅ 第四步（可选）：简化登录命令

编辑文件：

```bash
nano ~/.ssh/config
```

添加内容：

```bash
Host myserver
  HostName server_ip
  User username
  IdentityFile ~/.ssh/id_rsa
```

之后你只需执行：

```bash
ssh myserver
```

***

#### ✅ 第五步（可选）：加载密钥进 SSH Agent（适用于密钥有密码的情况）

如果你在生成密钥时设置了密码短语（passphrase），你可以运行：

```bash
eval "$(ssh-agent -s)"
ssh-add -K ~/.ssh/id_rsa   # -K 仅 macOS：保存进钥匙串
```

> 若你的密钥没设置密码（多数人选择空），则这步可以跳过。

***

### ✅ 完成效果

你现在已经实现：

| 功能                    | 是否实现      |
| --------------------- | --------- |
| 安全生成密钥对               | ✅         |
| 公钥添加到远程服务器            | ✅         |
| 登录时不输入服务器密码           | ✅         |
| 本地命令更简洁（ssh myserver） | ✅         |
| （可选）私钥密码记住不再重复输       | ✅（若设置了密码） |

***

如果你希望：

* 配多个服务器免密登录
* 用不同密钥连接 GitHub / GitLab / 跳板机
* 限制某个密钥只能跑某条命令（高安全场景）

也可以告诉我，我可以帮你继续配置 `~/.ssh/config` 或高级控制项。
