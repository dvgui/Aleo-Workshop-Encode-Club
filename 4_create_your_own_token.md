# \#4. Create and Test Your Token


Here we will create a token program of our own.

## Create a token contract

For this demo, our desired features are following:

- Mint Function: Able to mint user specific `amount` of `token` to the one who called the mint function.
- Transfer Function: Able to transfer other user (`recipient`) specific `amount` of the `token` that was minted using mint function.

### Step one: define your token record

Define a token struct with an owner and balance

```leo
record Token {
    // The token owner, any record must be defined with the `owner` field.
    owner: address,
    // Token balance of the user.
    balance: u64,
}
```

### Step two: define mint function
Define a mint transition that takes a balance and returns a token record.

```leo
transition mint(owner: address, amount: u64) -> Token {
        return Token {
            owner: owner,
            amount: amount,
        };
    }
```

You can refer to the [project directory](token_f3_vc) for setting up the project 

### Step three: Define transfer function
Define a transfer transition that takes a receiver, amount and token and returns two tokens records

```leo
 transition transfer(token: Token, to: address, amount: u64) -> (Token, Token) {
        // Checks the given token record has sufficient balance.
        // This `sub` operation is safe, and the proof will fail
        // if an overflow occurs.
        // `difference` holds the change amount to be returned to sender.
        let difference: u64 = token.amount - amount;

        // Produce a token record with the change amount for the sender.
        let remaining: Token = Token {
            owner: token.owner,
            amount: difference,
        };

        // Produce a token record for the specified receiver.
        let transferred: Token = Token {
            owner: to,
            amount: amount,
        };

        // Output the sender's change record and the receiver's record.
        return (remaining, transferred);
    }
```

## Test Program

### Test Mint function

First Test Mint Function.
```bash
leo run mint <owner address> 100u64
```

The output should be a record of new 100 tokens.

### Test Transfer function

Then go ahead and test Transfer Function, let's transfer 10 tokens to other address.
```bash
leo run transfer "<Token Record>" <recipient's address> 10u64
```

Then the output should be two record where 10 tokens are owned under recipient's address, and remaining 90 tokens are owned by the original owner.

Notes:
- Remember to replace <recipient's address> field to actual address of the recipient.
- input token record should be the one that is returned after you minted. 
- the record logged on terminal usually has ".private", ".public" keywords after all properties of the record. Those are just indicators to show whether certain properties of the record is public or private.
