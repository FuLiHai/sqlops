![image](https://raw.githubusercontent.com/hcymysql/sqlops/master/sqlops%E6%B5%81%E7%A8%8B.png)

10.22日更新

1)增加一键生成反向SQL回滚功能。

演示地址 http://fander.jios.org:8008/

普通上线账号：guest ，密码：123456

管理员审批账号：admin，密码：123456

感谢网友陈俊聪友情提供云主机。


-----------------------------------------------------
一、环境安装Centos6.8

1、php环境安装

# yum install httpd php mysql php-mysql php-devel php-pear libssh2 libssh2-devel -y

2、安装php ssh2扩展

pecl install -f ssh2

3、修改/etc/php.ini

在最后一行添加

extension=ssh2.so

4、关闭selinux

# vim /etc/selinux/config

SELINUX=disabled

5、美团网SQLAdvisor安装
请移步 https://github.com/Meituan-Dianping/SQLAdvisor/blob/master/doc/QUICK_START.md


6、binlog2sql安装
请移步 https://github.com/danfengcao/binlog2sql

-----------------------------------------------------

上线流程为：
开发提交SQL，系统自动审核（sql_review.php），审核通过后生成我的工单待管理员批复并且发邮件通知，管理员人工确认审核通过后，开发点击执行完成上线。

sqlops_approve/sql/sql_db.sql

涉及的表解释说明

1、login_user.sql  (sqlops平台系统登录表）

2、sql_order_wait.sql  （工单记录表）

3、dbinfo.sql	（数据库上线信息表）


脚本解释

1、index.html（用户登录入口）

2、login.php（用户密码校验）

3、main.php（首页框架栏）

4、header.php（用户登录欢迎页面，和注销）

5、left.php（导航栏）

6、sql_interface.php（SQL传参入口）

7、sql_review.php（SQL审核）

8、my_order.php（查看我的工单，执行，撤销）

9、wait_order.php（管理员人工批复：通过，否决）

10、update.php（管理员审批确认）

11、update_status.php（修改审批状态值）

12、execute.php（开发执行SQL工单）

13、execute_status.php（修改执行工单状态）

14、cancel.php（开发自行撤销工单）

15、cancel_status.php（修改撤销工单状态）

16、stat/show.html（工单动态统计图表）

17、db_config.php（DB配置信息的IP、端口、用户名、密码、库名）

18、sqladvisor_config.php（访问SQLAdvisor服务器的IP、SSH端口、SSH用户名、SSH密码）

19、rollback.php（生成回滚反向SQL）

20、mail/mail.php（提交工单时发送邮件通知）

---------------------
注：
1、客户端版本使用mysql5.5或者mariadb10.X。

5.6会出现Warning: Using a password on the command line interface can be insecure，导致上线失败。

2、php文件里的涉及连接数据库的用户名和密码要修改，这块没有做成统一个DB配置文件调用。

---------------------
#create审核

1、警告！表没有主键

2、警告！表主键字段名必须是id。

3、提示：id自增字段默认值为1，auto_increment=1

4、警告！表字段没有中文注释，COMMENT应该有默认值，如COMMENT '姓名'

5、警告！表没有中文注释，例：COMMENT='新版授信项表'

6、警告！表缺少utf8字符集，否则会出现乱码

7、警告！表存储引擎应设置为InnoDB

8、警告！表缺少update_time字段，方便抽数据使用，且给加上索引。

9、警告！表update_time字段类型应设置timestamp。

10、警告！表update_time字段缺少索引。

11、警告！表缺少create_time字段，方便抽数据使用，且给加上索引。


