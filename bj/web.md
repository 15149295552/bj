#项目结构

##创建项目

django-admin startproject mysite1

##运行项目

python3 manage.py runserver
python3 manage.py runserver 端口号

##关闭服务

1. Ctrl + c
2. sudo lsof -i:端口号 - 查看PID
   sudo kill -9 PID

## manage

python3 manage.py - 查看所有子命令

##项目同名文件夹