//@version=5
indicator(title="EMA多均线", overlay=true, timeframe="", timeframe_gaps=true)
//设定均线
len1 = input.int(5, minval=1, title="参数1")
len2 = input.int(30, minval=1, title="参数2")
len3 = input.int(77, minval=1, title="参数3")
len4 = input.int(84, minval=1, title="参数4")
len5 = input.int(144, minval=1, title="参数5")
len6 = input.int(169, minval=1, title="参数6")
len7 = input.int(200, minval=1, title="参数7")

//调用均线
src = input(close, title="Source")
out1 = ta.ema(src, len1)
out2 = ta.ema(src, len2)
out3 = ta.ema(src, len3)
out4 = ta.ema(src, len4)
out5 = ta.ema(src, len5)
out6 = ta.ema(src, len6)
out7 = ta.ema(src, len7)

//显示均线
plot(out1, title="EMA1", color=color.blue)
plot(out2, title="EMA2", color=color.blue)
plot(out3, title="EMA3", color=color.blue)
plot(out4, title="EMA4", color=color.blue)
plot(out5, title="EMA5", color=color.blue)
plot(out6, title="EMA6", color=color.blue)
plot(out7, title="EMA7", color=color.blue)

// 求均线
ema5 = ta.ema(close, 5)// Simple Moving Average
ema77 = ta.ema(close, 77)// Simple Moving Average


// 金叉死叉信号
gold = ta.crossover(ema5, ema77) // ema12 > ma26 and ma12[1] < ma26[1] 等价于 ta.crossover(ma12, ma26)
dead = ta.crossunder(ema5, ema77) // ema12 < ma26 and ma12[1] > ma26[1] 等价于 ta.crossunder(ma12, ma26)

// 金叉死叉信号绘制
plotchar(gold, char="▲", location=location.belowbar, color=color.green, size=size.tiny)
plotchar(dead, char="▼", location=location.abovebar, color=color.red, size=size.tiny)

//画均线
len8=plot(ema5,color=color.red)
len9=plot(ema77,color=color.blue)

//绘制背景
_color=ema5>ema77?color.new(#ff0000,50):color.new(#00ff00,50)
fill(len8,len9,color=_color,transp=50)
