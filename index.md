#### 1、先停止服务器

注：每台服务器都要执行

uwsgi --stop uwsgi.pid

nginx -s stop

#### 2、到仓库下载最新代码包

https://codehub-g.huawei.com/huben/CBGITSecurityPlatform/merge_requests

#### 3、把代码包上传到服务器上，然后解压

#### 4、如果此次上线涉及到模型数据库修改的

先迁移数据库，有脚本执行的执行数据库数据处理脚本

注：此步只需在160服务器上操作

#### 5、处理项目文件夹

删除原来项目huben目录下的除taskfile文件夹之外所有文件

将第2步解压后CBGITSecurityPlatform-master目录下的文件全部复制到huben目录下

#### 6、迁移数据库

注：此步只需在160服务器上操作

python3 manage.py makemigrations

python3 manage.py migrate

执行 python3 manage.py migrate 如果报错，请删除alarm、asset、learn、filing这4个模块下的迁移文件后，再执行python3 manage.py makemigrations和python3 manage.py migrate

#### 7、重启celery

supervisorctl restart all

#### 8、修改脚本的权限

chmod 777 /home/huben/huben/tools/cloc-1.84/cloc

#### 9、启动nginx和wusgi

nginx

uwsgi  --ini uwsgi.ini

#### 10、登录网站查看



[^1]: 日志文件所在目录：/applog
[^2]: 前端文件所在目录：/usr/share/nginx/html/dist



