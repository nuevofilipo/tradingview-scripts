//@version=5
indicator(title="Moving Average", shorttitle="MA", overlay=true, timeframe="", timeframe_gaps=true)
len = input.int(9, minval=1, title="Length")
src = input(close, title="Source")

//change the number you multilpy it with in order to move it upward
src1 = src * 1.03

src2 = input.int(title="Offset top/bottom", defval=0, minval=-80, maxval=80)

src3 = src*(1+(src2/80))

offset = input.int(title="Offset", defval=0, minval=-500, maxval=500)
out = ta.sma(src3, len)
plot(out, color=color.blue, title="MA", offset=offset)

ma(source, length, type) =>
    switch type
        "SMA" => ta.sma(source, length)
        "EMA" => ta.ema(source, length)
        "SMMA (RMA)" => ta.rma(source, length)
        "WMA" => ta.wma(source, length)
        "VWMA" => ta.vwma(source, length)

typeMA = input.string(title = "Method", defval = "SMA", options=["SMA", "EMA", "SMMA (RMA)", "WMA", "VWMA"], group="Smoothing")
smoothingLength = input.int(title = "Length", defval = 5, minval = 1, maxval = 100, group="Smoothing")

smoothingLine = ma(out, smoothingLength, typeMA)
plot(smoothingLine, title="Smoothing Line", color=#f37f20, offset=offset, display=display.none)
