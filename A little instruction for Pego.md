### ***A small example of how to transfer tokens from Umee to network ETH  and back***

First I will check my balance
```
umeed q bank balances umee1sjsxzwpg5kx4ugdq28r7eg5lcwt8ser02t9fny
```
```
balances:
- amount: "51500000"
  denom: peggy0x4884E2a214DC5040f52A41c3f21c765283170B6e
- amount: "22290327"
  denom: uumee
pagination:
  next_key: null
  total: "0"
```
Let's try to send 10 Umme, in Umme, the decimals value is 6
### ***If you use the keyring-backend "test" do not forget to specify this in the flag***
Check out the description of the flags
```
umeed tx peggy send-to-eth -h
```
```
umeed tx peggy send-to-eth 0xb2bbc5c33BD5cefE217fAC617CBd1174D69CCE85 10000000uumee  600uumee \
--from $UMEE_WALLET --chain-id=$CREATE_VALIDATOR_CHAIN --gas=auto   --keyring-backend os   --gas-adjustment=1.4
```
![Image Alt](https://github.com/studentmtk/Umee-Peggo/blob/main/screenshots/1.PNG)

https://umee-internal-peggy-1-explorer.nodes.guru/transactions/4A06D3815BEAD09BF36F5CE8167ADA5126D7BB4416F1067EA22393BC2C25EE6C

Our transaction was completed successfully. After a few minutes (sometimes longer, be patient) check if the tokens have arrived?

https://goerli.etherscan.io/tx/0xf7ec5951d460adbf67e3d785387cc656185cb9fe959d76f490a2d65b5ccf2bd9


Ok, let's send them back, I chose a random address from the explorer (umee1jskhj2mws74tkerxqdd4jgyht40hgv4suns00z)

To do this, we need to find out the address of the Umee token contract on the ETH network


![Image Alt](https://github.com/studentmtk/Umee-Peggo/blob/main/screenshots/2.png)

![Image Alt](https://github.com/studentmtk/Umee-Peggo/blob/main/screenshots/3.PNG)

0x3760b06e26dd5583462c3a0fc8cc4bc8079ebb0b - this is the address of the Umee token contract on the ETH network.

ETH_PK="YOUR_ETHEREUM_PRIVATE_KEY" 
### ***Please note that when sending tokens from the ETH network to the Umee network, we simply specify the number of tokens without adding denom***
Check out the description of the flags
```
peggo bridge send-to-cosmos -h
```
```
peggo bridge send-to-cosmos 0x3760b06e26dd5583462c3a0fc8cc4bc8079ebb0b umee1jskhj2mws74tkerxqdd4jgyht40hgv4suns00z 10000000 \
--eth-pk $ETH_PK --eth-rpc "https://goerli-light.nodes.guru/"
```

![Image Alt](https://github.com/studentmtk/Umee-Peggo/blob/main/screenshots/4.PNG)

https://goerli.etherscan.io/tx/0xe2c3b2fe0b1509486a4bd51dcf965401f232e0c0667ae17a0154677e560cb423

https://umee-internal-peggy-1-explorer.nodes.guru/transactions/11EA6E616110456BB6EA13409C88157B609509B2AEABCE9811181F4E3003611D

We check the balance, it has increased, everything is fine, we are well done

![Image Alt](https://github.com/studentmtk/Umee-Peggo/blob/main/screenshots/5.PNG)



Let's send to the Umee network for example UNI tokens
We go to the Uniswap application ( https://app.uniswap.org/ ), connect our metamask and change our test eth to UNI tokens.

### ***Make sure that you make exchanges on the Goerli test network!!!!***

Let's find out the UNI token contract, pay attention to the value of "Decimals" - 0x1f9840a85d5af5bf1d1762f925bdaddc4201f984

![Image Alt](https://github.com/studentmtk/Umee-Peggo/blob/main/screenshots/6.PNG)

Let's make a transaction with new parameters
```
peggo bridge send-to-cosmos 0x1f9840a85d5af5bf1d1762f925bdaddc4201f984 umee1jskhj2mws74tkerxqdd4jgyht40hgv4suns00z 100000000000000000 \
--eth-pk $ETH_PK --eth-rpc "https://goerli-light.nodes.guru/"
```
I made a mistake and didn't add 0, instead of 1 UNI, I sent 0.1 UNI, be careful

https://goerli.etherscan.io/tx/0xdf82c120deba0cdc0789c87d24d2a8f7a045dce8aeef8e70264c3da66351f098



https://umee-internal-peggy-1-explorer.nodes.guru/transactions/1CDAE63181862EE4326725CDA1C93369375CB3D68BEA179B499256A721F83782

https://umee-internal-peggy-1-explorer.nodes.guru/transactions/BC881A3EB6758B04FA466D90D411EF6D063863C2D96E13F4B6D65A88B9B949B8

https://umee-internal-peggy-1-explorer.nodes.guru/transactions/59413F8A7B5E7BA63DC65803EFC9BC4ABD7171BDE4BB0D16702778BA40E443F4

Check the balance, tokens in the wallet, we are well done

![Image Alt](https://github.com/studentmtk/Umee-Peggo/blob/main/screenshots/7.PNG)

### Be sure to read the description of the principles of operation of the Peggo device
https://github.com/umee-network/peggo#how-it-works

https://blog.althea.net/how-gravity-works/
