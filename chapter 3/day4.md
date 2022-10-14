# Chapter 3

## Day 4

#### 1. Explain, in your own words, the 2 things resource interfaces can be used for (we went over both in today's content)

- It is useful what information you have to show to the users.
- It is also useful to not expose a function.

#### 2. Define your own contract. Make your own resource interface and a resource that implements the interface. Create 2 functions. In the 1st function, show an example of not restricting the type of the resource and accessing its content. In the 2nd function, show an example of restricting the type of the resource and NOT being able to access its content.

```cadence

pub contract Cricket {

    pub resource interface IPlayers {
      pub let playerName: String
      pub let jerseyNumber: Int
    }

    pub resource Players: IPlayers {
      pub let playerName: String
      pub let strikeRate: Fix64
      pub let jerseyNumber : Int
      init() {
        self.playerName = "Virat Kohli"
        self.strikeRate = 59.60
        self.jerseyNumber = 18
      }
    }

    // it will show only interface has
    pub fun yesInterface(): @Players{IPlayers} {
      let player <- create Players()
      return <- player

    }

    // it will show everything
    pub fun noInterface(): @Players {
      let player <- create Players()
      return <- player

    }
}

```

#### 4. How would we fix this code?

```cadence

pub contract Stuff {

    pub struct interface ITest {
      pub var greeting: String
      pub var favouriteFruit: String
    }

    // ERROR:
    // `structure Stuff.Test does not conform
    // to structure interface Stuff.ITest`
    pub struct Test: ITest {
      pub var greeting: String

      pub fun changeGreeting(newGreeting: String): String {
        self.greeting = newGreeting
        return self.greeting // returns the new greeting
      }

      init() {
        self.greeting = "Hello!"
      }
    }

    pub fun fixThis() {
      let test: Test{ITest} = Test()
      let newGreeting = test.changeGreeting(newGreeting: "Bonjour!") // ERROR HERE: `member of restricted type is not accessible: changeGreeting`
      log(newGreeting)
    }
}

```

##### Answer

```cadence

pub contract Stuff {

    // function added
    pub struct interface ITest {
      pub var greeting: String
      pub var favouriteFruit: String
      pub fun changeGreeting(newGreeting: String): String
    }

    // Favourite Fruit added
    pub struct Test: ITest {
      pub var greeting: String
      pub var favouriteFruit: String


      pub fun changeGreeting(newGreeting: String): String {
        self.greeting = newGreeting
        return self.greeting
      }

    // Fruit name added
      init() {
        self.greeting = "Hello!"
        self.favouriteFruit = "Mango"
      }
    }

    pub fun fixThis() {
      let test: Test{ITest} = Test()
      let newGreeting = test.changeGreeting(newGreeting: "Bonjour!")
      log(newGreeting)
    }
}

```
