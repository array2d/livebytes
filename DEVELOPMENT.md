# 开发指南

## 开发环境设置

### 前置要求

（根据实际技术栈补充，例如：）
- Go 1.19 或更高版本
- Git
- 文本编辑器或 IDE

### 克隆项目

```bash
git clone https://github.com/array2d/livebytes.git
cd livebytes
```

### 安装依赖

```bash
# 待补充具体命令
```

## 项目结构

```
livebytes/
├── README.md              # 项目介绍
├── ARCHITECTURE.md        # 架构设计文档
├── DEVELOPMENT.md         # 开发指南（本文件）
├── LICENSE               # 许可证
├── .gitignore            # Git 忽略文件
├── cmd/                  # 命令行工具入口（待创建）
│   └── livebytes/        # 主程序入口
├── internal/             # 内部包（待创建）
│   ├── monitor/          # 文件系统监控器
│   ├── scheduler/        # 任务调度器
│   ├── engine/           # AI 处理引擎
│   └── manager/          # 结果管理器
├── pkg/                  # 公共包（待创建）
│   ├── config/           # 配置管理
│   ├── task/             # 任务定义
│   └── utils/            # 工具函数
├── docs/                 # 额外文档（待创建）
├── examples/             # 示例代码（待创建）
└── tests/                # 测试文件（待创建）
```

## 代码规范

### 注释规范

**所有文档注释必须使用中文**。这是项目的基本要求。

#### 包注释

```go
// Package monitor 实现文件系统监控功能。
// 它负责监控指定目录的文件变化，并触发相应的任务处理流程。
package monitor
```

#### 函数注释

```go
// StartMonitoring 开始监控指定的目录。
// 参数：
//   - path: 要监控的目录路径
//   - recursive: 是否递归监控子目录
// 返回值：
//   - error: 如果启动监控失败，返回错误信息
func StartMonitoring(path string, recursive bool) error {
    // 实现代码
}
```

#### 结构体注释

```go
// Task 表示一个待处理的任务。
type Task struct {
    // ID 是任务的唯一标识符
    ID string
    
    // InputPath 是任务输入文件的路径
    InputPath string
    
    // Status 表示任务的当前状态
    Status TaskStatus
    
    // CreatedAt 是任务创建的时间
    CreatedAt time.Time
}
```

#### 常量和变量注释

```go
// DefaultQueueSize 是任务队列的默认大小
const DefaultQueueSize = 100

// ErrInvalidPath 表示提供的路径无效
var ErrInvalidPath = errors.New("无效的路径")
```

### 命名规范

- **包名**：使用小写单词，简短且有意义
- **文件名**：使用小写字母和下划线，如 `file_monitor.go`
- **函数名**：使用驼峰命名法（CamelCase）
- **变量名**：使用驼峰命名法（camelCase）
- **常量名**：使用驼峰命名法（CamelCase）或全大写（UPPER_CASE）

### 错误处理

```go
// 始终检查错误
result, err := SomeFunction()
if err != nil {
    // 提供有意义的错误上下文（中文）
    return fmt.Errorf("执行某操作失败: %w", err)
}

// 使用自定义错误类型时，提供中文错误信息
type TaskError struct {
    TaskID  string
    Message string
}

func (e *TaskError) Error() string {
    return fmt.Sprintf("任务 %s 错误: %s", e.TaskID, e.Message)
}
```

## 开发工作流

### 1. 创建功能分支

```bash
git checkout -b feature/your-feature-name
```

### 2. 编写代码

- 确保所有注释使用中文
- 遵循代码规范
- 编写单元测试

### 3. 运行测试

```bash
# 待补充测试命令
go test ./...
```

### 4. 提交代码

```bash
git add .
git commit -m "feat: 添加某某功能"
```

提交信息格式：
- `feat:` 新功能
- `fix:` 修复 Bug
- `docs:` 文档更新
- `style:` 代码格式调整
- `refactor:` 代码重构
- `test:` 测试相关
- `chore:` 其他杂项

### 5. 推送并创建 Pull Request

```bash
git push origin feature/your-feature-name
```

然后在 GitHub 上创建 Pull Request。

## 测试指南

### 单元测试

每个包都应该有对应的测试文件：

```go
// file_monitor_test.go

package monitor

import "testing"

// TestStartMonitoring 测试监控启动功能
func TestStartMonitoring(t *testing.T) {
    // 测试实现
}
```

### 集成测试

在 `tests/` 目录下创建集成测试。

## 调试技巧

### 日志输出

使用统一的日志接口，所有日志消息使用中文：

```go
log.Info("开始处理任务", "taskID", task.ID)
log.Error("任务处理失败", "taskID", task.ID, "error", err)
```

### 调试工具

（待补充具体调试工具和方法）

## 性能优化

### 性能测试

```bash
# 待补充性能测试命令
go test -bench=. ./...
```

### 性能分析

（待补充性能分析工具和方法）

## 文档编写

### 文档要求

1. **必须使用中文**
2. 保持简洁明了
3. 提供代码示例
4. 及时更新

### 文档类型

- **README.md**: 项目概述和快速开始
- **ARCHITECTURE.md**: 架构设计详细说明
- **DEVELOPMENT.md**: 开发指南（本文件）
- **API.md**: API 文档（待创建）
- **USER_GUIDE.md**: 用户使用手册（待创建）

## 常见问题

### Q: 为什么必须使用中文注释？

A: 这是项目的设计决策，目的是让中文用户更容易理解和贡献代码。

### Q: 如何贡献代码？

A: 请参考上面的开发工作流部分，并确保所有代码注释使用中文。

### Q: 遇到问题怎么办？

A: 可以通过以下方式寻求帮助：
- 查看现有文档
- 搜索已有的 Issues
- 创建新的 Issue 描述问题
- 加入社区讨论（待建立）

## 相关资源

- [Go 语言文档](https://go.dev/doc/)
- [项目 GitHub 仓库](https://github.com/array2d/livebytes)
- [问题追踪](https://github.com/array2d/livebytes/issues)

## 更新日志

本文档会随着项目发展不断更新，请定期查看最新版本。
