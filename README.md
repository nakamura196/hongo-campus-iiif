# 東京大学 本郷キャンパス（安田講堂周辺）の点群 — IIIF 3D

航空レーザー測量の点群（2023年3〜4月計測）を、約 260 × 290 m の範囲で glTF にし、
IIIF Presentation 4.0（草案）の manifest で配布しています。建物には説明の注釈が付いています。

- ビューアで見る: https://3d.ldas.jp/ja/viewer?manifest=https%3A%2F%2Fnakamura196.github.io%2Fhongo-campus-iiif%2Fhongo.json
- manifest: https://nakamura196.github.io/hongo-campus-iiif/hongo.json

## ファイル

| ファイル | 点の数 | 大きさ | 内容 |
|---|---|---|---|
| hongo-light.glb | 約 40 万 | 2.3 MB | 1 m の立方体ごとに 1 点に間引いたもの |
| hongo-mid.glb | 約 117 万 | 6.4 MB | 0.5 m の立方体ごとに 1 点に間引いたもの |
| hongo-full.glb | 400 万 | 19.0 MB | 間引きなし |

いずれも位置を量子化し、EXT_meshopt_compression で圧縮しています（gltfpack 1.2.0）。
座標は x 東・y 上・z 南、単位 m、原点は範囲の中央（平面直角座標系 第IX系 EPSG:6677 で x=-6452, y=-31844）。

manifest では 3 つを `Choice` に軽い順で並べ、`behavior: ["progressive"]`（仕様にない独自の値）を付けています。
対応していないビューアは先頭の軽い版を表示します。

## 出典とライセンス

- 点群: 東京都「東京都デジタルツイン実現プロジェクト 区部点群データ」（CC BY 4.0）を加工して作成
- 建物の名前と位置: © OpenStreetMap contributors（ODbL）
- 建物の説明文: 東京大学の公開資料をもとに作成。各注釈に出典の URL を付けています

作成: 中村 覚（東京大学）
