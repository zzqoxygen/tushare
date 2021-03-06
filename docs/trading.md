.. highlightlang:: python

交易数据获取
=========
*交易类数据*提供股票的交易行情数据，通过简单的接口调用可获取相应的DataFrame格式数据，主要包括以下类别：

- 历史行情数据
- 实时行情数据
- 历史分笔数据
- 实时分笔数据

历史行情数据
------------
获取个股历史交易数据（包括均线数据）

    In[1]:import tushare.stock.trading as td

	In[2]:td.get_hist_data('600848') #一次性获取全部数据

结果显示：

> 日期 ，开盘价， 最高价， 收盘价， 最低价， 成交量， 价格变动 ，涨跌幅，5日均价，10日均价，20日均价，5日均量，10日均量，20日均量，换手率

    			 open    high   close     low     amount    p_change  ma5 \
	date                                                                     
	2012-01-11   6.880   7.380   7.060   6.880   14129.96     2.62   7.060   
	2012-01-12   7.050   7.100   6.980   6.900    7895.19    -1.13   7.020   
	2012-01-13   6.950   7.000   6.700   6.690    6611.87    -4.01   6.913   
	2012-01-16   6.680   6.750   6.510   6.480    2941.63    -2.84   6.813   
	2012-01-17   6.660   6.880   6.860   6.460    8642.57     5.38   6.822   
	2012-01-18   7.000   7.300   6.890   6.880   13075.40     0.44   6.788   
	2012-01-19   6.690   6.950   6.890   6.680    6117.32     0.00   6.770   
	2012-01-20   6.870   7.080   7.010   6.870    6813.09     1.74   6.832 

				 ma10    ma20      v_ma5     v_ma10     v_ma20     turnover  
	date                                                                  
	2012-01-11   7.060   7.060   14129.96   14129.96   14129.96     0.48  
	2012-01-12   7.020   7.020   11012.58   11012.58   11012.58     0.27  
	2012-01-13   6.913   6.913    9545.67    9545.67    9545.67     0.23  
	2012-01-16   6.813   6.813    7894.66    7894.66    7894.66     0.10  
	2012-01-17   6.822   6.822    8044.24    8044.24    8044.24     0.30  
	2012-01-18   6.833   6.833    7833.33    8882.77    8882.77     0.45  
	2012-01-19   6.841   6.841    7477.76    8487.71    8487.71     0.21  
	2012-01-20   6.863   6.863    7518.00    8278.38    8278.38     0.23  

设定历史数据的时间：      
	
	In [5]: td.get_hist_data('600848','2015-01-05','2015-01-09')
	Out[5]:
				open    high   close     low    amount p_change     ma5    ma10 \  
	date                                                                            
	2015-01-05  11.160  11.390  11.260  10.890  46383.57     1.26  11.156  11.212   
	2015-01-06  11.130  11.660  11.610  11.030  59199.93     3.11  11.182  11.155   
	2015-01-07  11.580  11.990  11.920  11.480  86681.38     2.67  11.366  11.251   
	2015-01-08  11.700  11.920  11.670  11.640  56845.71    -2.10  11.516  11.349   
	2015-01-09  11.680  11.710  11.230  11.190  44851.56    -3.77  11.538  11.363   
	 			ma20     v_ma5    v_ma10     v_ma20 	 turnover  
	date                                                        
	2015-01-05  11.198  58648.75  68429.87   97141.81     1.59  
	2015-01-06  11.382  54854.38  63401.05   98686.98     2.03  
	2015-01-07  11.543  55049.74  61628.07  103010.58     2.97  
	2015-01-08  11.647  57268.99  61376.00  105823.50     1.95  
	2015-01-09  11.682  58792.43  60665.93  107924.27     1.54  


实时行情数据
--------------
一次性获取当前交易所有股票的行情数据（如果是节假日，即为上一交易日，结果显示速度取决于网速）

	In[4]:import tushare.stock.trading as td

	In[5]:td.get_today_all()


结果显示：

