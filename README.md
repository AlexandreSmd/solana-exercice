# solana-exercice

How to Deploy the Solana Smart Contract Examples
When you are done writing a contract, such as one of the Solana smart contract examples mentioned in this article, you need a way to build and deploy them to the Solana network. Consequently, this section outlines the steps in this process by showing you how to deploy the ”hello_world” contract, which was one of our Solana smart contract examples from one of the previous sections.

First up, if you have not already, set up Rust, the Solana CLI, and a Solana wallet. Next up, open an IDE of your choice and start a new terminal. From there, set up a ”Hello World” Cargo project by running the following command in the terminal: 

cargo init hello_world --lib
This will create a Cargo library in your directory with the files for building the Solana smart contract examples. You can then navigate to the ”hello_world” file with the command below:

cd hello_world
Next, open the ”Cargo.toml” file, copy the code snippet below, and add it at the bottom of the file: 

[lib]
name = "hello_world"
crate-type = ["cdylib", "lib"]
You can then navigate back to the terminal and add the Solana program package by running this command: 

cargo add solana_program
Finally, open the ”src/lib.rs” file and replace all of its contents with the ”hello_world” contract code from the ”Solana Smart Contract Examples” section:

use solana_program::{
    account_info::AccountInfo, entrypoint, entrypoint::ProgramResult, msg, pubkey::Pubkey,
};
entrypoint!(hello_world);
pub fn hello_world(
    _program_id: &Pubkey, // Public key of the account the program was loaded into
    accounts: &[AccountInfo], // All accounts required to process the instruction
    _instruction_data: &[u8], // Serialized instruction-specific data
) -> ProgramResult {
    msg!("Hello {:}!!", accounts[0].key);
    Ok(())
}
With the contract code at your disposal, you should now be able to build the Solana smart contract by inputting the following Cargo command and running it in the terminal:

cargo build-bpf
From there, all that remains is to deploy the contract using the command below: 

solana program deploy ./target/deploy/hello_world.so
