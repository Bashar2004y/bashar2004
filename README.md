# bashar2004
import talib
import pandas as pd

def get_support_resistance(df, period=14):
    """
    يحدد مستويات الدعم والمقاومة باستخدام المتوسط ​​المتحرك البسيط.

    Args:
        df: إطار البيانات الذي يحتوي على بيانات الأسعار.
        period: فترة المتوسط ​​المتحرك البسيط.

    Returns:
        مؤشر يرسم خطوط الدعم والمقاومة.
    """

    sma = talib.SMA(df['Close'], period)

    support = df['Close'] - sma
    resistance = df['Close'] + sma

    return pd.DataFrame({
        'support': support,
        'resistance': resistance
    })

def main():
    """
    يرسم مستويات الدعم والمقاومة على الرسم البياني.
    """

    df = pd.read_csv('EURUSD.csv', index_col='Date')

    support_resistance = get_support_resistance(df, period=14)

    support_resistance.plot(figsize=(12, 8))

if __name__ == '__main__':
    main()
