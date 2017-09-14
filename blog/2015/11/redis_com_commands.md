{
    "id": 63,
    "user_id": 1,
    "category_id": 8,
    "author": "straysh",
    "title": "常用命令",
    "slug": "redis_com_commands",
    "hits": 68,
    "published_at": "1448344384",
    "created_at": 1448344384,
    "updated_at": 1504436998,
    "deleted_at": null
}
# 查看所有的key
```
straysh ~]$redis-cli keys *life*
1) "lifemenu_dish_rank"
2) "lifemenu_dish"
straysh ~]$redis-cli
127.0.0.1:6379> keys *
1) "lifemenu_dish_rank"
2) "laravel:373a0892f76a2dc50bc0df1677408ce3aabf3be3"
3) "lifemenu_dish"
```

# 压缩日志
```
bgrewriteaof
```