# الاكود التي استخدمت لتوجية اي زائر للموقع من خلال الاي بي وتحويله للدومين الاساسي الذي يعمل على السيرفر

## الاكود ذكرت في الفيديو في درس: تشغيل الورد برس على السيرفر بشكل اجباري من خلال الدومين وليس الاي بي


اجبار الدخول الى موقع الورد برس من خلال الدومين ومنع الدخول الى الموقع من خلال الاي بي للسيرفر الذي يعمل على
Lightsail
بواسطة
Bitnami

يجب تحرير 4 ملفات وهي
```
/opt/bitnami/apache2/conf/bitnami/bitnami.conf

/opt/bitnami/apache/conf/bitnami/bitnami-ssl.conf

/opt/bitnami/apache2/conf/vhosts/wordpress-vhost.conf

/opt/bitnami/apache2/conf/vhosts/wordpress-https-vhost.conf
```
وتعديل المحتوى 

مع مراعاة استبدال الدومين
www.lightsailcourse.com
بالدومين الخاص بك

نحرر الملف عن طريق الامر
```
sudo nano /opt/bitnami/apache2/conf/bitnami/bitnami.conf
```

```
# BEGIN: IP to Domain
RewriteEngine On
RewriteCond %{HTTP_HOST} !^(localhost|127.0.0.1)
RewriteRule ^(.*)$ https://www.lightsailcourse.com$1 [R=permanent,L]
# END: IP to Domain
```

نحرر الملف عن طريق الامر
sudo nano /opt/bitnami/apache/conf/bitnami/bitnami-ssl.conf

```
# BEGIN: IP to Domain
RewriteEngine On
RewriteCond %{HTTP_HOST} !^www.lightsailcourse.com$
RewriteCond %{HTTP_HOST} !^(localhost|127.0.0.1)
RewriteRule ^(.*)$ https://www.lightsailcourse.com$1 [R=permanent,L]
# END: IP to Domain
```
نحرر الملف عن طريق الامر
sudo nano /opt/bitnami/apache2/conf/vhosts/wordpress-vhost.conf

```
# BEGIN: IP to Domain
RewriteEngine On
RewriteCond %{HTTP_HOST} !^(localhost|127.0.0.1)
RewriteRule ^(.*)$ https://www.lightsailcourse.com$1 [R=permanent,L]
# END: IP to Domain
```

نحرر الملف عن طريق الامر
sudo nano /opt/bitnami/apache2/conf/vhosts/wordpress-https-vhost.conf

```
# BEGIN: IP to Domain
RewriteEngine On
RewriteCond %{HTTP_HOST} !^www.lightsailcourse.com$
RewriteCond %{HTTP_HOST} !^(localhost|127.0.0.1)
RewriteRule ^(.*)$ https://www.lightsailcourse.com$1 [R=permanent,L]
# END: IP to Domain
```


ثم تنفيذ الامر

sudo /opt/bitnami/ctlscript.sh restart apache

من اجل اعادة تشغيل الويب سيرفر
