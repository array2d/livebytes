# Config 包

## 功能说明

Config 包提供配置管理功能，包括：

- 读取配置文件
- 验证配置参数
- 提供默认配置
- 支持配置热加载

## 配置项说明

### 监控配置
- `monitor.path`: 监控的目录路径
- `monitor.recursive`: 是否递归监控子目录
- `monitor.filters`: 文件过滤规则

### 调度配置
- `scheduler.maxConcurrent`: 最大并发任务数
- `scheduler.queueSize`: 任务队列大小
- `scheduler.timeout`: 任务超时时间

### 引擎配置
- `engine.type`: AI 引擎类型
- `engine.model`: 使用的 AI 模型
- `engine.plugins`: 启用的插件列表

## 使用示例

```go
// 待实现
```
