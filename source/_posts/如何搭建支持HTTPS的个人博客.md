---
title: 如何搭建支持HTTPS的个人博客
date: 2019-04-30 00:00:00
updated: 2019-05-02 23:05:54
categories:
  - Hexo
tags:
  - Hexo
  - Github
  - HTTPS
description: 本文旨在介绍使用 Github Pages 服务，搭建一个基于 Hexo+NexT 的个人博客。
---

> 有利于提高生产力的知识应该被自由且有效地分享

真挚的情感或有用的经验，都值得通过文字和代码的方式传达给有需要的人，以减少信息熵增对我们个体不利的影响。如果你也这么觉得，一起来搭建一个属于自己博客（向网络世界展示自己的一个窗口），向世界分享你的见解吧！ 又或者只是单纯的把这段经历当作学会使用某些工具的试验行为，丰富业余生活。

---

## 概述

### 为什么是Github

Github是全球最大的软件源代码托管（同性交友）网站，同时也面向学生提供非常实用的[Student Developer Pack](https://education.github.com/pack) 。学生用户通过`.edu` 邮箱注册即可。
拥有Student Developer Pack的学生可在Namecheap上免费申请到一个以 `.me` 结尾的个人域名，免费使用一年，但如果想续期则需要付费。

Github还支持 Pages 服务，简单来说就是Github可以把用户托管的软件代码转换成一个链接为`用户名.github.io`的静态网站，并且可以选择强制https，这项服务是免费的。
2018年的国际劳动节，Github宣布在Pages服务中，如果用户使用自定义域名，也能够**直接得到 [Github提供的HTTPS](https://github.blog/2018-05-01-github-pages-custom-domains-https/) 支持**。如此一来，用户无需绕道使用CloudFlare等服务就可获得Github提供免费，实用的HTTPS支持。这种经济实用的解决方案非常适用于个人博客开发者和学生党。

### 使用Github Pages搭建个人网站

这部分主要参考的是 [基于Hexo+Coding+Github搭建个人博客的全过程](https://11.tt/posts/2018/set-up-hexo-with-coding-and-github/) 。具体步骤就不做多赘述。

值得注意的是，Coding.net 的个人开发者服务已经迁移到了腾讯开发者平台，特别是在创建Coding repo 的时候，名称不需要再加上`.coding.net` ，直接输入喜欢的名字即可。

配置好必须的设置文件后在`git bush`中运行以下代码：

```bash
$ hexo clean && hexo g && hexo d
```

且`git bash`界面最后显示为

```bash
INFO Deploy done: git
```

说明代码已被上传到GitHub repo，并且可以尝试通过`userID.github.io`进行访问。

## 自定义域名

如前所述，在校高校生可以使用Student Dev Pack在Namecheap中申请到为期一年的免费域名，并且Namecheap也提供免费的DNS解析服务和WhoisGuard服务。在Namecheap中申请成功后，参照以下操作设置指向Github的DNS。

### 在Dashboard中打开Advanced-DNS设置列表

![](/2019/04/30/如何搭建支持HTTPS的个人博客/dashboard.png)

### 设置DNS

参照[Github Pages帮助文档](https://help.github.com/en/articles/troubleshooting-custom-domains#https-errors)，在`HOST RECORDS`设置中填写三条records。

1. 点击 `ADD NEW RECORD`, `Type`为 `A Record类型`，`Host` 为`@`, `Value`以下四条中的任意一条，点击绿色的✔：
   - 185.199.108.153
   - 185.199.109.153
   - 185.199.110.153
   - 185.199.111.153

2. 重复以上，添加第二条`185.199.1XX.153` 。

3. 第三条record, `Type`为 `CNAME Record`，`Host` 为 `www`, `Value` 为已经建好的Github 博客默认地址 `userID.github.io.`，特别注意的是地址最后需要加一个点，就像这样`.io.`。

![](/2019/04/30/如何搭建支持HTTPS的个人博客/nds.png)

至此，自定义域名的DNS已设置完毕，由于DNS解析需要一定的时间后才会生效，现在只要安静的看个番，恰口茶耐心等就可以了。

回到`git bush`， `cd` 到本地博客的目录`/source` 下创建一个`CNAME` 文件。

```bash
$ touch CNAME
```

在`CNAME`中加入自定义域名地址`domainName.me`，并再次运行以下程序：

```bash
$ hexo clean && hexo g && hexo d
```

上传到Github后，可在博客所在repo中看到一个`CNAME`文件，内容为之前输入的自定义域名地址。

最后在GitHub repo的`Setting`中，找到GitHub Pages并确认`Enforce HTTPS`为开启状态，稍等片刻直到你看下图，说明你已经完成了所有的配置，并且可以正常访问带有绿色小锁（https支持）的个人博客。

![](/2019/04/30/如何搭建支持HTTPS的个人博客/pages.png)

---

## 总结

至此，使用https支持的个人网站就搭建完成了。在建站的过程中[Miaia](https://miaia.tt)，[Alex LEE](https://saili.science/)，[Alex](https://alexyxwang.me/2017/08/24/Hexo-Github-Namecheap-搭建个人博客/) 的帖子对我帮助很多，虽然与他们并不相识，但我很喜欢这个过程，就像我希望这篇帖子或许能够帮到你一样。
