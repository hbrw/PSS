# Changelogs

V0.99改进
* 重构HashTable，让结构更合理
* 添加对多PacketParse的配置文件支持，可以通过配置文件绑定指定的端口。
* 框架支持插件创建新的监听接口，并且在创建监听的时候必须指定PacketParseID。
* 提交对 cppcheck的迭代器++/--的性能警告修改
* 修改工作线程阻塞时，windows关闭bug
* 对服务器间连接open加锁，保证在异步close的时候，不影响open事件。
* 优化命名空间代码
* 在Proactor和reactor下关闭服务器间连接必须加锁，否则会引起多线程下的对方访问不一致，已修复。
* 添加细化监控内存使用量的部分。
* 支持Linux下多进程的PSS功能。
* 修正日志记录超时判断问题。
* 添加配置选项Msg_Buff_Max_Size，可以让开发者自己定义使用的包最大长度。
* 添加一个强制转义，指定pow函数参数类型。
* 修改线程统一参数导致core问题
* 去掉PACKET_HEAD这样的通用头大小声明，让代码变的更简洁。
* 统一active函数中关于线程创建参数定义。
* 按照@玉白石 的建议，合并了服务器间连接的函数优化关系，简化了代码。
* 提交在高版本G++下的一些编译警告修复。
* windows下默认生成64位PSS程序。因为默认系统都是64位了。
* 修改PSS在windows上以服务运行时关闭导致的coredump问题。
* 添加对Proactor下判定发送成功字节数一定小于等于预发送字节数

V0.98改进
* 使用HashTable替换所有框架中的map结构，极大的提升效率。
* 扩展支持数据发送后连接自动关闭接口。
* 解决一个获取工作线程ID不匹配的问题。
* 重写IPAccountIP统计逻辑。
* 添加kafka样例插件。
* 添加PSS的zookeeper插件。
* 添加自动测试工具集显示html样式。
* 插件代码自动生成功能迭代，不影响已经编写的代码。
* 新开发AutoTest功能支持多线程测试PSS。
* 添加XML2CPP中生成代码对connectID参数的追加。

V0.97改进
* 部分频繁访问的数据map替换成hash_map，提升效率
* 全部插件支持mpc编译模式，不再需要自己写makefile
* PacketParse彻底组件化，可以在框架配置文件里任意配置。
* 重新设置工作线程自检重启过程。
* 新开发了服务器间通讯数据异步接收模式，可以通过配置文件设置。
* 修复一些服务器间数据传输的BUG。
* 去掉EWOULDBLOCK的循环等待模式。
* 修复一个smtp的内存问题。
* 全部工程windows下从VS2008升级到VS2012
* 添加远程关闭服务器的功能。
* 添加新功能，支持信令对某一个监听端口达成。

V0.96改进
* 重新设计了弹性数据头信息的支持。
* 添加了插件自动生成工具，你需要学会怎么写XML就能让程序自己写插件代码。
* 整理Reactor和Proactor的消息流程，变的更合理。
* 框架支持插件自检功能。
* 根据路人甲的建议，更新UDP的一个地址获得的问题。
* 完善Linux下的守护进程状态输出信息功能。
* 修复一个发送数据包死锁的BUG。
* 添加Linux下添加发送数据包失败时候的断开连接处理。
* 完善数据包发送的一些数据检查。
* 优化Linux下数据收发的多线程锁。
* 修复一处关闭插件的内存泄露点。
* 更新一个线程数初值类型问题。
* 根据@玉白石 和@弄香花满衣 的反馈，修复了一些消息处理的BUG。
* 更新http解析器的一个虚接口文件。
* 提交对输出转文件的一处代码BUG修复。
* 完善对g++ 4.8.X的编译器的支持。
* 修复一个日志组件返回值的问题。
* 更新PSSLoginClient的列表刷新代码，感谢@单调同学的贡献。
* 解决Proxy用例在linux下关闭PSS的时候崩溃的问题。
* 发送数据块缓冲可以在main.xml进行配置。
* 优化发送内存缓冲队列。
* 考虑了一下，去掉SendDatamark参数设置，保持和m_u4BlockSize一致。
* 添加自动判断当前连接id是否已用功能。
* 添加服务器间通讯UDP广播功能。
* 添加新功能，支持信令对某一个监听端口达成。

V0.95改进
* 重新设计MessageServer多工作线程的支持。
* 支持多反应器客户端连接同步。
* 重构框架代码中所有的内存操作边界检查。
* 框架支持插件自检功能。
* 解决了群发消息的一处BUG。
* 添加服务器心跳超时事件，插件可订阅。
* 更新检查连接超时更新机制。
* 添加新的BloockSize相关设置。
* 提交对服务器断开连接的优化。
* 删除无用的信号量注册，Valgrind检测内存无泄漏和警告达成。
* 修改溢出PSS_ClientManager可能存在的BUG，
* 添加插件可以控制客户端连接断开的两种状态，一种是立即断开，一种是发送完成断开。
* 添加判断客户端连接是否存在的接口。
* 添加插件中获取框架所有插件信息
* 添加服务器间传输获取IClientMessage接口，以及通过ServerID获得远端IP的接口
* 添加监控工具邮件发送功能。
* 添加服务器间通讯第一次连接连接成功通知Reconnect()。
* 添加Lua测试插件，在Linux下编译运行测试通过。
* 重写了插件热加载功能。
* 添加对发送数据超时告警的插件通知机制。
* 添加对插件对本地监听端口获取的接口。

