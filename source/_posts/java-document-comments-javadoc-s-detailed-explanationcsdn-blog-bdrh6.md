<h1>Java文档注释用法+JavaDoc的使用详解-CSDN博客</h1>
<hr />
<ul>
<li><a href="https://blog.csdn.net/lsy0903/article/details/89893934">https://blog.csdn.net/lsy0903/article/details/89893934</a></li>
<li>Java文档注释+JavaDoc的使用详解简介文档注释负责描述类、接口、方法、构造器、成员属性。可以被JDK提供的工具 javadoc 所解析，自动生成一套以网页文件形式体现该程序说明文档的注释。注意：文档注释必须写在类、接口、方法、构造器、成员字段前面，写在其他位置无效。JavaDoc 官方说明How to Write Doc Comments for the Javadoc Tool..._javadoc</li>
<li>2023-10-24 14:03:02</li>
</ul>
<p>‍</p>
<hr />
<h2>Java文档注释+JavaDoc的使用详解</h2>
<h3>简介</h3>
<p>文档注释负责描述类、接口、方法、构造器、成员属性。可以被JDK提供的工具 javadoc 所解析，自动生成一套以网页文件形式体现该程序说明文档的注释。</p>
<p>注意：文档注释必须写在类、接口、方法、构造器、成员字段前面，写在其他位置无效。</p>
<p><a href="https://docs.oracle.com/javase/8/docs/technotes/tools/windows/javadoc.html">JavaDoc 官方说明</a><br />
<a href="https://www.oracle.com/technetwork/java/javase/documentation/index-137868.html">How to Write Doc Comments for the Javadoc Tool</a></p>
<h3>写在类上面的JavaDoc</h3>
<p>写在类上的文档标注一般分为三段：</p>
<ul>
<li>第一段：概要描述，通常用一句或者一段话简要描述该类的作用，以英文句号作为结束</li>
<li>第二段：详细描述，通常用一段或者多段话来详细描述该类的作用，一般每段话都以英文句号作为结束</li>
<li>第三段：文档标注，用于标注作者、创建时间、参阅类等信息</li>
</ul>
<h4>第一段：概要描述</h4>
<p>单行示例：</p>
<pre><code class="language-java">package org.springframework.jdbc.core;
/**
 * Simple adapter for {@link PreparedStatementSetter} that applies a given array of arguments.
 *
 */
public class ArgumentPreparedStatementSetter implements PreparedStatementSetter, ParameterDisposer { 
}
</code></pre>
<p>多行示例：</p>
<pre><code class="language-java">package java.lang;
/**
 * The {@code Long} class wraps a value of the primitive type {@code
 * long} in an object. An object of type {@code Long} contains a
 * single field whose type is {@code long}.
 *
 * &lt;p&gt; In addition, this class provides several methods for converting
 * a {@code long} to a {@code String} and a {@code String} to a {@code
 * long}, as well as other constants and methods useful when dealing
 * with a {@code long}.
 *
 * &lt;p&gt;Implementation note: The implementations of the &quot;bit twiddling&quot;
 * methods (such as {@link #highestOneBit(long) highestOneBit} and
 * {@link #numberOfTrailingZeros(long) numberOfTrailingZeros}) are
 * based on material from Henry S. Warren, Jr.'s &lt;i&gt;Hacker's
 * Delight&lt;/i&gt;, (Addison Wesley, 2002).
 *
 * @author  Lee Boynton
 * @author  Arthur van Hoff
 * @author  Josh Bloch
 * @author  Joseph D. Darcy
 * @since   JDK1.0
 */
