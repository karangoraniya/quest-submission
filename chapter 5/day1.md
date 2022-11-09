# Chapter 5

## Day 1

#### 1. Describe what an event is, and why it might be useful to a client.

Events are a way for a smart contract to communicate to the outside world if something happens on blockchain. Events are always public.

#### 2. Deploy a contract with an event in it, and emit the event somewhere else in the contract indicating that it happened.

```cadence
pub contract Cartoon {

  pub var name: String
  pub event Movie(name: String)

  pub fun MovieName(): String {
    return self.name
  }

    init() {
      self.name = "Toy Story"
      emit Movie(name: self.name)
    }

}
```

#### 3. Using the contract in step 2), add some pre conditions and post conditions to your contract to get used to writing them out.

```cadence
pub contract Cartoon {

  pub var name: String
  pub event Movie(name: String)

  pub fun MovieName(): String {
      pre {
          self.name == "Toy Story": "Movie doesn’t exist"
      }
    return self.name
  }

  pub fun newMovie(): String {
    post {
        self.name != "Minions": "Lost in space"
    }

    return self.name
  }
    init() {
      self.name = "Toy Story"
      emit Movie(name: self.name)
    }

}



```

#### 4. For each of the functions below (numberOne, numberTwo, numberThree), follow the instructions.

```cadence
pub contract Test {

  // TODO
  // Tell me whether or not this function will log the name.
  // name: 'Jacob'
  // Answers : Yes it will log name Jacob, becoz it match pre condition length 5 = jacob
  pub fun numberOne(name: String) {
    pre {
      name.length == 5: "This name is not cool enough."
    }
    log(name)
  }

  // TODO
  // Tell me whether or not this function will return a value.
  // name: 'Jacob'
  // Answers : Yes, it will return the value. length on name is greater then = zero.

  pub fun numberTwo(name: String): String {
    pre {
      name.length >= 0: "You must input a valid name."
    }
    post {
      result == "Jacob Tucker"
    }
    return name.concat(" Tucker")
  }

  pub resource TestResource {
    pub var number: Int

    // TODO
    // Tell me whether or not this function will log the updated number.
    // Also, tell me the value of `self.number` after it's run.
    // Answers : confused
    pub fun numberThree(): Int {
      post {
        before(self.number) == result + 1
      }
      self.number = self.number + 1
      return self.number
    }

    init() {
      self.number = 0
    }

  }

}
```
