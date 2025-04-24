1. http过程
    用户->>浏览器: 输入URL (e.g. https://www.example.com)
    浏览器->>DNS: 域名解析 (查询IP地址)
    DNS-->>浏览器: 返回IP (e.g. 93.184.216.34)
    浏览器->>服务器: 建立TCP连接 (三次握手)
    浏览器->>服务器: 发送HTTP请求 (GET /)
    服务器-->>浏览器: 返回HTTP响应 (HTML/CSS/JS)
    浏览器->>浏览器: 解析渲染页面

    步骤1：DNS 域名解析
    过程：
        浏览器检查本地缓存（如 Chrome 的 chrome://net-internals/#dns）。
        查询系统 hosts 文件（如 /etc/hosts）。
        向配置的 DNS 服务器发起递归查询（如 8.8.8.8）。
    输出：
        将域名转换为 IP 地址（如 www.example.com → 93.184.216.34）。

    步骤2：建立 TCP 连接
    三次握手：
        客户端发送 SYN 包（序列号 x）。
        服务端回复 SYN-ACK（序列号 y，确认号 x+1）。
        客户端发送 ACK（确认号 y+1）。
        HTTPS 额外步骤：TLS 握手（协商加密算法、交换密钥）。

    步骤3：发送 HTTP 请求
        GET / HTTP/1.1
        Host: www.example.com
        User-Agent: Mozilla/5.0
        Accept: text/html,application/xhtml+xml
        Connection: keep-alive

    步骤4：服务器处理请求
        Nginx（反向代理） → 应用服务器（如Node.js） → 数据库
        动态内容生成（如PHP/Python）：
            1.解析请求路径和参数。
            2.执行业务逻辑（查询数据库）。
            3.生成HTML响应。

    步骤5：返回 HTTP 响应
        HTTP/1.1 200 OK
        Content-Type: text/html; charset=UTF-8
        Content-Length: 1354
        <!DOCTYPE html>
        <html>
        <head><title>Example</title></head>
        <body>...</body>
        </html>

    步骤6：浏览器渲染
        解析HTML：构建DOM树。
        加载子资源：CSS/JS/图片（可能触发新的HTTP请求）。
        执行JavaScript：修改DOM/CSSOM。
        布局与绘制：生成渲染树（Render Tree），最终显示页面。