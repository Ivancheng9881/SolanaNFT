//check code is up to date and compatible with latest protocals
ts-node ~/Capstone-project/metaplex/js/packages/cli/src/candy-machine-v2-cli.ts —version

//solana-cli commands:
solana --version
solana address
solana balance
solana config

//create devnet wallet for testing
solana-keygen new --outfile ~/.config/solana/devnet.json  
//set as default keypair
solana config set --keypair ~/.config/solana/devnet.json

//set seller keypair 
solana config set -k ~/.config/solana/devnet.json

//make sure on devnet -- set to devnet:
solana config set --url https://api.devnet.solana.com

//airdrop funds to wallet:
solana airdrop 2 {wallet keypair json file location relative to root directory}

//update creator address in config file metadata of art generator

//generate spl token for presale/whitelist

1. create vanity keypair:
   solana-keygen new --outfile ~/.config/solana/devnetVanity.json
2. create spl-token:
   spl-token create-token ~/.config/solana/devnetVanity.json --decimals 0
3. create account for spl-token:
   spl-token create-account ~/.config/solana/devnetVanity.json
4. mint amount of spl-tokens:
   spl-token mint ~/.config/solana/devnetVanity.json 100

//create airdrop feature

1. create distribution list file
2. -k from seller keypair file to spl-token public address
   ts-node ./Capstone-project/metaplex/js/packages/cli/src/gumdrop-cli.ts create -k ~/.config/solana/devnet.json --claim-integration transfer --transfer-mint B2msgkmnqbfPdqB6FT4TTXoYh43L34ciBVbPjHHcHABF --distribution-method wallets --distribution-list distlist.json
3. white list folders urls to claim spl-token:
   .log/devnet-resp-Pe1tx19U2WvtJJigccbCfi9WgngWg5myXCujAjvuW7f.json

//create config.json file for nft collection options:
{
  "price": 0.1,
  "number": 100,
  "solTreasuryAccount": "EdmPws8yxprsYCa2StiEeZyH4dZpeWfzwCsuwHXR5rLo",
  "gatekeeper": {
    "gatekeeperNetwork": "ignREusXmGrscGNUesoU9mxfds9AiYTezUKex2PsZV6",
    "expireOnUse": true
  },
  "whitelistMintSettings": {
    "mode": { "burnEveryTime": true },
    "mint": "B2msgkmnqbfPdqB6FT4TTXoYh43L34ciBVbPjHHcHABF",
    "presale": true,
    "discountPrice": 0.05
  },
  "splTokenAccount": null,
  "splToken": null,
  "goLiveDate": "25 Dec 2022 00:00:00 GMT",
  "endSettings": null,
  "storage": "arweave",
  "hiddenSettings": null,
  "ipfsInfuraProjectId": null,
  "ipfsInfuraSecret": null,
  "awsS3Bucket": null,
  "noRetainAuthority": false,
  "noMutable": false
}

//get custom hash and run 1 chibi mint and get arweave link to replace hiddensettings uri


//verify assets are compatible with solana nft metadata structure:
ts-node ./Capstone-project/metaplex/js/packages/cli/src/candy-machine-v2-cli.ts verify_assets nftassets


//upload assets to arweave
ts-node ~/Capstone-project/metaplex/js/packages/cli/src/candy-machine-v2-cli.ts upload \
    -e devnet \
    -k ~/.config/solana/devnet.json \
    -cp config.json \
    -c example \
   nftassets

//save candy machine public key
3vGTWdJnQipUZpzW1R7PupgjPbbYvXnhTzyqV4D6Rk9W


//verify upload was successful
ts-node ~/Capstone-project/metaplex/js/packages/cli/src/candy-machine-v2-cli.ts verify_upload -k /Users/ivancheng/.config/solana/devnet.json -c example


//verify price of nft
ts-node ~/Capstone-project/metaplex/js/packages/cli/src/candy-machine-v2-cli.ts verify_price -k /Users/ivancheng/.config/solana/devnet.json -p 0.1 -c example

//candy machine cache file saved as "devnet-example.json in .cache folder


