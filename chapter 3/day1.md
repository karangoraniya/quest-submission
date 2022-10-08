# Chapter 3

## Day 1

#### 1. In words, list 3 reasons why structs are different from resources.

- Resources cannot be copy easily.
- Resources either move or destroy
- Resources cannot create whenever we want.
- Resources are harder to deal with them.

#### 2. Describe a situation where a resource might be better to use than a struct.

Resources might be better to use with precise things like documents, College Degree, MarkSheet, Identity etc...

#### 3. What is the keyword to make a new resource?

By using `create` keyword you can make a new resource.

#### 4. Can a resource be created in a script or transaction (assuming there isn't a public function to create one)?

No, You can create resource inside contract only.

#### 5. What is the type of the resource below?

```
pub resource Jacob {

}
```

#### Answer

@Jacob Resources

#### 6. Let's play the "I Spy" game from when we were kids. I Spy 4 things wrong with this code. Please fix them.

```
pub contract Test {

    // Hint: There's nothing wrong here ;)
    pub resource Jacob {
        pub let rocks: Bool
        init() {
            self.rocks = true
        }
    }

    pub fun createJacob(): Jacob { // there is 1 here
        let myJacob = Jacob() // there are 2 here
        return myJacob // there is 1 here
    }
}
```

#### Answer:-

```
pub contract Test {

    // Hint: There's nothing wrong here ;)
    pub resource Jacob {
        pub let rocks: Bool
        init() {
            self.rocks = true
        }
    }

    pub fun createJacob(): @Jacob { // @ was missing
        let myJacob <- create Jacob() // `<-` & `create` keyword
        return <- myJacob // `<-` missing
    }
}
```
