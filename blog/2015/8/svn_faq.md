{
    "id": 36,
    "user_id": 1,
    "category_id": 10,
    "author": "straysh",
    "title": "SVN_FAQ",
    "slug": "svn_faq",
    "hits": 66,
    "published_at": "1438654796",
    "created_at": 1438654796,
    "updated_at": 1504606093,
    "deleted_at": null
}
# 从trunk向branch合并
```bash
cd /branch
svn merge ^/trunk
```

# 从branch合并到trunk
```bash
svn merge -rooxx:HEAD ^/branch/abcd ^/trunk
```

# 回滚一个文件到指定版本
```bash
svn revert -r125:123 foo.php
```

# 撤销所有修改
```bash
svn revert -R .
```