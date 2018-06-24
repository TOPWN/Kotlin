# Kotlin Part 2 —— 基础


---

> 通过这篇文章来学习kotlin基础认识。

# lateinit vs lazy

lateinit和lazy是非常重要的 **property initialization**功能，我们在对变量进行初始化的时候需要知道应该使用哪一个。

 - lateinit
   > lateinit是late initialization.

   通常情况下，一个non-null类型的property需要在构造时被初始化，但是这样不是很方便，因为有的时候property是通过DI（Dependency Injection）的方式注入的或者是在一个初始化方法（init）中才能被赋值，这种情况下我们就不能在构造时给property赋予一个non-null的值，但是我们在这个类里引用该property的时候又想避免kotlin的空类型检查（null checks），怎么办呢？这个时候就可以使用lateinit标识符：

   ```kotlin
   private lateinit var mAdapter: RecyclerAdapter<Item>

   override fun onCreate(savedInstanceState: Bundle?) {
      super.onCreate(savedInstanceState)
      mAdapter = RecyclerAdapter(R.layout.item_layout)
   }

   fun updateItems() {
      mAdapter.notifyDataSetChanged()
   }
   ```

   lateinit只能用于声明为var的property，并且只有在property没有自定义getter或setter时才可以使用。property的类型必须是non-null的，并且它不能是原始类型（比如Int）。

 - lazy
   > lazy 是 lazy initialization.

   lazy()是一个带有lambda并且可以返回一个lazy对象的函数，首先计算lambda中的值，暂存起来，等真正需要使用到该对象的时候再把之前暂存的值赋予对象。比如：
   
   ```kotlin
   public class Example{
     val name: String by lazy { “This is lazy function” }
   }
   ```
  等调用到name变量的时候**name**才会被赋予 **"This is lazy function"**。

# 如何选择

 - lazy只能用于val的property，而lateinit只能用于var。
 - lateinit var可以在任何地方被初始化，如果你不清楚property会以何种方式被初始化，不妨试试lateinit。
