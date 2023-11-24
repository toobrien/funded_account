# DESCRIPTION

`prop.py` is a simulation for funded account trading. The default parameters are based on index futures traders participating in a standard funded account program modelled after TradeDay, a popular "prop firm". The traders are assumed to use a consistent strategy on stock index futures.

The program has two modes `funded` and `survival`, which are arguments supplied at the command line:

- `python prop.py funded`

- `python prop.py survival`

`funded` simulates a number of accounts, measuring the number of accounts that pass the trial period, and what fees they incur during the process. The simulation ends when the account either reaches the profit target (pass) or the maximum allowed drawdown (fail). `survival` goes a step further, measuring the amount of gross profit a trader accrues over a period of time.

Both modes assume random trading, which is appropriate for most new traders who are attracted to these firms. They are governed by a set of parameters common to most funded account "prop firms", which are:

- `N_TRIALS`:         the number of accounts to simulate.
- `PT_VALUE`:         the point value of the future being traded (default: 20, NQ).
- `TP`:               the number of points for the trader's profit target (default: 5).
- `SL`:               the number of points for the trader's stop loss (default: 5).
- `P_WIN`:            the probability of a trader winning (default: random, based on `TP` and `SL`).
- `P_LOSE`:           same as `P_WIN`.
- `COMMISSION`:       the round-turn commission for one contract (default: based on the Ninjatrader brokerage).
- `AMT_WIN`:          the dollar amount won in one winning trade (automatically calculated).
- `AMT_LOSE`:         the dollar amount lost in one losing trade (automatically calculated).
- `ACCT_SIZE`:        the size (in dollars) of the funded account, in dollars.
- `BLOWN`:            the maximum drawdown before the account is closed.
- `PASSED`:           the profit target that, when reached, allows the trader to begin withdrawing their winnings.
- `TRADES_PER_MONTH`: the number of trades that the trader takes per month (default: 100 or 5 per day).
- `MAX_TRADES`:       the maximum number of trades to run for each account. Effectively, this parameter determines the length of the simulation (default: 36 months)
- `MONTHLY_FEE`:      the dollar amount charged for the funded account (default: $165).
- `WITHDRAWAL`:       for the `survival` simulation, the amount a trader withdraws each month (default: $811.08, the worldwide median monthly income).
- `PROFIT_SHARE`:     the proportion of profits kept by the trader (default: 0.9 or 90%).

Traders can assume non-random results by replacing `P_WIN` and `P_LOSE` with their own assumed probability of winning and losing a trade.

# RESULTS

The default parameters are modelled after TradeDay's $50,000 funded account. The trader is challenged to meet a $2,500 profit target while avoiding a $2,000 trailing drawdown, which does not trail higher than $50,000. This is accounted for. Some small details of the challenge are not accounted for, such as the 10 day minimum and the per-day profit limits. Furthermore, the `funding` mode does not assume that the trader pays the monthly account fee out of their winnings, while the `survival` mode does.

Running the `funding` simulation with the default parameters (10,000 accounts, $2,500 profit target, $2,000 trailing drawdown, 5 point profit target and stop loss, etc.) results in a pass rate of around 1.8%, with the average pass requiring around 3 months, incurring around $425 in account payments.

The `survival` simulation--which uses the same parameters as the `funding` simulation, following 10,000 accounts over a maximum 36 month period--results in around 60-70 passes. Around 95-98% of this small group of traders make at least one withdrawal of the worldwide monthly median salary--and, on average, only one. The average gross profit--after fees and profit sharing, is around $1,300-$1,400. The best performing account generally survives between 7 and 9 months before hitting the maximum drawdown. Approximately half of the accounts are able to make one withdrawal, and around 80% of the accounts are able to make two withdrawals.

# FINAL THOUGHTS

Many traders are drawn to funded account "prop firms" for apparently cheap access to an attractive amount of capital. Some of these have a desire to make a living from these accounts, and are eager to bypass time spent practicing trading paper accounts or with small amounts of their own capital. They want to make "real money" trading products that retail "educators" market to them, such as stock index futures.

However, it is well known that most traders are not better a coin flip when it comes to picking the direction of stock indices. Accounts from those rare successes to emerge from the world of retail day trading commonly mention an unprofitable first few years. Without a real edge, one should expect random results from their first forays into the markets. With this in mind, using funded accounts is an expensive way to get practice. The fees for "renting" these accounts are generally on the order of 30-100 basis points per month--steep enough--and almost certainly much higher when compared to the trader's actual risk capital. A trader who has only several thousand dollars will be paying potentially hundreds of basis points per month on their risk capital to participate in a funded account program.

What can they expect for this trouble? The lucky ones will be able to make an extremely modest monthly salary for 1-2 months. 95-99% will likely not even be able to make one withdrawal.