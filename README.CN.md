# GitHub Action 入门模板

这是一个综合性的指南和示例项目，展示了 GitHub 最佳实践，包括 Actions 工作流、多平台代码同步和自动化部署。

[English Documentation](README.md)

## 功能特性

- **多平台代码同步**：自动同步代码到多个平台，如 Gitee、GitCode、Coding 等
  - 配置指南：[docs/SYNC.CN.md](docs/SYNC.CN.md)
  - 工作流实现：[.github/workflows/sync-repos.yml](.github/workflows/sync-repos.yml)

## 快速开始

### 代码同步设置

1. 在 GitHub Secrets 中配置同步目标（SYNC_CONFIG）
2. 按照 [docs/SYNC.CN.md](docs/SYNC.CN.md) 中的详细指南进行操作
3. 同步工作流会在以下情况自动运行：
   - 推送到 main 分支时
   - 通过 Actions 页面手动触发

详细配置选项和故障排除，请参考[同步配置指南](docs/SYNC.CN.md)。
