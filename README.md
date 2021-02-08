# go-simple-mq
Go语言开发简单实用的MQ消息队列服务，支持消息存储、重试、延迟队列

----------------------

特性：

1.    未完成的任务放在 sqlite 数据库，也包含失败的任务。   
       - 主题（没有的话，默认为main）, json消息体，失败次数（默认0），是否已完成（默认0）
       - 分配给worker的id，分配时间
       - 消息类型（0-普通消息，1-延迟消息，2-回调执行消息）
       - 是否是延迟队列，延迟到期时间，（延迟行为json体，见json消息体）
       - 是否为（回调）执行消息，回调命令（见json消息体）
       - 延迟或执行消息体格式， type：cmd（执行命令），http（请求http）。   body：具体命令。
2.    历史日志使用文件存储：
       - 已经完成的任务，存档在     finish-2021.01.log       
       - 所有的运行情况，存档在     info-2021.01.log         
       - 超过重试次数的失败任务，存档在  fail-2021.01.log
       -【按月份分卷压缩】规则：前6个月是log未压缩类型，超过6个月的tar.gz格式或者zip格式
3.    主线程、worker线程运行模式，可以设定worker线程数量； worker线程挂了之后，主线程可以重启；主线程负责分配任务给子线程，如果执行的任务长时间卡住，可设置超时时间，任务失败机制； 针对延迟队列，为了保障延迟队列的时效性，延迟队列单独分配worker线程。
4.    带有Web UI
5.    支持延迟队列，可以写入到期时间、到时间之后的回调
6.    支持HTTP API方式接入（支持GET、POST方式）
---------------------------
执行名称：  gosmq   


---
如java版本实现，名称 java-simple-mq