public final class Long extends Number implements Comparable&lt;Long&gt; { 
}
</code></pre>
<p>在注释中出现以@开头的东东被称之为Javadoc文档标记，是JDK定义好的如@author、@version、@since、@see、@link、@code、@param、@return、@exception、@throws等。</p>
<h5>@link： 用于快速链接到相关代码</h5>
<p>@link的使用语法<code>{@link 包名.类名#方法名(参数类型)}</code>​，其中当包名在当前类中已经导入了包名可以省略，可以只是一个​<strong>类名</strong>​，也可以是仅仅是一个​<strong>方法名</strong>​，也可以是​<strong>类名.方法名</strong>​，使用此文档标记的类或者方法，可用按住<strong>Ctrl键+鼠标单击</strong>快速跳到相应的类或者方法上，解析成html其实就是使用<code>&lt;code&gt;包名.类名#方法名(参数类型)&lt;/code&gt;</code>​</p>
<p>@link示例</p>
<pre><code class="language-java">// 完全限定的类名
{ @link java.nio.charset.CharsetEncoder}

// 省略包名
{ @link String} and { @link StringBuilder}

// 省略类名，表示指向当前的某个方法
{ @link #equals(Object)}

// 包名.类名#方法名(参数类型)
{ @link java.lang.Long#toString(long)} 
</code></pre>
<h5>@code： 将文本标记为code</h5>
<p>@code的使用语法<code>{@code text}</code>​ 会被解析成<code>&lt;code&gt;text&lt;/code&gt;</code>​<br />
将文本标记为代码样式的文本，在code内部可以使用 &lt; 、&gt; 等不会被解释成html标签, code标签有自己的样式</p>
<p>一般在Javadoc中只要涉及到类名或者方法名，都需要使用@code进行标记。</p>
<h4>第二段：详细描述</h4>
<p>详细描述一般用一段或多段来详细描述类的作用，详细描述中可以使用html标签，如<code>&lt;p&gt;</code>​、<code>&lt;pre&gt;</code>​、<code>&lt;a&gt;</code>​、<code>&lt;ul&gt;</code>​、<code>&lt;i&gt;</code>​ 等标签， 通常详细描述都以段落p标签开始。<br />
详细描述和概要描述中间通常有一个空行来分割， 实例如下</p>
<pre><code class="language-java">package org.springframework.util;
/**
 * Miscellaneous {@link String} utility methods.
 *
 * &lt;p&gt;Mainly for internal use within the framework; consider
 * &lt;a href=&quot;http://commons.apache.org/proper/commons-lang/&quot;&gt;Apache's Commons Lang&lt;/a&gt;
 * for a more comprehensive suite of {@code String} utilities.
 *
 * &lt;p&gt;This class delivers some simple functionality that should really be
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
</code></pre>
<p>一般段落都用p标签来标记，凡涉及到类名和方法名都用<code>@code</code>​标记，凡涉及到组织的，一般用a标签提供出来链接地址。</p>
<h5>@param</h5>
<p>一般类中支持泛型时会通过<code>@param</code>​来解释泛型的类型</p>
<pre><code class="language-java">package java.util;
/**
 * @param &lt;E&gt; the type of elements in this list
 *
 */
public interface List&lt;E&gt; extends Collection&lt;E&gt; { }
</code></pre>
<h5>@author</h5>
<p>详细描述后面一般使用<code>@author</code>​来标记作者，如果一个文件有多个作者来维护就标记多个<code>@author</code>​，<code>@author</code>​后面可以跟作者姓名(也可以附带邮箱地址)、组织名称(也可以附带组织官网地址)</p>
<pre><code class="language-java">// 纯文本作者
@author Rod Johnson

// 纯文本作者，邮件
@author Igor Hersht, igorh@ca.ibm.com

// 超链接邮件 纯文本作者
@author &lt;a href=&quot;mailto:ovidiu@cup.hp.com&quot;&gt;Ovidiu Predescu&lt;/a&gt;

// 纯文本邮件
@author shane_curcuru@us.ibm.com

// 纯文本 组织
@author Apache Software Foundation

// 超链接组织地址 纯文本组织
@author &lt;a href=&quot;https://jakarta.apache.org/turbine&quot;&gt; Apache Jakarta Turbine&lt;/a&gt;
</code></pre>
<h5>@see 另请参阅</h5>
<p>​<code>@see</code>​ 一般用于标记该类相关联的类,@see即可以用在类上，也可以用在方法上。</p>
<pre><code class="language-java">/**
 * @see IntStream
 * @see LongStream
 * @see DoubleStream
 * @see &lt;a href=&quot;package-summary.html&quot;&gt;java.util.stream&lt;/a&gt;
 * /
public interface Stream&lt;T&gt; extends BaseStream&lt;T, Stream&lt;T&gt;&gt; {}
</code></pre>
<h5>@since 从以下版本开始</h5>
<p>​<code>@since</code>​ 一般用于标记文件创建时项目当时对应的版本，一般后面跟版本号，也可以跟是一个时间，表示文件当前创建的时间</p>
<pre><code class="language-java">package java.util.stream;

/**
* @since 1.8
*/
public interface Stream&lt;T&gt; extends BaseStream&lt;T, Stream&lt;T&gt;&gt; { }
</code></pre>
<pre><code class="language-java">package org.springframework.util;

/**
* @since 16 April 2001
*/
public abstract class StringUtils { }
</code></pre>
<h5>@version 版本</h5>
<p>​<code>@version</code>​用于标记当前版本，默认为1.0</p>
<pre><code class="language-java"> package com.sun.org.apache.xml.internal.resolver;
 /**
 * @version 1.0
 */
public class CatalogManager { }
</code></pre>
<h3>写在方法上的JavaDoc</h3>
<p>写在方法上的文档标注一般分为三段：</p>
<ul>
<li>第一段：概要描述，通常用一句或者一段话简要描述该方法的作用，以英文句号作为结束</li>
<li>第二段：详细描述，通常用一段或者多段话来详细描述该方法的作用，一般每段话都以英文句号作为结束</li>
<li>第三段：文档标注，用于标注参数、返回值、异常、参阅等</li>
</ul>
<p>方法详细描述上经常使用html标签，通常都以p标签开始，而且p标签通常都是单标签，不使用结束标签，其中使用最多的就是p标签和pre标签,ul标签, i标签。</p>
<p>pre标签可定义预格式化的文本。被包围在pre标签中的文本通常会保留空格和换行符。而文本也会呈现为等宽字体，pre标签的一个常见应用就是用来表示计算机的源代码。</p>
<p>一般p经常结合pre使用，或者pre结合@code共同使用(推荐@code方式)<br />
一般经常使用pre来举例如何使用方法</p>
<p><strong>注意：pre标签中如果有小于号、大于号、例如泛型 在生产javadoc时会报错</strong></p>
<p>p结合pre使用</p>
<pre><code class="language-java">/**
 * Check that the given {@code CharSequence} is neither {@code null} nor
 * of length 0.
 * &lt;p&gt;Note: this method returns {@code true} for a {@code CharSequence}
 * that purely consists of whitespace.
 * &lt;p&gt;&lt;pre class=&quot;code&quot;&gt;
 * StringUtils.hasLength(null) = false
 * StringUtils.hasLength(&quot;&quot;) = false
 * StringUtils.hasLength(&quot; &quot;) = true
 * StringUtils.hasLength(&quot;Hello&quot;) = true
 * &lt;/pre&gt;
 * @param str the {@code CharSequence} to check (may be {@code null})
 * @return {@code true} if the {@code CharSequence} is not {@code null} and has length
 * @see #hasText(String)
 */
public static boolean hasLength(@Nullable CharSequence str) { 
	return (str != null &amp;&amp; str.length() &gt; 0);
}
</code></pre>
<p>pre结合@code使用</p>
<pre><code class="language-java">&lt;pre&gt;{ @code
     Person[] men = people.stream()
                        .filter(p -&gt; p.getGender() == MALE)
                        .toArray(Person[]::new);
}&lt;/pre&gt;
</code></pre>
<h5>@param</h5>
<p>​<code>@param</code>​ 后面跟参数名，再跟参数描述</p>
<pre><code class="language-java">/**
 * @param str the {@code CharSequence} to check (may be {@code null})
 */
public static boolean hasText(@Nullable CharSequence str) { 
	return (str != null &amp;&amp; str.length() &gt; 0 &amp;&amp; containsText(str));
}
</code></pre>
<h5>@return</h5>
<p>​<code>@return</code>​ 跟返回值的描述</p>
<pre><code class="language-java">/**
 * @return {@code true} if the {@code CharSequence} is not {@code null},
 * its length is greater than 0, and it does not contain whitespace only
 */
public static boolean hasText(@Nullable CharSequence str) { 
	return (str != null &amp;&amp; str.length() &gt; 0 &amp;&amp; containsText(str));
}
</code></pre>
<h5>@<a href="https://so.csdn.net/so/search?q=throws&amp;spm=1001.2101.3001.7020">throws</a></h5>
<p>​<code>@throws</code>​ 跟异常类型 异常描述 , 用于描述方法内部可能抛出的异常</p>
<pre><code class="language-java">/**
 * @throws IllegalArgumentException when the given source contains invalid encoded sequences
 */
public static String uriDecode(String source, Charset charset) { }
</code></pre>
<h5>@exception</h5>
<p>​<code>@exception</code>​ 用于描述方法签名throws对应的异常</p>
<pre><code class="language-java">package com.sun.jmx.remote.security;
/**
 * @exception LoginException if the logout fails.
 */
public boolean logout() throws LoginException { }
</code></pre>
<h5>@deprecated</h5>
<p>​<code>@deprecated</code>​ 用于标注一个类或成员已过期,通常配合<code>{@link}</code>​使用</p>
<pre><code class="language-java">/**
* @deprecated as of 5.0.4, in favor of {@link Locale#toLanguageTag()}
*/
@Deprecated
public static String toLanguageTag(Locale locale) { 
return locale.getLanguage() + (hasText(locale.getCountry()) ? &quot;-&quot; + locale.getCountry() : &quot;&quot;);
}
</code></pre>
<h5>@see</h5>
<p>​<code>@see</code>​ 既可以用来类上也可以用在方法上，表示可以参考的类或者方法</p>
<pre><code class="language-java">/**
* @see java.net.URLDecoder#decode(String, String)
*/
public static String uriDecode(String source, Charset charset) { }
</code></pre>
<h5>@value</h5>
<p>​<code>{@value}</code>​ 用于标注在常量上用于表示常量的值</p>
<pre><code class="language-java">/** 默认数量 {@value} */
private static final Integer QUANTITY = 1;
</code></pre>
<h5>@inheritDoc</h5>
<p>​<code>@inheritDoc</code>​ 用于注解在重写方法或者子类上，用于继承父类中的Javadoc</p>
<ul>
<li>基类的文档注释被继承到了子类</li>
<li>子类可以再加入自己的注释（特殊化扩展）</li>
<li>@return @param @throws 也会被继承</li>
</ul>
<h3>示例</h3>
<p>spring-core中的StringUtils 示例</p>
<pre><code class="language-java">package org.springframework.util;
/**
 * Miscellaneous {@link String} utility methods.
 *
 * &lt;p&gt;Mainly for internal use within the framework; consider
 * &lt;a href=&quot;http://commons.apache.org/proper/commons-lang/&quot;&gt;Apache's Commons Lang&lt;/a&gt;
 * for a more comprehensive suite of {@code String} utilities.
 *
 * &lt;p&gt;This class delivers some simple functionality that should really be
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
	 * &lt;p&gt;Note: this method returns {@code true} for a {@code CharSequence}
	 * that purely consists of whitespace.
	 * &lt;p&gt;&lt;pre class=&quot;code&quot;&gt;
	 * StringUtils.hasLength(null) = false
	 * StringUtils.hasLength(&quot;&quot;) = false
	 * StringUtils.hasLength(&quot; &quot;) = true
	 * StringUtils.hasLength(&quot;Hello&quot;) = true
	 * &lt;/pre&gt;
	 * @param str the {@code CharSequence} to check (may be {@code null})
	 * @return {@code true} if the {@code CharSequence} is not {@code null} and has length
	 * @see #hasText(String)
	 */
	public static boolean hasLength(@Nullable CharSequence str) { 
		return (str != null &amp;&amp; str.length() &gt; 0);
	}
}
</code></pre>
<p>亲自实践</p>
<pre><code class="language-java">package com.example.javadocdemo;

import java.math.BigDecimal;
import java.util.Objects;

/**
 * 类 {@code OrderService} 订单服务层.
 *
 * &lt;p&gt; 主要包括 创建订单、取消订单、查询订单等功能更
 *
 * @see Order
 * @author &lt;a href=&quot;mailto:lerryli@foxmail.com&quot;&gt;Lerry Li&lt;/a&gt;
 * @since 2019/05/06
 */
public class OrderService { 

    /** 默认数量 {@value} */
    private static final Integer QUANTITY = 1;

    /**
     * 创建订单.
     *
     * &lt;p&gt; 创建订单需要传用户id和商品列表(商品id和商品数量).
     *
     * &lt;pre&gt;{@code
     *  演示如何使用该方法
     *  List&lt;Goods&gt; items = new ArrayList&lt;&gt;();
     *  Goods goods = new Goods(1L, BigDecimal.ONE);
     *  Goods goods2 = new Goods(2L, BigDecimal.TEN);
     *  items.add(goods);
     *  items.add(goods2);
     *
     *  Order order1 = new Order();
     *  order.setUserId(&quot;1&quot;);
     *  order.setItems(items);
     *  OrderService#createOrder(order);
     * }
     * &lt;/pre&gt;
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

        List&lt;Goods&gt; items = order.getItems();
        items.forEach(goods -&gt; { 
            BigDecimal quantity = goods.getQuantity();
            if (quantity &lt;span style=&quot;font-weight: bold;&quot; class=&quot;mark&quot;&gt; null || BigDecimal.ZERO.compareTo(quantity) &lt;/span&gt; 0) { 
                throw new IllegalArgumentException();
            }
        });

        System.out.println(&quot;create order...&quot;);

        return true;
    }
}
</code></pre>
<h3>生成JavaDoc</h3>
<p>通过IDEA生成Javadoc： Tools –&gt; Generate JavaDoc<br />
注意要配置编码，如果不配置则生成的JavaDoc会乱码，还需要配置Output directory<br />
​<img src="http://127.0.0.1:6806/assets/20190506232720436-20231024140302-7qr2y3q.png" alt="Generate JavaDoc" /><br />
​<img src="http://127.0.0.1:6806/assets/20190506234058735-20231024140302-29lw0lj.png" alt="参数配置" /><br />
这里有几点要特别注意一下：</p>
<ol>
<li>IDEA 的 JavaDoc 生成功能在菜单 Tools-&gt;Generate JavaDoc 项里面。</li>
<li>点击上述菜单项后，会出现生成 JavaDoc 的对话框，一般的选项都很直观，不必细说。但是要注意生成 JavaDoc 的源代码对象的选择，一般以模块（Module）为主，必要时可以单独选择必要的 Java 源代码文件，不推荐以 Project 为 JavaDoc 生成的源范围。</li>
<li>里面有一个 Locale 可选填项，表示的是需要生成的 JavaDoc 以何种语言版本展示，根据 javadoc.exe 的帮助说明，这其实对应的就是 javadoc.exe 的 -locale 参数，如果不填，默认可能是英文或者是当前操作系统的语言，既然是国人，建议在此填写 zh_CN，这样生成的 JavaDoc 就是中文版本的，当然指的是 JavaDoc 的框架中各种通用的固定显示区域都是中文的。你自己编写的注释转换的内容还是根据你注释的内容来。</li>
<li>还有一个“Other command line arguments:”可选填项，非常重要，是填写直接向 javadoc.exe 传递的参数内容。因为有一些重要的设置，只能通过直接参数形式向 javadoc.exe 传递。这里必须要填写如下参数：</li>
</ol>
<pre><code>-encoding UTF-8 -charset UTF-8 -windowtitle &quot;JavaDoc使用详解&quot; -link https://docs.oracle.com/javase/8/docs/api
</code></pre>
<ol start="5">
<li>第一个参数 -encoding UTF-8 表示你的源代码（含有符合 JavaDoc 标准的注释）是基于 UTF-8 编码的，以免处理过程中出现中文等非英语字符乱码；第二个参数 -charset UTF-8 表示在处理并生成 JavaDoc 超文本时使用的字符集也是以 UTF-8 为编码，目前所有浏览器都支持 UTF-8，这样最具有通用性，支持中文非常好；第三个参数 -windowtitle 表示生成的 JavaDoc 超文本在浏览器中打开时，浏览器窗口标题栏显示的文字内容；第四个参数 -link 很重要，它表示你生成的 JavaDoc 中涉及到很多对其他外部 Java 类的引用，是使用全限定名称还是带有超链接的短名称，举个例子，我创建了一个方法 public void func(String arg)，这个方法在生成 JavaDoc 时如果不指定 -link 参数，则 JavaDoc 中对该方法的表述就会自动变为 public void func(java.lang.String arg)，因为 String 这个类对我自己实现的类来讲就是外部引用的类，虽然它是 Java 标准库的类。如果指定了 -link <a href="https://docs.oracle.com/javase/8/docs/api/">https://docs.oracle.com/javase/8/docs/api/</a> 参数，则 javadoc.exe 在生成 JavaDoc 时，会使用 String 这样的短名称而非全限定名称 java.lang.String，同时自动为 String 短名称生成一个超链接，指向官方 JavaSE 标准文档 <a href="https://docs.oracle.com/javase/8/docs/api/">https://docs.oracle.com/javase/8/docs/api/</a> 中对 String 类的详细文档地址。-link 实质上是告诉 javadoc.exe 根据提供的外部引用类的 JavaDoc 地址去找一个叫 package-list 的文本文件，在这个文本文件中包含了所有外部引用类的全限定名称，因此生成的新 JavaDoc 不必使用外部引用类的全限定名，只需要使用短名称，同时可以自动创建指向其外部引用 JavaDoc 中的详细文档超链接。每个 JavaDoc 都会在根目录下有一个 package-list 文件，包括我们自己生成的 JavaDoc。</li>
</ol>
<h3>查看成果</h3>
<p>配置完毕后点击<code>OK</code>​按钮,console看到如下日志输出则说明JavaDoc生成成功<br />
​<img src="http://127.0.0.1:6806/assets/20190506235158770-20231024140302-5ci4h2j.png" alt="生成JavaDoc" /><br />
JavaDoc 生成完毕，即可在其根目录下找到 index.html 文件，打开它就可以看到我们自己的标准 JavaDoc API 文档啦。<br />
​<img src="http://127.0.0.1:6806/assets/201905062353345-20231024140302-m70gtbv.png" alt="生成后的JavaDoc" /><br />
​<img src="http://127.0.0.1:6806/assets/20190506235431735-20231024140302-5cmeeml.png" alt="类结构" /><br />
​<img src="http://127.0.0.1:6806/assets/20190506235511278-20231024140302-29qmwak.png" alt="方法资料" />​</p>
<hr />
<p>​<img src="http://127.0.0.1:6806/assets/20180623202835803-20231024140302-s4rfuzd.png" alt="" />​</p>
