
# Projects Outlines
## Core
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
- Configurations
    - bot can restart trades from user's own last filled order (default = last market tick)

## Prediction / AI
### Adaptive Strategy
- Knowing which direction the market will go can help the bot make bigger profit.
- e.g. Big buy volume, small sell volume -> market moves to sell -> reprice sell orders at wider level

### Trade data
- Look for correlations
    - Leading and lagging pairs
    - Leading and lagging exchanges
    - Volume changes

- Crypto flow in and out at big exchanges
    - BTC flowing in = altcoins are going to go up
    - Altcoins moving in = altcoins going to go down. The only reason altcoins are entering an exchange is to be sold.
    - Need to observe exchanges' hot wallets.

### News data
#### News scorer
- Score a news article
- With the score metric, see how it impacts the market
    - News might lag the effect since news date corresponds to publication date
    - News might lead the effect or has long term effect (e.g. XRP's Japan-Korea real time test, Operation "Cryptosweep")
    - News about new crypto listing seems to have big positive impact.
    - News about ad ban, regulation / authority crackdown, seems to have big negative impact.   
- Cryptopanic has aggregate news articles tagged with relevant coin  

### Backtesting
- study free backtesting repos at Github

## Arbitrage
- Direct
    - fund is transferred directly for each tx through blockchain process.
    - risk is determined by the amount of time the fund is processed
- Reserves
    - maintain fund reserves / pools at different exchanges. Buy and sell orders will draw from the respective pools.
    - need to figure out refill window.

## Immediate projects
### Price, other market metrics (raw) data
- Need to have raw data for 100 top coins at 100 top exchanges
- This data should be public so no need to use api key

#### Historical past data
- Past data may not be available through api request, need to look around forums and github.
- Cryptocompare may have some past data.

#### Current data
- Build a real-time importer

#### High-order processing
- Produce less fine data set (seconds -> hours -> day)
- Produce relevant market indicator and features

### API lib in Java or Scala
- Need to translate api libs from CCXT for exchanges of interest to Java or Scala
- In order : OkEx, Binance, Huobi

### Flow map, exchanges
- Find out the amount of coin entering and leaving an exchange
- To do so we need to obtain **hot wallet address** for each coin at an exchange
- Then observe the flow of each address real time

### Flow map, whales
- We are focusing on NOAH https://etherscan.io/address/0x58a4884182d9e835597f405e5f258290e46ae7c2#tokentxns
- List top largest coin holders
- Observe transfers from and to these addresses, refresh list
- Alert if there's a massive amount being transferred
- Derive statistics like biggest daily transfers, biggest transfers all time, most active accounts


#### Getting wallet address
- The best way is ask around
- Open an account, fund each native wallet under that account with some crypto, observe where it goes to or where the fund comes from in case of withdrawal.
- XRP might use destination tag and associate it with a user.

### Data Visualization, general
- Present data on Trade View.

### Bot integration
- Integrate core elements and UI
- Think of how to package Java jar and non-Java UI module into a standalone app
- Think of other possibilities : offline browser app, PWA, etc

### Bot core
- [x]trade starts from own last data.
    - Do, add API call for own last trade
- ~~create "good enough" price level comparison, use it to reseed orders~~
- bot needs two modes: startWhenOrderbookEmpty (lastTrade, lastOwn), startWhenOrderbookNotEmpty (clear, keep)
- ~~if bot starts when orderbook not empty, fetch the last trades from the server and and match the orders with runtime's orders from the bot's shutdown time. The one that is missing is countered.~~
- do getOrderInfo on all orders on the memory.  
- list requirements for config
    - Need to create a config scrap repo for brainstorming

### Bot UI
- Config manipulation
- Real time updates
    - trading status
    - charts (Trade View)
    - other notifications
- Manual CRUD (Create, Delete, ~~Update~~)
- Research if Trade View can be embedded in desktop app, how much
- See Haasbot for reference

### Bot helper
- Restart is moved inside bot (only websocket needs this, rest doesn't).
    - Websocket needs to have cached requests which are matched everytime responds arrives (maybe a map of requestId -> request)
    - In case of disconnect, websocket will resend the cache   
- Read config change during runtime
- API packaging. Move API classes to external lib.
- Embed Sqlite
- Store own trade data to the db
- Support queries from the db to UI's charts
- Trim operation when dataset grows too large
- Counts how many pings and pongs taken within a time window (daily / hourly) to calculate profit

### Non-WS bot

- [x]Create polling to check active trades
- [x]Match active orders with cached orders to see which orders were consumed  
-Exchanges :
    - [x] Okex
    - https://yobit.net/en/api/
    - https://btc-alpha.github.io/api-docs/?python#orderbook-events

### XMM bot
- Expand it to cover other exchanges

### Cryptopanic price tagger
probably not feasible, considering the time of publication doesn't correspond to time of movement
- tags news on price chart

## Support
- create accounts
- do manual 2FA

## Infrastructure
- Prepare a project at GCP
- Put credentials at some shared doc
    - Haasbot creds
    - API keys


## Future Projects
### Arbitrage bot
#### Conditions
- Price tracker
- Optimal path calculator
    - check out https://github.com/manu354/cryptocurrency-arbitrage
- Reserve refill strategy

### Feature Set
- Extracting features from raw data
- Need to list various indicators

#### Conditions
- Market raw data
- News articles


### Prediction / Machine Learning
- Predicting market movement with market indicators

#### Conditions
- Feature set

### News analysis
- Predict the sentiment of crypto news
- Can start from https://github.com/xiamx/awesome-sentiment-analysis

#### Conditions
- Labeled news data

## Other projects
### New blockchain
- study possibilities of forking from Bitcoin

## Staff / Office
- rent
- computers
- smartphones
- sim cards (for different accounts)


## Misc
### Resources
- All relevant crypto / quant resources : https://github.com/EliteQuant/EliteQuant
- Arbitrage bot https://github.com/bitrinjani/r2
- Arbitrage opportunity : https://github.com/manu354/cryptocurrency-arbitrage
- Market making https://github.com/ctubio/Krypto-trading-bot

- Machine learning
    - https://web.stanford.edu/class/msande448/2017/Final/Reports/gr4.pdf
    - https://papers.nips.cc/paper/4910-adaptive-market-making-via-online-learning.pdf
    - http://webee.technion.ac.il/control/info/Projects/Students/2012/Ori%20Gil/Book/Market%20Making%20Article.pdf
    - https://pdfs.semanticscholar.org/88d3/893855c3b54b0acfd436075122319c1dd518.pdf (has a github repo)

### Notes
-  The three components

Order processing costs represent a fee arising from order execution like administrative cost and compensation for the market maker’s time.  

Inventory costs  originate  from  holding  unwanted  risky  securities  in  inventory  by  the
market maker.  

Adverse selection costs exist due to asymmetric information
between the market maker and informed traders.  Informed traders are individuals who are better informed about the expected price movement of the
underlying  security.


- Early correlation

Negative correlation between the bid-ask spread and security price, trading
volume  and  market  capitalization.   

On  the  other  hand,  bid-ask  spread  is
positive correlated with the volatility of the security price.
