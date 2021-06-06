
## <center>Product</center>   
- [**0x00 Introduction**](#0x00-introduction)    
- [**0x01 Version List**](#0x01-version-list)    
- [**0x02 Build Step**](#0x02-build-step)    
    - [**Build System**](#centerbuild-systemcenter)        
        - [**Step 1 - Create user**](#step-1---create-user)        
        - [**Step 2 - Link WinSCP**](#step-2---link-winscp)        
        - [**Step 3 - Change apt source**](#step-3---change-apt-source)        
        - [**Step 4 - Update SYS**](#step-4---update-sys)        
        - [**Step 5 - Install Tasksel**](#step-5---install-tasksel)        
        - [**Step 6 - Install Apache Mysql PHP**](#step-6---install-apache-mysql-php)        
        - [**Step 7 - Node.js & Npm**](#step-7---nodejs--npm)
        - [**Step 8 - Yarn**](#step-8---yarn)        
        - [**Step 9 - Composer**](#step-9---composer)        
        - [**Step 9 - imagick**](#step-9---imagick)        
        - [**Step 10 - Redis**](#step-10---redis)        
        - [**Step 11 - Install Zip**](#step-11---install-zip)        
        - [**Step 11 - Upload large size file**](#step-11---upload-large-size-file)    
    - [**Build Laravel**](#centerbuild-laravelcenter)        
        - [**Step 1 - Install Laravel**](#step-1---install-laravel)        
        - [**Step 2 - Install PackageManager**](#step-2---install-packagemanager)        
        - [**Step 3 - Setting .editorconfig**](#step-3---setting-editorconfig)        
        - [**Step 4 - Setting .env**](#step-4---setting-env)        
        - [**Step 5 - Setting config**](#step-5---setting-config)        
        - [**Step 6 - Change files permission**](#step-6---change-files-permission)
        - [**Step 7 - Apache2 URL**](#step-7---apache2-url)    
    - [**Install Packages**](#centerinstall-packagescenter)        
        - [**Step 1 - Install Bootstrap**](#step-1---install-bootstrap)        
        - [**Step 2 - Install fontawesome**](#step-2---install-fontawesome)        
        - [**Step 3 - Install laravel-ide-helper**](#step-3---install-laravel-ide-helper)        
        - [**Step 4 - Install Laravel-lang**](#step-4---install-laravel-lang)        
        - [**Step 5 - Install Captcha**](#step-5---install-captcha)        
        - [**Step 6 - Install Intervention Image**](#step-6---install-intervention-image)        
        - [**Step 7 - Install CKfinder**](#step-7---install-ckfinder)        
        - [**Step 7 - Install CKeditor**](#step-7---install-ckeditor)        
        - [**Step 7 - Install Voyager**](#step-7---install-voyager)

---
---

## **0x00 Introduction**
This document records some methods and commands for building a website

---
---

## **0x01 Version List**
- Ubuntu 18.04 LTS
- Laravel 6.x
- Php latest version
- Apache latest version
- Mysql latest version
- Npm latest version
- Yarn latest version

---
---
## **0x02 Build Step**
---
## <center>Build System</center>
---

### **Step 1 - Create user**

```
$ sudo passwd root
```


### **Step 2 - Link WinSCP**
- Find `/etc/ssh/sshd_config` file

    ```php
    ## Find
    LoginGraceTime 2m
    PermitRootLogin without-password
    StrictModes yes

    ## Change to 
    LoginGraceTime 2m
    PermitRootLogin yes
    StrictModes yes
    ```

    > <font color=#dea32c>**Warning:**</font> If choose "`PermitRootLogin yes`", the system safety have hidden risk.

    Restart System
    ```Shell
    $ sudo reboot
    ```



### **Step 3 - Change apt source**
Find `/etc/apt/sources.list` file
- USTC
    ```php
    deb https://mirrors.ustc.edu.cn/ubuntu/ bionic main restricted universe multiverse

    deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic main restricted universe multiverse

    deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse

    deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse

    deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse

    deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse

    deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-security main restricted universe multiverse

    deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-security main restricted universe multiverse

    deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse

    deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse
    ```

- Aliyun
    ```php
    deb http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse

    deb http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse

    deb http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse

    deb http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse

    deb http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse

    deb-src http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse

    deb-src http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse

    deb-src http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse

    deb-src http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse

    deb-src http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
    ```

### **Step 4 - Update SYS**
- Install 
    ```Shell
    $ sudo apt-get update && apt-get upgrade -y
    ```

### **Step 5 - Install Tasksel**
```Shell
$ sudo apt-get install tasksel
```

### **Step 6 - Install Apache Mysql PHP**

- Install LAMP
    ```Shell
    $ sudo tasksel install lamp-server
    ```

- Install Phpmyadmin
    ```Shell
    $ sudo apt-get install phpmyadmin

    $ sudo ln -s /usr/share/phpmyadmin/ /var/www/ 

    $ sudo /etc/init.d/apache2 restart 
    ```

- Make the database accessible externally

    Find `/etc/mysql/debian.cnf` file

    ```php
    user     = debian-sys-maint
    password = **********************
    ```
    > <font color=#dea32c>**Tips:**</font> Login phpmyadmin by "debian-sys-maint" Change MySQL User permissions(change localhost@root and add %@SQLAdmin).



- Find `/etc/mysql/mysql.conf.d/mysqld.cnf` file

    ```php
    ## Find this
    bind-address  = 127.0.0.1

    ## Change to 
    bind-address  = 0.0.0.0

    ## or
    bind-address  = 0.0.0.0
    ```

- Restart mysql
    ```Shell
    $ /etc/init.d/mysql restart
    ```

- Find `/etc/apache2/apache2.conf` file

    ```php
    ## Find this
    Options FollowSymLinks
    AllowOverride None
    Require all denied

    ## Change to 
    Options Indexes FollowSymLinks
    AllowOverride All
    Require all granted
    ```
- Enable Rewrite
    ```Shell
    $ sudo a2enmod rewrite

    $ sudo /etc/init.d/apache2 restart
    ```


### **Step 7 - Node.js & Npm**
><font color=#dea32c>**Tips :**</font> [Node.js documentation](https://nodejs.org/en/docs/)

- Install Node.js

    From [Node.js download page](https://nodejs.org/en/download/) get latest version or LTS version


    ```Shell
    ## add source
    $ curl -sL https://deb.nodesource.com/setup_16.x | sudo -E bash -

    ## install
    $ sudo apt-get install -y nodejs
    ```

    Check version
    ```Shell
    $ node -v

    $ npm -v
    ```


### **Step 8 - Yarn**
><font color=#dea32c>**Tips :**</font> [Yarn Document](https://yarn.bootcss.com/docs/install/#debian-stable)

- Install
    ```Shell
    $ curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -

    $ echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list

    $ sudo apt update && sudo apt install yarn
    ```

    Check version
    ```Shell
    $ yarn -v
    ```

### **Step 9 - Composer**
><font color=#dea32c>**Tips :**</font> [Composer Document](https://getcomposer.org/doc/)

- Install
    ```Shell
    ## download
    $ php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"

    ## install
    $ php composer-setup.php

    ## move it to call globally
    $ mv composer.phar /usr/local/bin/composer

    ## setting permissions
    $ chmod +x /usr/local/bin/composer
    ```

- Set composer source

    Aliyun
    
    ```shell
    ## the configuration only takes effect in the current project
    $ composer config repo.packagist composer https://mirrors.aliyun.com/composer/

    ## cancel current project configuration
    $ composer config --unset repos.packagist
    ```

    ```shell
    ## Configuration takes effect globally
    $ composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/

    ## Cancel global configuration
    $ composer config -g --unset repos.packagist
    ```

    List all available mirror sources, preceded by * represents the currently used mirror
    ```Shell
    $ composer repo:ls
    ```

### **Step 9 - imagick**
- Install php-dev
    ```shell
    $ apt-get install php-dev
    ```

- Install ImageMagick
    ```shell
    $ sudo apt-get install imagemagick
    ```

- Install unzip
    ```shell
    $ sudo apt-get install unzip
    ```

- Install imagemagick-dev
    ```shell
    $ sudo apt-get install libmagick++-dev
    ```

- Install imagick
    ```shell
    $ pecl install imagick
    ```

- Add imagick

    Find "`/etc/php/7.2/apache2/php.ini`" file 
    ```php
    extension=imagick.so
    ```


### **Step 10 - Redis**
><font color=#dea32c>**Tips :**</font> [Redis Document](https://redis.io/download)

- Installation
```shell
$ sudo apt-get install redis
```


### **Step 11 - Install Zip**
```shell
$ sudo apt-get install zip
```


### **Step 11 - Upload large size file**
- Change php config

    Find "`/etc/php/<version>/apache2/php.ini`" file
    ```php
    # allow file upload
    file_uploads=on

    # script execution max time, 600 = 60s
    max_execution_time=1200

    # script execution max memory limit
    memory_limit=2048M

    # max file size allowed to upload
    upload_max_filesize=2048M

    # upload file temp directory
    upload_tmp_dir

    # max file size allowed to upload by post
    post_max_size=4096M

    ```
    > <font color=#dea32c>**Tips :**</font> `post_max_size` need to be greater than `upload_max_filesize`

- Restart apache2
    ```shell
    $ /etc/init.d/apache2 restart
    ```

---
## <center>Build Laravel</center>
---
><font color=#dea32c>**Quick Build**</font>
> 
> `$ composer install`
>
> `$ yarn install`
>
> `$ cp .env.example .env`
>
> `$ php artisan key:generate`
> 
> `$ chmod -R 777 storage bootstrap/cache`
>
> `$ php artisan storage:link`
>
> `$ mkdir -m 777 storage/app/public/upload`
>
> `$ mkdir -m 777 storage/app/public/upload/files`
>
> `$ mkdir -m 777 storage/app/public/upload/images`
>
> `$ mkdir -m 777 storage/app/public/upload/videos`
>
> `$ php artisan ckfinder:download`
>
> `$ php artisan ide-helper:generate`
> 
> `$ npm run watch-poll`
> 
> Change voyager vendor([**Step 7 - Install Voyager**](#step-7---install-voyager))
>
> `$ php artisan voyager:install`
>
> Quick create user\
> `$ php artisan voyager:admin your@email.com --create`


--- 
### **Step 1 - Install Laravel**
```Shell
## composer create-project --prefer-dist laravel/laravel <App Name> <Laravel version>
## example
$ composer create-project --prefer-dist laravel/laravel web "6.*"
```


### **Step 2 - Install PackageManager**

```shell
$ npm install

## or
$ yarn install
```

><font color=#dea32c>**Tips :**</font> Change source
>
> ```shell
> ## Change source
> $ npm config set registry=https://registry.npm.taobao.org
>
> $ yarn config set registry https://registry.npm.taobao.org
>
> ## Reset source
> $ npm config set registry=https://registry.npmjs.org/
>
> $ yarn config set registry https://registry.yarnpkg.com/
> 
> ## Check config
> $ npm config get registry
>
> $ yarn config get registry
> ```
> --


### **Step 3 - Setting .editorconfig**
```
root = true

[*]
root = true

[*]
charset = utf-8
end_of_line = lf
insert_final_newline = true
indent_style = space
indent_size = 4
trim_trailing_whitespace = true

[*.md]
trim_trailing_whitespace = false

[*.{yml,yaml}]
indent_size = 2

[*.{js,html,blade.php,css,scss}]
indent_style = space
indent_size = 4
```


### **Step 4 - Setting .env**
Find "`/var/www/web/.env`" file
```
APP_NAME=Laravel 
APP_URL=http://localhost

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=homestead
DB_USERNAME=homestead
DB_PASSWORD=secret
```


### **Step 5 - Setting config**
Find "`../config/app.php`" file
```php
# Time zeon
'timezone' => 'Asia/Shanghai',

# default language
'locale' => 'zh-CN',
```

### **Step 6 - Change files permission**
```shell
$ chmod -R 777 storage bootstrap/cache
```


### **Step 7 - Apache2 URL**
- Copy apache2 conf
    ```shell
    $ cd /etc/apache2/sites-available
    $ mkdir web
    $ cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/web/web.conf
    ```

- Set URL
    Find "`/etc/apache2/sites-available/web/web.conf`" file
    ```shell
    <VirtualHost *:80>
        # The ServerName directive sets the request scheme, hostname and port that
        # the server uses to identify itself. This is used when creating
        # redirection URLs. In the context of virtual hosts, the ServerName
        # specifies what hostname must appear in the request's Host: header to
        # match this virtual host. For the default virtual host (this file) this
        # value is not decisive as it is used as a last resort host regardless.
        # However, you must set it for any further virtual host explicitly.
        #ServerName www.example.com

        ServerAdmin webmaster@localhost
        # ServerName www.website.com
        DocumentRoot /var/www/web/public

        # Available loglevels: trace8, ..., trace1, debug, info, notice, warn,
        # error, crit, alert, emerg.
        # It is also possible to configure the loglevel for particular
        # modules, e.g.
        #LogLevel info ssl:warn

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

        # For most configuration files from conf-available/, which are
        # enabled or disabled at a global level, it is possible to
        # include a line for only one particular virtual host. For example the
        # following line enables the CGI configuration for this host only
        # after it has been globally disabled with "a2disconf".
        #Include conf-available/serve-cgi-bin.conf
    </VirtualHost>

    # vim: syntax=apache ts=4 sw=4 sts=4 sr noet
    ```
    
- Add URL
    Find "`/etc/apache2/sites-available/000-default.conf`" file
    ```php
    Include "/etc/apache2/sites-available/web/*.conf"

    <VirtualHost *:80>
        # The ServerName directive sets the request scheme, hostname and port that
        # the server uses to identify itself. This is used when creating
        # redirection URLs. In the context of virtual hosts, the ServerName
        # specifies what hostname must appear in the request's Host: header to
        # match this virtual host. For the default virtual host (this file) this
        # value is not decisive as it is used as a last resort host regardless.
        # However, you must set it for any further virtual host explicitly.
        #ServerName www.example.com

        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/html

        # Available loglevels: trace8, ..., trace1, debug, info, notice, warn,
        # error, crit, alert, emerg.
        # It is also possible to configure the loglevel for particular
        # modules, e.g.
        #LogLevel info ssl:warn

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

        # For most configuration files from conf-available/, which are
        # enabled or disabled at a global level, it is possible to
        # include a line for only one particular virtual host. For example the
        # following line enables the CGI configuration for this host only
        # after it has been globally disabled with "a2disconf".
        #Include conf-available/serve-cgi-bin.conf
    </VirtualHost>

    # vim: syntax=apache ts=4 sw=4 sts=4 sr noet
    ```

- Restart Apache2
    ```shell
    $ /etc/init.d/apache2 restart
    ```


---
## <center>Install Packages</center>
---
### **Step 1 - Install Bootstrap**
><font color=#dea32c>**Tips :**</font> [Bootstrap document](https://getbootstrap.com/docs/4.5/getting-started/introduction/)

- Install
    ```shell
    $ composer require laravel/ui:^1.0 --dev
    ```

- Import
    ```shell
    $ php artisan ui bootstrap
    ```

- Install package
    ```shell
    $ yarn install
    ```

- Fix resources
    ```shell
    $ npm run watch-poll
    ```


### **Step 2 - Install fontawesome**
><font color=#dea32c>**Tips :**</font> [fontawesome document](https://fontawesome.com/how-to-use/on-the-web/referencing-icons/basic-use)

- Install
    ```shell
    $ yarn add @fortawesome/fontawesome-free
    ```

- Load
    Find "`resources/sass/app.scss`" file, add:
    ```scss
    // Fontawesome
    @import '~@fortawesome/fontawesome-free/scss/fontawesome';
    @import '~@fortawesome/fontawesome-free/scss/regular';
    @import '~@fortawesome/fontawesome-free/scss/solid';
    @import '~@fortawesome/fontawesome-free/scss/brands';
    ```

- Fix resources
    ```shell
    $ npm run watch-poll
    ```

### **Step 3 - Install laravel-ide-helper**
><font color=#dea32c>**Tips :**</font> [laravel-ide-helper document](https://github.com/barryvdh/laravel-ide-helper)

- Install
    ```shell
    $ composer require barryvdh/laravel-ide-helper --dev
    ```

- Add config
    Find "`app/Providers/AppServiceProvider.php`" file, add:
    ```php
    public function register()
    {
        if ($this->app->environment() !== 'production') {
            $this->app->register(\Barryvdh\LaravelIdeHelper\IdeHelperServiceProvider::class);
        }
        // ...
    }
    ```

- Publish configuration
    ```shell
    ## PHPDoc generation for Laravel Facades
    $ php artisan ide-helper:generate

    ## PHPDocs for models
    $ php artisan ide-helper:models 

    ## PhpStorm Meta file
    $ php artisan ide-helper:meta
    ```

- Add file to `.gitignore`
    ```shell
    .idea
    _ide_helper.php
    _ide_helper_models.php
    .phpstorm.meta.php
    ```

### **Step 4 - Install Laravel-lang**
><font color=#dea32c>**Tips :**</font> [Laravel-lang document](https://github.com/overtrue/laravel-lang)

- Install
    ```shell
    $ composer require "overtrue/laravel-lang:~3.0"
    ```

- Change config

    Find "`config/app.php`" file
    ```php
    # Find this
    Illuminate\Translation\TranslationServiceProvider::class,

    # Replace 
    Overtrue\LaravelLang\TranslationServiceProvider::class,
    ```

- Publish configuration
    ```shell
    $ php artisan lang:publish [LOCALES] {--force}

    ## example
    $ php artisan lang:publish zh-CN,zh-HK,th,tk
    ```


### **Step 5 - Install Captcha**
><font color=#dea32c>**Tips :**</font> [Captcha for Laravel document](https://github.com/mewebstudio/captcha)

- Install
    ```shell
    $ composer require mews/captcha
    ```

- Publish configuration
    ```shell
    $ php artisan vendor:publish --provider='Mews\Captcha\CaptchaServiceProvider' 
    ```

### **Step 6 - Install Intervention Image**
><font color=#dea32c>**Tips :**</font> [Intervention Image document](http://image.intervention.io/)

- Install
    ```shell
    $ composer require intervention/image
    ```

- Publish configuration
    ```shell
    $ php artisan vendor:publish --provider="Intervention\Image\ImageServiceProviderLaravelRecent"
    ```

### **Step 7 - Install CKfinder**
><font color=#dea32c>**Tips 1 :**</font> [CKFinder 3 document](https://ckeditor.com/docs/ckfinder/latest/)
>
><font color=#dea32c>**Tips 2 :**</font> [CKFinder 3 – PHP Connector Documentation
](https://ckeditor.com/docs/ckfinder/ckfinder3-php/index.html)
>
><font color=#dea32c>**Tips 3 :**</font> [CKFinder 3 Laravel github](https://github.com/ckfinder/ckfinder-laravel-package)

- Add a Composer dependency and install the package
    ```shell
    $ composer require ckfinder/ckfinder-laravel-package
    ```

- Run the command to download the CKFinder code
    ```shell
    $ php artisan ckfinder:download
    ```

- Publish the CKFinder connector configuration and assets.
    ```shell
    $ php artisan vendor:publish --tag=ckfinder-assets --tag=ckfinder-config
    ```


- Create a directory for CKFinder files and allow for write access to it.
    ```shell
    ## example
    $ mkdir -m 777 storage/app/public/upload/files

    $ mkdir -m 777 storage/app/public/upload/images

    $ mkdir -m 777 storage/app/public/upload/videos
    ```

    ><font color=#d64f44>**NOTE :**</font> Since usually setting permissions to `0777` is insecure, it is advisable to change the group ownership of the directory to the same user as Apache and add group write permissions instead. Please contact your system administrator in case of any doubts.

- Add cookie name

    Find "`app/Http/Middleware/EncryptCookies.php`" file
    ```php

    namespace App\Http\Middleware;

    use Illuminate\Cookie\Middleware\EncryptCookies as Middleware;

    class EncryptCookies extends Middleware
    {
        /**
        * The names of the cookies that should not be encrypted.
        *
        * @var array
        */
        protected $except = [
            'ckCsrfToken', //add
            // ...
        ];
    }
    ```

    Find "`app/Http/Middleware/VerifyCsrfToken.php`" file
    ```php

    namespace App\Http\Middleware;

    use Illuminate\Foundation\Http\Middleware\VerifyCsrfToken as Middleware;

    class VerifyCsrfToken extends Middleware
    {
        /**
        * The URIs that should be excluded from CSRF verification.
        *
        * @var array
        */
        protected $except = [
            'ckfinder/*', //add
            // ...
        ];
    }
    ```

- Configuring authentication
    ```shell
    $ php artisan make:middleware CustomCKFinderAuth
    ```

    Find "`App\Http\Middleware\CustomCKFinderAuth.php`"

    ```php
    namespace App\Http\Middleware;

    use Closure;
    use Auth;

    class CustomCKFinderAuth
    {
        /**
        * Handle an incoming request.
        *
        * @param  \Illuminate\Http\Request  $request
        * @param  \Closure  $next
        * @return mixed
        */
        public function handle($request, Closure $next)
        {
            config(['ckfinder.authentication' => function() {
                
                //return true;
                return Auth::check();

            }]);
            return $next($request);
        }
    }
    ```

- Change ckfinder config
    Find "`config/ckfinder.php`" file
    ```php
    ...
    # set ckfinder url
    $config['loadRoutes'] = false;
    
    ...
    # set ckfinder authentication Middleware
    $config['authentication'] = 'App\Http\Middleware\CustomCKFinderAuth';

    ...
    # set licenseName and licenseKey, please visit https://ckeditor.com/pricing/?
    $config['licenseName'] = '';
    $config['licenseKey']  = '';

    ...
    # set backends file path
    $config['backends']['default'] = array(
    'name'         => 'default',
    'adapter'      => 'local',
    'baseUrl'      => config('app.url').'/storage/upload/',
    'root'         => public_path('/storage/upload/'),
    'chmodFiles'   => 0777,
    'chmodFolders' => 0755,
    'filesystemEncoding' => 'UTF-8'
    );

    ...
    # add resources type
    $config['resourceTypes'][] = array(
    'name'              => 'Images',
    'directory'         => 'images',
    'maxSize'           => 0,
    'allowedExtensions' => 'bmp,gif,jpeg,jpg,png',
    'deniedExtensions'  => '',
    'backend'           => 'default'
    );

    $config['resourceTypes'][] = array(
        'name'              => 'Videos',
        'directory'         => 'videos',
        'maxSize'           => 0,
        'allowedExtensions' => 'mp4,mov,avi',
        'deniedExtensions'  => '',
        'backend'           => 'default'
    );
    ```

- Set Route
    Find "`routes\web.php`" file
    ```php
    # add ckfinder route
    Route::any('/ckfinder/connector', '\CKSource\CKFinderBridge\Controller\CKFinderController@requestAction')
    ->name('ckfinder_connector');

    Route::any('/ckfinder/browser', '\CKSource\CKFinderBridge\Controller\CKFinderController@browserAction')
        ->name('ckfinder_browser');
    ```

- View example
    ```php
    @extends('layouts.app')
    @section('title', 'ckfinder Demo')

    @section('styles')
        <link href="{{ asset('js/ckfinder/samples/css/sample.css') }}" rel="stylesheet">
    @endsection

    @section('content')
        <h1>Widget Mode</h1>

        <div id="ckfinder-widget"></div>

    @stop

    @section('scripts')
        <script src="{{ asset('js/ckfinder/ckfinder.js') }}"></script>

        <script>
            CKFinder.config( { connectorPath: '/ckfinder/connector' } );
            CKFinder.widget( 'ckfinder-widget', {
                language: 'zh-cn',
                width: '100%',
                height: 400
            } );
        </script>


    @endsection
    ```

### **Step 7 - Install CKeditor**
><font color=#dea32c>**Tips :**</font> [CKEditor 4 document](https://ckeditor.com/docs/ckeditor4/latest/guide/index.html)

- Download CKeditor 
    Download CkEditor package from online builder [website](https://ckeditor.com/cke4/builder)

- Import to "`public/js`"

- Set Config
    ```js
    /**
    * @license Copyright (c) 2003-2019, CKSource - Frederico Knabben. All rights reserved.
    * For licensing, see https://ckeditor.com/legal/ckeditor-oss-license
    */

    CKEDITOR.editorConfig = function( config ) {
        // Define changes to default configuration here. For example:
        // config.language = 'fr';
        // config.uiColor = '#AADC6E';
        config.uiColor = '#e3e3e3';
        config.language = 'zh-cn';

        config.height = 400;

        config.embed_provider = '//iframe.ly/api/oembed?url={url}&callback={callback}&api_key=5b1cb2abc71e16e533c085';

        config.mathJaxLib = '//cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.4/MathJax.js?config=TeX-AMS_HTML';

        config.codeSnippet_theme = 'sunburst';

        config.fontawesome = {'path':'~@fortawesome/fontawesome-free/css/all.min.css'};


        config.toolbarGroups = [
            { name: 'clipboard', groups: [ 'undo', 'clipboard' ] },
            { name: 'document', groups: [ 'mode', 'document', 'doctools' ] },
            { name: 'tools', groups: [ 'tools' ] },
            '/',
            { name: 'editing', groups: [ 'find', 'selection', 'spellchecker', 'editing' ] },
            { name: 'emoji', groups: [ 'emoji' ] },
            { name: 'links', groups: [ 'links' ] },
            { name: 'insert', groups: [ 'insert' ] },
            '/',
            { name: 'paragraph', groups: [ 'list', 'indent', 'blocks', 'align', 'bidi', 'paragraph' ] },
            { name: 'forms', groups: [ 'forms' ] },
            '/',
            { name: 'styles', groups: [ 'styles' ] },
            { name: 'basicstyles', groups: [ 'basicstyles', 'cleanup' ] },
            { name: 'colors', groups: [ 'colors' ] },
            { name: 'others', groups: [ 'others' ] },
            { name: 'about', groups: [ 'about' ] }
        ];

        config.removeButtons = 'About,Source,Flash,Smiley';
    };
    ```

- Editor Page Example
    ```php
    @extends('layouts.app')
    @section('title', 'CKEditor Demo')

    @section('styles')

    @endsection

    @section('content')
        <textarea name="editor1" id="editor1" rows="10" cols="80">
            This is my textarea to be replaced with CKEditor.
        </textarea>

    @stop

    @section('scripts')

        <script src="{{asset('js/ckfinder/ckfinder.js')}}"></script>
        <script src="{{asset('js/ckeditor/ckeditor.js')}}"></script>
        <script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.4/MathJax.js?config=TeX-AMS_HTML"></script>


        <script>
            CKFinder.config( { connectorPath: '/ckfinder/connector' } );
            // Replace the <textarea id="editor1"> with a CKEditor
            // instance, using default configuration.
            var editor = CKEDITOR.replace( 'editor1' );
            CKFinder.setupCKEditor( editor );
        </script>

    @endsection
    ```

- Target page
    ```html
    <head>
        ...
    <link href="{{asset('js/ckeditor/plugins/codesnippet/lib/highlight/styles/sunburst.css') }}" rel="stylesheet">
    </head>
    
    <script src="{{asset('js/ckeditor/plugins/codesnippet/lib/highlight/highlight.pack.js')}}"></script>
    <script>hljs.initHighlightingOnLoad();</script>
    ```


### **Step 7 - Install Voyager**
><font color=#dea32c>**Tips :**</font> [Voyager document](https://voyager-docs.devdojo.com/)

- Install
    ```shell
    $ composer require tcg/voyager
    ```

- Set .env
    ```shell
    ...
    APP_URL=http://localhost

    ...
    DB_HOST=localhost
    DB_DATABASE=homestead
    DB_USERNAME=homestead
    DB_PASSWORD=secret
    ```

- Move "`User.php`" 
    Find "`App/User.php`" move to "`App/Models/User.php`"

- Change related information

    Find "`App/Models/User.php`"
    ```php
    # original
    namespace App;

    # change
    namespace App\Models;
    ```

    Use hot key "`Ctrl + Shift + R`" global search
    ```php
    # original
    App\User

    # change
    App\Models\User
    ```

- Change vendor file
    Find "`vendor/tcg/voyager/src/Commands/InstallCommand.php`" file
    ```php
    # original
    $this->info('Attempting to set Voyager User model as parent to App\User');
    if (file_exists(app_path('User.php'))) {
        $str = file_get_contents(app_path('User.php'));

        if ($str !== false) {
            $str = str_replace('extends Authenticatable', "extends \TCG\Voyager\Models\User", $str);

            file_put_contents(app_path('User.php'), $str);
        }

    # change
    $userPath = config('voyager.user.default_path', app_path('User.php'));
    $this->info('Attempting to set Voyager User model as parent to ' . $userPath);        
    if (file_exists($userPath)) {
        $str = file_get_contents($userPath);

        if ($str !== false) {
            $str = str_replace('extends Authenticatable', "extends \TCG\Voyager\Models\User", $str);

            file_put_contents($userPath, $str);
        }

    ```

    Find "`vendor/tcg/voyager/src/VoyagerServiceProvider.php`" file
    ```php
    # original
    private function registerPublishableResources()
    {
        ...

        $publishable = [
            'voyager_avatar' => [
                "{$publishablePath}/dummy_content/users/" => storage_path('app/public/users'),
            ],
            ...
    }

    # change
    private function registerPublishableResources()
    {
        ...

        $publishable = [
            'voyager_avatar' => [
                "{$publishablePath}/dummy_content/users/" => storage_path('app/public/upload/users'),
            ],

            ...

    }
    ```

    Find "`vendor/tcg/voyager/migrations/2016_01_01_000000_add_voyager_user_fields.php`" file
    ```php
    # original
    public function up()
    {
        Schema::table('users', function ($table) {
            if (!Schema::hasColumn('users', 'avatar')) {
                $table->string('avatar')->nullable()->after('email')->default('users/default.png');
            }
            $table->bigInteger('role_id')->nullable()->after('id');
        });
    }

    # change
    public function up()
    {
        Schema::table('users', function ($table) {
            if (!Schema::hasColumn('users', 'avatar')) {
                $table->string('avatar')->nullable()->after('email')->default('upload/users/default.png');
            }
            $table->bigInteger('role_id')->nullable()->after('id');
        });
    }
    ```

- Change Config
    Find "`config/voyager.php`" file
    ```php
    # original
    ...
    'user' => [
        'add_default_role_on_register' => true,
        'default_role'                 => 'user',
        'default_avatar'               => 'users/default.png',
        'redirect'                     => '/admin',
    ],

    ...
    'models' => [
        //'namespace' => 'App\\',
    ],


    # change
    ...
    'user' => [
        'add_default_role_on_register' => true,
        'default_role'                 => 'user',
        'default_avatar'               => 'upload/users/default.png',
        'default_path'                 => app_path('Models/User.php'),
        'namespace'                    => App\Models\User::class,
        'redirect'                     => '/admin',
    ],

    ...
    'models' => [
        'namespace' => 'App\\Models\\',
    ],
    ```

- Publish configuration
    ```shell
    $ composer dump-autoload

    $ php artisan voyager:install
    ```

- Quick create new admin user
    ```shell
    $ php artisan voyager:admin <email> --create

    ## example
    $ php artisan voyager:admin your@email.com --create
    ``` 