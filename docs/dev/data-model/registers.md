# Registers

[ErgoScript](/dev/scs/ergoscript) (as well as [ErgoTree](/dev/scs/ergotree)) is **typed**, so accessing a register is an operation that involves some expected type given in brackets. 

Thus, the `SELF.R4[Int]` expression should evaluate a valid value of the `Option[Int]` type.
    
For example, `val x = SELF.R4[Int]` expects the register - if it is present - to have type `Int`. 

There are three cases:

1. If the register doesn't exist. Then `val x = SELF.R4[Int]` succeeds and returns the None value, which conforms to any value of type `Option[T]` for any T. (In the example above, T is equal to `Int`). Calling `x.get` fails when x is equal to None, but `x.isDefined` succeeds and returns `false`.
2. If the register contains a value `v` of type `Int`. Then `val x = SELF.R4[Int]` succeeds and returns `Some(v)`, which is a valid value of type `Option[Int]`. In this case, calling `x.get` succeeds and returns the value `v` of type `Int`. Calling `x.isDefined` returns `true`.
3. If the register contains a value `v` of type T other than `Int`. Then `val x = SELF.R4[Int]` fails because there is no way to return a valid value of type `Option[Int]`. The register value is present, so returning it as None would break the typed semantics of registers collection.
    
Within some use cases, a register may have values of different types. To access such a register, we can use an additional register as a tag.

```scala
val tagOpt = SELF.R5[Int]
val res = if (tagOpt.isDefined) {
  val tag = tagOpt.get
  if (tag == 1) {
    val x = SELF.R4[Int].get
    // compute res using value x is of type Int
  } else if (tag == 2) {
    val x = SELF.R4[GroupElement].get
    // compute res using value x is of type GroupElement
  } else if (tag == 3) {
    val x = SELF.R4[ Array[Byte] ].get
    // compute res using value x of type Array[Byte]
  } else {
    // compute `res` when `tag` is not 1, 2 or 3
  }
} else {
  // compute value of res when register is not present
}
```