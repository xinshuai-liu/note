1. DNS 域名解析流程
    A[浏览器] -->|1. 查询缓存| B[本地缓存]
    B -->|未命中| C[系统Hosts文件]
    C -->|未命中| D[本地DNS服务器]
    D -->|未命中| E[根DNS服务器]
    E -->|返回.com顶级域地址| D
    D -->|查询.com服务器| F[.com顶级DNS]
    F -->|返回example.com权威DNS| D
    D -->|查询权威DNS| G[example.com权威DNS]
    G -->|返回IP| D
    D -->|缓存并返回IP| A

2. 本地 Hosts 文件
    Windows	C:\Windows\System32\drivers\etc\hosts
    刷新DNS缓存：ipconfig /flushdns

    Linux/macOS	/etc/hosts
    刷新DNS缓存：sudo systemctl restart nscd  # 若使用缓存服务