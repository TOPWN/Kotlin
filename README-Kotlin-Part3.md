# Kotlin Part 3 —— 学会用let


---

> 通过这篇文章来学习**let**的使用。

# let

我目前所知道的let的使用场景是避免一些non-null checks，比如：

```kotlin
    val order: Order? = findOrder()
    if (order != null){
        println(order.customer.name)
    }
```
这种情况可以用**let**写的更加漂亮一点：

```kotlin
   findOrder()?.let { println(it.customer.name) }
```
另外，**let**的这个特性还可以避免一些不好的强制非空（**!!**）的使用，比如下面这种代码示：
```kotlin
   private var mPhotoUrl: String? = null
    fun uploadClicked() {
    if (mPhotoUrl != null) {
        uploadPhoto(mPhotoUrl) //（1）
    }
}
```
标记了（1）的那行代码会提示一个很常见的编译时错误："Smart cast to 'String' is impossible, because 'mPhotoUrl' is a mutable property that could have been changed by this time"，意思是变量mPhotoUrl的值是可变的（因为是var）,在uploadPhoto方法调用的时候mPhotoUrl的值可能已经改变了，有可能变为了null，当然我们可以很快修复这个错误提示，通过这样：
```kotlin
   private var mPhotoUrl: String? = null
    fun uploadClicked() {
    if (mPhotoUrl != null) {
        uploadPhoto(mPhotoUrl!!)
    }
}
```
问题是可以解决，但是使用双感叹号（**!!**）这种方式不太优雅，也不安全，我们可以看看用**let**解决这个问题的话，代码会是什么样子：
```kotlin
    private var mPhotoUrl: String? = null
    fun uploadClicked() {
        mPhotoUrl?.let { uploadPhoto(it) }
    }
}
```

这样既可以让代码更加优雅，也增强了null类型安全。


