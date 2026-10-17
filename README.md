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

## 比較用: 上野駅周辺（点群と PLATEAU 建物モデル）

同じ大きさの範囲（256 × 288 m、EPSG:6677 で x=-5134〜-4878, y=-32100〜-31812）を、点群と PLATEAU の LOD2 建物（空中写真のテクスチャつき）で作り、`Choice` で切り替えられるようにしました。

- ビューアで見る: https://3d.ldas.jp/ja/viewer?manifest=https%3A%2F%2Fnakamura196.github.io%2Fhongo-campus-iiif%2Fueno.json
- manifest: https://nakamura196.github.io/hongo-campus-iiif/ueno.json

| ファイル | 内容 | 大きさ |
|---|---|---|
| plateau-ueno.glb | PLATEAU の建物 186 棟（LOD2、写真 380 枚）と、点群の地面の点から作った地表 | 7.3 MB |
| ueno-points-light.glb | 点群（約 27 万点、1 m の立方体ごとに 1 点） | 1.7 MB |
| ueno-points-mid.glb | 点群（約 79 万点、0.5 m の立方体ごとに 1 点） | 4.5 MB |
| ueno-points-full.glb | 点群（約 379 万点、間引きなし） | 17.5 MB |

範囲内の建物のうち、PLATEAU に名前（`gml:name`）がある 3 棟（上野駅・上野警察署上野駅前交番・上野病院）と、いちばん高い建物（62 m）に、屋根の上の印を `commenting` 注釈（`PointSelector`）で付けています。本文は PLATEAU の計測高さです。英語名は手で付けました。印ごとに、斜め上から見る視点を `<注釈の id>/camera` の `PerspectiveCamera` で入れています（3d.ldas.jp は、印を押したときにこの視点へ移ります）。

## 地図との対応（Georeference）

どちらの manifest にも、地図上の位置と模型上の位置の対応点を、IIIF Georeference Extension の `georeferencing` 注釈で入れています（本郷は注釈を付けた建物ごと、上野は範囲の四隅）。3D の位置（`resourceCoords` が x, y, z の 3 つ）は拡張の仕様にない使い方で、3d.ldas.jp の地図ページ（`/ja/georef?manifest=...`）が読みます。範囲の外形は `navPlace` に入れています。

## 出典とライセンス

- 点群: 東京都「東京都デジタルツイン実現プロジェクト 区部点群データ」（CC BY 4.0）を加工して作成
- 建物の名前と位置（本郷）: © OpenStreetMap contributors（ODbL）
- 建物モデル（上野）: 国土交通省 Project PLATEAU「3D都市モデル（Project PLATEAU）台東区（2025年度）」（https://www.geospatial.jp/ckan/dataset/plateau-13106-taito-ku-2025 、PLATEAU Site Policy による。CC BY 4.0 と互換）を加工して作成
- 建物の説明文: 東京大学の公開資料をもとに作成。各注釈に出典の URL を付けています

作成: 中村 覚（東京大学）
