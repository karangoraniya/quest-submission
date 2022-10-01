# Chapter 2

## Day 1

#### 1. Explain why we wouldn't call `changeGreeting` in a script.

We cannot modify information using script, by using script we can only view information.

#### 2. What does the `AuthAccount` mean in the `prepare` phase of the transaction?

Compared to other blockchain `Flow` stored NFT in account. Whenever a user sends a transaction, we have to give a small amount of gas fees to get access to your account. We use `AuthAccount` then we can easily approve the transactions.

#### 3. What is the difference between the `prepare` phase and the `execute` phase in the transaction?

In the `prepare` phase, the main aim is to access the information/data from your account. The `execute` phase cannot do this task. `Execute` phase only calls the functions & changes the data on the blockchain.

#### 4. This is the hardest quest so far, so if it takes you some time, do not worry! I can help you in the Discord if you have questions.

- Add two new things inside your contract:

  - A variable named `myNumber` that has type `Int` (set it to 0 when the contract is deployed)
  - A function named `updateMyNumber` that takes in a new number named `newNumber` as a parameter that has type `Int` and updates `myNumber` to be `newNumber`

  ```Cadence
  pub contract HelloWorld {

    pub var greeting: String
    pub var myNumber: Int

    pub fun changeGreeting(newGreeting: String) {
        self.greeting = newGreeting
    }

    pub fun updateMyNumber(newNumber: Int) {
        self.myNumber = newNumber
    }

    init() {
        self.greeting = "Hello, World!"
        self.myNumber = 0
    }
  }

  ```

- Add a script that reads `myNumber` from the contract

```Cadence
    import HelloWorld from 0x01

    pub fun main():String  {
      return HelloWorld.myNumber
    }
```

- Add a transaction that takes in a parameter named `myNewNumber` and passes it into the `updateMyNumber` function. Verify that your number changed by running the script again.

```Cadence
    import HelloWorld from 0x01

    transaction(myNewNumber: Int) {

    prepare(signer: AuthAccount) {}

    execute {
     HelloWorld.updateMyNumber(newNumber: myNewNumber)
    }
}
```
