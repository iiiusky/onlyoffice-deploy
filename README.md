

# ![logo](http://public-bisheng.oss-cn-zhangjiakou.aliyuncs.com/resource/logo.png)毕升文档云平台安装步骤

[毕升文档](https://ibisheng.cn)| 协同编辑 | 在线Office| onlyOffice

## 硬件要求

安装过程时在centos7系统下进行的，系统为4核8G虚拟云主机服务器。建议使用新安装的系统来安装毕升文档云平台。需要注意的是所有的安装都是root用户执行的。如果您的安装环境不能使用root用户，理论上是不会有问题的，如果碰到权限相关问题请自行搜索资料解决。

## 步骤

1. 从[github](https://github.com/ibisheng/deploy.git)上clone相关的部署脚本到服务器上

   ```shell
   git clone https://github.com/ibisheng/deploy.git
   cd deploy
   ```

2. 安装docker以及docker-compose

   毕升文档云平台所有的服务均是基于docker-compose安装的，在进行下一步安装之前，请确保你的服务器上已经安装了docker已经docker-compose。你可以使用我们准备的脚本安装,也可以自行参考资料进行安装。r如果你是使用脚步安装可以直接执行 preinstall.sh脚本

   ```shell
   sh preinstall.sh
   ```

   如果自行安装可以参考docker安装资料：**[docker 安装](https://docs.docker.com/install/linux/docker-ce/centos/#install-docker-ce)**，而docker-compose安装则可以执行如下命令进行：

   ```shell
   curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
   chmod +x /usr/local/bin/docker-compose
   systemctl start docker
   systemctl enable docker
   ```

   在安装完成之后，可以通过命令行参看docker以及dockder-compose的版本

   ![image-20190225144902164](https://public-bisheng.oss-cn-zhangjiakou.aliyuncs.com/resource/docker-version.png)

3. 一键安装毕升文档云平台

   在完成以上步骤之后，可以通过install.sh脚本来安装毕升文档

   ```shell
   sh install.sh /data 192.168.2.108
   ```

   该安装命令需要两个参数：一个是参数是安装目录，该目录是毕升文档的工作目录，所以的数据都会保存在该目录，需要保证该目录所有在的存储设备上有较大的空间。在上面的脚步是我们是使用 /data目录作为安装目录；另外一个参数是本机的IP，安装完成之后可以通过这个IP来访问毕升文档。需要注意的是，**该IP不能为127.0.0.1，该IP地址需要在docker容器里面也能够连接上**

4. 测试

   待上一步骤脚本执行完成之后，先检查所有的docker容易是否全部正常启动。

   ```shell
   cd service
   docker-compose ps
   cd ../workspace/
   export basedir=/data
   docker-compose ps
   ```

   注意：进入 service目录之后 docker-compose ps 查看的是毕升文档依赖服务的docker容器；进入到workspace 目录查看的是毕升文档所有的服务的容器。export basedir=/data指定的环境变量值为毕升文档安装目录。

   ![image-20190225150645223](https://public-bisheng.oss-cn-zhangjiakou.aliyuncs.com/resource/docker-status.png)

   如果以上容器状态都正常则表明安装已经完成。

5. 如何使用

   1. 以上安装完成之后，输入地址 http://192.168.2.108:3000即可进入到毕升文档主页面。其中IP为第三步安装过程中指定的IP。 

   ![image-20190225153147382](https://public-bisheng.oss-cn-zhangjiakou.aliyuncs.com/resource/ibisheng.png)

6. 如何配置

   完成前面5步操作之后，你的毕升文档系统需要进行简单的[license配置](https://ibisheng.cn)之后就可以正常使用。