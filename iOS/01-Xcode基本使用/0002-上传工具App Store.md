[toc]

---



# 上传工具

在 App Store Connect 中创建 App 记录后，您便可以通过 Xcode、macOS 版 Transporter 或 altool 上传构建版本。如果您使用 [App Store Connect API](https://developer.apple.com/documentation/appstoreconnectapi)，则建议您通过命令行工具 Transporter 和 JSON 网络令牌（JWT）验证来上传二进制文件。用于 API 的 JWT 也可以用于上传二进制文件。

## 通过 Xcode 上传您 App 的二进制文件

Xcode 是 Apple 的集成开发环境（IDE）。Xcode 可用于为 Apple 产品（包括 iPad、iPhone、Apple Watch、Apple TV 和 Mac）构建 App。Xcode 提供诸多工具，能帮助您管理整个开发工作流程——包括创建、测试、优化 App 并将其提交至 App Store。

若要了解如何通过 Xcode 上传您 App 的二进制文件，请前往“[Upload an app to App Store Connect（上传 App 至 App Store Connect）](https://help.apple.com/xcode/mac/current/#/dev442d7f2ca)”，或者在 Xcode 中选择“Help（帮助）”>“Xcode Help（Xcode 帮助）”并搜索“Upload an app（上传 App）”。

请在 Mac App Store 中[下载 Xcode](https://apps.apple.com/cn/app/xcode/id497799835?mt=12)。

### 支持的 Xcode 版本

App Store Connect 支持您使用以下 Xcode 版本上传 App 以便在 App Store 中分发，或通过 TestFlight 将 App 发送给测试员。

| 目标类型            | 使用 Xcode 构建       | 使用 Xcode 上传      |
| :------------------ | :-------------------- | :------------------- |
| iOS AppiOS App 扩展 | Xcode 10.1 及更高版本 | Xcode 6 及更高版本   |
| macOS App           | Xcode 6 及更高版本    | Xcode 6 及更高版本   |
| Apple tvOS App      | Xcode 7.1 及更高版本  | Xcode 7.1 及更高版本 |

所有目标类型均可通过 macOS 版 Transporter 和 altool 进行上传。

## 通过 altool 上传您 App 的二进制文件

您可以使用 `xcrun`（包含在 Xcode 中）来调用 altool，该命令行工具用于公证、验证并上传您 App 的二进制文件至 App Store。在“终端”的命令行中指定以下命令之一：

```
$ xcrun altool --validate-app -f file -t platform -u username [-p password] [--output-format xml]

$ xcrun altool --upload-app -f file -t platform -u username [-p password] [—output-format xml]
```

*【注】*如果您使用自动构建系统，则可以将公证过程集成到现有构建脚本中。Xcode 中的 altool 和 stapler 命令行工具可将您的软件上传至 Apple 公证服务，并将生成的凭证附加到您的可执行文件中。altool 位于：`/Applications/Xcode.app/Contents/Developer/usr/bin/altool`。

有关更多信息，请参见[《altool 指南》](https://help.apple.com/asc/appsaltool/)。

## 通过 Transporter App 上传您 App 的二进制文件

通过 macOS 版 Transporter App，您可以便捷地将 App 上传至 App Store Connect 以便在 App Store 上分发。除了上传构建版本，您还可以查看交付进度（包括警告、错误和交付日志）以及交付历史。

您可以在 Mac App Store 中[下载 Transporter App](https://apps.apple.com/cn/app/transporter/id1450874784?mt=12)。

有关更多信息，请参见“[macOS 版 Transporter 帮助](https://help.apple.com/itc/transporter/)”。