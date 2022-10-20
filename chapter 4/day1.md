# Chapter 4

## Day 1

#### 1. Explain what lives inside of an account.

- Contract Code
- Account Storage

#### 2. What is the difference between the /storage/, /public/, and /private/ paths?

`Storage` is the entry point to access data in your account & only owner can access.
Anyone can see & access to the `Public` data
`Private` can access by only owner & owner who gave access to someone.

#### 3. What does .save() do? What does .load() do? What does .borrow() do?

`.save()` store the data to the account.
`.load()` fetch the stored data from the account.
`.borrow()` borrow reference from the account

#### 4. Explain why we couldn't save something to our account storage inside of a script.

Because `Script` is only for reading & Execute the output of the contract. If you want to write something in contract then you have to use Transaction.

#### 5. Explain why I couldn't save something to your account.

To save something to your account you have to give access by using `prepare(signer: AuthAccount)`.

#### 6. Define a contract that returns a resource that has at least 1 field in it. Then, write 2 transactions:

```cadence
pub contract Blockchains {

  pub resource Flow {
    pub var price: UFix64
    init() {
      self.price = 1.447
    }
  }

  pub fun createFlowPrice(): @Flow {
    return <- create Flow()
  }

}




```

##### i. A transaction that first saves the resource to account storage, then loads it out of account storage, logs a field inside the resource, and destroys it.

```cadence
import Blockchains from 0x01
transaction() {
  prepare(signer: AuthAccount) {

    // It will sotred data in account
    let flowPrice <- Blockchains.createFlowPrice()
    signer.save(<- flowPrice, to: /storage/flowPrice)

    // It will loads from the account storage & we will also add panice if there is no data so we can gave error
    let fetchFlowPrice <- signer.load<@Blockchains.Flow>(from: /storage/flowPrice) ?? panic("Lost in account storage")
    log(fetchFlowPrice.price)

    destroy fetchFlowPrice
  }

  execute {

  }
}
```

##### ii. A transaction that first saves the resource to account storage, then borrows a reference to it, and logs a field inside the resource.

```cadence
import Blockchains from 0x01
transaction() {
  prepare(signer: AuthAccount) {

    // It will sotred data in account
    let flowPrice <- Blockchains.createFlowPrice()
    signer.save(<- flowPrice, to: /storage/flowPrice)

    // It will borrow from the resources we are using signer.borrow instead of load
    let borrowFlowPrice = signer.borrow<&Blockchains.Flow>(from: /storage/flowPrice) ?? panic("Lost in account storage no ones there")
    log(borrowFlowPrice.price)
  }

  execute {

  }
}



```
