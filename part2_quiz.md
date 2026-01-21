# Pandasプログラミング: 理解確認問題

各問について、**最も適切なものを1つ選びなさい**。なお、AからCまでの選択肢の中で適切なものが見当たらないときは、「D. この中にはない」を選びなさい。

---

### Q1
Pandasにおける集計の多くが直接行われる対象はどれか。

- A. DataFrame
- B. Series
- C. Index
- D. この中にはない

---

### Q2
`df["産地名"]` の戻り値として正しいものはどれか。

- A. DataFrame
- B. Series
- C. list
- D. この中にはない

---

### Q3
次のうち Series に対して実行できるメソッドはどれか。

- A. `value_counts()`
- B. `read_excel()`
- C. `pivot_table()`
- D. この中にはない

---

### Q4
`value_counts()` の基本的な役割として正しいものはどれか。

- A. 値を合計する
- B. 値を平均する
- C. 値の出現回数を数える
- D. この中にはない

---

### Q5
`value_counts()` の返り値の型はどれか。

- A. DataFrame
- B. Series
- C. list
- D. この中にはない

---

### Q6
`value_counts()` を何も指定せずに実行した場合の並び順はどれか。

- A. インデックス順
- B. 昇順
- C. 出現回数の降順
- D. この中にはない

---

### Q7
出現割合（構成比）を求めたいときの正しい書き方はどれか。

- A. `value_counts(rate=True)`
- B. `value_counts(normalize=True)`
- C. `value_counts(percent=True)`
- D. この中にはない

---

### Q8
`normalize=True` を指定した `value_counts()` の結果として正しいものはどれか。

- A. 合計が 100 になる
- B. 合計が 1 になる
- C. 合計が元の行数になる
- D. この中にはない

---

### Q9
Series を値の大きさで並べ替えるメソッドはどれか。

- A. `sort_index()`
- B. `sort_values()`
- C. `order_by()`
- D. この中にはない

---

### Q10
`sort_values()` のデフォルトの並び順はどれか。

- A. 昇順
- B. 降順
- C. ランダム
- D. この中にはない

---

### Q11
値を大きい順に並べ替えたい場合の正しい指定はどれか。

- A. `sort_values(desc=True)`
- B. `sort_values(reverse=True)`
- C. `sort_values(ascending=False)`
- D. この中にはない

---

### Q12
インデックス（ラベル）順に並べ替えたい場合に使うメソッドはどれか。

- A. `sort_values()`
- B. `sort_index()`
- C. `reset_index()`
- D. この中にはない

---

### Q13
次の処理の正しい説明はどれか。

```python
df["産地名"].value_counts().sort_index()
```

- A. 出現回数の多い順に並べる
- B. 出現回数を昇順に並べる
- C. ラベル順に並べ替える
- D. この中にはない

---

### Q14
Series集計の典型的な流れとして正しいものはどれか。

- A. DataFrame → groupby → 集計
- B. 列抽出 → Series → 集計
- C. 行抽出 → DataFrame → 集計
- D. この中にはない

---

### Q15
`value_counts()` の結果を DataFrame として扱いたいときに使う操作はどれか。

- A. `to_frame()`
- B. `reset_index()`
- C. `astype()`
- D. この中にはない

---

### Q16
Series集計が特に有効なのはどの段階か。

- A. モデル構築
- B. データ取得
- C. 探索的データ分析（EDA）
- D. この中にはない

---

### Q17
次のうち、`value_counts()` を使うのに**最も適している**列はどれか。

- A. 連続的な価格データ
- B. カテゴリ変数（産地名など）
- C. 日付データ
- D. この中にはない

---

### Q18
`sort_values()` と `value_counts()` の関係として正しいものはどれか。

- A. value_counts は sort_values を内部で使っている
- B. sort_values は value_counts の別名である
- C. 両者は無関係である
- D. この中にはない

---

### Q19
次の説明のうち正しいものはどれか。

- A. 集計は必ず DataFrame で行う
- B. Series は集計に向いていない
- C. 集計結果は Series になることが多い
- D. この中にはない

