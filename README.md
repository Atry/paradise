# Scalameta Paradise Plugin

[![Join the chat at https://gitter.im/scalameta/scalameta](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/scalameta/scalameta?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

![](https://dl.dropboxusercontent.com/s/zqe336e8hm0595s/Screenshot%202016-05-10%2012.40.48.png?dl=0)

**Update**. Half a day later, the mission has been accomplished. Results can be reproduced with scala.meta 0.20.0 and macro paradise 3.0.0-M1.
```
$ cat Macros.scala
import scala.meta._

object main {
  inline def apply()(defn: Any) = meta {
    val q"..$mods object $name extends { ..$early } with ..$base { $self => ..$stats }" = defn
    val main = q"def main(args: Array[String]): Unit = { ..$stats }"
    q"..$mods object $name extends { ..$early } with ..$base { $self => $main }"
  }
}

$ scalac -cp <scala.meta> -Xplugin:<paradise> Macros.scala

$ cat Test.scala
@main object Test {
  println("hello world")
}

$ scalac -cp . -Xplugin:<paradise> Test.scala && scala Test
hello world
```

Visit Eugene Burmako's ScalaDays NYC talk to learn more: [http://event.scaladays.org/scaladays-nyc-2016#!#schedulePopupExtras-7540](http://event.scaladays.org/scaladays-nyc-2016#!#schedulePopupExtras-7540).
