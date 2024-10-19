---
类型: 公众号
公众号内容:
  - zotero教程
rating:
  - ⭐⭐⭐⭐⭐
简记: 确实不错，真的建议看
---

>第70期 插件教程！zotero7强大的重命名，正则表达式自定义实现
>
>zotero7在zotero6的基础上**极大的完善了重命名功能**
>
>包括**自定义规则，正则表达式使用，条件语句**
>
>本期介绍1：如何配置自己喜欢的**重命名规则** 2：提供**常用的重命名模板**可以直接用
>举一反三，可以根据模板让文件有**独属于自己喜好的重命名方式**

## 目录

[TOC]

## 展示效果

![image.png](https://pic-go-42.oss-cn-guangzhou.aliyuncs.com/img/202401150959025.png)

## 官方教程链接

file_renaming(https://www.zotero.org/support/file_renaming)

## 基础重命名

- zotero的命名元素由变量和参数两部分组成
- **变量**即作者；编辑；条目类型**等条目信息**
- **参数**即前缀后缀连接词**等变量修饰元素**
- 每一个**命名元素**为{{变量 参数=参数数值}}
- **以{{ title truncate="100" }}{{ year prefix=" - " }}为例**
- 表示命名**由标题和日期组成**；标题最多100字符，日期的前缀由”-“连接
- 如果是字符串连接，也可以直接写，不需要前缀如{{ title truncate="100" }}{{ year prefix=" - " }}等价于{{title truncate="100" }}-{{ year}}

## 常用变量的选择

![image.png](https://pic-go-42.oss-cn-guangzhou.aliyuncs.com/img/202401151051525.png)

## 常用参数的选择

![image.png](https://pic-go-42.oss-cn-guangzhou.aliyuncs.com/img/202401151055141.png)

## 所有支持字段

![image.png](https://pic-go-42.oss-cn-guangzhou.aliyuncs.com/img/202401151051803.png)

## 支持条件表达式

模板还支持条件，可以使用 `if` 、 `elseif` 、 `else` 的组合来包含或排除模板的某些部分。条件必须以 `endif` 结尾。下面的模板将使用 DOI 表示期刊文章和预印本，使用 ISBN 表示书籍，使用标题表示任何其他项目类型：

**{{ if itemType == "book" }}{{ISBN}}{{ elseif itemType == "preprint" }}{{ DOI }}{{ elseif itemType == "journalArticle" }}{{ DOI }}{{ else }}{{ title }}{{ endif }}**

## 模板提供

### 标题+日期（-连接）

![image.png](https://pic-go-42.oss-cn-guangzhou.aliyuncs.com/img/202401151020223.png)

### 标题＋作者（多于2个作者省略）

![image.png](https://pic-go-42.oss-cn-guangzhou.aliyuncs.com/img/202401151022249.png)

### 标题+作者（作者名多于2个用etal省略）

![image.png](https://pic-go-42.oss-cn-guangzhou.aliyuncs.com/img/202401151025593.png)

### 中英双语样式命名：中文用”和“ ”等“；英文用”&“ ”etal“

**条目语言为en和us生效**

```
{{ title truncate="100" }}{{ if language == "en" }} {{ if firstCreator == creators }}{{ firstCreator }}{{ else }} {{ creators join=" & " max="2" suffix=" et al." }}{{ endif }}{{ elseif language == "zh" }}{{ if firstCreator == creators }}{{ firstCreator prefix=" " }}{{ else }}{{ creators join=" 和 " max="2" suffix=" 等" prefix=" " }}{{ endif }}{{ endif }}
```

![image.png](https://pic-go-42.oss-cn-guangzhou.aliyuncs.com/img/202401151038100.png)

### 不同条目类型使用不同命名方式

```
{{ if itemType == "blogPost" }} {{ websiteType }}-{{ title }}-{{ year }}{{ else }}{{ title }}-{{ year }}{{ endif }}
```

![image.png](https://pic-go-42.oss-cn-guangzhou.aliyuncs.com/img/202401151047274.png)
