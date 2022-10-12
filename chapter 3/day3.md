# Chapter 3

## Day 3

#### 1. Define your own contract that stores a dictionary of resources. Add a function to get a reference to one of the resources in the dictionary.

```cadence
pub contract Crypto {

    pub var dictionaryOfCoin: @{String: Coins}

    pub resource Coins {
        pub let token: String
        init(_token: String) {
            self.token = _token
        }
    }

    pub fun getReference(key: String): &Coins? {
        return &self.dictionaryOfCoin[key] as &Coins?
    }

    init() {
        self.dictionaryOfCoin <- {
            "Flow!": <- create Coins(_token: "Coin "),
            "Dogecoin": <- create Coins(_token: "Shit Coin")
        }
    }
}
```

#### 2. Create a script that reads information from that resource using the reference from the function you defined in part 1.

```cadence
import Crypto from 0x01

pub fun main(): String {
  let ref = Crypto.getReference(key: "Flow")
  let ref = Crypto.coinsReference(key: "flow") ?? panic("key not found")
  return ref.token
}
```

#### 3. Explain, in your own words, why references can be useful in Cadence.

- We can use `reference` to get information without moving resource. It can also use with `Struct`.
