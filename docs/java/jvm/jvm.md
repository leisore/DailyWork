### HeapDump

------

##### HotSpot
配置当内存溢出时生成heapdump文件配置如下
    -Xloggc:${dir}/gc.log                 GC日志文件
    -XX:+HeapDumpOnOutOfMemoryError       存溢出时生成heapdump文件
    -XX:HeapDumpPath=${dir}               heapdump文件存放位置

jdk6.0取消了-XX:+HeapDumpOnCtrlBreak配置参数通过ctrl+break的方式,如果要即时动态生成heapdump文件可以使用jmap命令:
    jmap -dump:format=b,file=temp_heapdump.hprof <pid>

##### HP JVM
    -Xloggc:${dir}/gc.log                 GC日志文件
    -XX:+HeapDumpOnOutOfMemoryError       存溢出时生成heapdump文件
    -XX:HeapDumpPath=${dir}               heapdump文件存放位置
    -XX:+HeapDumpOnCtrlBreak              可以通过ctrl+break组合键动态生成heapdump文件

##### IBM J9
Unix操作系统环境中

    -XverboseGClog: ${dir}/gc.log                       GC日志文件
    -Xdump:heap:events=user,file=${dir}/pid%uid%pid.phd 表示可以根据需要通过kill -3 <pid>产生DUMP文件，%uid和%pid为变量

Windows操作系统环境中

    启动wsadmin,进入wsadmin环境
    wsadmin> set jvm [$AdminControl completeObjectName type=JVM,process=server1,*]
    wsadmin> $AdminControl invoke $jvm generateHeapDump
    wsadmin> $AdminControl invoke $jvm dumpThreads