## Deploying the smart contract 

  Ubuntu 22.04
   
## Server Preparation
  
  Upgrade packages and the system

  ```
  apt update 
  ```
    
  ``` 
  apt upgrade
  ```
    
  Installing Git
  
  ``` 
  apt install curl git -y
  ```
  
  Installing Rust  
  
  ``` 
  curl — proto ‘=https’ — tlsv1.2 -sSf https://sh.rustup.rs | sh 
  ```
  select the number "1"
  
  ``` 
  source "$HOME/.cargo/env"
  ```
  
  Downloading fuelup
 
  ``` 
  curl — proto ‘=https’ — tlsv1.2 -sSf https://fuellabs.github.io/fuelup/fuelup-init.sh | sh
  ```
  
  Confirm by pressing "Y"

  Set the variables

  ``` 
  export PATH="${HOME}/.fuelup/bin:${PATH}"
  ```
  
  Creating a directory  
  
  ``` 
  mkdir fuel-project
  ```
  
  go to the directory
  
  ``` 
  cd fuel-project
  ```
    
  ``` 
  forc new counter-contract
  ```
  
 Go to the path ```/root/fuel-project/counter-contract/src/main.sw```  
 
 Or run the commands:
 
  ``` 
  sudo apt install vim
  ```
  
  ``` 
  vim counter-contract/src/main.sw
  ```

delete the contents of the file main.sw
  
copy the contract code and paste it into the file ```main.sw```
 
 ``` 
 contract;

storage {
    counter: u64 = 0,
}

abi Counter {
    #[storage(read, write)]
    fn increment();

    #[storage(read)]
    fn count() -> u64;
}

impl Counter for Contract {
    #[storage(read)]
    fn count() -> u64 {
        storage.counter
    }

    #[storage(read, write)]
    fn increment() {
        storage.counter = storage.counter + 1;
    }
}

 ```
 official web site https://fuellabs.github.io/fuel-docs/master/developer-quickstart.html
 
 loading components
 
  ``` 
  fuelup toolchain new test_toolchain
  ```
  
  ``` 
  fuelup component add forc@0.31.1
  ```
  
  ``` 
  fuelup component add forc-wallet
  ```
  
  go to the directory
  
  ``` 
  cd counter-contract
  ```
  
  Build packages
  
  ``` 
  forc build
  ```
 
 Create a wallet and make up a password (be sure to save the mnemonic phrase)
 
  ``` 
  forc-wallet init
  ```
  
  ``` 
  forc-wallet new
  ```
  
  Copy the wallet address and get test tokens from the [faucet](https://faucet-beta-2.fuel.network/)
  
  Executing Deploy
  
  ``` 
  forc deploy --url https://node-beta-2.fuel.network/graphql --gas-price 1
  ```
  
  Insert the wallet address and get the Tx id to sign
  
  **Then connect to the same host or open a second session** 
  
  Executing commands in the second session:
  
  ``` 
  cd fuel-project
  ```
  
  ``` 
  cd counter-contract
  ```
  
  ``` 
  export PATH="${HOME}/.fuelup/bin:${PATH}"
  ```
  
  ``` 
  forc wallet sign "Tx id to sign **from first session**" 0
  ```
  
  Copy the signature and paste it into the first session
  
  We end up with the **TransactionId**

copy **TransactionId** and add 0x at the beginning of the line 
Then we check our transaction in the [explorer](https://fuellabs.github.io/block-explorer-v2/)

If you originally had **Beta-1** you should upgrade to **Beta-2** 
Click on Tesnet Beta-1 [Pngtree-vector-right-arrow-icon-4231911.png](https://postimg.cc/14W2SQjy) Add Custom Network and replace the line node-beta-1 with node-beta-2 and click **Switch**

After that we check our contract


  
  
  
           
  
  
 
