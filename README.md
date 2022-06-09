# 毕业设计
李小龙  
20184522  
基于深度强化学习的多智能体游戏的设计与实现  

### 服务器基本环境
* 任意Linux操作系统
* Mysql数据库
* dotnet core 6.0
* 导入fan.sql数据库文件
****
## 游戏模块
* 编译依赖
  * 客户端
    * Visual Studio 2019
    * Unity3D 2020
    * .NET Framework 3.0
  * 服务端
    * MySql.Data包
* 使用方法
  * 修改服务端命令台项目Server05下Utils.cs文件中数据库连接字符串
    ```Csharp
    public static string sqlconnect = "data source=127.0.0.1;database=agar;user id=root;password=123456;pooling=true;charset=utf8;";
    ```
  * 修改服务端命令台项目Server05下Server05.cs文件44行中的IP地址为服务器内网IP  
    ```Csharp
    TcpUdpServer tcpServer = new TcpUdpServer("192.168.0.4", 1234);
    ```
  * 使用Unity3D打开工程文件Myproject2，修改TcpClientCon.cs文件45行中IP为服务器公网IP
    ```Csharp
    string ip = "106.13.226.191";
    ```
  * 在服务器中启动Server05项目，终端打印出“服务端已开启”代表启动成功
    ```
    dotnet run Server05.csproj
    ```
  * 在Unity3D中进行调试和发布
  * 游戏运行出现输入账号密码页面即为运行成功
****
## Web模块
* 编译依赖
  * IntelliJ IDEA 2021
  * java 11
* 使用方法
  * 用IDEA打开Spring Boot项目demo4，修改demo4/src/main/resources/static文件夹中所有html文件中IP地址为服务器公网IP
  * 在Maven中依次点击clean，package等待编译结束，将打包好的jar包放在服务器运行
    ```
    java -jar demo4-0.0.1-SNAPSHOT.jar
    ```
  * 在服务器运行dotnet命令台项目ELOScore
    ```
    dotnet run ELOScore.csproj
    ```
  * 在浏览器中输入IP:9999出现网站主页面即为运行成功（IP需替换成使用的服务器公网IP）
****
## 强化学习环境模块
* 编译依赖
  * Visual Studio 2019
  * Windows10操作系统
* 使用方法
  * 通过TeamGame类获取环境
    ```Csharp
    TeamGame env = new TeamGame();
    ```
  * Reset()函数刷新环境
    ```Csharp
    env.Reset();
    ```
  * updatastep()函数提交动作
    ```Csharp
    env.updatastep(actions);
    ```
  * Render()函数可视化本局游戏
    ```Csharp
    env.Render();
    ```
  * game.players[i].Obs()方法获取编号为i的玩家当前状态
    ```Csharp
    Obs obs = env.game.players[i].Obs();
    ```
****
## 游戏AI模块
* 编译依赖
  * Visual Studio 2019
  * TensorFlow.NET包
  * TensorFlow.Keras包
  * SciSharp.TensorFlow.Redist-Linux-GPU包
* 硬件环境
  * RTX 2080 Ti 11GB显存
  * Intel(R) Xeon(R) Platinum 8255C CPU @ 2.50GHz
  * 内存45GB
* 使用方法
  * 修改命令台项目Trainer下Utils.cs文件中的模型权重保存路径
    ```Csharp
    public static string save_path = "E:/vsProject/Trainer/";
    ```
  * 根据硬件设备显存适当修改命令台项目Trainer下Utils.cs文件中的batch_size防止显存爆炸
    ```Csharp
    public static int batch_size = 128;
    ```
  * 点击开始运行程序即为开始训练
