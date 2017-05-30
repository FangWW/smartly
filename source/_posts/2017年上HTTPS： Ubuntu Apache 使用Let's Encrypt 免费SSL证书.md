title: 2017年上HTTPS： Ubuntu Apache 使用Let's Encrypt 免费SSL证书
date: 2017-01-02 00:26:56


cover: https://raw.githubusercontent.com/FangWW/makedown_demo/master/Lets-Encrypt_00.gif
---


  **在Google和Apple对https支持推进下，2017注定是http更变为https的大年。**

  Google已将现有Chrome特性在非安全站点上禁用，同时新的特性将只支持HTTPS，意在[推进HTTPS的普及](https://www.chromium.org/Home/chromium-security/deprecating-powerful-features-on-insecure-origins)。Chrome浏览器[自50版本以后已禁止通过HTTP做地理定位](https://developers.google.com/web/updates/2016/04/geolocation-on-secure-contexts-only)和使用[getUserMedia](https://www.sitepoint.com/introduction-getusermedia-api/)功能（该功能可访问用户的摄像头或话筒），并即将实施对[加密媒体扩展](https://en.wikipedia.org/wiki/Encrypted_Media_Extensions)、[应用缓存](http://www.w3schools.com/html/html5_app_cache.asp)、设备移动/方向检测等特性的限制。

  在chrome56版本中非https的网址直接会将之前的感叹号变成直接提示出来‘不安全’，如下。

![](https://raw.githubusercontent.com/FangWW/makedown_demo/master/1.png)

  Apple则明确规定：到2017年1月1日 App Store中的所有应用都必须启用 App Transport Security安全功能。App Transport Security（ATS）是苹果在iOS 9中引入的一项隐私保护功能，屏蔽明文HTTP资源加载，连接必须经过更安全的HTTPS。

  [https ssl 解决的问题](http://baike.baidu.com/link?url=aAzpFUCnEHloYDAkMbIsfHhb_AbNulGdztBc1pwp568SEMKrv_E7R4usaecvhrw9Oi9iIz3zJj4PuyksJLUipq#3)

<div class="para" style="padding-left: 30px;">1）认证用户和服务器，确保数据发送到正确的客户机和服务器</div>

<div class="para" style="padding-left: 30px;">2）加密数据以防止数据中途被窃取</div>

<div class="para" style="padding-left: 30px;">3）维护数据的完整性，确保数据在传输过程中不被改变。</div>

  故此，网站开始了https支持之路。

  获取Let's Encrypt免费SSL证书

![](https://raw.githubusercontent.com/FangWW/makedown_demo/master/Lets-Encrypt_00.gif)

**1,Let's Encrypt官网（评价一个字：好）：**

*   1、官方网站：[https://letsencrypt.org/](https://letsencrypt.org/)
*   2、项目主页：[https://github.com/letsencrypt/letsencrypt](https://github.com/letsencrypt/letsencrypt)

**2,获取证书和安装**

*   1、git clone [https://github.com/letsencrypt/letsencrypt](https://github.com/letsencrypt/letsencrypt)
*   2、cd letsencrypt
*   3、./letsencrypt-auto
*   4、一路输入确定安装~
*   5、最终生成的密钥在/etc/letsencrypt/live/安装时输入的域名/中
*   6、cert.pem  chain.pem  fullchain.pem（公钥）  privkey.pem（私钥）

**3,Apache配置SSL**

*   1、注：ubuntu中apache中没有httpd.conf 对应的是apache2.conf  conf-available  conf-enabled  mods-available  mods-enabled sites-available  sites-enabled 进去分别看一看就懂了
*   2、cd /etc/apache2/sites-enabled 
*   3、有两个默认配置000-default.conf  default-ssl.conf 看名称就懂ssl就是我们要配置的https的配置
*   4、vim default-ssl.conf    主要填写上SSLCertificateFile SSLCertificateKeyFile pem证书的路径
*   ```

                    ServerAdmin webmaster@localhost
                    ServerName panzijiang.com:443
                DocumentRoot /var/www/
    		ProxyPass / http://localhost:8080/
    		ProxyPassReverse / http://localhost:8080/
                    ErrorLog ${APACHE_LOG_DIR}/error_adminer.log
                    CustomLog ${APACHE_LOG_DIR}/access_adminer.log combined
                    SSLEngine on
                    SSLCertificateFile /etc/letsencrypt/live/安装时填写的域名/fullchain.pem
                    SSLCertificateKeyFile /etc/letsencrypt/live/安装时填写的域名/privkey.pem
                    <FilesMatch "\.(cgi|shtml|phtml|php)$">
                                    SSLOptions +StdEnvVars

                                    SSLOptions +StdEnvVars

    	    BrowserMatch "MSIE [2-6]" \
                                    nokeepalive ssl-unclean-shutdown \
                                    downgrade-1.0 force-response-1.0
                    # MSIE 7 and newer should be able to use keepalive
                    BrowserMatch "MSIE [17-9]" ssl-unclean-shutdown

    ```

*   5、a2enmod ssl (apache 加载ssl模块)

*   6、 service apache2 restart   就可以看到的浏览器你的域名前就有一个小绿锁了~

**至此HTTPS大功告成**

**![](https://raw.githubusercontent.com/FangWW/makedown_demo/master/QQ%E6%88%AA%E5%9B%BE20170102140202.png)**

**注：**

Let's Encrypt免费SSL证书期限为90天，到期后可先停止apache服务再使用如下命令续期

```
./certbot-auto renew
```