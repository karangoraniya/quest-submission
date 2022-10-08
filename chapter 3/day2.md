# Chapter 3

## Day 2

#### 1. Write your own smart contract that contains two state variables: an array of resources, and a dictionary of resources. Add functions to remove and add to each of them. They must be different from the examples above.

```
pub contract computer {

    pub var computerParts: @{String: Parts}
    pub var computerParts_2: @[Parts_2]

    pub resource Parts {
        pub let message: String
        init() {
            self.message = "Mouse!"
        }
    }

    pub resource Parts_2 {
        pub let message: String
        init() {
            self.message = "Keyboard!"
        }
    }


    pub fun addParts(parts: @Parts) {
        let key = parts.message
        self.computerParts[key] <-! parts
    }

    pub fun removeParts(key: String): @Parts {
    let parts <- self.computerParts.remove(key: key) ?? panic("Lost in space!")
    return <- parts
}
    pub fun addParts_2(parts: @Parts_2) {
        self.computerParts_2.append(<- parts)
    }

    pub fun removeParts_2(index: Int): @Parts_2 {
        return <- self.computerParts_2.remove(at: index)
    }

    init() {
        self.computerParts <- {}
        self.computerParts_2 <- []
    }

}
```
