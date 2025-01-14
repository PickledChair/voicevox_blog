# VOICEVOX BLOG

VOICEVOXの公式サイトのリポジトリです。  
https://voicevox.hiroshiba.jp/

## 環境構築

Node v14.17.4、npm v6.14.14を用いて開発されています。

```bash
npm ci
```

## ローカル環境でチェック

```bash
npm run develop
```

もしくは

```bash
npm run build && npm run serve
```

## deploy

```bash
npm run clean && npm run deploy
```

## add resource

```bash
resource_url="https://raw.githubusercontent.com/VOICEVOX/voicevox_resource"
tag="0.9.4"

# 規約
curl -s "$resource_url/$tag/editor/README.md" > src/markdowns/softwareReadme.md
curl -s "$resource_url/$tag/character_info/01_metan/policy.md" > src/markdowns/libraryReadmeTohoku.md
curl -s "$resource_url/$tag/character_info/03_tsumugi/policy.md" > src/markdowns/libraryReadmeTsumugi.md
curl -s "$resource_url/$tag/character_info/04_hau/policy.md" > src/markdowns/libraryReadmeHau.md
curl -s "$resource_url/$tag/character_info/05_ritsu/policy.md" > src/markdowns/libraryReadmeRitsu.md

# 使い方
editor_url="https://raw.githubusercontent.com/VOICEVOX/voicevox"
curl -s "$editor_url/$tag/public/howtouse.md" > src/markdowns/howToUse.md
sed -r 's|src="([^"]+?)"|src="'$editor_url/$tag'/public/\1"|g' -i src/markdowns/howToUse.md

# 音声
# 24kHzのwavファイルはiPhoneで再生できないので、48kHzのflacにする
# sudo apt install sox libsox-fmt-all
find src/audios -name '*.wav' -printf "%P\n" | while read f; do
    sox src/audios/$f -r 48000 src/audios/$(echo $f | sed -r 's/.wav/.flac/g')
    rm src/audios/$f
done
```

## LICENSE

VOICEVOX の開発のための利用のみ許可されます。  
異なるライセンスを取得したい場合は、ヒホ（twitter: @hiho_karuta）に求めてください。

## 謝辞

`src/images/nc238325.jpg` ･･･ https://commons.nicovideo.jp/material/nc238325
