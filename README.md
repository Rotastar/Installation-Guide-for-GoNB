本篇教程用于在Windows系统上使用Docker Desktop on Windows部署GoNB项目的Docker并运行
该链接为下面可能用到的所有文件的集合下载链接：https://pan.baidu.com/s/1_bmmXI2MVDD9joRWXk2bPQ?pwd=wts9 推荐边下载边看本篇教程

0：安装Docker Desktop前的准备.

开启WSL2/Hyper-v（二者任选其一，我倾向于WSL2）
二者任选其一即可（貌似不开启也能运行？）

1：安装Docker Desktop.

  前往docker官网 https://www.docker.com/ (该网站需要使用科学)，根据你的计算机系统下载对应的安装包，以教程的amd64为例，点击如下按钮即可下载。
  ![image](https://github.com/user-attachments/assets/051306c0-38ec-47a9-9c29-6ff5444195bc)
若有科学环境，一般直接点击下载即可。(如果你不知道什么是科学，那请下面的教程安装没有科学进行)

考虑到本篇教程的使用者有可能没有科学环境，本人在此处也放一个百度网盘的共享链接：Docker-4.34-windows-x86.exe 链接：https://pan.baidu.com/s/1z-lOQTzqD-AtblqsbQlbFw?pwd=wqyy 

双击运行之后，安装包会自动展开并自动验证完整性，然后进入到这一界面：

第一个框代表了你是要使用WSL还是Hyper-v，如果你使用WSL保持默认即可，使用Hyper-v则取消勾选

第二个框代表了是否创建桌面快捷方式，默认勾选代表创建

点击下一步就开始了安装，安装完成后会自动要求你重启，建议重启以进行下一步

2：配置Docker Desktop并汉化

  1.初始化
  
    重启完成后双击桌面出现的快捷方式或用其他方式打开Docker Desktop
    第一个设置保持默认即可，直接点击下一步
    接下来会进入如图的界面，如果你有谷歌/github账号可以选择直接登录，或者直接创建一个新的账号（并未尝试过创建）（注册/登录也需要科学）
    大概率是没有账号的，所以我们选择最下面一行的跳过接下来进入到这个界面，是让你选择自己的身份，直接选择skip即可进入Docker的界面。
    
  2.汉化
    本人使用的汉化教程参考了https://github.com/asxez/DockerDesktop-CN 这篇教程中的这部分：
    
    1.关闭Docker Desktop
    2.在Docker安装目录（Windows下默认为C:\Program Files\Docker\Docker\frontend\resources，Macos下默认为/Applications/Docker.app/Contents/MacOS/Docker Desktop.app/Contents/Resources）找到app.asar文件并将其备份，防止出现意外。
    3.将从本仓库下载的asar文件改名为app.asar后替换原文件
    
  仍然是考虑到缺少科学上网的环境，照例我在这里放一个百度网盘的链接：app-4.34-windows.asar 链接：https://pan.baidu.com/s/1ttlgEFAeC0EjFNk7ZQwwTw?pwd=tutx 
  
  使用4.34的汉化包，遵循上方的教程即可成功汉化（注意要点是关闭Docker Desktop要彻底，否则可能存在文件被占用的可能性）

  成功替换后即可双击运行启动，发现大部分内容被汉化即成功

  1.如果你有科学，开启科学进入软件后，在扩展里搜索名为Copacetic的扩展（一般为第一个）并安装
  ![image](https://github.com/user-attachments/assets/72f0f217-087d-4196-9dec-33c772f4097f)
  过会就会出现这样的界面，点击Open后会出现如图
  ![image](https://github.com/user-attachments/assets/a0ab4935-6be3-4d8f-aa75-2f2b9cd58d4f)
  在此处直接import GONB的两个包即可，照例端上两个包的下载链接：
  ![image](https://github.com/user-attachments/assets/96011ec4-04e8-4a58-9d31-0cac3d3baee5)
  等待一段时间后就会出现如图这些镜像（真的会很久）
  ![image](https://github.com/user-attachments/assets/e2da9f46-74ca-4f1b-8735-46d293750a24)
  2.如果你没有科学,请按如下步骤进行：
  
  打开你存放2.5G和500M tar文件的路径，然后执行
  
    docker load -i gonb_jupyterlab.tar
    docker load -i gophernotes.tar
    
  等待一会docker里的镜像里应该就会出现两个镜像了（真的会很久）
  
  依次点击含有go字样的你导入的大小分别为2.5G和500M的两个镜像右侧的run
  ![image](https://github.com/user-attachments/assets/fa0ce9f3-7ea8-4e9f-8d20-f973253cd3bb)
  如图配置第一个run，Host port为你访问的端口号，8888只是参考端口号
  
  Host path为你本地的地址，图上的仅为参考，实际用你本地实际存在的地址即可，在docker上的更改会同步到本地，推荐地址：Documents\GoNB(此为相对地址，Documents即"文档"的目录不同电脑不同，不要照抄)

  Container path填/notebooks/host 意为Host path挂载到docker内的地址
  
  点击run之后会出现如图的界面
  ![image](https://github.com/user-attachments/assets/cab92abe-d8ab-4f1d-acb7-a3c1260e26ae)
  点击该链接即可访问GoNB的网页界面，到这里，GoNB的配置就完成了

  接下来就是配置另外一个
  ![image](https://github.com/user-attachments/assets/4ec51649-e9c6-41cf-b649-6e8fddb61939)
  如图配置，与上一个的区别在于端口号不得相同否则会冲突，8889也只是一个参考端口号，Host path与Container path与上一个配置保持相同
  
  配置完成后同样会有一个链接，点击即可访问后台数据库
  
  到这里，你的GoNB就部署成功了
  

  
  


