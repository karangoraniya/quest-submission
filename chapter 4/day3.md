# Chapter 4

## Day 3

#### 1. Why did we add a Collection to this contract? List the two main reasons.

- To create many NFT that it will hard to store & give us error already data is stored

- Nobody can gave us NFT, only account owner can do that.

#### 2. What do you have to do if you have resources "nested" inside of another resource? ("Nested resources")

When we use nested resources we have to must declare a destroy function it will delete nested resources.

#### 3. Brainstorm some extra things we may want to add to this contract. Think about what might be problematic with this contract and how we could fix it.

- Idea #1: Do we really want everyone to be able to mint an NFT? 🤔.
  We can whitelist the address which we want them to mint NFT.

- Idea #2: If we want to read information about our NFTs inside our Collection, right now we have to take it out of the Collection to do so. Is this good?

No, You can use `borrow` keyword & path of the collection.
