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

### Check this for iOS:

[https://stackoverflow.com/questions/54966200/does-swift-have-standard-scope-functions-like-in-kotlin](https://stackoverflow.com/questions/54966200/does-swift-have-standard-scope-functions-like-in-kotlin)

```
extension Optional {
    func `let`(do: (Wrapped)->()) {
        guard let v = self else { return }
        `do`(v)
    }
}

var str: String? = "text"
str.let {
    print( $0 ) // prints `text`
}
str = nil

str.let {
    print( $0 ) // not executed if str == nil
}
```

[kakajika/ScopeFuncs.swift](https://gist.github.com/kakajika/0bb3fd14f4afd5e5c2ec)

[Making Kotlin Scope Functions in Swift](https://elye-project.medium.com/making-kotlin-scope-function-in-swift-ea694dafa059)








