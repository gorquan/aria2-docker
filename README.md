# aria2-docker

* 前段时间需要搞个离线下载，通过rclone和fast.io利用一下GD盘，然后就发现了一个好东西[Aria2-Pro](https://p3terx.com/archives/docker-aria2-pro.html),但是没有Aria2前端面板，于是我花了点时间把Aria2-Pro、AriaNg和Nginx整合在一起

* 使用方法
    1. 前往Digitalocean[生成Nginx配置](https://www.digitalocean.com/community/tools/nginx)或手动编写Nginx配置
    2. 前往[AriaNg](https://github.com/mayswind/AriaNg/releases)下载AriaNg源码
    3. 创建`aria-2-nginx-config`文件夹，并将修改好的`Nginx配置`移动到`aria-2-nginx-config`文件夹下
    4. 创建`aria-2-web`文件夹，将`AriaNg`源码根目录移动到`aria-2-web`文件夹下
    5. 修改docker-compose.yaml，将`/var/www/domain/public`中的`domain`替换为你的网站域名，与`Nginx配置`中的`root`对应
    6. 修改docker-compose.yaml,将`RPC_SECRET`中的`secret`修改为你的密码，用于连接AriaNg
    7. 创建aria2-config和aria2-downloads文件夹
    8. 运行，等待容器全部启动

    ``` shell
    docker-compose up -d
    ```

    9. 参考文章配置Aria2-Pro
    10. 重启容器，等待容器全部启动

    ``` shell
    docker-compose down
    docker-compose up -d
    ```
    11. 浏览器访问`domain:7000`，在AriaNg添加你设定的`secret`，即可访问Aria2-Pro

* 其他命令
    * 停止容器

    ``` shell
    docker-compose down
    ```

    * 查看运行状态

    ``` shell
    docker ps 
    ```
* 注意
    * 如果配置发生更改，请执行`使用方法`中的第`10`步对容器进行重启
    * 如果需要添加其他高级配置，请参考`Aria2配置`中的文章
    * 与Aria2-Pro有关的故障请参考`Aria2配置`中的文章进行调试解决
    * 若要添加Aria2-Pro中的命令行参数，请在`docker-compose.yaml`进行修改

* Aria2配置
    * 配置Aria2-pro
        * 请参考文章[Aria2-Pro](https://p3terx.com/archives/docker-aria2-pro.html)
    * 配置AriaNg
        * 请参考文章[AriaNg](https://p3terx.com/archives/aria2-frontend-ariang-tutorial.html)

* 开放端口
    * AriaNg Web端口：`*:7000`(如果需要修改为其他端口请在docker-compose.yaml中进行修改)
    * Aria2 端口: 6800/TCP, 6888/TCP, 6888/UDP (请勿改动)

* 参考连接
    * [AriaNg](https://github.com/mayswind/AriaNg)
    * [Aria2-Pro](https://github.com/P3TERX/docker-aria2-pro)
    * [Aira2-Pro参考文档](https://p3terx.com/archives/docker-aria2-pro.html)
    * [AriaNg参考文档](https://p3terx.com/archives/aria2-frontend-ariang-tutorial.html)

* 辅助工具
    * [Nginx配置生成](https://www.digitalocean.com/community/tools/nginx)

* ISSUE与PR
    * 如果有任何问题，欢迎提交ISSUE
    * 如果有自己的想法或者程序出现问题，并且已经实现，欢迎提交PR
