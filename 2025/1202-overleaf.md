# 1202-overleaf

***

## Overleaf CE 安装全过程总结（精简但完整）

### **1. 安装 Docker / docker compose**

你在服务器上执行：

```bash
sudo apt update
sudo apt install -y ca-certificates curl gnupg git
```

添加 Docker 源后安装：

```bash
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

验证：

```bash
docker --version
docker compose version
```

***

### **2. 获取 Overleaf Toolkit**

在你选择的目录：

```bash
git clone https://github.com/overleaf/toolkit.git /opt/overleaf-toolkit
cd /opt/overleaf-toolkit
bin/init
```

这一步生成了：

* `bin/`：管理脚本
* `config/`：配置文件目录
* `data/`：存储用户项目、数据库内容
* `docker-compose.yml`

***

### **3. 配置 Overleaf 监听端口 + 开启注册功能**

编辑：

```bash
nano config/overleaf.rc
```

你添加了：

```bash
OVERLEAF_LISTEN_IP=0.0.0.0
OVERLEAF_PORT=80
OVERLEAF_ALLOW_USER_REGISTRATION=true
OVERLEAF_EMAIL_CONFIRMATION_DISABLED=true
```

这允许用户自助注册账号，无需邮件。

***

### **4. 启动 Overleaf**

初次启动：

```bash
bin/up
```

后台运行：

```bash
bin/start
```

停止：

```bash
bin/stop
```

状态检查（重要）：

```bash
docker ps
```

应该看到：

```
sharelatex  Up
mongo       Up
redis       Up
```

***

### **5. 浏览器访问并创建管理员**

访问：

```
http://服务器IP/launchpad
```

创建管理员，之后访问：

```
http://服务器IP
```

即可登录 Overleaf。

***

### **6. 进入容器安装完整 TeX Live（关键）**

进入容器：

```bash
docker exec -it sharelatex bash
```

换国内源：

```bash
tlmgr option repository http://mirrors.tuna.tsinghua.edu.cn/CTAN/systems/texlive/tlnet
```

更新 tlmgr：

```bash
tlmgr update --self
```

安装完整 TeX Live：

```bash
tlmgr install scheme-full
```

安装成功后退出容器：

```
exit
```

***

### **7. 用户创建机制**

你开启了自助注册，因此用户可直接在登录页点击：

**Register / Sign up**

无需管理员干预。

管理员可在后台查看用户列表：

```
http://服务器IP/admin
```

***

## 强烈建议收藏：Overleaf CE 常用命令大全

### **容器管理**

#### 查看运行状态：

```bash
docker ps
```

#### 查看日志：

```bash
cd /opt/overleaf-toolkit
bin/logs sharelatex
```

或直接：

```bash
docker logs sharelatex -f
```

#### 重启全部服务：

```bash
cd /opt/overleaf-toolkit
bin/stop
bin/start
```

***

### **容器内部操作**

进入主容器：

```bash
docker exec -it sharelatex bash
```

退出容器：

```
exit
```

***

### **TeX Live 相关**

查看 TeX Live 版本：

```bash
tlmgr --version
```

查看某宏包是否存在：

```bash
kpsewhich <file>
```

例如：

```bash
kpsewhich revtex4-1.cls
kpsewhich tikz.sty
```

更新所有宏包：

```bash
tlmgr update --all
```

***

### **Toolkit 管理命令（最常用）**

在 `/opt/overleaf-toolkit` 中：

```bash
bin/up        # 前台启动
bin/start     # 后台启动
bin/stop      # 停止
bin/logs      # 查看日志
bin/upgrade   # Toolkit 更新
```

***

### **数据备份目录结构（非常重要）**

Overleaf 的用户项目、数据库等数据都保存在：

```
/opt/overleaf-toolkit/data/
```

里面包括：

* `mongo/`
* `redis/`
* `sharelatex/`（用户项目数据）

你可以定期备份这个目录即可防止数据丢失。

***

## 最后给你一句“使用 Overleaf CE 的黄金准则”

**Overleaf 的逻辑是：容器随时可以删除重建，但 `data/` 目录永远不能丢。**

只要你备份好 data/

