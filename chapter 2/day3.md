# Chapter 2

## Day 1

#### 1. In a script, initialize an array (that has length == 3) of your favourite people, represented as `String`s, and `log` it.

```
    var dost:String = ["Sunny", "Bunny", "Tunny"]
    log(dost)
    log(dost.length) // length of array

```

#### 2. In a script, initialize a dictionary that maps the `String`s Facebook, Instagram, Twitter, YouTube, Reddit, and LinkedIn to a `UInt64` that represents the order in which you use them from most to least. For example, YouTube --> 1, Reddit --> 2, etc. If you've never used one before, map it to 0!

```
var techGiants:{String:Int} = ["Facebook" : 5, "Instagram" : 4, "Twitter" : 0, "Youtube" : 1, "Reddit" : 3, "LinkedIn" : 2]
log(techGiants["Twitter"])

```

#### 3. Explain what the force unwrap operator `!` does, with an example different from the one I showed you (you can just change the type).

The force unwrap operator `!` uses to either condition suppose if there is `nil` value then it will panic, if the value is not nil then it will return the value.

#### 4. Using this picture below, explain...

- What the error message means
  The return type is String but it's returning optional
- Why we're getting this error
  The returning value is not string we have declare the string, it's should return `thing` Array
- How to fix it
  We have to use the force wrap operator `return thing[0x03]!` or add optional where we declare the type `String?`, So it will either return type value or nil.

<img src="../images/1.png" alt="drawing" size="400" />
