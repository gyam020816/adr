## commandline productivity

- [github/hub](https://github.com/github/hub) *to create pull requests from the commandline*
- dotfiles *to manage aliases*
- tig *to browse git log*
- [sdkman](https://sdkman.io/) *to install and manage multiple versions of development kits*

## architectural

- Documenting architecture decisions, or [ADR (architecture decision records)](http://thinkrelevance.com/blog/2011/11/15/documenting-architecture-decisions)

## note taking
- [Boostnote](https://boostnote.io/) *to facilitate note-taking as a developer*

## other

- awaiting on multiple deferreds, idiomatic: https://github.com/Kotlin/kotlinx.coroutines/issues/171#issuecomment-379293467

> @... We try to keep kotlinx.coroutines idiomatic with respect to Kotlin stdlib. We don't plan to have any multiple-arity overloads. Idiomatic way to write your code is:

```kotlin
data class Joined<A, B, C>(a: A, b: B, c: C)

val op1: Deferred<A> = async { ... }
val op2: Deferred<B> = async { ... }
val op3: Deferred<C> = async { ... }

val results = Joined(op1.await(), op2.await(), op3.await())
```
