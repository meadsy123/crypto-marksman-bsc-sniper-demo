# Crypto Marksman Demo - BSC Pancakeswap V2
A Pancakeswap V2 listing sniper bot on the binance smart chain, includes a simple GUI and much more.

If you have any questions or inquiries, you can contact me via telegram: <b>meadzy</b>

<H2>Prerequisites</H2>

- An BSC wallet address and private key
- A Windows machine x64

<H2>Getting started</H2>

1. Read prerequisites

2. Download the latest release which will include "demo.exe.py", "tokens.json", "configfile.py" from the repository.

3. Open "configfile.py" (with notepad for instance) and add your bsc address and private key at the bottom of the file between the quotation marks('').

<pre>...
my_address = ''
my_pk = ''
</pre>

3. Run "demo.exe" - Make sure the release files and its contents folder locations stay as they are, otherwise this program will not run properly.

4. Edit settings according to choice.

<H2>Exchange - Pancakeswap V2 testnet</H2>

The testnet I have used is not the official Pancakeswap testnet due to inconsistencies/unsupported features on their side etc.

https://bsc.kiemtienonline360.com/

There are a few tokens listed on the website above, if you use a token that is not listed then you will get errors as they will not exist. You can add these to the tokens.json for example

<pre>
[
  {
    "symbol": "BUSD",
    "token_name": "BUSD",
    "ethaddress": "0x78867BbEeF44f2326bF8DDd1941a4439382EF2A7",
    "decimals": "18"
  },
  {
    "symbol": "USDT",
    "token_name": "USDT",
    "ethaddress": "0x7ef95a0fee0dd31b22626fa2e10ee6a223f8a684",
    "decimals": "18"
  },
  {
    "symbol": "DAI",
    "token_name": "DAI",
    "ethaddress": "0x8a9424745056Eb399FD19a0EC26A14316684e274",
    "decimals": "18"
  }
]
</pre>

<H2>How to create a test account on Metamask</H2>

To test the application, you will need to setup your wallet and connect to the binance smart chain testnet... Follow this guide for metamask.

https://medium.com/spartanprotocol/how-to-connect-metamask-to-bsc-testnet-7d89c111ab2

<H2>How to get BNB sent to your test account</H2>

To test the application, you need to have BNB, please get it from the following link: https://testnet.binance.org/faucet-smart. After that, you can use BNB to swap for any other tokens that the system supports. Sometimes this does take a while.

<H2>Fields</H2>

<b>Selected Token</b>: The dropdwon will be populated from the tokens list set in tokens.json, once selected the token fields will be automatically populated.

The first swap pair token will have to be WBNB, so you will need to make sure the token you are buying has a pair contract with WBNB. for example WBNB/SAFEMOON. This basically means that you are able to swap the selected token for BNB.

<b>Trade Action</b>: There are 3 trade actions you need to be aware of
1. BUY - a buy transaction will be created, using the token selected. The trade will consist of trading BNB for the selected token.
2. SELL - a sell transaction will be created, the trade consist of the selected token for BNB.
3. BUY/SELL - A buy transaction will be created, then the fields/settings will depend on what instance a sell transaction will be created.

<b>BNB to trade</b>: How many BNB do you wish to use for the transaction.

<b>Token start price</b>: The price used to get the price percentage increase in the price thread which populates the prices/balances at the bottom of the program.

<b>Token to buy</b>: Instead of using the "BNB to trade" which will get as many tokens as possible, this field will use the exact output and calculate the amount of BNB that will be used in the trade at that given time

<b>Max overall slippage</b>
The max slippage you want the bot to handle. Can be set from 1 to 100%. 100%= the bot only will
accept a trade if the minimal amount of tokens it gets is 0 (=always accepting).
Slippage is the expected % difference between these quoted and executed prices. Low liquidity can
also cause increased slippage, which is why larger orders tend to face higher slippage.

<b>Gas limit</b>
Please set this at 500000, so an order will never fail because you didn’t accept a higher gas.

<b>GWEI fee to use for trade</b>
This field is the amount of GWEI (fee) you want to use for a trade. For sniping you want to keep this much higher than normal trading, so the block is mined as fast as possible. I recommend using more than 20 when sniping maybe even more. (normal trading is done at 5 GWEI). How much higher depends on the token (how
much people are going to snipe), your latency with the RPC and if you really want to compete with
the fastest guys, or just don’t want to make a profit. The fastest snipes use the highest GWEI and are
only worth it when you play with a lot of BNB.

<H3>Buy</H3>

