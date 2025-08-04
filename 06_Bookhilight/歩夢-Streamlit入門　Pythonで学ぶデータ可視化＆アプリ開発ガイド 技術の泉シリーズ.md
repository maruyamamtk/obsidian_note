---
kindle-sync:
  bookId: '60903'
  title: Streamlit入門　Pythonで学ぶデータ可視化＆アプリ開発ガイド 技術の泉シリーズ
  author: 山口 歩夢
  asin: B0DP6SSQ67
  lastAnnotatedDate: '2025-02-01'
  bookImageUrl: 'https://m.media-amazon.com/images/I/81AWPLGUd6L._SY160.jpg'
  highlightsCount: 19
---
# Streamlit入門　Pythonで学ぶデータ可視化＆アプリ開発ガイド 技術の泉シリーズ
## Metadata
* Author: [山口 歩夢](https://www.amazon.comundefined)
* ASIN: B0DP6SSQ67
* Reference: https://www.amazon.com/dp/B0DP6SSQ67
* [Kindle link](kindle://book?action=open&asin=B0DP6SSQ67)

## Highlights
Streamlitで開発したアプリケーションは、「streamlit run *.py」コマンドを実行すると動きます。「streamlit run」コマンドを実行すると、コンピューターはPythonを使用してStreamlitサーバーを起動します。 — location: [181](kindle://book?action=open&asin=B0DP6SSQ67&location=181) ^ref-62427

---
以下のコマンドで作成したコードを実行します。 — location: [288](kindle://book?action=open&asin=B0DP6SSQ67&location=288) ^ref-48248

環境変数が設定されていない場合は、以下のコマンドを実行する必要がある
python -m streamlit run .\streamlit_app.py

---
こちらのアプリケーションのボタンをクリックしてみると、「0」に「1」が足されます。(図2.14)しかし、何度ボタンをクリックしても「1」から「2」になることはありません。理由は、第1章の「Python スクリプト実行の仕組み」にて解説した通り、ボタンがクリックされる度にPythonスクリプトが最初から実行され、「count」変数が「0」に初期化された上で「1」が足されているためです。 — location: [484](kindle://book?action=open&asin=B0DP6SSQ67&location=484) ^ref-64271

---
Session Stateを更新したときに、最初にコールバックに指定しているPythonの関数が実行され、次にアプリケーション全体が実行されるという順で処理が走ります。 — location: [505](kindle://book?action=open&asin=B0DP6SSQ67&location=505) ^ref-10981

---
「st.fragment」について簡単に解説します。先程述べた通り、Streamlitはアプリケーションの操作が実施される度に、Pythonスクリプトを全て再実行します。しかし、「st.fragment」を使うことで、アプリケーションの操作がされる度にPythonスクリプト全体を更新するのではなく、fragment内部のスクリプトだけを再実行するように実装することができます。 — location: [523](kindle://book?action=open&asin=B0DP6SSQ67&location=523) ^ref-19808

---
Streamlitでは、安定性の低い機能には「st.experimental_」が先頭に付く命名規則があります。 — location: [547](kindle://book?action=open&asin=B0DP6SSQ67&location=547) ^ref-22489

---
キャッシュの処理の流れを簡単に説明します。Streamlitでキャッシュ機能を使用するには、「st.cache_data」または「st.cache_resource」を使用します。これらを関数の上部に付与することで、関数が呼び出されるたびに、「st.cache_data」や「st.cache_resource」が関数の引数や関数の中身をチェックしてくれます。 — location: [556](kindle://book?action=open&asin=B0DP6SSQ67&location=556) ^ref-28201

---
処理の流れとしては、「st.cache_data」と似ていますが、ひとつ大きな違いがあります。「st.cache_data」は関数の戻り値のコピーを作成してキャッシュに保存するのに対し、「st.cache_resource」はオブジェクトそのもの、つまりDBの接続情報をそのままキャッシュに保存します。 — location: [578](kindle://book?action=open&asin=B0DP6SSQ67&location=578) ^ref-64616

---
公式ドキュメント 6 にて推奨されているユースケースや戻り値の表が掲載されているのですが、ほとんどの場合が「st.cache_data」を使用することが推奨されていることがわかります。「 — location: [587](kindle://book?action=open&asin=B0DP6SSQ67&location=587) ^ref-32524

---
10: @st.cache_data(hash_funcs={MyCustomClass: hash_func}) 11: def multiply_score(obj: MyCustomClass, multiplier: int) -> int: 12: return obj.my_score * multiplier — location: [638](kindle://book?action=open&asin=B0DP6SSQ67&location=638) ^ref-61346

---
Markdown形式でテキストを表示します。Streamlitにはテキスト表示系の関数が多く用意されていますが、こちらの関数で多くの範囲をカバーできるため、非常に便利です。(図3.4) — location: [729](kindle://book?action=open&asin=B0DP6SSQ67&location=729) ^ref-33199

---
3.1.5　st.write 　テキストやグラフ、画像など、さまざまな種類のオブジェクトを表示します。この関数は、テキストに限らず、グラフや画像など様々なオブジェクトを出力することができます。 — location: [749](kindle://book?action=open&asin=B0DP6SSQ67&location=749) ^ref-16181

---
また、オブジェクトを複数同時に渡しても、全て出力してくれます。 — location: [751](kindle://book?action=open&asin=B0DP6SSQ67&location=751) ^ref-61196

---
コードとコードの出力結果を同時に表示します。 — location: [795](kindle://book?action=open&asin=B0DP6SSQ67&location=795) ^ref-56726

---
with表記法の中に、ポップオーバーを展開したときに表示したいものを記述しておくことで活用できます。( — location: [964](kindle://book?action=open&asin=B0DP6SSQ67&location=964) ^ref-6328

---
アプリケーション使用者のデータエディターの行の追加・削除の可不可を指定します。「 — location: [1512](kindle://book?action=open&asin=B0DP6SSQ67&location=1512) ^ref-12629

---
カラムの編集の可不可を設定します。 — location: [1516](kindle://book?action=open&asin=B0DP6SSQ67&location=1516) ^ref-37515

---
関数を指定することでボタンをクリックしたときに、その関数を呼び出すことができます。 — location: [2100](kindle://book?action=open&asin=B0DP6SSQ67&location=2100) ^ref-52657

---
12: columns = st.columns(4) — location: [3286](kindle://book?action=open&asin=B0DP6SSQ67&location=3286) ^ref-48350

columns関数の返り値を1オブジェクトにして指定することもできる

---
