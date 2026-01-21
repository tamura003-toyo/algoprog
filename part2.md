# データフレームプログラミング

:::{note}
- Pandasにおける **表データ（行×列）** の基本構造
- Excelの表に似ているが、**プログラムで操作することが前提**
- 行・列のどちらにも **インデックス（名前）** が付いている
:::


## インデックスの考え方（超重要）
DataFrameには2種類のインデックスがある。

- **行インデックス**：各行を識別するためのラベル  
  - 既定では 0,1,2,… の整数
- **列インデックス**：各列（変数名）を識別するラベル  
  - Excelの1行目が自動で使われることが多い

DataFrame操作は、**インデックスで行や列を選ぶ** ことが基本。

## 直接選ぶ：`loc`と`iloc`
### `.loc`：ラベル（名前）で選ぶ
#### 基本形
```python
df.loc[行インデックス, 列インデックス]
```
例
```python
df.loc[4, "日"]    # 行インデックス=4(3行目)の、変数"日"を選ぶ
df.loc[:, "市場名"] # 変数"市場名"の全ての行(:)を選ぶ
df.loc[[1,2,3], ["年","月","日"]] # リストで指定
```
:::{important}
* `loc`は、ラベル（名前）で指定
    * **スライシングでは終点を含む**
:::

### `.iloc`：整数位置で選ぶ
#### 基本形
```python
df.iloc[行位置, 列位置]
```

例

```python
df.iloc[0:3, 0:3]
df.iloc[2:, :4]
```
:::{important}
* `iloc`：0から始まる整数位置
    * **スライシングでは終点を含まない**（← Python共通ルール）
:::

#### loc と iloc の違いまとめ

```{list-table}
:header-rows: 1

* - メソッド
  - 指定方法
  - 終点は含む？
* - loc
  - ラベル（名前）
  - 含む
* - iloc
  - 整数位置
  - 含まない
```

## 列指定の簡略記法
列だけを取り出す場合は、次の書き方も可能。

```python
df["市場名"]          # Series
df[["年","月","日"]]  # DataFrame
```

:::{note}
この方法では **行は指定できない**
:::

### DataFrameのスライシング: 連続した範囲を指定する
- `start : end` という書式
- `df[:, "年":"日"]`：`df`の`年`から`日`までの**連続した列**が選ばれる

:::{important}
- loc：`end` を含む  
- iloc：`end` を含まない  
:::

---

## 表データの構造：横持ちと縦持ち
### 横持ち（wide）
- 人間には見やすい
- 列数が変動しやすく、**プログラムに不向き**

### 縦持ち（long）
- 列数は固定、行が増える
- **データ分析に最適**

### 横持ち・縦持ちの変換
- 横 → 縦：`melt`
- 縦 → 横：`pivot_table`

多くのPandasデータフレーム操作は、**縦持ちデータを想定して実装されている**。

---

## マスク（ブールインデックス）とは
- 各行について  
  **条件を満たすかどうか（True / False）** を並べたもの
- 比較演算子・論理演算子で作られる
- 型は **Series（bool）**

```python
# データフレームの各行について、
# 変数"性別"の値が"男"となる行はTrue、それ以外はFalse
# を判定したSeriesオブジェクトを作る
mask = df["性別"] == "男" 
```

### フィルター：マスクを使って行を選ぶ
```python
df_male = df[mask]
```

- mask が True の行だけが選ばれる。
    - Excelでフィルターをかけたときと同様の操作
- 注意：元の DataFrame とは **別のオブジェクト**(結果がコピーされる)。

#### フィルターの基本3ステップ（暗記）
1. 列を取り出す  
2. 条件からマスクを作る  
3. `df[mask]` で抽出する  

* **いつも同じ順番**


### 論理演算子を使った条件指定
Pandasでは次を使う。

- AND：`&`
- OR：`|`
- NOT：`~`

```python
mask = (points >= 50) & (points < 70)
df_selected = df[mask]
# 論理演算子を含む式を直接使うこともある（こちらが主流）
df_selected = df[(points >= 50) & (points < 70)]
```
* 各条件は **必ず () で括る**

---

## Excelデータ読み込み時の注意
- 政府統計などは **管理コード行** を含むことが多い
- `read_excel` は既定で **1行目を列名として使用**

### skiprows の利用
```python
# 1行目はスキップして、2行目を変数(列名)として採用
pd.read_excel("SSDSE-C.xlsx", skiprows=[0])
```

## 集計技法の基本

:::{important}
- Pandasの集計の多くは **Series に対して行われる**
- DataFrame全体ではなく、  
  **「1列を取り出して考える」** のが基本
:::

```python
s = df["産地名"]   # ← Series
```

### Series
- DataFrameの **1列**
- インデックス（行ラベル）と値の組
- 多くの集計メソッドは Series に定義されている

```python
type(df["市場名"])  # pandas.core.series.Series。通称 "Series"
```

###  value_counts：頻度を数える

基本

```python
df["産地名"].value_counts()
```

- 変数(列)の各値が **何回出現したか** を数える
- 結果は **Series**
- デフォルトでは **出現回数の多い順** に並ぶ

結果のイメージ

```text
北海道    120
長崎県     85
茨城県     60
name: 産地名, dtype: int64
```

#### value_counts のよく使うオプション

昇順に並べる
```python
df["産地名"].value_counts(ascending=True)
```

割合で表示する

```python
df["産地名"].value_counts(normalize=True)
```

- 合計が 1 になる
- **構成比** として解釈できる

### sort_values：値で並べ替える

#### Seriesの並べ替え
```python
df["価格"].sort_values()
```

- 小さい順がデフォルト
- 降順に並べるには、オプション`ascending=False`を指定

```python
df["価格"].sort_values(ascending=False)
```

#### value_counts と sort_values の組み合わせ
- value_counts は **すでに降順**
- ただし、加工後に再ソートしたい場合もある

```python
vc = df["産地名"].value_counts()
vc.sort_values(ascending=True)
```

### インデックスで並べ替える
値ではなく **ラベル順** にしたい場合：

```python
df["産地名"].value_counts().sort_index()
```

### Series集計の典型パターン

:::{important}
```text
① 列を取り出す
② Seriesにする
③ value_counts / sort_values
```
:::

### DataFrameに戻す（必要なとき）

集計結果を DataFrame として扱いたい場合：

```python
vc = df["産地名"].value_counts()
vc_df = vc.reset_index()
```

- 分析・可視化でよく使う形