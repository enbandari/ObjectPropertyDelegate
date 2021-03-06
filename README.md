# ObjectPropertyDelegate
ObjectPropertyDelegate for Kotlin class properties &amp; functions.

# Demo

Suppose you have a class called `Wrapped` which owns some properties and functions.

```kotlin
class Wrapped(var x: Boolean) {
    val z = 10L
    fun setY(y: Int) {

    }

    fun getY() = 12
}
```

Now you want to wrap it into another class called `Wrapper`, and you may need to delegate properties or functions with properties declared in `Wrapper`.

You can use this library to handle that easily.

```kotlin
class Wrapper {
    private val wrapped: Wrapped = Wrapped(false)

    var x by wrapped::x.delegator()
    var y by wrapped::setY.delegator(defaultValue = 0)
    val yGetter by wrapped::getY.delegator()
    val z by wrapped::z.delegator()
}
```

For those who want to delegate lazy initialized properties, such as:

```kotlin
class MainActivity: Activity() {
    // This would lead to null pointer exception.
    val name by delegateOf(TextView::getText, TextView::setText, textView)
    // or
    val name by delegateOf(textView::getText, textView::setText)

}
```

`nameView` may be initialized after the content view setting up, so we need a lazy delegate for that:

 ```kotlin
 class MainActivity: Activity() {
 
     val name by delegateLazyOf(TextView::getText, TextView::setText) { textView }
 
 }
 ```

Only accessing `nameView` when `name` is accessed.

Works like a charm.

# Use in your project

It has been deployed to jCenter.

```
implementation("com.bennyhuo.kotlin:delegates:1.0")
```

# Issue

Please feel free to issue and pull request.

# License

[MIT License](LICENSE)