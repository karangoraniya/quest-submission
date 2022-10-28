# Chapter 4

## Day 2

#### 1. What does .link() do?

`.link()` provides the path to storage and link of the target.
It takes two parameter path & target.

#### 2. In your own words (no code), explain how we can use resource interfaces to only expose certain things to the /public/ path.

We can use resources interfaces to hide unwanted function which are bring vulnerability to contract so we use `link` to specific path to access them.

#### 3. Deploy a contract that contains a resource that implements a resource interface. Then, do the following:

```cadence
pub contract Blockchains {

  pub resource interface IFlow {
      pub var price: UFix64
    }

  pub resource Flow:IFlow {
    pub var price: UFix64
    pub var type: String
    init() {
      self.price = 1.447
      self.type = "POS"
    }
  }

  pub fun createFlowPrice(): @Flow {
    return <- create Flow()
  }

}
```

##### i. In a transaction, save the resource to storage and link it to the public with the restrictive interface.

```cadence
import Blockchains from 0x01

transaction() {

  prepare(signer: AuthAccount) {

    signer.save(<- Blockchains.createFlowPrice(), to: /storage/MyFlowResource)

    signer.link<&Blockchains.Flow{Blockchains.IFlow}>(/public/MyFlowResource, target: /storage/MyFlowResource)
  }

  execute {

  }
}

```

##### ii. Run a script that tries to access a non-exposed field in the resource interface, and see the error pop up.

```cadence
import Blockchains from 0x01

pub fun main(address: Address): String {
  let publicCapability: Capability<&Blockchains.Flow{Blockchains.IFlow}> =
    getAccount(address).getCapability<&Blockchains.Flow{Blockchains.IFlow}>(/public/MyFlowResource)

  let flowResource: &Blockchains.Flow{Blockchains.IFlow} = publicCapability.borrow() ?? panic("The capability doesn't exist or you did not specify the right type when you got the capability.")

  return flowResource.type
}


```

##### iii. Run the script and access something you CAN read from. Return it from the script.

```cadence
import Blockchains from 0x01

pub fun main(address: Address): UFix64 {
  let publicCapability: Capability<&Blockchains.Flow{Blockchains.IFlow}> =
    getAccount(address).getCapability<&Blockchains.Flow{Blockchains.IFlow}>(/public/MyFlowResource)

  let flowResource: &Blockchains.Flow{Blockchains.IFlow} = publicCapability.borrow() ?? panic("The capability doesn't exist or you did not specify the right type when you got the capability.")

  return flowResource.price
}


```
