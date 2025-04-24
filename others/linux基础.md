1. 系统
文件操作
        open
        close
    读写操作:
        read
        write
    文件指针操作:
        lseek
    文件控制:
        fcntl
    内存映射:
        mmap
        munmap
    文件属性管理
    元数据获取:
        stat
        lstat
    权限/所有权:
        chmod
        chown
        fchown
        lchown
    文件描述符复制:
        dup 
    文件截断:
        truncate
        ftruncate
目录操作
    创建/删除:
        mkdir
        rmdir (仅能删除空目录)
    目录流操作:
        opendir (返回目录流指针)
        readdir
        closedir
    工作目录:
        chdir
        getcwd (标准库函数，非系统函数)
链接与同步
    硬链接/符号链接:
        link (创建硬链接)
        symlink (创建符号链接)
        readlink (读取符号链接目标)
        unlink (删除文件或符号链接)
    数据同步:
        fsync (同步文件数据和元数据)
        fdatasync (仅同步文件数据)
        sync (同步所有缓冲区)
临时文件    
mkstemp（系统调用，直接创建并返回文件描述符）

2. c标准库
1. 文件打开/关闭
标准库函数：
FILE *fopen(const char *path, const char *mode);
int fclose(FILE *stream);

2. 文件读写
标准库函数：

size_t fread(void *ptr, size_t size, size_t nmemb, FILE *stream);
size_t fwrite(const void *ptr, size_t size, size_t nmemb, FILE *stream);
int fprintf(FILE *stream, const char *format, ...);
int fscanf(FILE *stream, const char *format, ...);

3. 文件定位
int fseek(FILE *stream, long offset, int whence);
long ftell(FILE *stream);
void rewind(FILE *stream);

4. 文件状态与错误处理
char *strerror(int errno);（将错误码转为可读字符串，属于 <string.h>）
int feof(FILE *stream);（检查文件结束标志）
int ferror(FILE *stream);（检查文件错误标志）
5. 缓冲区控制
int fflush(FILE *stream);（强制刷新缓冲区，底层可能调用 write）
setbuf / setvbuf（设置缓冲区模式）
6. 临时文件
FILE *tmpfile(void);（创建自动删除的临时文件，底层可能调用 open + unlink）
char *tmpnam(char *s);（生成临时文件名，不安全）





io复用

elect/poll/epoll


IPC
    pipe
    fifo
    POSIX 消息队列
    POSIX 共享内存
    POSIX 信号量
    Socket
    文件锁定(File Locking)
    mmap
信号