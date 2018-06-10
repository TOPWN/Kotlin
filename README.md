# Kotlin Part 1 —— 走马观花


---

> 通过这篇文章来对kotlin有个大概的认识。

#Kotlin
先来看一段 **MainActivity.kt**的示例：
``` kotlin
package me.androidapp.kotlin

import android.support.v7.app.AppCompatActivity
import android.os.Bundle

class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
    }
}
```
以 **.kt** 作为扩展名表示这是一个 **Kotlin** 文件.   

**MainActivity : AppCompatActivity()** 的意思是MainActivity继承自AppCompatActivity。

Kotlin中所有的方法都必须带有`fun`关键字。

Kotlin中行尾的分号`;`不是必须要写的。

重写方法要用`override`关键字，而不是再像Java那样把它当做注解。

**savedInstanceState: Bundle?** 又是什么意思？它表示作为参数的savedInstanceState可以是 **Bundle** 类型也可以是一个 **null** ，毕竟 **Kotlin** 是一种 **null safety** 的语言。如果你像这样定义一个变量：
> var a : String

IDE会给你一个编译错误，因为变量 **a** 必须要被初始化，它不能是一个 **null** 值。所以你可以修改成这样：
> var a : String = "Init value"

另外，如果你接下来对变量**a**再次赋予一个**null**值，同样会出现编译错误：
> a = null

在这种场景下，如果你想让变量**a**可以为**null**，那么就必须要这样写：
> var a : String?

为什么说**null safety**是Kotlin的一个非常重要的功能？很明显，因为它能帮我们避免空指针异常，作为一个Android开放者，我已经受够了**NPE**。甚至就连null类型的创造者[Tony Hoare][1]都对创造出**null**表示懊悔。


假设我们有一个可空的变量**nameTextView**，如果它为null，下面的代码会出现NPE：
> nameTextView.setEnabled(true)

但是Kotlin就不会允许我们这样做，它会强制我们使用`?`或者`!!`操作符，如果使用`?`：
> nameTextView?.setEnabled(true)

这段代码就只有在nameTextView不为null的情况下才会真正起作用，如果使用`!!`：
> nameTextView!!.setEnabled(true)

如果nameTextView为null，同样会报空指针异常，所以这个操作符要慎用。

这是一些对Kotlin的简单介绍，之后的文章会对Kotlin的语法细节做详细的介绍。


  [1]: https://en.wikipedia.org/wiki/Tony_Hoare
