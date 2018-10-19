## 同步节点数据

```
witness_node --rpc-endpoint="url"
```

就是这样了, 根据上面的步骤:

* 启动了一个节点监听在 `127.0.0.1:38090`

* 区块信息被保存在 `witness_node_data_dir` 默认目录下

友情提示

* 根据机器配置同步区块大约需要几个小时的时间。


查看日志

```
tail -f trusted_node/logs/witness.log
```

节点同步完成后，日志看起来是这样的:

```
2018-06-28T03:43:03 th_a:invoke handle_block         handle_block ] Got block: #10731531 time: 2018-06-28T03:43:03 latency: 60 ms from: init0  irreversible: 10731513 (-18)			application.cpp:489
2018-06-28T03:43:06 th_a:invoke handle_block         handle_block ] Got block: #10731532 time: 2018-06-28T03:43:06 latency: 16 ms from: init1  irreversible: 10731515 (-17)			application.cpp:489
2018-06-28T03:43:09 th_a:invoke handle_block         handle_block ] Got block: #10731533 time: 2018-06-28T03:43:09 latency: 49 ms from: init2  irreversible: 10731515 (-18)			application.cpp:489
2018-06-28T03:43:12 th_a:invoke handle_block         handle_block ] Got block: #10731534 time: 2018-06-28T03:43:12 latency: 42 ms from: init3  irreversible: 10731516 (-18)			application.cpp:489
2018-06-28T03:43:15 th_a:invoke handle_block         handle_block ] Got block: #10731535 time: 2018-06-28T03:43:15 latency: 10 ms from: init4  irreversible: 10731516 (-19)			application.cpp:489
```
