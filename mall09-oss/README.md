mall09-oss 工程完全参考作者下面的教程搭建
- [mall整合OSS实现文件上传](https://juejin.im/post/5cff9944e51d4577555508a9)

结合QueueEnum理解RabbitMQ的消息模型
- 枚举类

    QUEUE_ORDER_CANCEL("mall.order.direct", "mall.order.cancel", "mall.order.cancel")
    QUEUE_TTL_ORDER_CANCEL("mall.order.direct.ttl", "mall.order.cancel.ttl", "mall.order.cancel.ttl");

- 枚举类的解释

    "mall.order.direct"代表交换机，"mall.order.cancel"代表队列，"mall.order.cancel"代表路由的key值

- 怎样找到队列

    对于交换机,根据路由的key值，就能找到对应的队列


RabbitMqConfig.java
- 初始化交换机"mall.order.direct",队列"mall.order.cancel"
根据路由的key值"mall.order.cancel"将交换机和队列绑定（以后指定交换机和路由的key值就能找到对应的队列）

- 初始化交换机"mall.order.direct.ttl",队列"mall.order.cancel.ttl"
根据路由的key值"mall.order.cancel.ttl"将交换机和队列绑定(同上)

- "mall.order.cancel.ttl"是一个死信队列，这个队列里面的消息
到期后会自动将消息转发给实际消费队列"mall.order.cancel"

下单分析
- 下单之后，就向死信队列（即延迟队列）"mall.order.cancel.ttl" 发送一个消息，
消息里面直接传的订单id。
- 同时设置延迟时间，在时间到之前，消息会一直保存在延迟队列里面。
- 时间到了之后，消息会被转发给实际消费队列"mall.order.cancel"
- CancelOrderReceiver这个组件一直监听着这个队列"mall.order.cancel"，一旦队列里面有消息，就立即进行消费，取消订单
