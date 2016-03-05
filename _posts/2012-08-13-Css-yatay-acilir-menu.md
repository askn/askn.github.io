---
layout: post
title: CSS İle Yatay Açılır Menü Yapımı
comments: true
categories: [ yazılım ]
tags: [ web ]
description: "css, yatay açılır menü, horizontal"
keywords: "css, yatay açılır menü, horizontal"
# asides: []
# author:
---

Css ile basit bir menü tasarlayalım.Menü aşağıdaki gibidir.

<!-- more -->

<img src="http://i.imgur.com/Xu6AL.png" alt="menu" />

Html dosyamız:
{% highlight html %}
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <title></title>
    <link href="Style.css" rel="stylesheet" type="text/css" />
    <link href="reset.css" rel="stylesheet" type="text/css" />
</head>
<body>
    <div class="menu">
        <ul>
            <li><a href="">deneme</a>
                <ul>
                    <li><a href="">deneme</a></li>
                    <li><a href="">deneme</a></li>
                    <li><a href="">deneme</a></li>
                    <li><a href="">deneme</a></li>
                </ul>
            </li>
            <li><a href="">deneme</a>
                 <ul>
                    <li><a href="">deneme</a></li>
                    <li><a href="">deneme</a></li>
                    <li><a href="">deneme</a></li>
                    <li><a href="">deneme</a></li>
                </ul>
            </li>
            <li><a href="">deneme</a></li>
            <li><a href="">deneme</a></li>
        </ul>
        <div style="clear: both"></div>
    </div>
</body>
</html>
{% endhighlight %}

Menu classına verdiğimiz stillerin float uyguladığımız taglarıda kapsaması için
{% highlight html %}
<div style="clear: both"></div>
{% endhighlight %}

satırını  yazdık.

Css kodlarımız:
{% highlight css %}
.menu
{
    background: lightgray;
}
.menu ul li
{
    padding: 10px;
    float: left;
}
.menu ul li:hover
{
    position: relative;
}
.menu ul li ul
{
    background: lightgray;
    display: none;
    position: absolute;
    left: 0;
    margin-top: 10px; /* padding-top 10px (menu ul li) */
}
.menu ul li:hover ul
{
    display: block;
    clear: both;
}
{% endhighlight %}
