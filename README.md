
## Projects Outlines
### Core
- Desktop App
    - bot runs from desktop directly to exchanges. We do NOT want to store or handle anyones' secret keys, api keys, passwords.
    - any data will be stored locally on Sqlite.
    - has graceful restart. Right now the bot uses systemd to capture kill signal and restart it.
    - interface - core integration
    - support charts, possibly TradingView
- User Interface
    - Minimalist no bulshit interface
    - UI will only manipulate a json file which is read by the bot during runtime. The bot will be able to run without UI.
- Expansion to other exchanges
- Profit calculation

#### DB models
- txs
    - bot can restart trades from user's own last filled order (default = last market tick)

### Optimization
- Look for correlations
    - Leading and lagging pairs
    - Leading and lagging exchanges
    - Volume changes (100 of them, )
    - BTC, altcoins movements
    -

- Adaptive strategy  
    - Knowing which direction the market will go can help the bot make bigger profit.
    - Eg. Big buy volume, small sell volume -> market moves to sell -> reprice sell orders at wider level

- Crypto flow map at big exchanges
    - BTC flowing in = altcoins are going to go up
    - Altcoins moving in = altcoins going to go down. The only reason altcoins are entering an exchange is to be sold.
    - Need to observe exchanges' cold wallets and hot wallets.

- Historical data
    - Save historical data for top coins

- Backtesting
    - study free repos for backtesting at Github


### News scorer
- Score a news article given the effect it has on price
- Cryptopanic has aggregate news articles tagged with relevant coin  



### Arbitrage
- Direct
    - fund is transferred directly for each tx through blockchain process.
    - risk is determined by the amount of time the fund is processed
- Reserves
    - maintain fund reserves / pools at different exchanges. Buy and sell orders will draw from the respective pools.
    - need to figure out refill window.


## Immediate projects
- Price data
    - Need to investigate github, others for sources 
- OkEx bot implementations
    - Requires seapration of API lib
- CCXT API implementations in Scala
    - in order : OkEX, Binance, Huobi
- Altcoins flowmap
    - find out hot wallet / cold wallet addresses
- Cryptopanic price tagger : tags news on price chart


#### Some resources
- All relevant crypto / quant resources : https://github.com/EliteQuant/EliteQuant
- Arbitrage bot https://github.com/bitrinjani/r2
- Arbitrage oppurtunity : https://github.com/manu354/cryptocurrency-arbitrage
- Market making https://github.com/ctubio/Krypto-trading-bot


- Machine learning
    - https://web.stanford.edu/class/msande448/2017/Final/Reports/gr4.pdf
    - https://papers.nips.cc/paper/4910-adaptive-market-making-via-online-learning.pdf
    - http://webee.technion.ac.il/control/info/Projects/Students/2012/Ori%20Gil/Book/Market%20Making%20Article.pdf
    - https://pdfs.semanticscholar.org/88d3/893855c3b54b0acfd436075122319c1dd518.pdf (has a github repo)


####
-  The three components

Order processing costs represent a fee arising from order execution like ad-
ministrative cost and compensation for the market maker’s time.  

Inventory costs  originate  from  holding  unwanted  risky  securities  in  inventory  by  the
market maker.  

Adverse selection costs exist due to asymmetric information
between the market maker and informed traders.  Informed traders are indi-
viduals who are better informed about the expected price movement of the
underlying  security.


- Early correlation

Negative correlation between the bid-ask spread and security price, trading
volume  and  market  capitalization.   

On  the  other  hand,  bid-ask  spread  is
positive correlated with the volatility of the security price.
