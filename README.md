# NCMM (LazyCat)

网易云音乐人助手（一键签到、自动任务、接力刷播），打包为 LazyCat LPK v2。上游项目：[3899/ncmm](https://github.com/3899/ncmm)。

## 部署信息

- **包名**：`cloud.lazycat.app.ncmm`
- **版本**：跟随上游镜像 SemVer tag 自动更新（当前 1.2.5；每日 UTC 03:17 检查）
- **交付模式**：mirror（镜像引用 + digest 校验）
- **min_os_version**：1.5.0

## 初始化与登录（免密设计）

1. 安装向导提供 `admin_password`（默认随机生成 16 位）
2. **首次启动**：`setup_script` 在容器启动前预置 WebUI 管理员密码（`ncmm auth reset-password`）
3. **登录页自动填充**：`simple-inject-password` 注入 `#password-input`，登录无需手动输入
4. 若向导未设置密码（CLI 场景）：首次打开 WebUI 按原生流程手动设置密码

## 数据

- 数据持久化：`/lzcapp/var/data:/data`（配置、Cookie、日志、调度规则）

## 文件结构

```
package.yml              # 包元数据
lzc-manifest.yml         # 运行结构（ncmm 服务 + injects 免密登录）
lzc-deploy-params.yml    # 安装向导参数（admin_password）
lzc-build.yml            # 构建配置
icon.png                 # 应用图标（网易云音乐人图标）
.github/lazycat-action.yml      # Action 配置（mirror / 喵喵商店）
.github/workflows/lazycat.yml   # 发布工作流
```
