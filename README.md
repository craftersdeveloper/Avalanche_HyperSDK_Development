# Avalanche HyperSDK Introduction 

The HyperSDK provides the ability to create a custom virtual machine, which offers complete control over a custom blockchain. With the HyperSDK, you can design a blockchain that perfectly suits your needs, such as creating and transferring tokens or implementing a traditional order book for asset trading. This level of customization provides a powerful tool for businesses and organizations seeking a tailored solution.

By using the HyperSDK, you have full control over the rules and functionality of your chain, allowing you to create a custom blockchain that is tailored to your startup's specific needs. This offers an unparalleled level of control and flexibility, making it a valuable tool for organizations seeking a custom solution.

**Objective -**Your startup has identified a need to create a custom virtual machine to enable users to mint and transfer tokens. The HyperSDK provides a powerful solution for this task by allowing you to build a custom blockchain tailored to your specific needs. With the HyperSDK, you can define the rules and functionality of your chain, including the ability to create and transfer tokens and manage order books for trading assets.

Creating custom Virtual Machines (VMs) is one of the most powerful ways to build on Avalanche. HyperSDK is designed to simplify and accelerate custom VM development, making it safer and easier to launch your own optimized blockchain.

By abstracting away common runtime complexities, HyperSDK provides industry-leading performance and empowers builders to focus on customizations that matter to them. For example, an operator can launch an on-chain video game with the flexibility of fine tuning the architecture for better gameplay, knowing that HyperSDK will execute their transactions quickly and efficiently behind-the-scenes.

HyperSDK is structured so that developers can plug-into a lightning fast execution environment without writing massive amounts of code from scratch, reducing the time it takes to build your own blockchain runtime from many months to just a few days.

## Function 

The first step to running these demos is to launch your own tokenvm Subnet. You can do so by running the following command from this location (may take a few minutes):

```bash
./scripts/run.sh
```

By default, this allocates all funds on the network to `token1rvzhmceq997zntgvravfagsks6w0ryud3rylh4cdvayry0dl97nsjzf3yp`. The private key for this address is `0x323b1d8f4eed5f0da9da93071b034f2dce9d2d22692c172f3cb252a64ddfafd01b057de320297c29ad0c1f589ea216869cf1938d88c9fbd70d6748323dbf2fa7`. For convenience, this key is also stored at `demo.pk`.

If you don't need 2 Subnets for your testing, you can run:

```bash
MODE="run-single" ./scripts/run.sh
```

To make it easy to interact with the tokenvm, we implemented the `token-cli`. Next, you'll need to build this. You can use the following command from this location to do so:

```bash
./scripts/build.sh
```

This command will put the compiled CLI in `./build/token-cli`.

Lastly, you'll need to add the chains you created and the default key to the `token-cli`. You can use the following commands from this location to do so:

```bash
./build/token-cli key import demo.pk
./build/token-cli chain import-anr
```

`chain import-anr` connects to the Avalanche Network Runner server running in the background and pulls the URIs of all nodes tracking each chain you created.

### Mint and Trade

**Step 1: Create Your Asset**  
First up, let's create our own asset. You can do so by running the following command from this location:

```bash
./build/token-cli action create-asset
```

When you are done, the output should look something like this:

```
database: .token-cli
address: token1rvzhmceq997zntgvravfagsks6w0ryud3rylh4cdvayry0dl97nsjzf3yp
chainID: Em2pZtHr7rDCzii43an2bBi1M2mTFyLN33QP1Xfjy7BcWtaH9
metadata (can be changed later): MarioCoin
continue (y/n): y
✅ txID: 27grFs9vE2YP9kwLM5hQJGLDvqEY9ii71zzdoRHNGC4Appavug
```

The "loaded address" here is the address of the default private key (`demo.pk`). We use this key to authenticate all interactions with the tokenvm.

**Step 2: Mint Your Asset**  
After we've created our own asset, we can now mint some of it. You can do so by running the following command from this location:

```bash
./build/token-cli action mint-asset
```

When you are done, the output should look something like this:

```
database: .token-cli
address: token1rvzhmceq997zntgvravfagsks6w0ryud3rylh4cdvayry0dl97nsjzf3yp
chainID: Em2pZtHr7rDCzii43an2bBi1M2mTFyLN33QP1Xfjy7BcWtaH9
assetID: 27grFs9vE2YP9kwLM5hQJGLDvqEY9ii71zzdoRHNGC4Appavug
metadata: MarioCoin supply: 0
recipient: token1rvzhmceq997zntgvravfagsks6w0ryud3rylh4cdvayry0dl97nsjzf3yp
amount: 10000
continue (y/n): y
✅ txID: X1E5CVFgFFgniFyWcj5wweGg66TyzjK2bMWWTzFwJcwFYkF72
```

**Step 3: View Your Balance**  
Now, let's check that the mint worked right by checking our balance. You can do so by running the following command from this location:

```bash
./build/token-cli key balance
```

When you are done, the output should look something like this:

