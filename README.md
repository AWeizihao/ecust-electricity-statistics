如果你要fork本仓库：
+ 本仓库不是原始仓库！
+ 本仓库的前端代码全部储存在html文件中，包含全部css样式。
+ 数据计算部分逻辑待修改，“每月用电量”等数据暂不可信
# ecust-electricity-statistics

华东理工大学电费统计：拒绝一切不透明操作。通过 Github Actions 自动获取并记录每天的宿舍电量剩余，并通过 PushPlus 自动推送到微信端。

- secrets
  <!-- prettier-ignore -->
    |name|option|function|
    | :-: | :-: | :-: |
    |URL|必填|电费查询来源|
    |PUSH_PLUS_TOKEN|选填|[推送选项](#启用推送)|

## 开始记录

1. 华理信息办 - 微门户 - 电费充值 - 查询您的宿舍电量 - 复制链接。（本例中宿舍为随机选出）

<img alt="复制链接" src="https://user-images.githubusercontent.com/88281489/205481212-aaca1699-79ef-4c17-b3e3-a7e477ad55db.png"  width="30%" height="30%"/>

2. 右上角 fork 仓库

![fork](https://user-images.githubusercontent.com/88281489/205480982-a221a67c-c789-4298-9a45-34a35c820b71.png)

3. 在 Code 界面下，点击 `data.js` ，将其删除。

![删除 AbsoluteX 的数据](https://github.com/lxl66566/ecust-electricity-statistics/assets/88281489/bb12d4b9-4680-4499-9994-b0bd84d7fe1f)

4. _Settings - Secrets and variables - Actions - New repository secret_

- Name 填写 `URL`，Secret 填写 第一步复制的链接

![找到 Secrets](https://user-images.githubusercontent.com/88281489/205481390-292a3fc3-fa69-4c2f-886c-b0bc573f5470.png)
![填写](https://user-images.githubusercontent.com/88281489/205481486-3b5cafc9-f00d-4ca3-a0d8-eaedfffff7df.png)

5. _Settings - Actions - General_ 界面，拉到最下，选择 _Workflow permissions_ 为 _Read and write permissions_

<img alt="界面" src="https://user-images.githubusercontent.com/88281489/229278107-8a623cea-0ff9-435c-b729-e248c17ae827.png"  width="70%" height="70%"/>

![选择权限](https://user-images.githubusercontent.com/88281489/229278162-e65383df-17a4-4b66-8981-5fc23d2413a7.png)

6. _Actions - enable them_，然后在 AutoRecord 下点击 Enable workflow

![image](https://user-images.githubusercontent.com/88281489/229278566-17ec1798-5e26-4c42-8f82-91386955d4fc.png)
![image](https://user-images.githubusercontent.com/88281489/205481894-022e114f-5023-45d5-881d-d5fbc9d4a6ba.png)

## 查看数据

### Github Pages（推荐）

使用 Github Pages 构建。请确保您已获取到电量数据。

Settings - Pages - Deploy from a branch - 选中 main - Save

等待网站构建完毕后（约 1 min），刷新页面，点击 Visit site 即可查看数据。

![image](https://user-images.githubusercontent.com/88281489/205528351-399f221b-96e8-4ca5-86d0-32eb6cdb9286.png)

### 图表

1. 使用 `git clone` 或下载 zip
2. 解压，双击打开 `index.html` 文件

### 生数据

直接点击 `data.js` 查看

## PushPlus 推送（可选）

### 启用推送

1. Settings - Secrets and variables - Actions - New repository secret
2. Name 填写 `PUSH_PLUS_TOKEN`，Secret 填写你的 PushPlus 的 TOKEN 信息

### 其他配置

> 前置条件：启用推送

编辑 `config.ini` 文件，详情见文件注释。

![20231017-1744](https://github.com/lxl66566/ecust-electricity-statistics/assets/88281489/ef1b0a26-4f77-4c5c-8281-cac1f3d2d3cd)

|       参数        | 默认值 |
| :---------------: | :----: |
|   days_to_show    |   10   |
|      detail       |  true  |
|      warning      |   10   |
| push_warning_only |  true  |

请注意由于 `push_warning_only`，默认情况下不会推送每日数据。

## 注意事项

- fork 此仓库后请不要再次 sync fork，否则可能会造成数据丢失。若确实需要更新到最新版本，请自行备份 `data.js` 并使用 git 恢复数据。
- `data.js` 会被作为 _json_ 处理。若自行修改，请遵守 _json_ 格式规范，注意不要有多余的逗号。
- 对文件进行修改和删除后，**别忘了 commit changes**...

## 贡献指南

- [![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)
- pr 保留 `data.js` 中的数据
