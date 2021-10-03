# sqlite3

### 表创建后的操作

###### 创建后设置主外键

```python
# 执行原生sql语句
        # 设置主键
conn.execute("alter table tableName add constraint p_key_name primary key (index_code)")

# 从表设置外键
conn.execute(f"alter table tableName add  foreign key (index_code) references tableName(index_code)")
```



### 表的创建时操作

###### 自增主键

```sqlite
CREATE TABLE w_user( 
id integer primary key autoincrement, --自增主键
username varchar(32), 
); 
```



###### 联合主键设置样式

```sqlite
CREATE TABLE tb_test ( 
bh varchar(5), 
id integer, 
ch varchar(20),
--在创建联合主键时，主键创建要放在所有字段最后面，否则也会创建失败
primary key (id,bh)); 
```

###### 外键设置

约束外键的时候 如果主表中的 键不是主键 需要在后面添加描述UNIQUE 不然会报 foreign key mismatch 的错误

因为sqlite3外键默认是关闭的,所以你要使用就要先打开:

```sqlite
PRAGMA foreign_keys = ON
```



```sqlite
CREATE TABLE IF NOT EXISTS parent (
    id text PRIMARY KEY NOT NULL UNIQUE);--作为外键，要添加unique（如果不是主键）

CREATE TABLE IF NOT EXISTS child (
id text PRIMARY KEY NOT NULL ,
parentID TEXT,
FOREIGN KEY (parentID") REFERENCES parent(id) ON DELETE CASCADE ON UPDATE CASCADE);
```

ON DELETE 和 ON UPDATE,表示当发生delete和update时,会发生什么行为

- NO ACTION:默认的,表示没有什么行为.
- RESTRICT:当有一个child关联到parent时,禁止delete或update parent
- SET NULL:当parent被delete或update时,child的的关联字段被置为null(如果字段有not null,就出错)
- SET DEFAULT:类似于SET NULL (是不是设置默认值?没有试过)
- CASCADE:将实施在parent上的删除或更新操作,传播给你吧与之关联的child上.
   对于 ON DELETE CASCADE, 同被删除的父表中的行 相关联的子表中的每1行,也会被删除.
   对于ON UPDATE CASCADE,  存储在子表中的每1行,对应的字段的值会被自动修改成同新的父键匹配

### 模糊查询

一般模糊语句如下：

SELECT 字段 FROM 表 WHERE 某字段 Like 条件



其中关于条件，SQL提供了四种匹配模式：

1. ：表示任意0个或多个字符。可匹配任意类型和长度的字符，有些情况下若是中文，请使用两个百分号（%%）表示。

比如 

```sqlite
SELECT * FROM [user] WHERE u_name LIKE '%三%'
```

将会把u_name为“张三”，“张猫三”、“三脚猫”，“唐三藏”等等有“三”的记录全找出来。

另外，如果需要找出u_name中既有“三”又有“猫”的记录，请使用and条件

```sqlite
SELECT * FROM [user] WHERE u_name LIKE '%三%' AND u_name LIKE '%猫%'
```

若使用

```sqlite
 SELECT * FROM [user] WHERE u_name LIKE '%三%猫%' 
```

虽然能搜索出“三脚猫”，但不能搜索出符合条件的“张猫三”。

2. **_**： 表示任意单个字符。匹配单个任意字符，它常用来限制表达式的字符长度语句：

比如 

```sqlite
SELECT * FROM [user] WHERE u_name LIKE '_三_'
```

只找出“唐三藏”这样u_name为三个字且中间一个字是“三”的；

再比如

```sqlite
 SELECT * FROM [user] WHERE u_name LIKE '三__';
```

只找出“三脚猫”这样name为三个字且第一个字是“三”的；



3. [ ]：表示括号内所列字符中的一个（类似正则表达式）。指定一个字符、字符串或范围，要求所匹配对象为它们中的任一个。

比如

```sqlite
 SELECT * FROM [user] WHERE u_name LIKE '[张李王]三'
```

将找出“张三”、“李三”、“王三”（而不是“张李王三”）；

如 [ ] 内有一系列字符（01234、abcde之类的）则可略写为“0-4”、“a-e”

```sqlite
SELECT * FROM [user] WHERE u_name LIKE '老[1-9]'
```

将找出“老1”、“老2”、……、“老9”；

4. \[^ ]：表示不在括号所列之内的单个字符。其取值和 [] 相同，但它要求所匹配对象为指定字符以外的任一个字符。

比如 

```sqlite
SELECT * FROM [user] WHERE u_name LIKE '[^张李王]三'
```

将找出不姓“张”、“李”、“王”的“赵三”、“孙三”等；

```sqlite
SELECT * FROM [user] WHERE u_name LIKE '老[^1-4]';
```

将排除“老1”到“老4”，寻找“老5”、“老6”、……

5. **查询内容包含通配符时**

由于通配符的缘故，导致我们查询特殊字符“%”、“_”、“[”的语句无法正常实现，而把特殊字符用“[ ]”括起便可正常查询。据此我们写出以下函数：

```sqlite
 function sqlencode(str) 
 str=replace(str,"[","[[]") --此句一定要在最前 
 str=replace(str,"_","[_]") 
 str=replace(str,"%","[%]") 
 sqlencode=str 
 end function 
```

```sqlite
updata
```

