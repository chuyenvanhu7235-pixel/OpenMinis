# GitHub Actions 打包 OpenMinis IPA（无需 Mac）

仓库 fork: https://github.com/chuyenvanhu7235-pixel/OpenMinis

## 1. 在 GitHub 设置 Secrets

打开: **Settings → Secrets and variables → Actions → New repository secret**

| Secret 名称 | 内容 |
|-------------|------|
| `DEVELOPMENT_TEAM` | 10 位 Team ID，如 `ABCDE12345` |
| `IOS_P12_BASE64` | 证书 .p12 文件转 base64（见下方命令） |
| `IOS_P12_PASSWORD` | .p12 导出密码 |
| `IOS_PROFILE_BASE64` | 描述文件 .mobileprovision 转 base64（可选但推荐） |
| `KEYCHAIN_PASSWORD` | 任意字符串，如 `ci-keychain-pass-123` |

### Windows 转 base64（PowerShell）

```powershell
# 证书
[Convert]::ToBase64String([IO.File]::ReadAllBytes("C:\path\to\cert.p12")) | Set-Clipboard

# 描述文件
[Convert]::ToBase64String([IO.File]::ReadAllBytes("C:\path\to\profile.mobileprovision")) | Set-Clipboard
```

## 2. 触发打包

1. 打开 https://github.com/chuyenvanhu7235-pixel/OpenMinis/actions
2. 选择 **Build iOS IPA**
3. 点击 **Run workflow**
4. 选择 export_method（development / ad-hoc 等）
5. 等待约 1–2 小时（首次编译原生依赖较慢）

## 3. 下载 IPA

构建完成后 → 进入该次 run → **Artifacts** → 下载 `OpenMinis-iOS-ipa`

## 4. 装到 iPhone

用 **Sideloadly**（Windows）或 Xcode 设备安装。
