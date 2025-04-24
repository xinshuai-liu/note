第一步：检查本地主机是否已经存在ssh key(id_rsa 和 id_rsa.pub)
    cd ~/.ssh
第二步：生成ssh key
    ssh-keygen -t rsa -C "xxx@xxx.com"    //执行后一直回车即可
第三步：获取ssh key公钥内容（id_rsa.pub）
    cd ~/.ssh
    cat id_rsa.pub
第四步：Github账号上添加公钥
第五步：验证是否设置成功
    ssh -T git@github.com
