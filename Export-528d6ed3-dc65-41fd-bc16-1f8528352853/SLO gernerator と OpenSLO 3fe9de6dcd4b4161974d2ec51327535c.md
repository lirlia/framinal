# SLO gernerator  と OpenSLO

レベル: レベル1 聞いたことがある

SLOについての考え方の整理と、SLOのIaC、すなわちSLOの宣言文書からSLOの計装や可視化などを自動生成するためのツールおよび標準化、の動向についての紹介でした。

googleが主導しているSLO Generatorという実装とOpenSLOというフォーマットが積極的な動きを見せていて、フォーマットはOpenSLOが標準になりそうな動きらしいです。

SLOについてYAMLで宣言すると、PrometheusやDatadogが設定されてSLOが計測可能になる、という便利な世界が実現しつつあるようなので、引き続きウォッチしていきたいです。

[SLO策定のIaC化によるSREの加速 | CloudNative Days Tokyo 2022](https://event.cloudnativedays.jp/cndt2022/talks/1580)

エラーバジェットをちゃんとトラックするという動き

![Untitled](SLO%20gernerator%20%E3%81%A8%20OpenSLO%203fe9de6dcd4b4161974d2ec51327535c/Untitled.png)

CUJ = Critical User Journey

![Untitled](SLO%20gernerator%20%E3%81%A8%20OpenSLO%203fe9de6dcd4b4161974d2ec51327535c/Untitled%201.png)

![Untitled](SLO%20gernerator%20%E3%81%A8%20OpenSLO%203fe9de6dcd4b4161974d2ec51327535c/Untitled%202.png)

![Untitled](SLO%20gernerator%20%E3%81%A8%20OpenSLO%203fe9de6dcd4b4161974d2ec51327535c/Untitled%203.png)

![Untitled](SLO%20gernerator%20%E3%81%A8%20OpenSLO%203fe9de6dcd4b4161974d2ec51327535c/Untitled%204.png)

この例で言うと、ユーザのプロフィールを参照する機能を分解すると

- APIリクエスト
- アセット取得
- 画像ダウンロード

とある。画像壊れてたり、CDNはこっちでハンドリングできないので、APIリクエストが一番大事と言うことになる。このレベルでCUJを洗い出す

![Untitled](SLO%20gernerator%20%E3%81%A8%20OpenSLO%203fe9de6dcd4b4161974d2ec51327535c/Untitled%205.png)

SLI : サービス レベル指標

![Untitled](SLO%20gernerator%20%E3%81%A8%20OpenSLO%203fe9de6dcd4b4161974d2ec51327535c/Untitled%206.png)

SLIを決めて、期間を決めてSLOを設定する。

![Untitled](SLO%20gernerator%20%E3%81%A8%20OpenSLO%203fe9de6dcd4b4161974d2ec51327535c/Untitled%207.png)

![Untitled](SLO%20gernerator%20%E3%81%A8%20OpenSLO%203fe9de6dcd4b4161974d2ec51327535c/Untitled%208.png)

![Untitled](SLO%20gernerator%20%E3%81%A8%20OpenSLO%203fe9de6dcd4b4161974d2ec51327535c/Untitled%209.png)

エラーバジェットへの変換をすると見やすい

![Untitled](SLO%20gernerator%20%E3%81%A8%20OpenSLO%203fe9de6dcd4b4161974d2ec51327535c/Untitled%2010.png)

減ってる時にアラートを出す

![Untitled](SLO%20gernerator%20%E3%81%A8%20OpenSLO%203fe9de6dcd4b4161974d2ec51327535c/Untitled%2011.png)

28d でエラーバジェットを消費するようにすることをバーンレート1という。

これが2になってたらアラートを出す。

![Untitled](SLO%20gernerator%20%E3%81%A8%20OpenSLO%203fe9de6dcd4b4161974d2ec51327535c/Untitled%2012.png)

![Untitled](SLO%20gernerator%20%E3%81%A8%20OpenSLO%203fe9de6dcd4b4161974d2ec51327535c/Untitled%2013.png)

これを繰り返す

- SLI / SLO はこれ
- アプリに組み込む
- モニタリング、ダッシュボード作る
- 運用する

![Untitled](SLO%20gernerator%20%E3%81%A8%20OpenSLO%203fe9de6dcd4b4161974d2ec51327535c/Untitled%2014.png)

SLI / SLO がドキュメントで IaC 化されてない。

![Untitled](SLO%20gernerator%20%E3%81%A8%20OpenSLO%203fe9de6dcd4b4161974d2ec51327535c/Untitled%2015.png)

![Untitled](SLO%20gernerator%20%E3%81%A8%20OpenSLO%203fe9de6dcd4b4161974d2ec51327535c/Untitled%2016.png)

![Untitled](SLO%20gernerator%20%E3%81%A8%20OpenSLO%203fe9de6dcd4b4161974d2ec51327535c/Untitled%2017.png)

![Untitled](SLO%20gernerator%20%E3%81%A8%20OpenSLO%203fe9de6dcd4b4161974d2ec51327535c/Untitled%2018.png)

PSO：professional service

CRE : Google を使ってる大きなサービスを運用している人向けのSRE

![Untitled](SLO%20gernerator%20%E3%81%A8%20OpenSLO%203fe9de6dcd4b4161974d2ec51327535c/Untitled%2019.png)

![Untitled](SLO%20gernerator%20%E3%81%A8%20OpenSLO%203fe9de6dcd4b4161974d2ec51327535c/Untitled%2020.png)

`backend` がどこからデータを引っ張るか

`exporter` がどこに計算結果を保存するか

![Untitled](SLO%20gernerator%20%E3%81%A8%20OpenSLO%203fe9de6dcd4b4161974d2ec51327535c/Untitled%2021.png)

Uptime Check 使って、定期的に Cloud Run を呼び出す（という動き面白いな）

![Untitled](SLO%20gernerator%20%E3%81%A8%20OpenSLO%203fe9de6dcd4b4161974d2ec51327535c/Untitled%2022.png)

ベンダー中立で作ってる

![Untitled](SLO%20gernerator%20%E3%81%A8%20OpenSLO%203fe9de6dcd4b4161974d2ec51327535c/Untitled%2023.png)

![Untitled](SLO%20gernerator%20%E3%81%A8%20OpenSLO%203fe9de6dcd4b4161974d2ec51327535c/Untitled%2024.png)

![Untitled](SLO%20gernerator%20%E3%81%A8%20OpenSLO%203fe9de6dcd4b4161974d2ec51327535c/Untitled%2025.png)

![Untitled](SLO%20gernerator%20%E3%81%A8%20OpenSLO%203fe9de6dcd4b4161974d2ec51327535c/Untitled%2026.png)

SLO をイテレートしていくのが半年ぐらいだと旨味が少ないので、まだあんまり流行ってないのかな？という印象とのこと。

---

[OpenSLOについて | フューチャー技術ブログ](https://future-architect.github.io/articles/20220518a/)

[https://github.com/OpenSLO/OpenSLO](https://github.com/OpenSLO/OpenSLO)

[https://github.com/google/slo-generator](https://github.com/google/slo-generator)