# MaaYuan 发行分支

`main` 跟踪 Aliothmoon/MaaFwApp；`maayuan` 是 MaaYuan Android 发布使用的分支。
资源、Python 依赖和发布流程由 syoius/MaaYuan 的 `android/` 与 `install` workflow 管理，
每次构建固定到本仓库的完整提交 SHA。

此分支保留：

- 上游 PR #40 的逻辑 contact / Android pointerId 隔离。
- 上游 PR #41 的全屏方向、触控边界与退出按钮修复。
- MaaYuan 所需的 720×1280 / 1080×1920 竖屏分辨率，以及港台游戏包名别名。
- GitHub APK 文件名前缀与 ABI 筛选；未配置 MirrorChyan 时默认使用 GitHub。
- `BUILD_VERSION_NAME` 和 `BUILD_VERSION_CODE` 构建参数，分别来自 MaaYuan 统一版本和 CI 递增序号。
- 进程连接器先登记启动状态再调度后台任务，避免进程立即退出时丢失错误回调；保留确定性竞态回归测试。

发布时以 MaaYuan 仓库的 `meta.tag` 同时设置 APK versionName 和 PI version，
无需在这里另行发布与 MaaYuan 不同的版本号。正式发布签名由 MaaYuan 仓库的 Secrets 提供。

同步上游时合并 upstream/main，运行单元测试与 APK 构建，再更新 MaaYuan 固定的源码 SHA。
上游已接收的补丁保留其合并历史，避免重复维护；业务资源与签名文件不放在此仓库。
