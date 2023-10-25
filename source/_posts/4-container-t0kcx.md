<h1>4. 容器</h1>
<h1>array</h1>
<blockquote>
<p>头文件：#include <array></p>
</blockquote>
<p>使用 array 模板类创建：</p>
<pre><code class="language-c">array&lt;数据类型, 长度&gt; 变量名 = {xx, xx, xx};
</code></pre>
<p>array 和数组的对比：</p>
<ul>
<li>array 和数组一样，可以通过下标取值。</li>
<li>array 可以整体赋值（值拷贝）：<code>数组1 = 数组2</code></li>
<li>array 是一个对象，可以调用方法。</li>
</ul>
<p>相关方法：</p>
<pre><code class="language-c">.size()			// 获取长度
.fill(value)	// 使用相同的值填充数组	
</code></pre>
<h1>vector</h1>
<p>vector 是一个动态长度的数组。</p>
<blockquote>
<p>头文件：#include <vector></p>
</blockquote>
<p>定义方式：</p>
<pre><code class="language-c">vector&lt;数据类型&gt; 变量名;		// 创建一个空容器

// 指定元素内容
vector&lt;数据类型&gt; 变量名 =  {1, 2, 3};
vector&lt;数据类型&gt; 变量名 {1, 2, 3};

// 通过构造函数初定义
vector&lt;数据类型&gt; 变量名(length);				// 指定元素个数（默认全为 0）
vector&lt;数据类型&gt; 变量名(length, default)		// 指定元素个数和默认值
vector&lt;数据类型&gt; 变量名(对象);				// 拷贝另一个 vecotr 对象的值
</code></pre>
<p>取值：</p>
<pre><code class="language-c">变量[index]
</code></pre>
<p>相关方法：</p>
<pre><code class="language-c">.size()			// 获取元素个数
.at(index)		// 获取指定位置的元素
    
.push_back()	// 在末尾添加元素
.pop_back()		// 删除末尾元素
.clear()		// 清空容器
.empty()		// 判断是否为空
</code></pre>
<p>vector 对比 list：</p>
<ul>
<li>vector 底层是动态数组，list 底层是双链表。</li>
<li>vector 的访问速度更快。</li>
</ul>
<h1>pair 对组</h1>
<p>创建对组：</p>
<pre><code class="language-cpp">pair&lt;数据类型, 数据类型&gt; 变量名(value1, value2);

pari&lt;数据类型, 数据类型&gt; 变量名 = make_pair(value1, value2);
</code></pre>
<p>相关操作：</p>
<pre><code class="language-cpp">.first			// 获取第一个元素
.second			// 获取第二个元素
</code></pre>
<h1>map</h1>
<blockquote>
<p>头文件：#include <map></p>
</blockquote>
<p>关于 map：</p>
<ul>
<li>map 中的所有元素都是 pair。</li>
<li>map 通过 key 获取 value。</li>
<li>map 中的所有元素按键值自动排序。</li>
<li>底层通过二叉树实现。</li>
</ul>
<p>创建 map：</p>
<pre><code class="language-cpp">map&lt;数据类型, 数据类型&gt; 变量;

map&lt;string, string&gt; myMap = {
	{&quot;name&quot;, &quot;root&quot;},
	{&quot;pwd&quot;, &quot;root&quot;}
}
</code></pre>
<p>插入 key：</p>
<pre><code class="language-cpp">变量[key] = value;
.insert(pair&lt;type, type&gt;(value1, value2))		// 插入一个 pair
.insert(make_pair(key, value))					// 插入一个 pair
</code></pre>
<p>相关方法：</p>
<pre><code class="language-cpp">.insert(value)			// 插入值
[key]					// 通过 key 获取 value
.at(key)				// 通过 key 获取 value
.size()					// 获取大小
.empty()				// 判断是否为空
.clear()				// 清空容器
.erase(key)				// 通过 key 删除元素
.count(key)				// 统计出现次数（判断 key 是否存在）
.find(key)				// 查找元素，返回迭代器，不存在返回.end()
</code></pre>
<p>判断元素是否存在：</p>
<pre><code class="language-cpp">if (myMap.count(&quot;apple&quot;) &gt; 0) {
    // 元素存在
} else {
    // 元素不存在
}

</code></pre>
<p>查找元素：</p>
<pre><code class="language-cpp">auto iter = myMap.find(&quot;banana&quot;);  // 查找指定键的元素
if (iter != myMap.end()) {
    // 找到了元素
    int value = iter-&gt;second;  // 获取值
} else {
    // 未找到元素
}
</code></pre>
<h1>unordered_map</h1>
<p>unordered 对比 map：</p>
<ul>
<li>底层：unordered 底层基于哈希表，map 底层基于红黑树。</li>
<li>排序：map 会对 key 进行排序，unordered_map 是无序的。</li>
<li>查找效率：unordered_map（哈希表）的查找效率为常数级，map（红黑树）的查找效率为对数级。</li>
<li>内存消耗：为了维持红黑树的结构，map 比 unordered_map 占用的内存更多。</li>
<li>稳定性：unordered_map 的迭代器在插入、删除元素后可能会失效，map 则能保持稳定。</li>
</ul>
<p>创建 unordered_map：</p>
<pre><code class="language-cpp">unordered_map&lt;数据类型, 数据类型&gt; 变量;
</code></pre>
<p>插入元素：</p>
<pre><code class="language-cpp">变量[key] = value;
</code></pre>
<h1>迭代器</h1>
<p>创建迭代器类型的变量：</p>
<pre><code class="language-cpp">vector&lt;int&gt;::iterator it;
</code></pre>
<p>获取迭代器的开始位置：</p>
<pre><code class="language-cpp">容器.begin()
</code></pre>
<p>获取迭代器的结束位置：</p>
<pre><code class="language-cpp">容器.end()
</code></pre>
<p>移动迭代器：</p>
<pre><code class="language-cpp">it++;
</code></pre>
<p>获取当前元素：</p>
<pre><code class="language-cpp">*it;
</code></pre>
<p>使用迭代器遍历：</p>
<pre><code class="language-cpp">for (vector&lt;int&gt;::iterator it - vec.begin(); it != vec.end(); i++) {
    cout &lt;&lt; * it;
}
</code></pre>
