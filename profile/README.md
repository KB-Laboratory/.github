# KB Lab

> 🚀 Empowering digital companies to leverage web3 for their business success by harnessing the power of open source software and community of practice.

## About KB Lab

At KB Lab, our mission is to empower digital companies with innovative web3 solutions. Our products combine blockchain technology with open source practices, ensuring transparency, security, and community-driven innovation.


For more information or to get involved, please reach out via:
- **Email:** [aungkokothet@gmail.com](mailto:aungkokothet@gmail.com), [aungmyatmoe834@gmail.com](mailto:aungmyatmoe834@gmail.com)
- **Website:** [www.kblab.co](http://www.kblab.co)


## Our Products
Have to put list of products and images.

## How to embrace Web3 Open Source and Blockchain

### Transfer Points Between Wallets
```ts
export class StellarServie {

 async sendAmount(
    issuer: any,
    source: any,
    destination: any,
    amount: number,
    url?: string
  ) {
    var server = new StellarSdk.Server(url || this.horizonSourceURL, {
      headers: {
        "api-key": process.env.NOWNODES_API_KEY,
      },
      apiKey: process.env.NOWNODES_API_KEY,
    });
    var parentAccount = await server.loadAccount(source.publicKey()); //make sure the parent account exists on ledger

    var drunkDuck = new Asset(this.asset, issuer.publicKey());

    console.log("start here");
    //create a transacion object.
    var transferAmountTxn = new StellarSdk.TransactionBuilder(parentAccount, {
      fee: StellarSdk.BASE_FEE,
      networkPassphrase: StellarSdk.Networks.PUBLIC,
    });

    console.log("start here 1");
    transferAmountTxn = await transferAmountTxn
      .addOperation(
        Operation.payment({
          destination: destination.publicKey(),
          asset: drunkDuck,
          amount: amount ? `${amount}` : "10",
        })
      )
      .addMemo(StellarSdk.Memo.text("Test Transaction")) // TODO: add more meaningful memo
      .setTimeout(180)
      .build();

    console.log("start here 3");
    //sign the transaction with the account that was created from friendbot.
    await transferAmountTxn.sign(source);

    //submit the transaction
    const response = await server.submitTransaction(transferAmountTxn);

    return response;
  }
}

const stellerService = new StellarServie()
stellerService.sendAmount(
    issuer: any,
    source: any,
    destination: any,
    amount: number,
    url?: string
  )
stellerService.checkBalance(source: any, url?: string)```
```
## Minting NFT

```ts
export class AlchemyService {
  public async mintMultipleNFTs(
    description: string,
    image_url: string
  ): Promise<void> {
    try {
      const numberOfTokens = 1;

      for (let i = 1; i <= numberOfTokens; i++) {
        const metadata = this.createMetadataObject(i, description, image_url);
        const metadataBuffer = Buffer.from(JSON.stringify(metadata));
        const tokenUri = await this.uploadToPinata(metadataBuffer);

        const mintTxn = await this.myNftContract.mintNFT(
          this.signer.address,
          tokenUri
        );
        await mintTxn.wait();
        console.log(`NFT #${i} minted! Txn Hash: ${mintTxn.hash}`);
      }
    } catch (error: any) {
      console.error("Error minting NFT: ", error.message);
    }
  }
}

const nftService = new AlchemyService(description: string, image_url: string);
```
