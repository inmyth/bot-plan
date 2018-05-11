
## Projects Outlines
### Core
- Desktop App
    - bot runs from desktop directly to exchanges. We do NOT want to store or handle anyones' secret keys, api keys, passwords.
    - any data will be stored locally on Sqlite.
    - has graceful restart. Right now the bot uses systemd to capture kill signal and restart it.
    - interface - core integration
- User Interface
    - Minimalist no bulshit interface
    - UI will only manipulate a json file which is read by the bot during runtime. The bot will be able to run without UI.
- Expansion to other exchanges
    - in order : Huobi, OkEX, Binance
- Profit calculation

#### DB models
- txs
    - bot can restart trades from user's own last filled order (default = last market tick)

### Optimization
- Adaptive strategy : Machine learning, prediction model.
    - Knowing which direction the market will go can help the bot make bigger profit.
    - Eg. Big buy volume, small sell volume -> market moves to sell -> reprice sell orders at wider level

- Cypto flow map at big exchanges
    - BTC flowing in = altcoins are going to go up
    - Altcoins moving in = altcoins going to go down. The only reason altcoins are entering an exchange is to be sold.
    - Need to observe exchanges' cold wallets and hot wallets.

- Arbitrage
    - buying and selling at different exchanges

### Arbitrage
- Direct
    - fund is transferred directly for each tx through blockchain process.
    - risk is determined by the amount of time the fund is processed
- Reserves
    - maintain fund reserves / pools at different exchanges. Buy and sell orders will draw from the respective pools.
    - need to figure out refill window.

#### Some resources
- Machine learning
    - https://web.stanford.edu/class/msande448/2017/Final/Reports/gr4.pdf
    - https://papers.nips.cc/paper/4910-adaptive-market-making-via-online-learning.pdf
    - http://webee.technion.ac.il/control/info/Projects/Students/2012/Ori%20Gil/Book/Market%20Making%20Article.pdf
    - https://pdfs.semanticscholar.org/88d3/893855c3b54b0acfd436075122319c1dd518.pdf (has a github repo)