V0.94改进
* 服务器间连接支持指定本地IP和端口功能。(有些需求远端需要指定本地IP和端口)
* 添加单位时间连接量和断开量统计功能。
* 添加单位时间连接量和断开量统计告警功能。
* 添加告警邮件自动发送功能。
* 添加新的BuffPacket支持类型,支持String类型的导入导出。
* 修复Linux PSS关闭时在某些情况下程序不退出的BUG。
* 修改Reactor主线程为监控线程。
* 重新设计告警配置文件，并支持邮件告警功能。
* 添加对PSS的允许最大连接数的远程控制功能。
* 修复UDP数据发送的一个BUG。
* 优化对无头数据包解析用例的代码。
* 添加了数据包头信息代码样例。
* 修改例子代码支持新的PacketParse功能以及新接口。
* 添加日志跟踪器工具。
* 添加了自动添加和关闭指定监听端口功能，支持插件内管理以及管理工具管理。
* 开放关于链接别名的函数给逻辑插件使用。
* 添加服务器间连接异常的时候返回远程IP功能。
* 解决一个HTTP数据包解析造成堆栈崩溃的BUG。
* 添加定时器插件用例。
* 优化框架代码，减少不必要的代码，优化流程以及代码顺序。

V0.93改进
* 支持只有包头不含包体的数据。
* 添加了Websocket对接协议的PacketParse用例。
* 添加了Http对接协议的PacketParse用例。
* 添加了对ACE_DEBUG日志输出文本规格化的支持。
* 修复了一个ACE_DEBUG死锁的问题。
* 更新TcpPost用例，添加数据回发完整性判定。 
* 添加了在Linux下对epollet模式的支持。
* 修复了一些Reactor和Proactor下的BUG。

V0.92改进
* 优化ConnectHander的代码结构
* 添加发送超时配置文件
* 添加了新用例，ftp用例，实现相关了目录浏览，下载和上传(PSS插件以及测试客户端)。
* 添加如果二级缓冲用例，实现共享内存和数据库的同步(PSS插件以及测试客户端)。
* 添加了插件间相互调用用例，实现了插件间的通讯((PSS插件以及测试客户端)。
* 添加Linux下自动设置当前工作目录的功能。
* 添加了PSS自测插件功能，实现PSS数据包自测用例(PSS插件以及测试客户端)。
* 更新了PassTCP工具，可以支持二进制和文本的数据包发送。
* 重写了PSS日志接口，支持输出到屏幕和文件的选择，并支持文本和二进制的记录。
* 添加了Proxy代理服务器数据包转发插件，实现了PSS网关功能(PSS插件以及测试客户端)。
* 添加了新的API，允许插件可以获得工作线程的数量以及当前工作线程的ID。
* 添加了uint64位数据的网络字序和主机字序的转换函数。
* 添加了再Linux下自检当前文件并发数的功能，如果文件并发数小于配置文件设置则框架会自动尝试提升当前文件并发数，如果失败则提示框架启动失败。
* 添加了对core文件的设置，开发者可以通过配置core文件大小来启动当前PSS。
* 添加了发送缓冲区自检功能，当发送字节和对端收到字节不成正比时，按照配置文件的规则回收当前连接。
* 添加了对BACKLOG的设置，可以提升在大并发连接下的连接效率。
  
V0.91改进
* 修改了dev_poll下设置并行最大连接数配置文件对应关系。
* 再次更新PacketParse接口，优化了接口结构，使得开发者更清晰的看到自己要实现代码的地方。
* 更新插件压力测试工具。支持TCP和UDP压力测试，并会生成测试报告。
* 更新MakePacket回应包添加CommandID参数，你可以根据不同的连接ID决定处理你的发送组包逻辑（比如加解密的随机算法）
* 服务器添加了对UDP recv超时的设置
* 更新了UDP Proactor模式下的UDP设置参数。
* 添加对IPv4和IPv6的支持。服务器可以使用IPV6的地址，但是前提是OS必须支持IPV6
* 添加类视图文档，以PDF文档形式提供。
* 更新插件压测工具，提供多线程压测插件功能。
* 修改了TCP和TCP服务器间测试用例，实现了透传数据的压测用例。
* 添加了Linux下结束进程的脚本
* 添加了时间成本宏，你可以用于你的逻辑中，测试函数执行效能
* 添加三个Try catch宏用于程序调控。你可以用于你的逻辑中，套在函数里。
* 添加了服务器发送数据水位标，如果服务器发快客户端收慢，那么会有一个阀值保证正常的连接不受影响。
* 修改了若干测试出的BUG，具体可以浏览SVN更新日志。
* 添加了DEBUG模式，在debug下支持输出所有的数据包文件。这些数据包可以变为压测的回放的依据。