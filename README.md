# zip2seq

OCHA HDXのHOT OSM extractから教育施設のGeoJSONデータ（ZIPアーカイブ）をストリーミングで取得し、
各Featureにtippecanoe用メタデータを付加したGeoJSON Text Sequence（GeoJSONSeq）として出力し、
複数国・複数ジオメトリ型のデータを結合してPMTiles形式のベクタータイルを自動生成するパイプラインです。

## Demo

- [東ティモール 教育施設 PMTiles デモ](https://pmtiles.io/#url=https://hfu.github.io/zip2seq/tls_education_facilities.pmtiles)
- [パナマ 教育施設 PMTiles デモ](https://pmtiles.io/#url=https://hfu.github.io/zip2seq/pan_education_facilities.pmtiles)
- [バヌアツ 教育施設 PMTiles デモ](https://pmtiles.io/#url=https://hfu.github.io/zip2seq/vut_education_facilities.pmtiles)
- [タイ 教育施設 PMTiles デモ](https://pmtiles.io/#url=https://hfu.github.io/zip2seq/tha_education_facilities.pmtiles)
- [ミャンマー 教育施設 PMTiles デモ](https://pmtiles.io/#url=https://hfu.github.io/zip2seq/mmr_education_facilities.pmtiles)
- [ケニア 教育施設 PMTiles デモ](https://pmtiles.io/#url=https://hfu.github.io/zip2seq/ken_education_facilities.pmtiles)
- [ジブチ 教育施設 PMTiles デモ](https://pmtiles.io/#url=https://hfu.github.io/zip2seq/dji_education_facilities.pmtiles)
- [セネガル 教育施設 PMTiles デモ](https://pmtiles.io/#url=https://hfu.github.io/zip2seq/sen_education_facilities.pmtiles)
- [ヨルダン 教育施設 PMTiles デモ](https://pmtiles.io/#url=https://hfu.github.io/zip2seq/jor_education_facilities.pmtiles)

## 概要

- 9カ国（東ティモール, パナマ, バヌアツ, タイ, ミャンマー, ケニア, ジブチ, セネガル, ヨルダン）の教育施設データを対象
- 各国ごとに `polygons` と `points` の2種類のジオメトリ型を結合
- ストリーム処理でZIPからGeoJSONを抽出し、tippecanoe用layer情報を付加
- すべての処理はRakefileで自動化
- 出力は `docs/*.pmtiles` ファイル（GitHub Pagesで公開可能）

## ライセンス

MIT License  
詳細は [LICENSE](LICENSE) を参照してください。

OSMデータのライセンスは ODbL です。