> 代码，名称，涨跌幅，现价，开盘价，最高价，最低价，最日收盘价，成交量，换手率

		  code    name     changepercent  trade   open   high    low  settlement \  
	0     002738  中矿资源         10.023  19.32  19.32  19.32  19.32       17.56   
	1     300410  正业科技         10.022  25.03  25.03  25.03  25.03       22.75   
	2     002736  国信证券         10.013  16.37  16.37  16.37  16.37       14.88   
	3     300412  迦南科技         10.010  31.54  31.54  31.54  31.54       28.67   
	4     300411  金盾股份         10.007  29.68  29.68  29.68  29.68       26.98   
	5     603636  南威软件         10.006  38.15  38.15  38.15  38.15       34.68   
	6     002664  信质电机         10.004  30.68  29.00  30.68  28.30       27.89   
	7     300367  东方网力         10.004  86.76  78.00  86.76  77.87       78.87   
	8     601299  中国北车         10.000  11.44  11.44  11.44  11.29       10.40   
	9     601880   大连港         10.000   5.72   5.34   5.72   5.22        5.20   
	10    000856  冀东装备         10.000   8.91   8.18   8.91   8.18        8.10  
			volume  	 turnoverratio  
	0        375100        1.25033  
	1         85800        0.57200  
	2       1058925        0.08824  
	3         69400        0.51791  
	4        252220        1.26110  
	5       1374630        5.49852  
	6       6448748        9.32700  
	7       2025030        6.88669  
	8     433453523        4.28056  
	9     323469835        9.61735  
	10     25768152       19.51090  


历史分笔数据
-----------


    In [1]: import tushare.stock.trading as td
	In [2]: df = td.get_tick_data('600848','2014-01-09')
	In [3]: df.head(10)

结果显示：

>成交时间、成交价格、价格变动，成交手、成交金额(元)，买卖类型

    Out[3]: 
     	 time  		price change  volume  amount  type
	0    15:00:00   6.05     --       8    4840   卖盘
	1    14:59:55   6.05     --      50   30250   卖盘
	2    14:59:35   6.05     --      20   12100   卖盘
	3    14:59:30   6.05  -0.01     165   99825   卖盘
	4    14:59:20   6.06   0.01       4    2424   买盘
	5    14:59:05   6.05  -0.01       2    1210   卖盘
	6    14:58:55   6.06     --       4    2424   买盘
	7    14:58:45   6.06     --       2    1212   买盘
	8    14:58:35   6.06   0.01       2    1212   买盘
	9    14:58:25   6.05  -0.01      20   12100   卖盘
	10   14:58:05   6.06     --       5    3030   买盘

实时分笔数据
------------

	In [1]:import tushare.stock.trading as td
	In [2]:td.get_realtime_quotes('000581') #Single stock symbol

结果显示：

	0：name，股票名字
	1：open，今日开盘价
	2：pre_close，昨日收盘价
	3：price，当前价格
	4：high，今日最高价
	5：low，今日最低价
	6：bid，竞买价，即“买一”报价
	7：ask，竞卖价，即“卖一”报价
	8：volumn，成交量 maybe you need do volumn/100
	9：amount，成交金额（元 CNY）
	10：b1_v，委买一（笔数 bid volume）
	11：b1_p，委买一（价格 bid price）
	12：b2_v，“买二”
	13：b2_p，“买二”
	14：b3_v，“买三”
	15：b3_p，“买三”
	16：b4_v，“买四”
	17：b4_p，“买四”
	18：b5_v，“买五”
	19：b5_p，“买五”
	20：a1_v，委卖一（笔数 ask volume）
	21：a1_p，委卖一（价格 ask price）
	...
	30：date，日期；
	31：time，时间；

	Out[2]:
	  name      open pre_close  price   high    low    bid    ask    volume  \  
	0 威孚高科  31.50     31.38  30.25  31.63  30.08  30.25  30.27  10148935 
	  amount      ...        a2_p a3_v   a3_p a4_v   a4_p a5_v   a5_p  \
	0 314310351.22      ...       30.29    2  30.30  234  30.31   19  30.32 \
	  date      	time     code  
	0  2015-01-14  14:30:46  000581  
	  
请求多个股票方法（一次最好不要超过30个）：
    
	In [3]:td.get_realtime_quotes(['600848','000980','000981']) #symbols from a list
	In [4]:td.get_realtime_quotes(df['code'].tail(10)) #from a Series

