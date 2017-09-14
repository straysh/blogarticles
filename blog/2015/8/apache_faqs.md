{
    "id": 35,
    "user_id": 1,
    "category_id": 16,
    "author": "straysh",
    "title": "FAQ",
    "slug": "apache_faqs",
    "hits": 69,
    "published_at": "1438654607",
    "created_at": 1438654607,
    "updated_at": 1504697543,
    "deleted_at": null
}
* 反向代理
```
<VirtualHost *:80>
    ... ...
    
    #反向代理设置
    ProxyPass /dev http://activity.lifemenu.local:8010
    ProxyPassReverse /dev http://activity.lifemenu.local:8010
</VirtualHost>
<VirtualHost *:8010>
    ServerName activity.lifemenu.local
    DocumentRoot /data0/www/Lifemenu/branches/weixin_20151026/public

    ErrorLog /data3/logs/apache/error.log
    CustomLog /data3/logs/apache/access.log combined
    <Directory /data0/www/Lifemenu/branches/weixin_20151026/public>
        AllowOverride All
        Options -Indexes +FollowSymLinks -MultiViews
        Require all granted
    </Directory>
</VirtualHost>
#针对单独的ip做反向代理
<Location /bar>
    Allow from 1.2.3.4 2.3.4.5 ...
    ProxyPass http://example.com/bar
    ProxyPassReverse http://example.com/bar
</Location>
```
