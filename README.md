# Scope-Functions

Example how about `apply` and `let`, in both case we have `this` parameters

```
fun test(context: Context) {

    var txtView1 = TextView(context)
    txtView.text = "Original Text"
    txtView.textSize = 15F

    var txtView2 = TextView(context).apply {
        text = "Holi"
        textSize = 20F
    }

    with(txtView1) {
        text = "Modify Text"
        textSize = 25F
    }

}
```

# Become Custon `apply`

## First Example:

```
        val textView: TextView = TextView(activity).apply {
            this.text = "Hello"
            this.hint = "Good Bye"
            this.textSize = 20f
        }
```
Custom `apply`:

```
fun <T> T.apply2(body: T.() -> Unit) : T {
    this.body()
    return this
}
```

Custon `run`

```
fun <T, U> T.run2(body: T.() -> U) : U {
    return this.body()
}
```
-

```
fun <T> T.apply2(body: T.() -> Unit) : T {
    this.body()
    return this
}

fun <T, U> T.run2(body: T.() -> U) : U {
    return this.body()
}

fun <T, U> T.let2(body: (T) -> U) : U {
    return body(this)
}

fun <T, U> with2(receiver: T, body: T.() -> U) : U {
    return receiver.body()
}

fun <T> T.also2(body: (T) -> Unit) : T {
    body(this)
    return this
}
```








