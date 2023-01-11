##Deploying the smart contract 

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
  
  Change the current directory
  
  ``` 
  cd fuel-project
  ```
    
  ``` 
  forc new counter-contract
  ```
  
 Go to the path /root/fuel-project/counter-contract/src/main.sw
 
 Or run the commands:
 
  ``` 
  sudo apt install vim
  ```
  
  ``` 
  vim counter-contract/src/main.sw
  ```

delete the contents of the file main.sw
  
copy the contract code and paste it into the file main.sw
 
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
  
  ``` 
  cd counter-contract
  ```
  
  ``` 
  forc build
  ```
  
  ``` 
  forc-wallet init
  ```
  
  
 
