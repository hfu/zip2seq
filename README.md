# zip2seq

OCHA HDXのHOT OSM extractから教育施設のGeoJSONデータ（ZIPアーカイブ）をストリーミングで取得し、
各Featureにtippecanoe用メタデータを付加したGeoJSON Text Sequence（GeoJSONSeq）として出力し、
複数国・複数ジオメトリ型のデータを結合してPMTiles形式のベクタータイルを自動生成するパイプラインです。

This pipeline streams education facility GeoJSON data (ZIP archive) from HOT OSM extracts on OCHA HDX, adds tippecanoe metadata to each feature, outputs as GeoJSON Text Sequence (GeoJSONSeq), merges data from multiple countries and geometry types, and automatically generates PMTiles vector tiles.

## Demo / デモ

- [東ティモール 教育施設 PMTiles デモ](https://pmtiles.io/#url=https://hfu.github.io/zip2seq/tls_education_facilities.pmtiles)
- [Timor-Leste Education Facilities PMTiles Demo](https://pmtiles.io/#url=https://hfu.github.io/zip2seq/tls_education_facilities.pmtiles)
- [東ティモール 教育施設 GeoJSON デモ](https://geojson.io/#id=github:hfu/zip2seq/blob/main/docs/tls_education_facilities.geojson)
- [Timor-Leste Education Facilities GeoJSON Demo](https://geojson.io/#id=github:hfu/zip2seq/blob/main/docs/tls_education_facilities.geojson)
- [パナマ 教育施設 PMTiles デモ](https://pmtiles.io/#url=https://hfu.github.io/zip2seq/pan_education_facilities.pmtiles)
- [Panama Education Facilities PMTiles Demo](https://pmtiles.io/#url=https://hfu.github.io/zip2seq/pan_education_facilities.pmtiles)
- [パナマ 教育施設 GeoJSON デモ](https://geojson.io/#id=github:hfu/zip2seq/blob/main/docs/pan_education_facilities.geojson)
- [Panama Education Facilities GeoJSON Demo](https://geojson.io/#id=github:hfu/zip2seq/blob/main/docs/pan_education_facilities.geojson)
- [バヌアツ 教育施設 PMTiles デモ](https://pmtiles.io/#url=https://hfu.github.io/zip2seq/vut_education_facilities.pmtiles)
- [Vanuatu Education Facilities PMTiles Demo](https://pmtiles.io/#url=https://hfu.github.io/zip2seq/vut_education_facilities.pmtiles)
- [バヌアツ 教育施設 GeoJSON デモ](https://geojson.io/#id=github:hfu/zip2seq/blob/main/docs/vut_education_facilities.geojson)
- [Vanuatu Education Facilities GeoJSON Demo](https://geojson.io/#id=github:hfu/zip2seq/blob/main/docs/vut_education_facilities.geojson)
- [タイ 教育施設 PMTiles デモ](https://pmtiles.io/#url=https://hfu.github.io/zip2seq/tha_education_facilities.pmtiles)
- [Thailand Education Facilities PMTiles Demo](https://pmtiles.io/#url=https://hfu.github.io/zip2seq/tha_education_facilities.pmtiles)
- [タイ 教育施設 GeoJSON デモ](https://geojson.io/#id=github:hfu/zip2seq/blob/main/docs/tha_education_facilities.geojson)
- [Thailand Education Facilities GeoJSON Demo](https://geojson.io/#id=github:hfu/zip2seq/blob/main/docs/tha_education_facilities.geojson)
- [ミャンマー 教育施設 PMTiles デモ](https://pmtiles.io/#url=https://hfu.github.io/zip2seq/mmr_education_facilities.pmtiles)
- [Myanmar Education Facilities PMTiles Demo](https://pmtiles.io/#url=https://hfu.github.io/zip2seq/mmr_education_facilities.pmtiles)
- [ミャンマー 教育施設 GeoJSON デモ](https://geojson.io/#id=github:hfu/zip2seq/blob/main/docs/mmr_education_facilities.geojson)
- [Myanmar Education Facilities GeoJSON Demo](https://geojson.io/#id=github:hfu/zip2seq/blob/main/docs/mmr_education_facilities.geojson)
- [ケニア 教育施設 PMTiles デモ](https://pmtiles.io/#url=https://hfu.github.io/zip2seq/ken_education_facilities.pmtiles)
- [Kenya Education Facilities PMTiles Demo](https://pmtiles.io/#url=https://hfu.github.io/zip2seq/ken_education_facilities.pmtiles)
- [ケニア 教育施設 GeoJSON デモ](https://geojson.io/#id=github:hfu/zip2seq/blob/main/docs/ken_education_facilities.geojson)
- [Kenya Education Facilities GeoJSON Demo](https://geojson.io/#id=github:hfu/zip2seq/blob/main/docs/ken_education_facilities.geojson)
- [ジブチ 教育施設 PMTiles デモ](https://pmtiles.io/#url=https://hfu.github.io/zip2seq/dji_education_facilities.pmtiles)
- [Djibouti Education Facilities PMTiles Demo](https://pmtiles.io/#url=https://hfu.github.io/zip2seq/dji_education_facilities.pmtiles)
- [ジブチ 教育施設 GeoJSON デモ](https://geojson.io/#id=github:hfu/zip2seq/blob/main/docs/dji_education_facilities.geojson)
- [Djibouti Education Facilities GeoJSON Demo](https://geojson.io/#id=github:hfu/zip2seq/blob/main/docs/dji_education_facilities.geojson)
- [セネガル 教育施設 PMTiles デモ](https://pmtiles.io/#url=https://hfu.github.io/zip2seq/sen_education_facilities.pmtiles)
- [Senegal Education Facilities PMTiles Demo](https://pmtiles.io/#url=https://hfu.github.io/zip2seq/sen_education_facilities.pmtiles)
- [セネガル 教育施設 GeoJSON デモ](https://geojson.io/#id=github:hfu/zip2seq/blob/main/docs/sen_education_facilities.geojson)
- [Senegal Education Facilities GeoJSON Demo](https://geojson.io/#id=github:hfu/zip2seq/blob/main/docs/sen_education_facilities.geojson)
- [ヨルダン 教育施設 PMTiles デモ](https://pmtiles.io/#url=https://hfu.github.io/zip2seq/jor_education_facilities.pmtiles)
- [Jordan Education Facilities PMTiles Demo](https://pmtiles.io/#url=https://hfu.github.io/zip2seq/jor_education_facilities.pmtiles)
- [ヨルダン 教育施設 GeoJSON デモ](https://geojson.io/#id=github:hfu/zip2seq/blob/main/docs/jor_education_facilities.geojson)
- [Jordan Education Facilities GeoJSON Demo](https://geojson.io/#id=github:hfu/zip2seq/blob/main/docs/jor_education_facilities.geojson)

## 概要 / Overview

- 9カ国（東ティモール, パナマ, バヌアツ, タイ, ミャンマー, ケニア, ジブチ, セネガル, ヨルダン）の教育施設データを対象
- Covers education facility data for 9 countries: Timor-Leste, Panama, Vanuatu, Thailand, Myanmar, Kenya, Djibouti, Senegal, Jordan
- 各国ごとに `polygons` と `points` の2種類のジオメトリ型を結合
- Merges two geometry types (`polygons` and `points`) for each country
- ストリーム処理でZIPからGeoJSONを抽出し、tippecanoe用layer情報を付加
- Extracts GeoJSON from ZIP by streaming and adds tippecanoe layer info
- すべての処理はRakefileで自動化
- All processing is automated by Rakefile
- 出力は `docs/*.pmtiles` ファイル（GitHub Pagesで公開可能）
- Output is `docs/*.pmtiles` files (publishable on GitHub Pages)

## ライセンス / License

MIT License  
詳細は [LICENSE](LICENSE) を参照してください。

See [LICENSE](LICENSE) for details (MIT License).

OSMデータのライセンスは ODbL です。

OSM data is licensed under ODbL.