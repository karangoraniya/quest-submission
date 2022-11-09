# Chapter 5

## Day 2

#### 1. Explain why standards can be beneficial to the Flow ecosystem.

Standard are more useful for easy interaction and easy to use for everyone. It came with audit and security & time saving. Suppose you have to make any Dapp it will easy to use NFT standard.

#### 2. What is YOUR favourite food?

Aura and Rotola

#### 3. Please fix this code (Hint: There are two things wrong):

The Contract Interface:

```cadence
pub contract interface ITest {
  pub var number: Int

  pub fun updateNumber(newNumber: Int) {
    pre {
      newNumber >= 0: "We don't like negative numbers for some reason. We're mean."
    }
    post {
      self.number == newNumber: "Didn't update the number to be the new number."
    }
  }

  pub resource interface IStuff {
    pub var favouriteActivity: String
  }

  pub resource Stuff {
    pub var favouriteActivity: String
  }
}
```

The implementing contract:

```cadence
// import was missing
import ITest from 0x01

//
pub contract Test:ITest {
  pub var number: Int

  pub fun updateNumber(newNumber: Int) {
    self.number = 5
  }

  pub resource interface IStuff {
    pub var favouriteActivity: String
  }

 // ITest was missing here
  pub resource Stuff: ITest.IStuff {
    pub var favouriteActivity: String

    init() {
      self.favouriteActivity = "Playing League of Legends."
    }
  }

  init() {
    self.number = 0
  }
}
```
