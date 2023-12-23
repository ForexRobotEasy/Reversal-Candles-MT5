# Reversal Candles MT5 ReadMe

This repository contains the code for the Reversal Candles MT5 indicator. This indicator is designed to identify potential reversal points in the market based on the color of the last closed candle. It is developed by the Forex Robot Easy Team and can be found on their website [forexroboteasy.com](https://forexroboteasy.com).

## Indicator Initialization

The indicator is initialized in the `OnInit()` function. In this function, the indicator buffers are mapped, indicator line labels are set, and indicator buffers direction is defined.

```c++
// Indicator buffers mapping
SetIndexBuffer(0, UpArrowBuffer, INDICATOR_DATA);
SetIndexBuffer(1, DownArrowBuffer, INDICATOR_DATA);

// Set indicator line labels
IndicatorSetString(INDICATOR_SHORTNAME, 'Reversal Candles MT5');

// Indicator buffers direction
SetIndexStyle(0, DRAW_ARROW);
SetIndexArrow(0, SYMBOL_ARROWUP);
SetIndexStyle(1, DRAW_ARROW);
SetIndexArrow(1, SYMBOL_ARROWDOWN);
```

Additionally, there is customization for user-preferred darker color. If the buy color is darker, the indicator digits are set to 1, otherwise, they are set to 0.

## Indicator Calculation

The indicator calculation is performed in the `OnCalculate()` function. In this function, signals are calculated based on the color of the last closed candle.

```c++
// Calculate signals based on color of the last closed candle
for (int i = prev_calculated; i < rates_total; i++)
{
    if (close[i] > open[i])
    {
        // Buy signal
        if (buyColor != CLR_NONE)
        {
            UpArrowBuffer[i] = low[i] - Point; // Display up arrow below the darker colored candle
            DownArrowBuffer[i] = 0;
        }
    }
    else if (close[i] < open[i])
    {
        // Sell signal
        if (buyColor != CLR_NONE)
        {
            UpArrowBuffer[i] = 0;
            DownArrowBuffer[i] = high[i] + Point; // Paint down arrow above the darker colored candle
        }
    }
    else
    {
        // No signal
        UpArrowBuffer[i] = 0;
        DownArrowBuffer[i] = 0;
    }
}
```

If the last closed candle is bullish (close > open), a buy signal is generated and an up arrow is displayed below the darker colored candle. If the last closed candle is bearish (close < open), a sell signal is generated and a down arrow is painted above the darker colored candle. If the last closed candle is neutral (close = open), no signal is generated.

## Product Description

**Reversal Candles MT5** is a predictive forex software tool developed by the Forex Robot Easy Team. This indicator is designed to identify potential reversal points in the market based on the color of the last closed candle. It is a valuable tool for traders who want to spot possible trend reversals and make informed trading decisions.

With Reversal Candles MT5, you can:

- Identify potential reversal points in the market
- Receive clear buy and sell signals based on candle color
- Customize the indicator to match your preferred darker color

Please note that ForexRobotEasy is not the official developer of this product. We are showcasing sample code that can work as described in this product. To find the official developer of Reversal Candles MT5 and access detailed reviews and trading results, please visit the [official product page](https://forexroboteasy.com/forex-robot-review/reversal-candles-mt5-review-predictive-forex-software-tool/). For any technical support or inquiries, please refer to the official developer through the MQL5 platform.
