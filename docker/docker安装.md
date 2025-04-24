一、更新系统 首先，确保您的系统软件包是最新的
    sudo apt update
    sudo apt upgrade -y
    （注：网络管理器可以有问题 sudo systemctl restart NetworkManager.service ）

二、安装必要的依赖
    sudo apt install apt-transport-https ca-certificates curl software-properties-common -y

​三、添加Docker的官方GPG密钥 为了确保下载的软件包的安全性 （可能一次不行，多运行几次）
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

四、添加Docker的APT源 将Docker的APT源添加到系统的源列表中
    echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

五、更新APT包索引
    sudo apt update

六、安装Docker引擎
    sudo apt install docker-ce docker-ce-cli containerd.io -y

七、启动Docker并设置开机自启
    sudo systemctl start docker
    sudo systemctl enable docker

八、设置镜像源
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

    （注：不行请更换镜像源）

九、验证Docker安装
    sudo docker run hello-world


十、使用非root运行docker
    先确认group存在
        grep docker /etc/group

    sudo usermod -aG docker username

十一、安装docker compose（一个用于定义和运行多容器Docker应用程序的工具）
    1.下载最新版本的Docker Compose：
        sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
    2.为Docker Compose二进制文件添加执行权限：
        sudo chmod +x /usr/local/bin/docker-compose
    3.验证安装是否成功：
        docker-compose --version




---
docker不用root权限也能执行 加入docker组
    1.检查是否有docker用户
    sudo cat /etc/group |grep docker
        docker:x:999:
    2*.如果没有手动添加
    sudo groupadd docker
    3.把普通用户添加docker用户组
    sudo gpasswd -a xsl docker
    4.重启docker
    sudo systemctl restart docker
    5.重启电脑
    ​



