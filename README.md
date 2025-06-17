# Demo

- [TLS 教育施設 PMTiles デモ](https://pmtiles.io/#url=https://hfu.github.io/zip2seq/docs/tls_education_facilities.pmtiles)
- [PAN 教育施設 PMTiles デモ](https://pmtiles.io/#url=https://hfu.github.io/zip2seq/docs/pan_education_facilities.pmtiles)
- [VUT 教育施設 PMTiles デモ](https://pmtiles.io/#url=https://hfu.github.io/zip2seq/docs/vut_education_facilities.pmtiles)
- [THA 教育施設 PMTiles デモ](https://pmtiles.io/#url=https://hfu.github.io/zip2seq/docs/tha_education_facilities.pmtiles)
- [MMR 教育施設 PMTiles デモ](https://pmtiles.io/#url=https://hfu.github.io/zip2seq/docs/mmr_education_facilities.pmtiles)

# zip2seq
PoC Pipeline conversion from OCHA HDX OSM extract GeoJSON by HOT into GeoJSON Text Sequence

`zip2seq` は、リモート公開された ZIP アーカイブから GeoJSON ファイルをストリーミングで取り出し、  
各 Feature に tippecanoe 用メタデータを付加した上で標準出力に Newline-Delimited GeoJSON（NDJSON）形式で出力する小さなパイプラインツール集です。

---

## 特徴

- ZIP をローカルに保存せずにストリーム処理  
- `curl` + `bsdtar`（libarchive-tools）+ `jq` のみで完結  
- 国（ISO3）、テーマ、ジオメトリ型をパラメタ化  
- 各 Feature に `tippecanoe: { layer: "<iso3>_<theme>_<geom>" }` を自動付加  
- tippecanoe で直接タイル化できる NDJSON 出力  

---

## 前提条件

- シェル環境（bash, zsh など）  
- curl  
- libarchive-tools（bsdtar）  
- jq  

### Debian／Raspberry Pi OS でのインストール例

```sh
sudo apt update
sudo apt install -y curl libarchive-tools jq
```

---

## 使い方

以下の３つの環境変数を設定してパイプラインを実行します。  

- `ISO3`：国の ISO-3166-1 alpha-3 コード（例: TLS）  
- `THEME`：テーマ名（例: education_facilities）  
- `GEOM`：ジオメトリ型（例: point）  

```sh
export ISO3="tls"
export THEME="education_facilities"
export GEOM="points"
```

### スクリプト例

```sh
ISO3="tls"
THEME="education_facilities"
GEOM="polygons"

URL="https://s3.dualstack.us-east-1.amazonaws.com/production-raw-data-api/ISO3/${ISO3^^}/${THEME}/${GEOM}/hotosm_${ISO3}_${THEME}_${GEOM}_geojson.zip"
ENTRY="hotosm_${ISO3}_${THEME}_${GEOM}_geojson.geojson"
LAYER="${ISO3}_${THEME}_${GEOM}"

curl -L "$URL" \
  | bsdtar -xOf - "$ENTRY" \
  | jq -c '.features[] | .tippecanoe = { layer: '"'"$LAYER"'"' }'
```

- `curl -L`：リダイレクト追跡しつつ ZIP をストリーム取得  
- `bsdtar -xOf - "$ENTRY"`：stdin の ZIP から指定エントリを stdout に展開  
- `jq -c`：各 Feature をコンパクトな JSON（1行1Feature）で出力し、  
  `.tippecanoe.layer` を `<iso3>_<theme>_<geom>` に設定  

---

## 次のステップ

1. 出力した NDJSON を `> features.ndjson` のようにファイル化  
2. tippecanoe でタイル化  
   ```sh
   tippecanoe -o tiles.mbtiles features.ndjson
   ```
3. タイルサーバーや地図フレームワークへデプロイ  

---

## ライセンス

MIT License  
詳細は [LICENSE](LICENSE) を参照してください。 

OSM データのライセンスは ODbL です。
