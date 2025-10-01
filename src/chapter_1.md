# 第1章 ファイル入出力

これは mdBook + KaTeX の最小サンプルです。

インライン数式の例：$y = mx + b$。

ブロック数式の例：
$$
\mathrm{Var}(X) = \mathbb{E}\!\left[(X - \mathbb{E}[X])^2\right]
$$

```python
import pandas as pd

df = pd.read_csv("a.csv")
if pd.isnan(df):
    print("this is illegal")

```

## 数式ブロック

$$
\begin{align}
a &= 1 \\
c+d &= a
\end{align}
$$

$$
\begin{equation}
X - Y = Z
\end{equation}
$$

となります。ここで、$A=\{a_i, b_i, c_i\, \int_{0}^{10}f(a)da\}$です。
