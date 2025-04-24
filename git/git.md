1. 初始配置
    # 设置用户名
    git config --global user.name "你的名字"
    # 设置邮箱
    git config --global user.email "你的邮箱"
    # 查看配置
    git config --list
    # 设置默认编辑器为VS Code
    git config --global core.editor "code --wait"

2. 初始化仓库
    # 新建仓库
    git init
    # 克隆现有仓库
    git clone <仓库地址>

3. 基本工作流
# 查看当前状态
git status

# 添加文件到暂存区
git add <文件名>       # 添加特定文件
git add .             # 添加所有更改

# 提交更改
git commit -m "提交信息"

# 查看提交历史
git log
git log --oneline     # 简洁版
git log --graph       # 图形化显示