flume-safe-rollingfilesink
==========================
基于org.apache.flume.sink.RollingFileSink修改的实现,配置参数基本与其相同 只是增加了一个临时目录 在文件被完成之后移动到另外一个目录中 另外不会生成空文件

```sh
agent1.channels.ch1.type = memory

agent1.sources.avro-source1.channels = ch1
agent1.sources.avro-source1.type = netcat
agent1.sources.avro-source1.bind = 127.0.0.1
agent1.sources.avro-source1.port = 41414


agent1.sinks.file-sink1.type = org.apache.flume.sink.SafeRollingFileSink #这里指定Sink的全限定名
agent1.sinks.file-sink1.channel = ch1
agent1.sinks.file-sink1.sink.directory = /var/flume/example
agent1.sinks.file-sink1.sink.tmpdirectory = /var/flume/example/temp	 #这里指文件的临时目录
agent1.sinks.file-sink1.sink.rollInterval = 20

agent1.channels = ch1
agent1.sources = avro-source1
agent1.sinks = file-sink1
```
