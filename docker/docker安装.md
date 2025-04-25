# 一、更新系统确保系统软件包是最新的
```bash
sudo apt update
sudo apt upgrade -y 
```
- `-y` : 自动确认安装（无需交互确认）

**如果网络管理器有问题使用**
    ``` 
    sudo systemctl restart NetworkManager.service 
    ```

# 二、安装必要的依赖
```bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
```
- `apt-transport-https` : 允许APT包管理器通过HTTPS协议传输数据
- `ca-certificates` : 提供CA根证书集
- `curl` : 命令行下载工具
- `software-properties-common` : 提供管理软件源的工具
- `-y` : 自动确认安装（无需交互确认）

# ​三、添加Docker的官方GPG密钥 为了确保下载的软件包的安全性 （可能一次不行，多运行几次）
```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```
- `-f/--fail` : 静默失败(不显示错误页面)
- `-s/--silent` :  静默模式(不显示进度)
- `-S/--show-error` : 显示错误信息
- `-L/--location` : 跟随重定向
---
- `--dearmor` : 将ASCII格式密钥转换为二进制格式
- `-o` : 指定输出文件位置
- `存储路径` : /usr/share/keyrings/ (标准密钥环目录)
    ```bash
    # 将ASCII密钥转为二进制
    gpg --dearmor -o output.gpg input.asc
    ```

# 四、添加Docker的APT源 将Docker的APT源添加到系统的源列表中
```bash
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
- `deb` : 表示二进制软件仓库
- `arch=amd64` : 限定CPU架构为amd64
- `signed-by=...` : 指定GPG密钥路径
- `https://...` : Docker官方仓库URL
- `$(lsb_release -cs)` : 自动获取当前系统代号(如focal/jammy)
- `stable` : 使用稳定版软件通道

graph LR
A[下载的docker包] --> B[用signed-by指定的GPG密钥验证]
B --> C{验证通过?}
C -->|是| D[允许安装]
C -->|否| E[拒绝安装]

# 五、更新APT包索引
```bash
sudo apt update
```

# 六、安装Docker引擎
```bash
sudo apt install docker-ce docker-ce-cli containerd.io -y
```

# 七、启动Docker并设置开机自启
```bash
sudo systemctl start docker
sudo systemctl enable docker
```

# 八、设置镜像源
```bash
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
    "registry-mirrors": [
        "https://docker.1ms.run",
        "https://docker.xuanyuan.me",
        "https://docker.mirrors.ustc.edu.cn",
        "https://rjiom0q7.mirror.aliyuncs.com"
    ]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```
（注：不行请更换镜像源）

# 九、验证Docker安装
```bash
sudo docker run hello-world
```

# 十、使用非root运行docker
1. 检查 docker 用户组是否存在
    ```bash   
    grep docker /etc/group
    ```
2. 如果docker组不存在，则创建
    ```bash
    sudo groupadd docker
    ```
3. 将指定的用户（username）添加到 docker 用户组 
    ```bash
    sudo usermod -aG docker username
    ```
    - 参数说明
        - `-a` ：追加用户到组（避免移除原有组）
        - `-G docker` ：指定目标组为 docker
        - `<username>` ：替换为实际用户名（如 ubuntu）
4. 使组权限生效
    ```bash
    newgrp docker
    ```
    (注：不行重启电脑)

5. 验证是否配置成功
    ```bash
    docker run hello-world
    ```

# 十一、安装docker compose（一个用于定义和运行多容器Docker应用程序的工具）
1. 下载最新版本的Docker Compose
    ```bash
    sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
    ```
2. 为Docker Compose二进制文件添加执行权限
    ```bash
    sudo chmod +x /usr/local/bin/docker-compose
    ```
3. 验证安装是否成功：
    ```bash
    docker-compose --version
    ```
---

    ​



