---
layout: default-cn
title: CSS-o-Gram
description: neat, intuitive, fast - like SSG, but peaceful

context: inner-page cssg
---

## 先说最重要的

任何问题 - 都可以通过 [email](mailto:wdybih@gmail.com) 询问项目作者.  
所有内容都可以自由分发.  
复制素材时[链接到源头](https://github.com/XOP/css-o-gram) 是强制的.

**CSSG Generator tool** 正在开发中. 敬请期待!

### 快速导航

* [Overview](#intro)
* [Let's begin](#basics)
* [Let's dig in](#advanced)
* [Syntax reference](#legend)

<a id="intro"></a>
## 概览

CSSG 代表 "CSS 图解", 事实上是一个 CSS 文件中的注释块, 描述了用 CSS 类标识的物质结构.物质可以是元素,块或者项目.

它是你在大型项目中的小伙伴,领导班子建设中的助手,如果你在团队中工作的话. 学习门槛低 - 只有常规语法和一些逻辑规则被使用.  


### 为谁和为了什么

* 更好的代码结构和加入新的代码
* 领导班子和开发者的交流工具, 远离前端
* 检测可能存在的布局"瓶颈"(过多的 DOM 嵌套, 类的数量等等)
* 更容易的排错和重构
* 这是美丽的!

-----
<a id="basics"></a>
## 咱们开始吧
 
CSSG 描述了用相似的层叠 CSS 类标识的物质结构.
类的命名根据你或者你的公司的公认规则.
Classes standing apart of substance classes are added near main class.  
As a rule, auxillary (cosmetic) classes are not added, except for special cases (described in [Advanced section](#advanced)) 

Along this documentation fictional substance "post" is used as an example.  
Let's assume it's the post in blog or any other block that has head, body, footer and secondary elements.

### 你的第一个 CSSG

假设你的 HTML 看上去像这样:

        <div class="post">
            <div class="post_h">
                <div class="post_h_name">Header</div>
            </div>
            <div class="post_b">
                Content
            </div>
            <div class="post_f">
                Additional information
            </div>
        </div>

CSS 是这样的:

    .post {
        font-size: 14px;
    }
    
    .post_h {
        font-weight: bold;
    }
    
    etc.

CSSG 把 HTML 结构用 CSS 的术语表达并且把说明文档放在所有其它规则的 _前面_ :

    /*
        
        post
            post_h
                post_h_name
                post_h_date
        
            post_b
                ...
    
            post_f
        
    */
    
    .post {
        font-size: 14px;
    }
 
如果你用过 HAML 或者认识它的语法, 这个结构对你来说就会很熟悉. 
默认情况下所有的结构元素都没有特定的 DOM 呈现, 所以 _class_ 优先于 _tag_
如果有必要夸大 tag-class 的链接, 可以使用 zen-coding 式的习惯:

    /*
        
        post
            post_h
                post_h_name
                i.post_h_date
        
    */

一些语法笔记:

> descendants illustrated by tab  
> siblings separated by extra line in case of having child elements  
> CSSG structure should fit screen height due to viewing comfort

### 关键内容

关键内容用省略号(...)表示, 其他内容被忽略. 
省略号意味着这里没有嵌套或者没有相关的描述结构
不正确的 CSSG 例子:

    /*
        
        post
            post_h
                post_h_name
                    ...
                post_h_date
                    ...
        
            post_b
                ...
    
            post_f
                ...
        
    */

关键内容可以被放置在其它重要的物质部分旁边:

    /*
        
        post
            post_h
                post_h_name
                post_h_date
        
            post_b
                ...
                post_b_author
    
            post_f
        
    */

Apart substance, but still related to project, is denoted with figure brackets.除了物质,仍然相关于项目,意味着括号内的数字

Key content, complemented with apart substance, is denoted with ellipsis placed nearby.
关键内容, 相隔的物质的补码, 意味着附近的省略号.


    /*
    
        post
            post_h
                {date}
            post_b
                post_cnt
                    {... article}
    
    */

### 链接

如果发生了结构的复杂化, 用链接来混合各个部分在 CSS 文档的头部能更方便的描述结构构架.

    >> CSS start
    
    /*
    
        post
            #header
            #body
            #aux
    
    */
    
    >> CSS continues
    
    /* #header
    
        post_h
            post_h_name
        
    */

> 链接各个部分用符号 - # 来表示

### 修饰器和项目类(混合)

HTML 布局改变了 - 由于上下文或者自身的原因. CSS 修饰器允许改变物质的外观.
修饰器事实上是 CSS 类就像 **.post\_\_new** 或者 **.\_\_compact**, 被放在主类的旁边.
项目类(混合)允许重用物质并且被放在和主类分开的地方, 比如 **.post-featured**.

在 CSSG 所有的可能的求事其都被放在目标类右边(和嵌套层独立对齐).
You choose distance manually, regarding diagram size and reading comfort.  

If project (mix-in) is implied, it is placed _before_ modificators list.


    /*
    
        post                        -project __new __featured
            post_h
            post_b
                post_b              __compact
    
    */

> modificators list in such way points to _availability_ of their simultaneous presence, without extra logic  
> more detailed information about modificators in [Advanced section](#advanced)

### Optional parts

Parts of substance, that may absent (or not compulsory for current substance) are enclosed in square brackets.  
If it's single class, brackets placed on the same line, on the contrary they are placed on separate lines for more convenient reading.

    /*
    
        post
            [post_teaser]
            post_h
            post_b
                [
                post_b_top
                    post_b_top_tx
                ]
    
    */

If optional part is a wrapper, following syntax is used:

    /*
    
        [post_w]
            post
                post_h
                post_b
                    [post_b_cnt]
                        [post_b_tx]
                            ...
                        [/post_b_tx]
                    [/post_b_cnt]
        [/post_w]
    
    */

> hyphens and spaces are not dogmatic in this case. Mind code purity and reading comfort in the first place.  
> furthermore, team might want to choose single syntax, equal for every member.

### Persistent blocks

Practically, large project or framework implies structures, that remain contant in spite of context. 
Examples of such structures - button, form element, social widget etc.

When they can't be ignored or on the contrary - it's _necessary_ to illustrate their presence - following syntax is used:

    /*
    
        post
            post_h
            post_b
            post_f
                post_f_ac
                    <social>
    
    */

> it is important to make up list of persistent, re-usable blocks  
> developers team should obtain single list of blocks

-----
<a id="advanced"></a>
## Let's dig in

### Multiplicity

Multiplicity happens to be typical for some substances, e.g. list elements or some blocks sequence.

In CSSG it will look like this:

    /*
    
        post_cnt
            post_cnt_ul
                post_cnt_li +
    
    */

or like that:

    /*
    
        post_cnt
            post_cnt_i *
    
    */

The main difference between '+' and '\*' is in multiplicity specifics.  
'+' says that element will appear at least 1 time (which is typical for list items - \<li\>)  
'\*' however says that element may appear more than 0 times (any other elements - you name it)

> it's important to feel the distinction between optional elements ([element]) and appearing 0 and more times (element *)  
> insignificant on the first sight, it appears to have contextual meaning

### Modificators - more and meaningful

As it was mentioned in [Basics](#basics), modificators complement substance and theoretically their simultaneous presence is possible.  
Crucial logic described with the help of special syntax.

For example, alternative is illustrated this way:

    /*
        
        post                            ( __current | __regular ) __deleted
    
    */

and even like this:

    /*
    
        post                            ( ( __current | __regular ) | __compact ) __deleted
    
    */

Dot (.) illustrates robust connection between class and another class or modificator

    /*
    
        post                            __compact __featured
            post_h
                post_h_tx . __bold
            post_b
                post_b_cnt
                    ...
    
    */

> alignment on the right for connected class is not necessary

### Inheritance

Substance can be direct descendant of other substance.  
To point this out, define ancestor via "@" symbol.

    /*
    
        post-advanced @ post
            post-advanced_h
            post-advanced_b
    
    */

> it's not necessary to list all modificators, because they inherited by default  
> however, if there is any difference, we must list all possible classes  
> it's accepted that these defined modificators will only be possible

For instance, it is illustrated in the following code, that **post-advanced** will have one possible modificator **__new**, regardless the fact, that **post** has some modificators as well

    /*
    
        post-advanced @ post                __new
            post-advanced_h
            post-advanced_b
    
    */

### Nominal templates

Inheritance is directly connected with nominal templates.  
We simplify illustration of descendant substance and avoid code duplication by setting changeable parts in ancestor substance.  
This is not mandatory, but turns out to be helpful if you have at least two such substances.

As an example, let's say ancestor substance looks like this:

    /*
    
        post
            post_cnt
                % content %
    
    */

or like this, if there is any default content 

    /*
    
        post
            post_cnt
                % content %
                    post_cnt_i
    
    */
 
descendant substance

    /*
    
        post-advanced @ post
    
        % content
            post-advanced_cnt
                post-advanced_cnt_i
    
    */

> when "filling" the template second % symbol is unnecessary

In this case **post-advanced\_cnt** will be inside **post\_cnt** and will override default content from second code piece.  
Without nominal templates, CSSG may look like this:

    /*
    
        post-advanced @ post
    
            post_cnt
                post-advanced_cnt
                    post-advanced_cnt_i
    
    */

There's almost no difference in this case.  
However all notation potential can be seen in context of describing more complex structure

> the **% content %** element has no DOM implementation, it is just a template name

### 动态

By dynamics it's meant that some class or element may appear in layout due to scripts and user activity.

    /*
     
        post                    $__disabled | $__active
            post_h
            post_b
                post_cnt
    
    */  

To define dynamic blocks complemented syntax for optional parts is used:

    /*
     
        post
            $[post_msg]                     
            post_h
            post_b
                post_cnt
                    $[post_cnt_msg]
                        post_cnt_tx
                    $[/post_cnt_msg]
    
    */  

### 这是复杂的

复杂的 CSS 可以被 CSSG 描述.

Alternative (mutual exclusive) blocks example:

    /*
    
        post
            post_b
                
                [1]
                post_cnt
                    post_cnt_lst
                
                [2]
                post_cnt2
                    ...
     
    */

When it's necessary to illustrate some valueable class somewhere high in DOM tree:

    /*
        
        blog . __complex    
        
        ///
        
        post
            post_b
                post_cnt
     
    */

CSSG 是一个自解释的 _规则_, 但是有些情况下需要注释:

    /*
    
        post
            post_h (1)
            post_b
                post_cnt (2)
        _______________________________________________
     
        (1) comment on post_h
        (2) another comment
    
    */


-----
<a id="legend"></a>
## 语法参考

    element                                             element classname
    ...                                                 key content
    #name                                               link to compound section
    span.element                                        tag detalization
    element . __fixed                                   not applicable without this class
    element                 __modificator               modificators list
    element                 ( __yes | __no ) __maybe    modificators logic
    element                 $__dynamic                  dynamic modificator
    [element]                                           optional element
    $[dynamic]                                          dynamically optional element
    list-item +                                         appears at least 1 time
    common-item *                                       appears at least 0 times
    ///                                                 code break
    [1]                                                 variative block marker                          
    descendant @ ancestor                               inheritance
    % template %                                        template
    (1)                                                 comment link
    -------------------                                 comments break line 
    (1) comment on code                                 comment
