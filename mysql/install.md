# mysql安装过程

## 目录
- [zip](#zip)
    - [安装](#安装)


## zip

### 安装：
1. 解压zip包到安装目录

    D:\Program Files\MySql

2. 添加配置文件

由于在解压目录中并没有my.ini或my-default.ini，故在D:\Program Files\MySql下添加my.ini并写入配置：

    [mysqld]
    # 设置3306端口
    port=3306
    # 设置mysql的安装目录
    basedir=D:\Program Files\MySql
    # 设置mysql数据库的数据的存放目录
    datadir=G:\DataBase\MySql
    # 允许最大连接数
    max_connections=200
    # 允许连接失败的次数。这是为了防止有人从该主机试图攻击数据库系统
    max_connect_errors=10
    # 服务端使用的字符集默认为UTF8
    character-set-server=utf8
    # 创建新表时将使用的默认存储引擎
    default-storage-engine=INNODB
    # 默认使用“mysql_native_password”插件认证
    default_authentication_plugin=mysql_native_password
    [mysql]
    # 设置mysql客户端默认字符集
    default-character-set=utf8
    [client]
    # 设置mysql客户端连接服务端时默认使用的端口
    port=3306
    default-character-set=utf8
参考：mysql配置项：https://dev.mysql.com/doc/refman/8.0/en/mysqld-option-tables.html

3. 初始化数据

在D:\Program Files\MySq\bin执行命令：

    mysqld --initialize --console
注意在执行输出的其中一段：

    [Note] [MY-010454] [Server] A temporary password is generated for root@localhost: rI5rvf5x5G,E
其中root@localhost:后面的“;tWkXlj*Y0ur”就是初始密码（不含首位空格）。在没有更改密码前，需要记住这个密码，后续登录需要用到

参考：https://dev.mysql.com/doc/refman/8.0/en/data-directory-initialization-mysqld.html

4. 安装服务

在MySQL安装目录的 bin 目录下执行命令（以管理员身份打开cmd命令行）：

    mysqld --install [服务名]
后面的服务名可以不写，默认的名字为 mysql。当然，如果你的电脑上需要安装多个MySQL服务，就可以用不同的名字区分了，比如 mysql5 和 mysql8。

安装完成之后，通过命令：

    net start mysql
启动MySQL的服务。

* 设置密码

　　在MySQL安装目录的 bin 目录下执行命令：

    mysql -u root -p

　　使用第3步中的密码登录，修改密码

    ALTER USER USER() IDENTIFIED BY 'Jwliet-123';
注意：

以上命令都是在CMD下执行，若在PowerShell下可能出现

    PS D:\Program Files\MySql\bin> mysqld --initialize --console
    mysqld : 无法将“mysqld”项识别为 cmdlet、函数、脚本文件或可运行程序的名称。请检查名称的拼写，如果包括路径，请确保路径
    正确，然后再试一次。
    所在位置 行:1 字符: 1
    + mysqld --initialize --console
    + ~~~~~~
        + CategoryInfo          : ObjectNotFound: (mysqld:String) [], CommandNotFoundException
        + FullyQualifiedErrorId : CommandNotFoundException
在执行安装服务时可能出现服务安装失败的情况，以管理员身份运行可解决

    Install/Remove of the Service Denied！
