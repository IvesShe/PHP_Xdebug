# PHP Xdebug

# 下載

Xdebug 2.6.1

Release date: 2018-08-02

https://xdebug.org/download/historical

![image](./images/20210110142156.png)

# 準備安裝

拷貝到對應的資料夾

![image](./images/20210110142425.png)

解壓

```bash
tar -zxvf xdebug-2.6.1.tgz
```

```bash
cd xdebug-2.6.1
```

查看一下，並沒有configure檔(綠色的)

![image](./images/20210110142631.png)

找到phpize的位置

```bash
find / -name phpize
```

![image](./images/20210110142631.png)

![image](./images/20210110143001.png)



執行phpize

```bash
/usr/local/webserver/php/bin/phpize

或

/usr/bin/phpize

```

產生對應的configure檔案了

![image](./images/20210110143101.png)

# configure

找到php-config的位置

在/usr/local/webserver/php/bin/php-config

```bash
find / -name php-config
```

![image](./images/20210110143403.png)

--with-php-config= 填入對應的目錄

```bash
./configure --enable-xdebug --with-php-config=/usr/local/webserver/php/bin/php-config

或

./configure --enable-xdebug --with-php-config=/usr/bin/php-config

```

![image](./images/20210110144006.png)

![image](./images/20210110143951.png)

# make

```bash
make
```

![image](./images/20210110144053.png)

# make install

```bash
make install
```

![image](./images/20210110144104.png)

### 設定配置檔(作法一)

找尋php.ini檔
```bash
find / -name php.ini
```
拷貝一份並在最下面加上擴展

```bash
zend_extension=xdebug.so

xdebug.remote_autostart=1
xdebug.remote_host=196.168.160.128
xdebug.remote_port=8000
xdebug.remote_enable=on
```

存放到php-fpm的設定檔目錄(依自己安裝的目錄而有異動)

再重啟php-fmp下指令php-m應該就可以看到xdebug了!!

```bash
php -m
```

### 設定配置檔(作法二-VM)
```bash
cd /etc/php.d/
```
在/etc/php.d/隨意拷一個設定檔，改名成swoole.ini，並修改內容增加擴展

```bash
cp 20-mysqlnd.ini xdebug.ini
vi xdebug.ini
```

```bash
zend_extension=xdebug.so

xdebug.remote_autostart=1
xdebug.remote_host=196.168.160.128
xdebug.remote_port=8000
xdebug.remote_enable=on
```

![image](./images/20210110145008.png)

```bash
php -m
```

![image](./images/20210110145220.png)

# xdebug.ini

```ini
zend_extension=xdebug.so

xdebug.remote_autostart=1
xdebug.remote_host=196.168.160.128
xdebug.remote_port=8000
xdebug.remote_enable=on
```