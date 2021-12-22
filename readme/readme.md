# 开源软件技术期末大作业

项目：银行信息管理系统

姓名：刘嘉豪

学号：190110910718

没有使用token，使用ssh上传的GitHub。

指导老师：潘峰

# 一.项目设计

## 1.项目总体构成

​	安装方法：npm install 

​	运行方法：打开vscode运行app.js或者打开cmd输入node app.js

​	部署网站：http://localhost:10718

​	数据库名字：190110910718

​	本项目是银行信息管理系统，实现银行经理employee和客户customer账号的注册登录。customer登录后，可以实现修改个人信息、申请创建银行账户（银行卡）、查看每个账户的转账交易记录、查看每个账户的余额、开支票、设置收款人。employee登录后，可以审批customer申请银行账户信息、查看修改个人信息、查看修改客户信息和银行卡信息、实现支票转账。

## 2.数据库介绍

本项目数据库为：

accounts：存储账户信息

benificiaries：存储转账人信息

cards：存储银行卡信息

checks：存储支票信息

customers：存储客户信息

employee：存储经理信息

transactions：存储转账记录

users：存储所有用户信息

![image-20211219004039631](image-20211219004039631.png)

## 3.项目目录结构

Bank

├─ app.js    主函数

├─ data       用于密码解码编译

│  ├─ 27017

│  ├─ 27018

│  └─ 27019

├─ models   定义数据库

│  ├─ account.js  定义账户数据库

│  ├─ benificiary.js  定义转账人数据库

│  ├─ card.js   定义银行卡数据库

│  ├─ checks.js  定义支票数据库

│  ├─ customer.js  定义顾客数据库

│  ├─ employee.js  定义经理数据库

│  ├─ seqid.js  定义编号数据库

│  ├─ transactions.js  定义交易记录数据库

│  └─ user.js  定义用户数据库（customer+employee）

├─ package-lock.json

├─ package.json

├─ public  css目录

│  ├─ img

│  ├─ js

├─ routes 数据库增删改查

│  ├─ account.js  账户数据库增删改查

│  ├─ accountstats.js  转账人数据库增删改查

│  ├─ auth.js  实现用户登录注册

│  ├─ benificiary.js  转账人数据库增删改查

│  ├─ check.js  支票数据库增删改查

│  ├─ customer.js  顾客数据库增删改查

│  ├─ employee.js  经理数据库增删改查

│  └─ transactions.js  交易记录数据库增删改查

├─ seed.js 创建数据库

└─ views 系统页面设计

   ├─ accounts 账户模块界面

   │  ├─ new.ejs

   │  ├─ profile.ejs

   │  └─ show.ejs

   ├─ accountstats 交易记录界面

   │  ├─ entry.ejs

   │  └─ tables.ejs

   ├─ benificiary  转账人界面

   │  ├─ benificiary.ejs

   │  ├─ entry.ejs

   │  └─ new.ejs

   ├─ checks  支票模块界面

   │  ├─ empcheck.ejs

   │  ├─ entry.ejs

   │  ├─ gencheck.ejs

   │  └─ show.ejs

   ├─ employee  经理界面

   │  ├─ customers.ejs

   │  ├─ edit.ejs

   │  ├─ request.ejs

   │  └─ view.ejs

   ├─ home.ejs  主界面(部分)

   ├─ index.ejs

   ├─ login.ejs 登录界面

   ├─ partials 侧边栏

   │  ├─ footer.ejs

   │  └─ header.ejs

   ├─ signup.ejs  注册界面

# 二.使用说明

### 1.登录注册功能：

在第一次使用本系统时可以先注册账号，可以注册客户和经理两种账号。

![image-20211219000539371](image-20211219000539371.png)

注册后注册信息会出现在数据库中：

![image-20211219000953523](image-20211219000953523.png)

登录后进入主界面：

![image-20211219000658138](image-20211219000658138.png)

![image-20211219000710699](image-20211219000710699.png)

### 2.经理账号功能介绍：

#### （1）查看编辑个人信息：

![image-20211219001132022](image-20211219001132022.png)

### （2）查看或编辑所有客户信息（包括客户所拥有的账户，更新客户账户信息）：

![image-20211219001213394](image-20211219001213394.png)

![image-20211219001413227](image-20211219001413227.png)

![image-20211219001444464](image-20211219001444464.png)

### （3）审批客户申请开通账户的请求，接受后客户账户即可使用，未通过则无法使用：

![image-20211219001541856](image-20211219001541856.png)

### （4）实现支票转账，可以输入转出账户和转入账户，并且输入转出账户的支票编号可以实现转账：

![image-20211219001737155](image-20211219001737155.png)

例：使用账号**20200007**向账号**20200003**转账，使用支票**CHECK0014**转账**2000**元。

转账成功后后台会记录账户余额的变化，并且在数据库transactions中生成一笔交易记录：

![image-20211219002540488](image-20211219002540488.png)

### 3.客户账号功能介绍

#### （1）查看并修改个人信息，以及查看客户名下的账户信息（包括余额）：

![image-20211219002859488](image-20211219002859488.png)

![image-20211219002930342](image-20211219002930342.png)

#### （2）申请账户，申请账户需要经理同意后才能使用：

![image-20211219003024250](image-20211219003024250.png)

#### （3）查看账户的交易信息：

![image-20211219003129493](image-20211219003129493.png)

刚刚的例子中，**20200007**账户转出2000，在这里记录了交易信息和金额变化，在账户的余额也会有体现。![image-20211219003156084](image-20211219003156084.png)

#### （4）在这里可以查看每个账户添加的收款人信息，以及添加收款人信息：

![image-20211219003406805](image-20211219003406805.png)

![image-20211219003519117](image-20211219003519117.png)

![image-20211219003530830](image-20211219003530830.png)

#### （5）在这里可以给每个账户开支票，开的支票可以在employee经理端实现转账，并且查看支票的使用情况：

![image-20211219003730520](image-20211219003730520.png)

![image-20211219003738091](image-20211219003738091.png)

在刚刚的实例中账户**20200007**的支票**CHECK0014**被使用，状态则为Used。

# 三.开发日记

First commit：创建仓库

Second  commit：找到前端模板，并修改成ejs形式，并存储在views文件夹下。

Third commit：定义所有所需要数据库，数据库关系参考论文中银行管理系统的形式，存储在model文件夹下。

Fourth commit：实现数据库的增删改查，存储在routes文件夹下。

Fifth commit：建立主函数app.js,seed.js。

Sixth commit：添加data，实现登录密码的封装，并且提交readme。



