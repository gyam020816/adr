## kotlin

- awaiting on multiple deferreds, idiomatic: https://github.com/Kotlin/kotlinx.coroutines/issues/171#issuecomment-379293467

> @... We try to keep kotlinx.coroutines idiomatic with respect to Kotlin stdlib. We don't plan to have any multiple-arity overloads. Idiomatic way to write your code is:

```kotlin
data class Joined<A, B, C>(a: A, b: B, c: C)

val op1: Deferred<A> = async { ... }
val op2: Deferred<B> = async { ... }
val op3: Deferred<C> = async { ... }

val results = Joined(op1.await(), op2.await(), op3.await())
```
