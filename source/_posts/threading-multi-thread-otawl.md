<h1>threading (多线程)</h1>
<h1>创建线程</h1>
<ul>
<li>程序运行时，默认会有一个主线程。</li>
<li>线程之间，没有固定的执行顺序。</li>
</ul>
<p>基本用法：</p>
<pre><code class="language-python">import threading

# 线程需要执行的函数
def fun():
    print(&quot;这是一个单独的线程&quot;)

# 创建一个线程
thread = threading.Thread(target = fun)
# 启动线程
thread.start()
</code></pre>
<h2>Thread 构造函数</h2>
<pre><code class="language-python">thread = threading.Thread(
    target = fun,		# 指定线程需要执行的函数
    args = (&quot;url&quot;, ),	# 传递函数参数（元组，只有一个元素也要加逗号）
	name = &quot;t1&quot;,		# 为线程命名（可选）
    daemon = True		# 守护线程（可选）
)
</code></pre>
<p>获取线程信息：</p>
<pre><code class="language-python">threading.active_count()		# 获取当前线程数
threading.enumerate()			# 获取所有线程
threading.current_thread()		# 获取当前线程

# 对象属性
.name		# 获取线程名
</code></pre>
<h2>守护线程</h2>
<ul>
<li>默认情况：当主线程任务完成后，其他线程继续执行（直到任务完成）。</li>
<li>守护线程：当主线程任务完成后，其他线程立即结束（不管任务是否完成）。</li>
</ul>
<p>开启守护线程：<code>daemon = True</code></p>
<pre><code class="language-python">threading.Thread(target = fun, daemon = True)
</code></pre>
<h1>线程间的等待</h1>
<p>方法：<code>.join()</code><br />
作用：当前线程等待另一个线程执行完成后，再继续执行。<br />
用法：</p>
<pre><code class="language-python">t = threading.Thread(target = fun, name = &quot;t1&quot;)
t.join()		# 主线程等待线程 t1 执行完成后，再继续执行
</code></pre>
<p>示例（等待所有线程执行完毕）：</p>
<pre><code class="language-python">threads = []

# 不能在启动线程时等待，不然会堵塞启动
for _ in range(3):
    t = threading.Thread(target = fun)
    t.start()
    threads.append(t)

# 主线程等待所有线程执行完成
for t in threads:
    t.join()
    
print(&quot;执行完毕&quot;)
</code></pre>
<h1>线程间的资源竞争</h1>
<p>多个线程更新同一个变量，可能会出现问题。<br />
<strong>更新变量的步骤：</strong></p>
<ol>
<li>读取变量</li>
<li>计算变量</li>
<li>写入变量的值</li>
</ol>
<p><strong>可能的原因：</strong></p>
<ol>
<li>多个线程同时读取到变量。</li>
<li>计算后写入相同的值。</li>
<li>计算重复后，实际值小于预期值。</li>
</ol>
<p><strong>解决方法：</strong></p>
<ol>
<li>使用 lock 将变量锁住。</li>
<li>同时只允许一个线程更新变量。</li>
</ol>
<pre><code class="language-css">lock = threading.Lock()		# 创建一个锁

lock.acquire()
count += 1
lock.release()
</code></pre>
