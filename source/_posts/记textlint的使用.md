---
title: 记textlint的使用
date: 2022-06-05 18:02:17
description: The pluggable linting tool for text and markdown. Textlint is similar to ESLint, but it's for use with natural language.
tags: others 
categories: others
cover: https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206211154356.png
password: 
---
{% note info flat %}
文章可能有不完善之处，详见[这里](https://pandalandala.github.io/2022/06/06/TO-DO-LIST/)；如在阅读过程中遇到其他问题或 bug，或对 blog 有更多的意见或建议，欢迎[在这里提issue](https://github.com/pandalandala/pandalandala.github.io/issues)或点击下方链接发送邮件！[![Mail](https://img.shields.io/badge/Email-zxrshawn@icloud.com-blue?style=flat&logo=mail.ru)](mailto:zxrshawn@icloud.com)
{% endnote %}

{% note warning flat %}文章图片设置为 lazyload（延迟加载）；如遇图片加载失败请尝试刷新当前网页或科学上网。
{% endnote %}

[textlint](https://textlint.github.io/)是一款为`.md`和`.txt`格式文本（默认）进行语言分析的工具。接下来就顺着它[github](https://github.com/textlint/textlint)上的 wiki 一点一点往下捋。其实它各种文档写的已经很详细了，只是记录一下自己的探索和使用。

# 1 特性

没有预先内置的检查语法的规则。如果需要另外的规则的话可以在[这里](https://github.com/textlint/textlint/wiki/Collection-of-textlint-rule)查看和安装。

安装插件以支持`HTML`和其他文件格式。

# 2 快速入门

[Getting Started](https://github.com/textlint/textlint/blob/master/docs/getting-started.md) quickly.

你需要：

+ `Node.js` 6.0.0+
+ `npm` 2.0.0+

# 3 使用

简单了解和安装完之后来到了这一步。

说一下我自己的使用初衷。最开始是想给写的`.md`文章里面的某些内容之间加空格（例如中英文之间的空格）。开发者是日本人，所以如果写日语的话也可以用 textlint 很好地应付某些场景。大部分规则支持的是日语和英语，不过部分日语规则在汉语下还是可以正常使用的。（我自己事先都安装好了才想起来搞个文档，但实在是懒得搞图了，~~相信大家自己都能判断什么样的输出没有报错~~，如果输出一大堆日文应该也是正常的）

## 3.1 自动添加空格

自动添加空格的规则是为日语开发的，不过实测中文也能用。先在根目录下运行如下命令：

```
npm install textlint-rule-ja-space-between-half-and-full-width --global
```

这样的话根目录下所有文件都可以被处理了。然后执行：

```
textlint --init
```

会生成一个`.textlintrc`配置文件，长这样：

```yml
{
  "filters": {},
  "rules": {}
}
```

然后添加规则：

```yml
{
    "filters": {},
    "rules": {
        "ja-space-between-half-and-full-width": {
            "space": "always"
        }
    }
}
```

这样的话执行规则时就会保证全角和半角字符之间有一个空格，也就是中文和英文之间、中文和数字之间都会有一个空格。

接下来只要执行 `textlint .` 命令，即可对目录下所有文件实行格式检查了，你可以看到所有格式有异的地方。也可以指定某一个文件来检查： `textlint markdown.md`。这一步只是检查，并不是真正修复。想要修复的话只需要`textlint --fix markdown.md`即可。

## 3.2 便捷使用

对于希望不时检查根目录下某几个文件夹中文档的格式，可以在根目录新建一个`.bat`文件，然后在其中按行写好你要输入的命令，如下图所示，我会切换到希望检查格式的目录下，然后对格式进行修正。每次希望检查的时候直接运行这个`.bat`文件即可。

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206192116059.png" alt="image-20220619211610011" style="zoom:150%;" />

## 3.3 一些其他的有用的规则

+ [检查文档行数](https://github.com/textlint-rule/textlint-rule-max-number-of-lines)
+ [检查长句子中逗号数量](https://github.com/textlint-rule/textlint-rule-max-comma)
+ [检查外链是否有效](https://github.com/textlint-rule/textlint-rule-no-dead-link)