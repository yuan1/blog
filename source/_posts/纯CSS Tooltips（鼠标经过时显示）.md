---
title: 纯CSS Tooltips（鼠标经过时显示）
date: 2017-11-24 17:7:57
tags: [Html,CSS,Tooltips]
categories:
  - Html
---
<style type="text/css">  
    /*Tooltips*/  
    .tooltips{  
        position:relative; /*这个是关键*/  
        z-index:2;  
    }  
    .tooltips:hover{  
        z-index:3;  
        background:none; /*没有这个在IE中不可用*/  
    }  
    .tooltips span{  
        display: none;  
    }  
    .tooltips:hover span{ /*span 标签仅在 :hover 状态时显示*/  
        display:block;  
        position:absolute;  
        top:21px;  
        left:9px;  
        width:15em;  
        border:1px solid black;  
        background-color:#ccFFFF;  
        padding: 3px;  
        color:black;  
    }  
</style>
<a class="tooltips" href="#tooltips">这就是Tooltips<span>如你所见，这些附加的说明文字在鼠标经过的时候显示。</span></a>  
HTML:
```html
<a class="tooltips" href="#tooltips">这就是Tooltips<span>如你所见，这些附加的说明文字在鼠标经过的时候显示。</span></a>  
```
CSS:
```css
<style type="text/css">  
    /*Tooltips*/  
    .tooltips{  
        position:relative; /*这个是关键*/  
        z-index:2;  
    }  
    .tooltips:hover{  
        z-index:3;  
        background:none; /*没有这个在IE中不可用*/  
    }  
    .tooltips span{  
        display: none;  
    }  
    .tooltips:hover span{ /*span 标签仅在 :hover 状态时显示*/  
        display:block;  
        position:absolute;  
        top:21px;  
        left:9px;  
        width:15em;  
        border:1px solid black;  
        background-color:#ccFFFF;  
        padding: 3px;  
        color:black;  
    }  
</style>  
```