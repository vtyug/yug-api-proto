## 测试各个接口的 grpcurl 命令

### 发送单个点赞消息

```bash
grpcurl -plaintext -d '{
  "user_id": 1001,
  "object_id": 2001,
  "object_type": 1,
  "is_like": true,
  "timestamp": "2023-12-25T10:00:00Z"
}' localhost:9002 com.vtyug.yug.queue.grpc.v1.Queue/SendLikeMessage
```

### 发送批量点赞消息

```bash
grpcurl -plaintext -d '{
  "messages": [
    {
      "user_id": 1001,
      "object_id": 2001,
      "object_type": 1,
      "is_like": true,
      "timestamp": "2023-12-25T10:00:00Z"
    },
    {
      "user_id": 1002,
      "object_id": 2002,
      "object_type": 1,
      "is_like": false,
      "timestamp": "2023-12-25T10:00:00Z"
    }
  ]
}' localhost:9002 com.vtyug.yug.queue.grpc.v1.Queue/BatchSendLikeMessage
```

## 获取队列统计信息：

```bash
grpcurl -plaintext -d '{
  "topic": "likes"
}' localhost:9002 com.vtyug.yug.queue.grpc.v1.Queue/GetQueueStats
```

## 启动消费者：

```bash
grpcurl -plaintext -d '{
  "group_id": "test-consumer-group",
  "topics": ["likes"],
  "concurrent_count": 2
}' localhost:9002 com.vtyug.yug.queue.grpc.v1.Queue/StartConsumer
```

## 停止消费者：

```bash
grpcurl -plaintext -d '{
  "group_id": "test-consumer-group"
}' localhost:9002 com.vtyug.yug.queue.grpc.v1.Queue/StopConsumer
```
