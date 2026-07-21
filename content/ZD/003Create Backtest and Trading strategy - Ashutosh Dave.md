## Day 2: The finer details: Working with data, formulating and backtesting a trading strategy

- Discuss various strategy paradigms.
- Learn about the strategy workflow.
- Take a short detour about data we can use.
- Explore data sources.
- Formulate a strategy and backtest it.

https://www.youtube.com/live/WiiQBg71Mz4?feature=shared&t=2706

- get the idea
- convert into rules
- backtest 
- paper trade/demo
- live trade

![[Pasted image 20231106054340.png]]
1. Quant research
	1. we'll research  using data
2. Alpha seeking
	1. this is **why** part in our idea
	2. ![[Pasted image 20231106054433.png]]
	3. how to generate data? ![[Pasted image 20231106054536.png]]
3. Universe selection
	1. ![[Pasted image 20231106054605.png]]
	2. ![[Pasted image 20231106054642.png]]
4. what are our entry and exit rules
	1. ![[Pasted image 20231106054706.png]]
5. convert the entry/exit logic into logic blocks
	1. ![[Pasted image 20231106054733.png]]
6. backtest
	1. ![[Pasted image 20231106054758.png]]


# Sample trading strategy
![[Pasted image 20231106054849.png]]

![[Pasted image 20231106055002.png]]

we can combine multiple alpha
![[Pasted image 20231106055033.png]]
this data they've used is fundamentals stock data.

Second Alpha being used is RSI
![[Pasted image 20231106061642.png]]![[Pasted image 20231106061824.png]]

![[Pasted image 20231106061843.png]]


talib is RSI Library

![[Pasted image 20231106062019.png]]

![[Pasted image 20231106062443.png]]
vizualization is not explained
![[Pasted image 20231106062629.png]]
![[Pasted image 20231106062542.png]]


![[Pasted image 20231106062748.png]]

![[Pasted image 20231106062812.png]]
![[Pasted image 20231106062828.png]]

#  optimization
change the RSI to 50
![[Pasted image 20231106062954.png]]


![[Pasted image 20231106063047.png]]


this data does not have brokerage
slippage cost - cost lost in executing trade

- [x] https://www.youtube.com/live/WiiQBg71Mz4?feature=shared&t=3121 paused

![[Pasted image 20231106215116.png]]


inverted hammer
inverted hanging man
bearish engulfing
harami candles
[[backtesting library]]
