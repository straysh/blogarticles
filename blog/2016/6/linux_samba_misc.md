{
    "id": 64,
    "user_id": 1,
    "category_id": 13,
    "author": "straysh",
    "title": "Samba杂疑",
    "slug": "linux_samba_misc",
    "hits": 90,
    "published_at": "1465807341",
    "created_at": 1465807341,
    "updated_at": 1504491783,
    "deleted_at": null
}
* 现象:Window连接samba服务器正常, 其他linux客户机(centos、Ubuntu、Mac)经常timeout.
解决方法:在samba服务器上,检查`/etc/sysconfig/network`以及`/etc/hosts`两个文件,将主机名-ip映射加入.

例如:
```
root@y125 ~]$cat /etc/hosts
127.0.0.1   y125 localhost
::1         y125 localhost
```