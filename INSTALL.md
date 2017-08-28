## 环境准备
1. 请确保使用的Composer和Composer Asset Plugin是最新版本，如果不是，需要执行以下命令：

    ```bash
    composer self-update
    composer global require "fxp/composer-asset-plugin:^1.3.1" --no-plugins
    ```
2. 建议更改为国内镜像，可以有效提高下载速度（可跳过）
    ```bash
    composer config -g repo.packagist composer https://packagist.phpcomposer.com
    ```
## 安装说明
1. 新建名为`wocenter`的数据库
2. 克隆 WoCenter 项目

    切换到一个可以通过 Web 访问的目录（如：`/home/www`），执行如下命令即可安装 WoCenter ：
    ```bash
    git clone https://github.com/Wonail/wocenter_advanced.git
    cd wocenter_advanced #进入项目目录
    ```

3. 修改配置文件添加数据库相关信息

    开发环境
    > environments/dev/common/config/main-local.php

    正式环境
    > environments/prod/common/config/main-local.php

    ```php
        'components' => [
            'db' => [
                ……，
                'dsn' => 'mysql:host=localhost;dbname=wocenter', // 数据库名称，如果没有修改，默认为wocenter
                'username' => 'root', // 数据库用户名
                'password' => '', // 数据库密码
                ……，
            ],
            ……
        ]
    ```
4. 安装composer依赖
    ```bash
    composer install
    ```

5. 安装所需扩展

    打开`localhost/wocenter_advanced/requirements.php`检查所需扩展是否已经安装，WoCenter建议安装**Intl**

6. 使用 WoCenter 内置的安装方法完成剩余的安装步骤
    ```bash
    ./yii wocenter/install
    ```

## 使用说明
1. WoCenter 默认开启URL美化和隐藏index.php功能，所以需要先执行以下步骤确保应用可以正常运行：

    添加指向backend应用的虚拟主机：
    ```
    <VirtualHost backend.wocenter.dev:80>
            DocumentRoot /home/www/wocenter_advanced/backend/web #`/home/www`路径为wocneter项目所在的实际路径
    </VirtualHost>
    ```

    添加hosts域名映射：
    ```
    127.0.0.1	    backend.wocenter.dev
    ```

    启用rewrite模块并重启服务器：
    ```
    sudo a2enmod rewrite
    sudo service apache2 ressart
    ```

2. 进入网页`backend.wocenter.dev`即可登录

    账号：admin

    密码：admin123