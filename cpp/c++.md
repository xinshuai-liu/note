1. 用extern在头文件声明，在cpp中定义，可以保证变量不会被重复包含 如extern int a;

2. 引用&
引用是变量的别名，且在声明时必须初始化，不存在空引用，引用的类型必须与原类型完全一致

3. 
指针常量（const int*） ptr → ptr 是一个指针，指向 int 常量（值不可变）。
常量指针（int*） const ptr → ptr 是一个常量，类型是 int*（指针不可变）。

4. string

5. 多态
    定义：
        同一函数，不同行为
    目的：
        复用，灵活扩展
    使用方式：
        必须通过基类指针或引用调用函数
    概念：
        vtable通常位于只读段
        虚函数通常在代码段
        虚函数表：存有虚函数指针的指针数组
        有虚函数的多继承时，基类指针都可以接受派生类对象，但每个基类指针只能访问它所属基类的成员

    重载、重写、隐藏
        重载：相同名称，不同参数类型，个数，顺序
        重写：被重写的必须是虚函数，且是相同函数
        隐藏：派生类中有相同名称不同参数的函数（基类不是虚函数，参数可以一样）
    
    编译时多态、运行时多态
        编译时多态：函数重载、模板
        运行时多态：虚函数机制
    抽象类
    虚继承
    虚函数是如何实现运行时多态的？
        通过对象的虚表指针->虚函数表->虚函数

    为什么基类的析构函数通常要声明为虚函数？
        如果基类指针指向派生类对象时，在delete时基类指针只能使用自己的虚构函数，无法调用派生类的析构导致资源泄露

    构造函数中调用虚函数会发生什么？为什么？
        调用当前类的虚函数，派生类部分未完成构造

    final关键字在多态中有什么作用？
        用于类：禁止继承
        用于虚函数：禁止重写

    如何在没有虚函数的情况下实现多态？
        使用函数指针或std::function
        CRTP(奇异递归模板模式)：基类是模板类，将派生类自身作为模板参数传递给基类

    虚函数调用比普通函数调用慢多少？如何优化？
        通常多一次指针解引用(vptr->vtable->function)
        可能影响分支预测
        优化：
            避免不必要的虚函数
            使用final减少多态性
            模板替代虚函数
    ```cpp
    class A {
    public:
        virtual void foo() { cout << "A"; }
    };
    class B : public A {
    public:
        void foo() { cout << "B"; }
    };
    void callFoo(A a) { a.foo(); }

    int main() {
        B b;
        callFoo(b);
        return 0;
    }

    输出：A
    原因：因为B在进行值传递的时候，发生了对象切片，到函数callFoo时就变成了A

    ```

6. 内存管理
    内存布局
    new/delete,molloc/free
    内存泄漏，避免和检测
    raii
    智能指针
        unique_ptr
        shared_ptr
        weak_ptr
    常见的内存问题
        内存泄漏
        悬空指针、野指针
        双重释放
    std::move 语义
    移动构造函数/赋值
    栈内存和堆内存的区别？
    智能指针有哪些？各自特点是什么？
    什么是内存泄漏？如何检测和避免？
    shared_ptr的实现原理？
    weak_ptr的作用和使用场景？
    new/delete和malloc/free的区别？
    什么是悬空指针？如何避免？
    实现一个简易的unique_ptr
    make_shared vs new

7. STL
    基本概念：
        六大组件：容器、算法、迭代器、函数对象、适配器、分配器
    pair - 键值对
    容器：
        序列容器
            vector
            list
            deque
        关联容器
            set/multiset 
            map/multimap
        无序容器 (C++11)
            unordered_set/unordered_multiset
            unordered_map/unordered_multimap
    适配器
        stack - 栈
        queue - 队列
        priority_queue 优先队列
    算法
        std::sort(begin, end);                  // 快速排序
        std::stable_sort(begin, end);           // 稳定排序（保持相等元素相对顺序）

        auto it = std::find(begin, end, value); // 线性查找
        bool exists = std::binary_search(begin, end, value); // 二分查找（必须先排序）

        std::for_each(begin, end, [](auto& x) { /* 对x操作 */ }); // 遍历+操作

        int cnt = std::count(begin, end, value);         // 计数特定值
        int cnt = std::count_if(begin, end, predicate);  // 条件计数

        auto new_end = std::remove(begin, end, 3); // "删除"所有等于3的元素（实际是把非3元素前移）
        vec.erase(new_end, vec.end());  // 真正删除

        去除相邻重复（必须先排序）
        auto last = std::unique(begin, end);
        vec.erase(last, vec.end());

        填充/生成
        std::fill(begin, end, value);           // 填充固定值
        std::generate(begin, end, []{ return rand()%100; }); // 用函数生成

        拷贝/移动
        std::copy(src_begin, src_end, dest_begin);  // 拷贝范围
        std::move(src_begin, src_end, dest_begin);  // 移动语义(C++11)

        查找+删除组合
        vec.erase(std::remove_if(vec.begin(), vec.end(), [](int x){ return x%2==0;// 删除所有偶数 }), vec.end());

        排序+去重
        std::sort(vec.begin(), vec.end());
        vec.erase(std::unique(vec.begin(), vec.end()), vec.end());

        转换vector类型
        std::vector<int> src = {1,2,3};
        std::vector<std::string> dest;
        std::transform(src.begin(), src.end(), std::back_inserter(dest),[](int x){ return std::to_string(x); });

    常用迭代器
        begin/end    获取迭代器
        rbegin/rend  反向迭代器
        cbegin/cend  const迭代器

    

    

    
    

    

sizeof
左值，右值
C 与 C++ 的区别
C++ 的面向对象特性
指针与引用的区别
内存分配与释放
指针的运算和多级指针

const 关键字的使用
常量指针、指针常量和 const 修饰成员函数
宏与内联函数的比较
预处理器宏与 inline 的区别，宏的潜在问题
位操作和位域
如何利用位操作实现高效算法，位域在结构体中如何使用


多线程编程与并发问题
C++11 提供的线程库，线程同步机制（mutex、condition_variable 等）
内存模型与原子操作（atomic）的基本原理
虚函数表与多态实现机制
虚函数表（vtable）的工作原理
对象模型中多态与继承的内存布局问题
异常处理机制
try-catch 语句的使用，异常安全的编程实践

编写高效代码的技巧
如何在 C/C++ 中避免内存泄漏、悬空指针
代码优化：例如循环展开、缓存友好性以及编译器优化技巧
常见的面试题实例
编写一个单例模式的实现
如何实现一个简单的内存池

static 关键字的作用

局部变量：生命周期延长到程序结束，作用域不变。

全局变量/函数：限制作用域为当前文件（避免命名冲突）。

类成员：属于类而非对象，所有对象共享（如静态成员变量/函数）

宏（Macro）和内联函数（Inline Function）的区别

宏是预处理阶段的文本替换，无类型检查；

内联函数在编译时展开，有类型安全，适合短小代码。