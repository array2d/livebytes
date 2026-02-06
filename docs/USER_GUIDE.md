# 用户使用手册

## 欢迎使用 LiveBytes

LiveBytes 是一个基于文件系统的 AI Agent 框架。本手册将帮助您快速上手。

## 快速开始

### 安装

（待补充安装说明）

### 基本使用

1. **启动 LiveBytes**

```bash
# 待补充启动命令
./livebytes start
```

2. **提交任务**

在工作空间的 `input/` 目录中创建任务文件（使用专用后缀 `.lbtask`）：

```bash
# 创建一个文本处理任务
echo "需要处理的文本内容" > livebytes_root/var/workspace/input/task1.lbtask
```

3. **查看结果**

处理完成后，在 `output/` 目录中查看结果：

```bash
cat livebytes_root/var/workspace/output/task1_result.txt
```

## 系统目录结构

LiveBytes 参考 Linux 目录结构，在系统根目录下创建固定名称的目录：

```
livebytes_root/
├── etc/            # 系统配置目录
├── var/            # 运行数据目录
│   └── workspace/  # 工作空间目录
├── log/            # 日志目录
├── run/            # 运行时目录
└── tmp/            # 临时目录
```

## 工作空间结构

LiveBytes 使用统一的工作空间目录结构：

```
livebytes_root/var/workspace/
├── input/          # 放置待处理的文件（.lbtask）
├── output/         # 获取处理结果
├── processing/     # 正在处理的任务（系统管理）
├── completed/      # 已完成的任务（系统管理）
├── failed/         # 失败的任务（系统管理）
└── config/         # 任务配置文件
```

### 目录说明

#### input/ - 输入目录

这是您提交任务的地方。只需将 `.lbtask` 文件放入此目录，LiveBytes 会自动检测并开始处理。

**支持的操作**：
- 创建新文件：触发新任务
- 修改文件：可能触发重新处理（取决于配置）
- 删除文件：取消待处理任务（如果还未开始）

#### output/ - 输出目录

所有处理结果都会写入这个目录。结果文件名通常与输入文件相关。

**文件命名规则**：
- 默认：`{原文件名}_result.{扩展名}`
- 可通过配置自定义

#### processing/ - 处理中目录

系统自动管理，存放正在处理的任务文件。

**注意**：请勿手动修改此目录中的文件。

#### completed/ - 完成目录

存放已成功完成的任务。用于审计和历史查询。

**清理策略**：根据配置的保留时间自动清理。

#### failed/ - 失败目录

存放处理失败的任务，包含错误信息文件。

**错误文件格式**：
- `{原文件名}.error`：包含详细错误信息

#### config/ - 配置目录

存放任务特定的配置文件。

## 任务配置

### 全局配置

通过 `livebytes_root/etc/livebytes.yaml` 文件配置全局参数。参考 `config.example.yaml`。

### 任务级配置

为特定任务创建配置文件：

```yaml
# livebytes_root/var/workspace/config/task1.yaml
priority: high        # 任务优先级：low, normal, high
timeout: 120         # 超时时间（秒）
engine:
  model: gpt-4       # 使用的 AI 模型
  temperature: 0.7   # 模型参数
```

配置文件名应与输入文件名对应（不包括扩展名）。

## 任务类型

### 文本处理

支持各种文本处理任务：
- 内容分析
- 摘要生成
- 文本分类
- 情感分析

### 文档处理

支持常见文档格式：
- Markdown
- Plain Text
- JSON
- XML

### 代码分析

支持代码相关任务：
- 代码审查
- 漏洞检测
- 代码优化建议
- 文档生成

### 自定义任务

通过配置文件指定任务类型和处理方式。

## 高级功能

### 任务优先级

通过配置文件设置任务优先级：

```yaml
priority: high
```

### 任务依赖

配置任务之间的依赖关系：

```yaml
dependencies:
  - task_id_1
  - task_id_2
```

### 批量处理

一次性提交多个文件，系统自动并行处理。

### 任务链

配置多个任务按顺序执行：

```yaml
chain:
  - step: analyze
  - step: summarize
  - step: translate
```

## 监控和调试

### 查看日志

```bash
tail -f logs/livebytes.log
```

### 任务状态

通过文件位置判断任务状态：
- `input/`: 等待处理
- `processing/`: 处理中
- `completed/`: 已完成
- `failed/`: 处理失败

### 错误诊断

查看 `failed/` 目录中的 `.error` 文件了解失败原因。

## 最佳实践

### 1. 文件命名

使用有意义的文件名，便于识别和管理：
```
✓ user_feedback_20260206.lbtask
✗ file1.txt
```

### 2. 批量处理

对于大量文件，建议分批提交，避免系统过载。

### 3. 配置管理

为不同类型的任务创建配置模板，提高效率。

### 4. 定期清理

定期检查和清理 `completed/` 和 `failed/` 目录。

### 5. 备份重要文件

在提交处理之前，备份重要的原始文件。

## 故障排除

### 问题：任务长时间未处理

**可能原因**：
- 系统未启动
- 任务队列已满
- 文件格式不支持

**解决方法**：
1. 检查 LiveBytes 是否运行
2. 查看日志文件
3. 检查配置文件

### 问题：处理失败

**排查步骤**：
1. 查看 `failed/` 目录中的错误文件
2. 检查输入文件格式
3. 验证配置参数
4. 查看系统日志

### 问题：结果不符合预期

**改进方法**：
1. 调整 AI 模型参数
2. 提供更详细的任务配置
3. 使用不同的 AI 模型

## 常见问题

### Q: 支持哪些文件格式？

A: 目前支持文本文件、Markdown、JSON 等。具体支持的格式取决于配置的处理引擎。

### Q: 可以同时处理多少个任务？

A: 由配置文件中的 `maxConcurrent` 参数控制，默认值为 5。

### Q: 处理大文件时需要注意什么？

A: 建议：
- 增加超时时间配置
- 确保有足够的系统资源
- 考虑分割大文件

### Q: 如何取消正在处理的任务？

A: 目前需要重启 LiveBytes。后续版本会增加任务控制功能。

## 获取帮助

- 查看项目文档：[README.md](../README.md)
- 查看架构文档：[ARCHITECTURE.md](../ARCHITECTURE.md)
- 提交问题：[GitHub Issues](https://github.com/array2d/livebytes/issues)
- 参与讨论：（社区讨论链接待补充）

## 贡献

欢迎贡献代码、文档和使用案例！请参考 [DEVELOPMENT.md](../DEVELOPMENT.md)。

---

*本手册会随着项目发展持续更新。*
