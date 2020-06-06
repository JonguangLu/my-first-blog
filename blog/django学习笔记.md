## 创建虚拟空间
- <a href="https://wechat.python666.cn/static/djangogirl/djangogirl.html?page=2">安装python3虚拟空间参考文档</a>
- 在家目录下创建了一个django目录，路径是/home/jonguang/django
``` 
创建虚拟空间python3 -m venv myvenv
jonguang@Lu:~/django$ python3 -m venv myvenv

```
- 运行和进入虚拟空间
- source myvenv/bin/activate
```
jonguang@Lu:~/django$ source myvenv/bin/activate
(myvenv) jonguang@Lu:~/django$ 
成功进入myvenv虚拟空间
```

## 安装Django
- pip3 install django
- 国内镜像源更快pip3 install django==2.2.12 -i https://pypi.tuna.tsinghua.edu.cn/simple
    - 这是安装2.2.12版本。本地版本对应Python3.5.3
    - 不能直接pip，会报一堆错，还是需要pip3
- 创建一个django项目
```
django-admin startproject mysite .
```
### 更改设置
- 创建项目后，打开django/mysite/settings.py
- 更改时区：TIME_ZONE = 'Asia/Shanghai'
- 还需要添加 (我们会找出在教程后面所提到的静态文件和 CSS文件) 静态文件的路径。 我们下拉到文件的 最底部 , 就是在 STATIC_URL 条目的下面。添加新的一行内容为 STATIC_ROOT 
```
STATIC_URL = '/static/'
STATIC_ROOT = os.path.join(BASE_DIR, 'static')
```
### 设置数据库
- 为我们的博客创建一个数据库，，让我们运行以下命令在控制台中： python manage.py migrate （我们需要 django 目录中包含 manage.py 文件）。
```
(myvenv) jonguang@Lu:~/django$ python manage.py migrate
```
### 启动服务器
- 必须要进入包含 manage.py 文件的目录 （ djangogirls 目录）。 在控制台中，我们可以通过运行 python manage.py runserver 开启 web 服务器
```
(myvenv) jonguang@Lu:~/django$ python manage.py runserver
```
- 检查是否正确运行 http://127.0.0.1:8000/

# github
- git秘钥路径：/home/jonguang/.ssh/id_rsa 
- The key fingerprint is:
    - SHA256:2teIDBhDfzcXRotFKW6QGDG916Rylkp59ajS6YoAICk lujunguang@qq.com
    - 第二次尝试 SHA256:k1EpDclUlxxM8viZfogUdF1Gm8PCojNb8tpkDh83dU0 lujunguang@qq.com
- 在/home/jonguang/.ssh/id_rsa.pub文件中找到ssh并添加到github的Settings-SSH and GPG keys
- ssh -T git@github.com 验证连接是否成功
- 绑定账号名和邮箱
```
jonguang@Lu:~$ git config --global user.name"JonguangLu"
jonguang@Lu:~$ git config --global user.email"lujunguang@qq.com"
```
- 在服务器添加完公钥后报错
    -  sign_and_send_pubkey: signing failed: agent refused operation
　　<br>这个时候我们只要执行下 eval "$(ssh-agent -s)"

```
添加ssh公钥后，应该执行下面代码就可以了
echo "# django" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/JonguangLu/django.git
git push -u origin master
```
```
jonguang@Lu:~/django$ git add ~/django/mysite/settings.py
jonguang@Lu:~/django$ git commit -m "第一次作业"
jonguang@Lu:~/django$ git push -u django master
```
#### 一些教程
- https://zhuanlan.zhihu.com/p/92134291
### 操作记录
- 在.git/config文件最后添加了
```
[receive]
denyCurrentBranch = ignore
```

## django模型
- 参考网站：<a href='https://wechat.python666.cn/static/djangogirl/djangogirl.html?page=4'>这里</a>
- 创建应用程序
 - (myvenv) ~/djangogirls$ python manage.py startapp blog
 - 创建一个blog的目录

- 创建应用程序后，我们还需要告诉 Django 它应该使用它。 我们是在 mysite/settings.py 文件中这样做的。 我们需要找到 INSTALLED_APPS 并在它下面添加一行 'blog' 。

- 创建一个博客文章模型
    - 我们在 blog/models.py 文件中，定义所有的 Models 对象— — 我们将在其中都定义我们的博客文章。

- 在数据库中为模型创建数据表
    - 在这里的最后一步是将我们新的模型添加到我们的数据库。 首先我们必须让Django知道我们在我们的模型(我们刚刚创建的！) 有一些变更。 输入 python manage.py makemigrations blog 。
    - Django为我们准备了我们必须应用到我们数据库的迁移文件。输入 python manage.py migrate blog 

## <a href='https://wechat.python666.cn/static/djangogirl/djangogirl.html?page=5'>Django admin管理后台</a>


# 部署
## 设置 ALLOWED_HOSTS
- 如果你要将你的网站部署在其它地方（如 PythonAnywhere），那么你需要设置 ALLOWED_HOSTS 。 ALLOWED_HOSTS 是为了限定请求中的host值，以防止黑客构造包来发送请求，保证只有在列表中的host才能访问。如果现在不理解也没关系，让我们先来设置它。

- 打开你的 django 项目，进入 mysite/settings.py，找到里面的 ALLOWED_HOSTS ，未设置前应该是这样：
```
ALLOWED_HOSTS = []
```
- 现在，将你在 PythonAnywhere 的地址和本地地址加入 ALLOWED_HOSTS ，加入后应该是这样:
```
ALLOWED_HOSTS = ['Jonguang.pythonanywhere.com', '127.0.0.1']
```


## pythonanywhere
- 设置了一些东西
```
(myvenv) 09:59 ~/my-first-blog (master)$ python manage.py createsuperuser
Username: JonguangLu
Email address: lujunguang@qq.com
Password: q12122323
Password (again): q12122323
Superuser created successfully.
```