<b>Different deposit address</b>: Use this if you want the swap output to go to a different wallet address. There is a toggle for true/false and a field in config.py for the different address.

<b>Liquidity Check</b>: If the liquidty check toggle is set to true, a concurrent thread is created to continuosly check the liquidity. Firstly, the bot will check if the selected  pair contract is avaiable on the exchange factory contract for example (WBNB/SAFEMOON), if true the loop will start checking if the liquidity is available on the exchange router. Once liquidity is available the trade function is called as fast as possible. If the liquity check toggle is set to false, the trade function will start straight away. <b> This is not available on the demo due to testnet Pancakeswap factory contract not working.</b>

<b>Liquidity Speed</b>: The amount of time the bot has to wait per liquidity check. If this is set at 0ms, its fine.

<b>Only buy if price is less than </b>
This so you wont buy a token for too much $. Especially handy for failing buy orders due to too less
slippage or GWEI and for scam launches/IDO’s which add a token for too much $.

<H3>Sell</H3>

<b>Custom Slippage for selling</b>
The max slippage you want the bot to use when selling. Can be set from 1 to 100%. 100%= the bot only will
accept a trade if the minimal amount of tokens it gets is 0 (=always accepting).
Slippage is the expected % difference between these quoted and executed prices. Low liquidity can
also cause increased slippage, which is why larger orders tend to face higher slippage.

<b>Amount of seconds to wait until sell</b>
This field is used for the time between the buy transaction and the sell transaction.

<b>Sell when token price is more than</b>
The price will be checked continously until this price is greater than the buy price. At that point a sell transaction will ber created. slippage and fees will still apply.

<b>Sell when token price is % higher than buy</b>
The price will be checked continously until this price is greater the specified percentage higher than the buy price. At that point a sell transaction will be creates. slippage and fees will still apply.

<H2>Buttons</H2>

<b>Wallet Balance</b>: A list of tokens that are listed in the tokens.json are used to retrieve the token balance from your wallet and the token price to calculate your total price from pancakswap. 

<b>Start</b>: A thread is created which the sniping bot will run on. please be aware every click will create a new thread and therefore a new transaction.

<b>Stop</b>: Stops all concurrent threads, includes buy/sell transaction threads or price/balance thread.

<b>Check Latency</b>: The time taken for you to receive a response from the blockchain.

<H2>Logging and Reports</H2>

There is more extensive reporting/logging in the if you turn debug mode on, either using the GUI or by setting debugmode='1' in the configfile.py.

The logging is added to logs/console.log in the directory of the release.

All transactions data is added to the json/transactions.json file

![image](https://user-images.githubusercontent.com/16119958/131032421-ad2e3071-4deb-4086-ad57-60b2953ee25f.png)

Once you have the tx you can search your transactions up on 'https://testnet.bscscan.com/tx/ADD_YOUR_TX_HASH_HERE'


<H2>Common Errors</h2>

- Transaction is not in sync with the chain. This is due to either a processing transaction using the same nonce as the current transaction or your nonces are out of sync. simple solution send your 0 using a custom nonce (get the last nonce from tx list and add 1). this should reset your nonce.
- "Returned error: replacement transaction underpriced" 
  1. You have a pending transaction from your account
  2. The new transaction you are sending has the same nonce as that pending transaction
  3. The new transaction you sent has a gas price that is too small to replace the pending transaction
  
- 'transaction underpriced' Or your GWEI is too low or your max gas is too low.For max gas 700k (700000) is advisable, this way a transaction will never fail because of gas.

-'insufficient funds for gas * price + value', You didn’t have enough bnb on your account for the trade. transaction fee in bnb= (gwei* gas)* 0.000000001
- 'already known', This is the error you get when the bot was trying to approve a token, but that token was already approved in the end. 
- SSL errors. This is a problem is possibility that your vpn, anti-virus or firewall is blocking the bot.


<H2>BSC Errors</h2>
- Fail with error TransferHelper: ‘TRANSFER_FROM_FAILED’ ‘max gas' was too low. Please set the max-gas at 700k to be sure it never fails because of that.

<br> </br>
<H2>To do</H2>

- Add multiple exchanges to choose from.
- create multiple bots for all blockchains. eth, matic, cardano etc
- Add actual tokens bought to transactions.json file

<br> </br>
<H2>Author</H2>

If you have any questions you can contact me via telegram: meadzy

<br> </br>
<H2>Disclosure</H2>
Use the application at your own risk, I am not in any way responsible for losses.
