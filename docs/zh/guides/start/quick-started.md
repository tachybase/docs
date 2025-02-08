# 快速开始

## 安装

### 0.先决条件
 请确保你已经：

- 安装了 Node.js 20 + pnpm 9.15.x
- 配置并启动了所需数据库 MySQL 8.0.17+、MariaDB 10.9+、PostgreSQL 10+ 任选其一

如果你没有安装 Node.js 可以从官网下载并安装最新的 LTS 版本。如果你打算长期与 Node.js 打交道，推荐使用 nvm（Win 系统可以使用 nvm-windows ）来管理 Node.js 版本。

 ```bash
$ node -v 

v20.18.0
 ```

 推荐使用 pnpm 包管理器。

 ```bash
$ npm install --global pnpm

$ pnpm -v

9.15.1
```
 
由于国内网络环境的原因，强烈建议你更换国内镜像。

```bash
$ pnpm config set disable-self-update-check true
$ pnpm config set registry https://registry.npmmirror.com/
$ pnpm config set sqlite3_binary_host_mirror https://npmmirror.com/mirrors/sqlite3/
```

## 1.安装项目

### - create-tachybase-app安装

```bash
pnpm create tachybase-app  my-tachybase-app
```

### - Git 源码安装

```bash
git clone https://github.com/tachybase/tachybase.git -b main --depth=1 my-tachybase
```

## 2. 切换目录

```bash
cd my-tachybase-app
```

## 3. 安装依赖

📢 由于网络环境、系统配置等因素影响，接下来这一步骤可能需要十几分钟时间。

```bash
pnpm install
# 生产环境部署时，为了减少体积，可以只安装必要的依赖
pnpm install --production
```

## 4. 设置环境变量

Tachybase 所需的环境变量储存在根目录 `.env` 文件里，根据实际情况修改环境变量，如果你不知道怎么改，[点此查看环境变量说明](../env.md)，也可以保持默认。

```bash
TZ=Asia/Shanghai
APP_KEY=your-secret-key
DB_HOST=localhost
DB_PORT=5432
DB_DATABASE=postgres
DB_USER=tachybase
DB_PASSWORD=tachybase
```

:::warning

  - `TZ` 用于设置应用的时区，默认为操作系统时区；
  - `APP_KEY` 是应用的密钥，用于生成用户 token 等（如果 APP_KEY 修改了，旧的 token 也会随之失效）。它可以是任意随机字符串。请修改为自己的秘钥，并确保不对外泄露；
  - `DB_*` 为数据库相关，如果不是例子默认的数据库服务，请根据实际情况修改。

::: 




## 5. 安装 Tachybase

```bash
pnpm tachybase install --lang=zh-CN
```
## 6. 启动 Tachybase

开发环境

```bash
pnpm dev
```

生产环境

```bash
pnpm start
```

注：生产环境，如果代码有修改，需要执行 `pnpm build`，再重新启动 Tachybase

## 7. 登录 Tachybase

使用浏览器打开 [http://localhost:3000](http://localhost:3000) 初始化账号和密码是 `admin@tachybase.com` 和 `!Admin123.`。

