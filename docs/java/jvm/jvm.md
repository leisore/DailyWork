### HeapDump

------

##### HotSpot
���õ��ڴ����ʱ����heapdump�ļ���������
    -Xloggc:${dir}/gc.log                 GC��־�ļ�
    -XX:+HeapDumpOnOutOfMemoryError       �����ʱ����heapdump�ļ�
    -XX:HeapDumpPath=${dir}               heapdump�ļ����λ��

jdk6.0ȡ����-XX:+HeapDumpOnCtrlBreak���ò���ͨ��ctrl+break�ķ�ʽ,���Ҫ��ʱ��̬����heapdump�ļ�����ʹ��jmap����:
    jmap -dump:format=b,file=temp_heapdump.hprof <pid>

##### HP JVM
    -Xloggc:${dir}/gc.log                 GC��־�ļ�
    -XX:+HeapDumpOnOutOfMemoryError       �����ʱ����heapdump�ļ�
    -XX:HeapDumpPath=${dir}               heapdump�ļ����λ��
    -XX:+HeapDumpOnCtrlBreak              ����ͨ��ctrl+break��ϼ���̬����heapdump�ļ�

##### IBM J9
Unix����ϵͳ������

    -XverboseGClog: ${dir}/gc.log                       GC��־�ļ�
    -Xdump:heap:events=user,file=${dir}/pid%uid%pid.phd ��ʾ���Ը�����Ҫͨ��kill -3 <pid>����DUMP�ļ���%uid��%pidΪ����

Windows����ϵͳ������

    ����wsadmin,����wsadmin����
    wsadmin> set jvm [$AdminControl completeObjectName type=JVM,process=server1,*]
    wsadmin> $AdminControl invoke $jvm generateHeapDump
    wsadmin> $AdminControl invoke $jvm dumpThreads