```
database: .token-cli
address: token1rvzhmceq997zntgvravfagsks6w0ryud3rylh4cdvayry0dl97nsjzf3yp
chainID: Em2pZtHr7rDCzii43an2bBi1M2mTFyLN33QP1Xfjy7BcWtaH9
assetID (use TKN for native token): 27grFs9vE2YP9kwLM5hQJGLDvqEY9ii71zzdoRHNGC4Appavug
metadata: MarioCoin supply: 10000 warp: false
balance: 10000 27grFs9vE2YP9kwLM5hQJGLDvqEY9ii71zzdoRHNGC4Appavug
```

**Step 4: Create an Order**  
So, we have some of our token (MarioCoin)...now what? Let's put an order on-chain that will allow someone to trade the native token (TKN) for some. You can do so by running the following command from this location:

```bash
./build/token-cli action create-order
```

When you are done, the output should look something like this:

```
database: .token-cli
address: token1rvzhmceq997zntgvravfagsks6w0ryud3rylh4cdvayry0dl97nsjzf3yp
chainID: Em2pZtHr7rDCzii43an2bBi1M2mTFyLN33QP1Xfjy7BcWtaH9
in assetID (use TKN for native token): TKN
✔ in tick: 1█
out assetID (use TKN for native token): 27grFs9vE2YP9kwLM5hQJGLDvqEY9ii71zzdoRHNGC4Appavug
metadata: MarioCoin supply: 10000 warp: false
balance: 10000 27grFs9vE2YP9kwLM5hQJGLDvqEY9ii71zzdoRHNGC4Appavug
out tick: 10
supply (must be multiple of out tick): 100
continue (y/n): y
✅ txID: 2TdeT2ZsQtJhbWJuhLZ3eexuCY4UP6W7q5ZiAHMYtVfSSp1ids
```

The "in tick" is how much of the "in assetID" that someone must trade to get "out tick" of the "out assetID". Any fill of this order must send a multiple of "in tick" to be considered valid (this avoids ANY sort of precision issues with computing decimal rates on-chain).

**Step 5: Fill Part of the Order**  
Now that we have an order on-chain, let's fill it! You can do so by running the following command from this location:

```bash
./build/token-cli action fill-order
```

When you are done, the output should look something like this:

```
database: .token-cli
address: token1rvzhmceq997zntgvravfagsks6w0ryud3rylh4cdvayry0dl97nsjzf3yp
chainID: Em2pZtHr7rDCzii43an2bBi1M2mTFyLN33QP1Xfjy7BcWtaH9
in assetID (use TKN for native token): TKN
balance: 997.999993843 TKN
out assetID (use TKN for native token): 27grFs9vE2YP9kwLM5hQJGLDvqEY9ii71zzdoRHNGC4Appavug
metadata: MarioCoin supply: 10000 warp: false
available orders: 1
0) Rate(in/out): 100000000.0000 InTick: 1.000000000 TKN OutTick: 10 27grFs9vE2YP9kwLM5hQJGLDvqEY9ii71zzdoRHNGC4Appavug Remaining: 100 27grFs9vE2YP9kwLM5hQJGLDvqEY9ii71zzdoRHNGC4Appavug
select order: 0
value (must be multiple of in tick): 2
in: 2.000000000 TKN out: 20 27grFs9vE2YP9kwLM5hQJGLDvqEY9ii71zzdoRHNGC4Appavug
continue (y/n): y
✅ txID: uw9YrZcs4QQTEBSR3guVnzQTFyKKm5QFGVTvuGyntSTrx3a
```

### Advantages or Features

1. **User-Friendly Interface:** The CLI (`token-cli`) is designed to be straightforward, making it easy for users to interact with the tokenvm without needing deep technical knowledge.

2. **Custom Token Creation:** Users can create their own digital assets (tokens) with customizable metadata, which can be tailored to specific needs or projects.

3. **Minting Capabilities:** After creating a token, users can mint new tokens, increasing the supply as needed. This feature is crucial for projects that require flexible token issuance.

4. **Balance Verification:** The `token-cli` allows users to easily check their token balances, ensuring transparency and helping users keep track of their assets.

5. **Order Creation and Management:** Users can create, fill, and close orders for token trading directly through the CLI, enabling decentralized trading and liquidity provision.

6. **Interoperability:** The integration with the Avalanche Network Runner allows seamless interaction with multiple nodes and chains, enhancing network flexibility and robustness.

7. **Convenience of Private Key Management:** The default private key (`demo.pk`) simplifies authentication and interaction with the tokenvm, especially for demonstration and testing purposes.

8. **Decentralized Asset Trading:** The platform supports the creation and management of decentralized trading orders, facilitating peer-to-peer exchanges without intermediaries.

9. **Scalable Subnet Deployment:** Users can easily deploy and manage tokenvm Subnets, providing scalability for applications that require dedicated blockchain resources.

10. **Secure Transactions:** Built on Avalanche's secure and efficient blockchain infrastructure, ensuring high levels of security for all transactions and interactions.
