---
title: Java文档注释用法+JavaDoc的使用详解-CSDN博客
date: '2023-10-24 14:03:02'
updated: '2023-10-24 16:51:39'
permalink: >-
  /post/java-document-comments-javadoc-s-detailed-explanationcsdn-blog-bdrh6.html
comments: true
toc: true
---

# Java文档注释用法+JavaDoc的使用详解-CSDN博客

---

* [https://blog.csdn.net/lsy0903/article/details/89893934](https://blog.csdn.net/lsy0903/article/details/89893934)
* Java文档注释+JavaDoc的使用详解简介文档注释负责描述类、接口、方法、构造器、成员属性。可以被JDK提供的工具 javadoc 所解析，自动生成一套以网页文件形式体现该程序说明文档的注释。注意：文档注释必须写在类、接口、方法、构造器、成员字段前面，写在其他位置无效。JavaDoc 官方说明How to Write Doc Comments for the Javadoc Tool..._javadoc
* 2023-10-24 14:03:02

‍

---

## Java文档注释+JavaDoc的使用详解

### 简介

文档注释负责描述类、接口、方法、构造器、成员属性。可以被JDK提供的工具 javadoc 所解析，自动生成一套以网页文件形式体现该程序说明文档的注释。

注意：文档注释必须写在类、接口、方法、构造器、成员字段前面，写在其他位置无效。

[JavaDoc 官方说明](https://docs.oracle.com/javase/8/docs/technotes/tools/windows/javadoc.html)  
[How to Write Doc Comments for the Javadoc Tool](https://www.oracle.com/technetwork/java/javase/documentation/index-137868.html)

### 写在类上面的JavaDoc

写在类上的文档标注一般分为三段：

* 第一段：概要描述，通常用一句或者一段话简要描述该类的作用，以英文句号作为结束
* 第二段：详细描述，通常用一段或者多段话来详细描述该类的作用，一般每段话都以英文句号作为结束
* 第三段：文档标注，用于标注作者、创建时间、参阅类等信息

#### 第一段：概要描述

单行示例：

```java
package org.springframework.jdbc.core;
/**
 * Simple adapter for {@link PreparedStatementSetter} that applies a given array of arguments.
 *
 */
public class ArgumentPreparedStatementSetter implements PreparedStatementSetter, ParameterDisposer { 
}
```

多行示例：

```java
package java.lang;
/**
 * The {@code Long} class wraps a value of the primitive type {@code
 * long} in an object. An object of type {@code Long} contains a
 * single field whose type is {@code long}.
 *
 * <p> In addition, this class provides several methods for converting
 * a {@code long} to a {@code String} and a {@code String} to a {@code
 * long}, as well as other constants and methods useful when dealing
 * with a {@code long}.
 *
 * <p>Implementation note: The implementations of the "bit twiddling"
 * methods (such as {@link #highestOneBit(long) highestOneBit} and
 * {@link #numberOfTrailingZeros(long) numberOfTrailingZeros}) are
 * based on material from Henry S. Warren, Jr.'s <i>Hacker's
 * Delight</i>, (Addison Wesley, 2002).
 *
 * @author  Lee Boynton
 * @author  Arthur van Hoff
 * @author  Josh Bloch
 * @author  Joseph D. Darcy
 * @since   JDK1.0
 */
public final class Long extends Number implements Comparable<Long> { 
}
```

在注释中出现以@开头的东东被称之为Javadoc文档标记，是JDK定义好的如@author、@version、@since、@see、@link、@code、@param、@return、@exception、@throws等。

##### @link： {@link 包名.类名#方法名(参数类型)} 用于快速链接到相关代码

@link的使用语法`{@link 包名.类名#方法名(参数类型)}`​，其中当包名在当前类中已经导入了包名可以省略，可以只是一个​**类名**​，也可以是仅仅是一个​**方法名**​，也可以是​**类名.方法名**​，使用此文档标记的类或者方法，可用按住**Ctrl键+鼠标单击**快速跳到相应的类或者方法上，解析成html其实就是使用`<code>包名.类名#方法名(参数类型)</code>`​

@link示例

```java
// 完全限定的类名
{ @link java.nio.charset.CharsetEncoder}

// 省略包名
{ @link String} and { @link StringBuilder}

// 省略类名，表示指向当前的某个方法
{ @link #equals(Object)}

// 包名.类名#方法名(参数类型)
{ @link java.lang.Long#toString(long)} 
```

##### @code： {@code text} 将文本标记为code

@code的使用语法`{@code text}`​ 会被解析成`<code>text</code>`​  
将文本标记为代码样式的文本，在code内部可以使用 < 、> 等不会被解释成html标签, code标签有自己的样式

一般在Javadoc中只要涉及到类名或者方法名，都需要使用@code进行标记。

#### 第二段：详细描述

详细描述一般用一段或多段来详细描述类的作用，详细描述中可以使用html标签，如`<p>`​、`<pre>`​、`<a>`​、`<ul>`​、`<i>`​ 等标签， 通常详细描述都以段落p标签开始。  
详细描述和概要描述中间通常有一个空行来分割， 实例如下

```java
package org.springframework.util;
/**
 * Miscellaneous {@link String} utility methods.
 *
 * <p>Mainly for internal use within the framework; consider
 * <a href="http://commons.apache.org/proper/commons-lang/">Apache's Commons Lang</a>
 * for a more comprehensive suite of {@code String} utilities.
 *
 * <p>This class delivers some simple functionality that should really be
 * provided by the core Java {@link String} and {@link StringBuilder}
 * classes. It also provides easy-to-use methods to convert between
 * delimited strings, such as CSV strings, and collections and arrays.
 *
 * @author Rod Johnson
 * @author Juergen Hoeller
 * @author Keith Donald
 * @author Rob Harrop
 * @author Rick Evans
 * @author Arjen Poutsma
 * @author Sam Brannen
 * @author Brian Clozel
 * @since 16 April 2001
 */
public abstract class StringUtils { }
```

一般段落都用p标签来标记，凡涉及到类名和方法名都用`@code`​标记，凡涉及到组织的，一般用a标签提供出来链接地址。

##### @param

一般类中支持泛型时会通过`@param`​来解释泛型的类型

```java
package java.util;
/**
 * @param <E> the type of elements in this list
 *
 */
public interface List<E> extends Collection<E> { }
```

##### @author

详细描述后面一般使用`@author`​来标记作者，如果一个文件有多个作者来维护就标记多个`@author`​，`@author`​后面可以跟作者姓名(也可以附带邮箱地址)、组织名称(也可以附带组织官网地址)

```java
// 纯文本作者
@author Rod Johnson

// 纯文本作者，邮件
@author Igor Hersht, igorh@ca.ibm.com

// 超链接邮件 纯文本作者
@author <a href="mailto:ovidiu@cup.hp.com">Ovidiu Predescu</a>

// 纯文本邮件
@author shane_curcuru@us.ibm.com

// 纯文本 组织
@author Apache Software Foundation

// 超链接组织地址 纯文本组织
@author <a href="https://jakarta.apache.org/turbine"> Apache Jakarta Turbine</a>
```

##### @see 另请参阅

​`@see`​ 一般用于标记该类相关联的类,@see即可以用在类上，也可以用在方法上。

```java
/**
 * @see IntStream
 * @see LongStream
 * @see DoubleStream
 * @see <a href="package-summary.html">java.util.stream</a>
 * /
public interface Stream<T> extends BaseStream<T, Stream<T>> {}
```

##### @since 从以下版本开始

​`@since`​ 一般用于标记文件创建时项目当时对应的版本，一般后面跟版本号，也可以跟是一个时间，表示文件当前创建的时间

```java
package java.util.stream;

/**
* @since 1.8
*/
public interface Stream<T> extends BaseStream<T, Stream<T>> { }
```

```java
package org.springframework.util;

/**
* @since 16 April 2001
*/
public abstract class StringUtils { }
```

##### @version 版本

​`@version`​用于标记当前版本，默认为1.0

```java
 package com.sun.org.apache.xml.internal.resolver;
 /**
 * @version 1.0
 */
public class CatalogManager { }
```

### 写在方法上的JavaDoc

写在方法上的文档标注一般分为三段：

* 第一段：概要描述，通常用一句或者一段话简要描述该方法的作用，以英文句号作为结束
* 第二段：详细描述，通常用一段或者多段话来详细描述该方法的作用，一般每段话都以英文句号作为结束
* 第三段：文档标注，用于标注参数、返回值、异常、参阅等

方法详细描述上经常使用html标签，通常都以p标签开始，而且p标签通常都是单标签，不使用结束标签，其中使用最多的就是p标签和pre标签,ul标签, i标签。

pre标签可定义预格式化的文本。被包围在pre标签中的文本通常会保留空格和换行符。而文本也会呈现为等宽字体，pre标签的一个常见应用就是用来表示计算机的源代码。

一般p经常结合pre使用，或者pre结合@code共同使用(推荐@code方式)  
一般经常使用pre来举例如何使用方法

**注意：pre标签中如果有小于号、大于号、例如泛型 在生产javadoc时会报错**

p结合pre使用

```java
/**
 * Check that the given {@code CharSequence} is neither {@code null} nor
 * of length 0.
 * <p>Note: this method returns {@code true} for a {@code CharSequence}
 * that purely consists of whitespace.
 * <p><pre class="code">
 * StringUtils.hasLength(null) = false
 * StringUtils.hasLength("") = false
 * StringUtils.hasLength(" ") = true
 * StringUtils.hasLength("Hello") = true
 * </pre>
 * @param str the {@code CharSequence} to check (may be {@code null})
 * @return {@code true} if the {@code CharSequence} is not {@code null} and has length
 * @see #hasText(String)
 */
public static boolean hasLength(@Nullable CharSequence str) { 
	return (str != null && str.length() > 0);
}
```

pre结合@code使用

```java
<pre>{ @code
     Person[] men = people.stream()
                        .filter(p -> p.getGender() == MALE)
                        .toArray(Person[]::new);
}</pre>
```

##### @param

​`@param`​ 后面跟参数名，再跟参数描述

```java
/**
 * @param str the {@code CharSequence} to check (may be {@code null})
 */
public static boolean hasText(@Nullable CharSequence str) { 
	return (str != null && str.length() > 0 && containsText(str));
}
```

##### @return

​`@return`​ 跟返回值的描述

```java
/**
 * @return {@code true} if the {@code CharSequence} is not {@code null},
 * its length is greater than 0, and it does not contain whitespace only
 */
public static boolean hasText(@Nullable CharSequence str) { 
	return (str != null && str.length() > 0 && containsText(str));
}
```

##### @[throws](https://so.csdn.net/so/search?q=throws&spm=1001.2101.3001.7020)

​`@throws`​ 跟异常类型 异常描述 , 用于描述方法内部可能抛出的异常

```java
/**
 * @throws IllegalArgumentException when the given source contains invalid encoded sequences
 */
public static String uriDecode(String source, Charset charset) { }
```

##### @exception

​`@exception`​ 用于描述方法签名throws对应的异常

```java
package com.sun.jmx.remote.security;
/**
 * @exception LoginException if the logout fails.
 */
public boolean logout() throws LoginException { }
```

##### @deprecated

​`@deprecated`​ 用于标注一个类或成员已过期,通常配合`{@link}`​使用

```java
/**
* @deprecated as of 5.0.4, in favor of {@link Locale#toLanguageTag()}
*/
@Deprecated
public static String toLanguageTag(Locale locale) { 
return locale.getLanguage() + (hasText(locale.getCountry()) ? "-" + locale.getCountry() : "");
}
```

##### @see

​`@see`​ 既可以用来类上也可以用在方法上，表示可以参考的类或者方法

```java
/**
* @see java.net.URLDecoder#decode(String, String)
*/
public static String uriDecode(String source, Charset charset) { }
```

##### @value

​`{@value}`​ 用于标注在常量上用于表示常量的值

```java
/** 默认数量 {@value} */
private static final Integer QUANTITY = 1;
```

##### @inheritDoc

​`@inheritDoc`​ 用于注解在重写方法或者子类上，用于继承父类中的Javadoc

* 基类的文档注释被继承到了子类
* 子类可以再加入自己的注释（特殊化扩展）
* @return @param @throws 也会被继承

### 示例

spring-core中的StringUtils 示例

```java
package org.springframework.util;
/**
 * Miscellaneous {@link String} utility methods.
 *
 * <p>Mainly for internal use within the framework; consider
 * <a href="http://commons.apache.org/proper/commons-lang/">Apache's Commons Lang</a>
 * for a more comprehensive suite of {@code String} utilities.
 *
 * <p>This class delivers some simple functionality that should really be
 * provided by the core Java {@link String} and {@link StringBuilder}
 * classes. It also provides easy-to-use methods to convert between
 * delimited strings, such as CSV strings, and collections and arrays.
 *
 * @author Rod Johnson
 * @author Juergen Hoeller
 * @author Keith Donald
 * @author Rob Harrop
 * @author Rick Evans
 * @author Arjen Poutsma
 * @author Sam Brannen
 * @author Brian Clozel
 * @since 16 April 2001
 */
public abstract class StringUtils { 
	/**
	 * Check that the given {@code CharSequence} is neither {@code null} nor
	 * of length 0.
	 * <p>Note: this method returns {@code true} for a {@code CharSequence}
	 * that purely consists of whitespace.
	 * <p><pre class="code">
	 * StringUtils.hasLength(null) = false
	 * StringUtils.hasLength("") = false
	 * StringUtils.hasLength(" ") = true
	 * StringUtils.hasLength("Hello") = true
	 * </pre>
	 * @param str the {@code CharSequence} to check (may be {@code null})
	 * @return {@code true} if the {@code CharSequence} is not {@code null} and has length
	 * @see #hasText(String)
	 */
	public static boolean hasLength(@Nullable CharSequence str) { 
		return (str != null && str.length() > 0);
	}
}
```

亲自实践

```java
package com.example.javadocdemo;

import java.math.BigDecimal;
import java.util.Objects;

/**
 * 类 {@code OrderService} 订单服务层.
 *
 * <p> 主要包括 创建订单、取消订单、查询订单等功能更
 *
 * @see Order
 * @author <a href="mailto:lerryli@foxmail.com">Lerry Li</a>
 * @since 2019/05/06
 */
public class OrderService { 

    /** 默认数量 {@value} */
    private static final Integer QUANTITY = 1;

    /**
     * 创建订单.
     *
     * <p> 创建订单需要传用户id和商品列表(商品id和商品数量).
     *
     * <pre>{@code
     *  演示如何使用该方法
     *  List<Goods> items = new ArrayList<>();
     *  Goods goods = new Goods(1L, BigDecimal.ONE);
     *  Goods goods2 = new Goods(2L, BigDecimal.TEN);
     *  items.add(goods);
     *  items.add(goods2);
     *
     *  Order order1 = new Order();
     *  order.setUserId("1");
     *  order.setItems(items);
     *  OrderService#createOrder(order);
     * }
     * </pre>
     *
     * @param order 订单信息
     * @throws NullPointerException 参数信息为空
     * @exception IllegalArgumentException  数量不合法
     * @return 是否创建成功
     * @version 1.0
     * @see Order
     */
    public boolean createOrder(Order order) throws IllegalArgumentException{ 
        Objects.requireNonNull(order);

        List<Goods> items = order.getItems();
        items.forEach(goods -> { 
            BigDecimal quantity = goods.getQuantity();
            if (quantity <span style="font-weight: bold;" class="mark"> null || BigDecimal.ZERO.compareTo(quantity) </span> 0) { 
                throw new IllegalArgumentException();
            }
        });

        System.out.println("create order...");

        return true;
    }
}
```

### 生成JavaDoc

通过IDEA生成Javadoc： Tools –> Generate JavaDoc  
注意要配置编码，如果不配置则生成的JavaDoc会乱码，还需要配置Output directory  
​![Generate JavaDoc](http://127.0.0.1:6806/assets/20190506232720436-20231024140302-7qr2y3q.png)  
​![参数配置](http://127.0.0.1:6806/assets/20190506234058735-20231024140302-29lw0lj.png)  
这里有几点要特别注意一下：

1. IDEA 的 JavaDoc 生成功能在菜单 Tools->Generate JavaDoc 项里面。
2. 点击上述菜单项后，会出现生成 JavaDoc 的对话框，一般的选项都很直观，不必细说。但是要注意生成 JavaDoc 的源代码对象的选择，一般以模块（Module）为主，必要时可以单独选择必要的 Java 源代码文件，不推荐以 Project 为 JavaDoc 生成的源范围。
3. 里面有一个 Locale 可选填项，表示的是需要生成的 JavaDoc 以何种语言版本展示，根据 javadoc.exe 的帮助说明，这其实对应的就是 javadoc.exe 的 -locale 参数，如果不填，默认可能是英文或者是当前操作系统的语言，既然是国人，建议在此填写 zh_CN，这样生成的 JavaDoc 就是中文版本的，当然指的是 JavaDoc 的框架中各种通用的固定显示区域都是中文的。你自己编写的注释转换的内容还是根据你注释的内容来。
4. 还有一个“Other command line arguments:”可选填项，非常重要，是填写直接向 javadoc.exe 传递的参数内容。因为有一些重要的设置，只能通过直接参数形式向 javadoc.exe 传递。这里必须要填写如下参数：

```
-encoding UTF-8 -charset UTF-8 -windowtitle "JavaDoc使用详解" -link https://docs.oracle.com/javase/8/docs/api
```

5. 第一个参数 -encoding UTF-8 表示你的源代码（含有符合 JavaDoc 标准的注释）是基于 UTF-8 编码的，以免处理过程中出现中文等非英语字符乱码；第二个参数 -charset UTF-8 表示在处理并生成 JavaDoc 超文本时使用的字符集也是以 UTF-8 为编码，目前所有浏览器都支持 UTF-8，这样最具有通用性，支持中文非常好；第三个参数 -windowtitle 表示生成的 JavaDoc 超文本在浏览器中打开时，浏览器窗口标题栏显示的文字内容；第四个参数 -link 很重要，它表示你生成的 JavaDoc 中涉及到很多对其他外部 Java 类的引用，是使用全限定名称还是带有超链接的短名称，举个例子，我创建了一个方法 public void func(String arg)，这个方法在生成 JavaDoc 时如果不指定 -link 参数，则 JavaDoc 中对该方法的表述就会自动变为 public void func(java.lang.String arg)，因为 String 这个类对我自己实现的类来讲就是外部引用的类，虽然它是 Java 标准库的类。如果指定了 -link [https://docs.oracle.com/javase/8/docs/api/](https://docs.oracle.com/javase/8/docs/api/) 参数，则 javadoc.exe 在生成 JavaDoc 时，会使用 String 这样的短名称而非全限定名称 java.lang.String，同时自动为 String 短名称生成一个超链接，指向官方 JavaSE 标准文档 [https://docs.oracle.com/javase/8/docs/api/](https://docs.oracle.com/javase/8/docs/api/) 中对 String 类的详细文档地址。-link 实质上是告诉 javadoc.exe 根据提供的外部引用类的 JavaDoc 地址去找一个叫 package-list 的文本文件，在这个文本文件中包含了所有外部引用类的全限定名称，因此生成的新 JavaDoc 不必使用外部引用类的全限定名，只需要使用短名称，同时可以自动创建指向其外部引用 JavaDoc 中的详细文档超链接。每个 JavaDoc 都会在根目录下有一个 package-list 文件，包括我们自己生成的 JavaDoc。

### 查看成果

配置完毕后点击`OK`​按钮,console看到如下日志输出则说明JavaDoc生成成功  
​![生成JavaDoc](http://127.0.0.1:6806/assets/20190506235158770-20231024140302-5ci4h2j.png)  
JavaDoc 生成完毕，即可在其根目录下找到 index.html 文件，打开它就可以看到我们自己的标准 JavaDoc API 文档啦。  
​![生成后的JavaDoc](http://127.0.0.1:6806/assets/201905062353345-20231024140302-m70gtbv.png)  
​![类结构](http://127.0.0.1:6806/assets/20190506235431735-20231024140302-5cmeeml.png)  
​![方法资料](http://127.0.0.1:6806/assets/20190506235511278-20231024140302-29qmwak.png)​

---

​![](http://127.0.0.1:6806/assets/20180623202835803-20231024140302-s4rfuzd.png)​
