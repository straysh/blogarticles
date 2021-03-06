{
    "id": 62,
    "user_id": 1,
    "category_id": 7,
    "author": "straysh",
    "title": "中文分词",
    "slug": "sphinx_zh_seg_4",
    "hits": 91,
    "published_at": "1447813925",
    "created_at": 1447813925,
    "updated_at": 1504902458,
    "deleted_at": null
}
* [ICTCLAS(中科院)](http://sewm.pku.edu.cn/QA/reference/ICTCLAS/FreeICTCLAS/documents.html)
* [phpscws](https://github.com/hightman/scws)
* [robbe php](http://code.google.com/p/robbe/) [PHP 安装 Robbe 中文分词扩展](http://blog.aboutc.net/php/59/php-installation-robbe-chinese-word-extension)
* [phpcws](http://code.google.com/p/httpcws/)

# php scws 中文分词 (凡有需要指定编码之处均为utf8)
#### github地址[hightman/scws](https://github.com/hightman/scws)

#### 下载源码包(不要直接clone github源代码,下载release分支)
```
wget -q -O - http://www.xunsearch.com/scws/down/scws-1.2.1.tar.bz2 | tar xjf -
```

#### 编译
```
cd path/to/scws-1.2.1
autoconf
./configre --prefix=path/to/php_scws
make
sudo make install
```

#### 编译php扩展
```
cd phpext
phpize
./configure --with-scws=path/to/php_scws
make
make install
```

新增一个php_scws.ini的php模块配置项
```
sudo vim /etc/php5/modules-available/php_scws.ini

[scws]
; 注意请检查 php.ini 中的 extension_dir 的设定值是否正确, 否则请将 extension_dir 设为空，
; 再把 extension = scws.so 或 php_scws.dll 指定绝对路径。
extension = scws.so
scws.default.charset = utf8
scws.default.fpath = path/to/etc
```

重启apache之后,若`phpinfo()`中有scws但`php -m|grep scws`没有,需要在`/etc/php5/cli/`中也增加一个php_scws.ini配置文件

[php接口以及demo](https://github.com/hightman/scws/blob/master/phpext/README.md)

#### 下载词典文件
词典文件下载地址http://www.xunsearch.com/scws/download.php, [简体中文(UTF-8) (3.9MB，28万词，2015/04/02更新)] .

将加压后的`dict.utf8.xdb`文件复制到`/path/to/php_scws/etc/`目录下,并`chmod a+r ./*`

注:压缩包内有两个php文件`dump_xdb_file.php`和`make_xdb_file.php`,已经失效了.我测试的时候将源词典解压再压缩回去,测试样例'陈凯歌'跑失败了.

#### 命令行测试
```
scws -c utf8 -i cityname.txt -d /home/softwares/php_scws/etc/dict.utf8.xdb:/home/softwares/php_scws/etc/food.utf8.xdb 
鱼香肉丝 

陈凯歌 并 不是 《 无极 》 的 唯一 著作权人 ， 一 部 电影 的 整体 版权 归 电影 制片厂 所有 。 

一 部 电影 的 作者 包括 导演 、 摄影 、 编剧 等 创作 人员 ， 这些 创作 人员 对 他们 的 创作 是 有 版权 的 。 不 经过 制片人 授权 ， 其他人 不能 对 电影 做 拷贝 、 发行 、 反映 ， 不能 通过 网络 来 传播 ， 既 不能 把 电影 改编 成 小说 、 连环画 等 其他 艺术 形式 发表 ， 也 不能 把 一 部 几 个 小时 才能 放 完 的 电影 改编 成 半 个 小时 就 能 放 完 的 短片 。 

著作权 和 版权 在 我国 是 同一个 概念 ， 是 法律 赋予 作品 创作者 的 专有 权利 。 所谓 专有 权利 就是 没有 经过 权利人 许可 又 不是 法律 规定 的 例外 ， 要 使用 这个 作品 ， 就 必须 经过 作者 授权 ， 没有 授权 就是 侵权 。
```

#### 自定义词典
自定义词典格式:用\t分隔
```
# WORD  TF  IDF ATTR
鱼香肉丝	14.01	8.10	n
```

生成词典:
```
scws-gen-dict -i out/food.txt -o food.utf8.xdb -c utf8
```

# 附 常用中文分词
* 哈工大：[语言云（语言技术平台云 LTP-Cloud）](http://www.ltp-cloud.com/)
* 东北大学NiuTrans统计机器翻译系统：[东北大学自然语言处理实验室](http://www.nlplab.com/NiuPlan/NiuTrans.ch.html)
* 中科院张华平博士ICTCLAS ：[NLPIR汉语分词系统](http://ictclas.nlpir.org/)
* 波森科技：[首页 - BosonNLP](http://bosonnlp.com/)
* 结巴：[fxsjy/jieba · GitHub](https://github.com/fxsjy/jieba)
* Ansj分词：[中国自然语言开源组织](http://www.nlpcn.org/group)

# 附:汉语文本词性标注标记集(北大版)

北大标注集：
```
   代码    名称        帮助记忆的诠释
    Ag      形语素      形容词性语素。形容词代码为a，语素代码ｇ前面置以A。
    a       形容词      取英语形容词adjective的第1个字母。
    ad      副形词      直接作状语的形容词。形容词代码a和副词代码d并在一起。
    an      名形词      具有名词功能的形容词。形容词代码a和名词代码n并在一起。
    b       区别词      取汉字“别”的声母。
    c       连词        取英语连词conjunction的第1个字母。
    Dg      副语素      副词性语素。副词代码为d，语素代码ｇ前面置以D。
    d       副词        取adverb的第2个字母，因其第1个字母已用于形容词。
    e       叹词        取英语叹词exclamation的第1个字母。
    f       方位词      取汉字“方” 的声母。
    g       语素        绝大多数语素都能作为合成词的“词根”，取汉字“根”的声母。
    h       前接成分    取英语head的第1个字母。
    i       成语        取英语成语idiom的第1个字母。
    j       简称略语    取汉字“简”的声母。
    k       后接成分
    l       习用语      习用语尚未成为成语，有点“临时性”，取“临”的声母。
    m       数词        取英语numeral的第3个字母，n，u已有他用。
    Ng      名语素      名词性语素。名词代码为n，语素代码ｇ前面置以N。
    n       名词        取英语名词noun的第1个字母。
    nr      人名        名词代码n和“人(ren)”的声母并在一起。
    ns      地名        名词代码n和处所词代码s并在一起。
    nt      机构团体    “团”的声母为t，名词代码n和t并在一起。
    nz      其他专名    “专”的声母的第1个字母为z，名词代码n和z并在一起。 
    o       拟声词      取英语拟声词onomatopoeia的第1个字母。
    p       介词        取英语介词prepositional的第1个字母。
    q       量词        取英语quantity的第1个字母。
    r       代词        取英语代词pronoun的第2个字母,因p已用于介词。
    s       处所词      取英语space的第1个字母。
    Tg      时语素      时间词性语素。时间词代码为t,在语素的代码g前面置以T。
    t       时间词      取英语time的第1个字母。
    u       助词        取英语助词auxiliary 的第2个字母,因a已用于形容词。
    Vg      动语素      动词性语素。动词代码为v。在语素的代码g前面置以V。
    v       动词        取英语动词verb的第一个字母。
    vd      副动词      直接作状语的动词。动词和副词的代码并在一起。
    vn      名动词      指具有名词功能的动词。动词和名词的代码并在一起。
    w       标点符号   
    x       非语素字    非语素字只是一个符号，字母x通常用于代表未知数、符号。
    y       语气词      取汉字“语”的声母。
    z       状态词      取汉字“状”的声母的前一个字母。
```

计算所标注集（V5.0）：
0. 说明
计算所汉语词性标记集（共计99个，22个一类，66个二类，11个三类）主要用于中国科学院计算技术研究所研制的汉语词法分析器、句法分析器和汉英机器翻译系统。本标记集主要参考了以下词性标记集：
1. 北大《人民日报》语料库词性标记集；
2. 北大2002新版词性标记集（草稿）；
3. 清华大学汉语树库词性标记集；
4. 教育部语用所词性标记集（国家推荐标准草案2002版）；
5. 美国宾州大学中文树库（ChinesePennTreeBank）词性标记集；
由于计算所的汉语词法分析器主要采用北大《人民日报》语料库进行参数训练，因此本
词性标记集主要以北大《人民日报》语料库的词性标记集为蓝本，并参考了北大《汉语语法信息词典》中给出的汉语词的语法信息。
本标记集在制定过程中主要考虑了以下几方面的因素：
1. 有助于提高汉语词法分析器的切分和标注正确率；
2. 有助于提高汉语句法分析器的正确率；
3. 有助于汉英机器翻译系统进行翻译；
4. 易于从北大《人民日报》语料库词性标记集进行转换；
5. 对于语法功能不同的词，在不造成词法分析和句法分析歧义区分困难的情况下，尽可能细分子类。
基于以上考虑，我们在标注过程中尽量避免那些容易出错的词性标记，而采用那些不容易出错、而对提高汉语词法句法分析正确率有明显作用的标记。例如，在动词的子类中，我们参考了宾州大学中文树库的做法，把汉语动词“是”和“有”分别做成单独的标记，而没有采用“系动词”的标记。因为同样是“是”这个动词，其句法功能很多，作“系动词”只是其中一种功能，而要区分这些功能是非常困难的，会导致词法分析的正确率下降。
在名词子类中，我们区分了“汉语人名”、“日语人名”和“翻译人名”，这不仅仅是因为这三种人名要采用不同的参数进行训练与识别，而且在汉英机器翻译中也要采用不同的分析算法进行翻译。又如，我们把表示时间的“数词＋‘年’”（如“1995年”）合并成一个时间词，而表示年头的“数词＋‘年’”分别标注为“数词”和“量词”，这是因为我们通过实验发现这种区分在词法分析阶段通过统计方法可以达到较高的正确率，而且这种区分对于后续的句法分析和机器翻译有非常重要的作用。
对于某些词类（助词和标点符号），基本上是一个封闭集，而这些词类中各个词的语法功能相差很大，在这种情况下，我们尽可能地细分其子类。
另外，与其他词性标记集类似，在我们的标记体系中，小类只是大类中一些有必要区分的一些特例，但小类的划分不满足完备性。

1. 名词  (1个一类，7个二类，5个三类)
名词分为以下子类：
n 名词
nr 人名
nr1 汉语姓氏
nr2 汉语名字
nrj 日语人名
nrf 音译人名
ns 地名
nsf 音译地名
nt 机构团体名
nz 其它专名
nl 名词性惯用语
ng 名词性语素
2. 时间词(1个一类，1个二类)
t 时间词
tg 时间词性语素
3. 处所词(1个一类)
s 处所词
4. 方位词(1个一类)
f 方位词
5. 动词(1个一类，9个二类)
v 动词
vd 副动词
vn 名动词
vshi 动词“是”
vyou 动词“有”
vf 趋向动词
vx 形式动词
vi 不及物动词（内动词）
vl 动词性惯用语
vg 动词性语素
6. 形容词(1个一类，4个二类)
a 形容词
ad 副形词
an 名形词
ag 形容词性语素
al 形容词性惯用语
7. 区别词(1个一类，2个二类)
b 区别词
 
bl 区别词性惯用语
8. 状态词(1个一类)
z 状态词
9. 代词(1个一类，4个二类，6个三类)
r 代词
rr 人称代词
rz 指示代词
rzt 时间指示代词
rzs 处所指示代词
rzv 谓词性指示代词
ry 疑问代词
ryt 时间疑问代词
rys 处所疑问代词
ryv 谓词性疑问代词
rg 代词性语素
10. 数词(1个一类，1个二类)
m 数词
mq 数量词
11. 量词(1个一类，2个二类)
q 量词
qv 动量词
qt 时量词
12. 副词(1个一类)
d 副词
13. 介词(1个一类，2个二类)
p 介词
pba 介词“把”
pbei 介词“被”
14. 连词(1个一类，1个二类)
c 连词
cc 并列连词
15. 助词(1个一类，15个二类)
u 助词
uzhe 着
ule 了 喽
uguo 过
ude1 的 底
ude2 地
ude3 得
usuo 所
udeng 等 等等 云云
uyy 一样 一般 似的 般
udh 的话
uls 来讲 来说 而言 说来
 
uzhi 之
ulian 连 （“连小学生都会”）
 
16. 叹词(1个一类)
e 叹词
17. 语气词(1个一类)
y 语气词(delete yg)
18. 拟声词(1个一类)
o 拟声词
19. 前缀(1个一类)
h 前缀
20. 后缀(1个一类)
k 后缀
21. 字符串(1个一类，2个二类)
x 字符串
xx 非语素字
xu 网址URL
22. 标点符号(1个一类，16个二类)
w 标点符号
wkz 左括号，全角：（ 〔  ［  ｛  《 【  〖 〈   半角：( [ { <
wky 右括号，全角：） 〕  ］ ｝ 》  】 〗 〉 半角： ) ] { >
wyz 左引号，全角：“ ‘ 『  
wyy 右引号，全角：” ’ 』 
wj 句号，全角：。
ww 问号，全角：？ 半角：?
wt 叹号，全角：！ 半角：!
wd 逗号，全角：， 半角：,
wf 分号，全角：； 半角： ;
wn 顿号，全角：、
wm 冒号，全角：： 半角： :
ws 省略号，全角：……  …
wp 破折号，全角：——   －－   ——－   半角：---  ----
wb 百分号千分号，全角：％ ‰   半角：%
wh 单位符号，全角：￥ ＄ ￡  °  ℃  半角：$

