# Java 控制台书店管理系统

Java 课程练习，通过终端菜单实现账号、图书、购物车、订单与会员管理。项目用来练习类与枚举、集合存储、输入校验和菜单职责拆分，不依赖 Web 前端、数据库或第三方库。

所有数据保存在进程内存中：每次启动载入初始用户与图书，退出后不会保存注册、购物车、订单或管理员修改。

## 功能

- 普通用户：注册与登录、浏览图书、添加/移除购物车条目、结算及查看订单。
- 会员：普通、白银、黄金、钻石等级及对应折扣计算。
- 管理员：图书管理、订单状态操作、用户与会员等级管理。

程序入口是 [src/Main.java](src/Main.java)，不是 Maven 或 Gradle 工程。

## 编译与运行

需要已安装 JDK，并保证 `java` 和 `javac` 可用。本仓库命令使用 JDK 21 验证；源码也通过了 `javac --release 8` 的兼容性编译。

macOS / Linux，在仓库根目录执行：

```bash
mkdir -p out
javac -encoding UTF-8 -d out src/Main.java src/data/*.java src/lib/*.java
java -cp out Main
```

Windows PowerShell，在仓库根目录执行：

```powershell
New-Item -ItemType Directory -Force out | Out-Null
$bookSources = Get-ChildItem src -Recurse -Filter *.java | ForEach-Object { $_.FullName }
javac -encoding UTF-8 -d out $bookSources
java -cp out Main
```

也可以在 IntelliJ IDEA 中将 `src/` 设为源码目录，运行 `Main.main`。`out/` 和 `.class` 文件属于可重建产物。

## 演示账号

| 身份 | 用户名 | 密码 |
| --- | --- | --- |
| 普通用户 | `testuser1` | `password` |
| 普通用户 | `testuser2` | `secure` |
| 管理员 | `root` | `admin` |

这些账号来自源码中的课程演示数据。主菜单选择 `1` 进入用户登录，选择 `3` 进入管理员登录，选择 `4` 退出程序。

最短体验流程：用户登录 → 查看书库 → 选择图书加入购物车 → 查看购物车并结算 → 查看历史订单。管理员可以另行登录，查看订单和维护图书。

## 目录

```text
src/Main.java        初始化示例数据并打开主菜单
src/data/            账号、图书、订单、会员枚举与内存存储
src/lib/             菜单交互、输入与业务操作
```

## 当前边界

- 没有文件或 SQL 持久化，重启会恢复初始数据。
- 没有真实支付、物流或线上账号系统；结算与订单状态均为课程逻辑。
- 各菜单基于同步终端输入，未实现多用户并发。
- 当前没有自动化测试套件；修改业务逻辑后需手动检查注册、登录、购物车、订单和管理员流程。

## 授权说明

仓库目前未提供独立的项目许可证。
