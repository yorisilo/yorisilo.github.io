# Description
this repo is for Yorisilo's site.
Come on my site [依り代](http://yorisilo.github.io)

# Contents
* podcast
* something else stuff...

# ポッドキャスト収録方法
## 音声収録
* iPhone のボイスメモで行う
* AirMac とかを使って Mac へ転送する

## 変換
* iPhone のボイスメモを使うと m4a で録音されるので audacity で編集できるように mp3 へ変換する

`m4a -> mp3` へ変換するコマンド
``` shell
for i in *.m4a ; do b=`basename $i .m4a` ; mp4box -raw 1 $i ; ffmpeg -i "$b"_track1.aac $b.mp3 ; done
```

[mp4box と ffmpeg で m4a を mp3 に変換する - Qiita](https://qiita.com/yoya/items/2cefa9755c825ef84471)

## 編集
* レベル調整： コンプレッサーを使い、発声時に -6db くらいが平均になるようにする
* ノイズ除去： サーってホワイトノイズ部分をノイズとして認識させて、そのノイズを除去する
* 無音除去： やりすぎると違和感があるので適時調整

audacity を使って編集する

[podcasting-for-you | Ⅱ.audacityの便利ワザ](http://haruthanatos.wixsite.com/podcasting-for-you/blank-1)

## エンコード
* `MP3 44.1kHz mono CBR 96kbps ~ 128kbps`

audacity でエンコードし、タグを付ける。

| tag            | value        |
| :---           | :---         |
| アーティスト名 | yorisilo     |
| トラック名     | ep5 babadook |
| アルバム名     | yorisilo     |

## 音声アップロード
* ファイルサーバに音声をアップロードする
sakura のレンタルサーバをファイルサーバーとして使っているので ftp でアップロードする (ex. cyber duck とか)

duck コマンドっていうのがあってそれを使うと CUI からでも使えるので便利
``` shell
duck --upload example@example.sakura.ne.jp:/home/example/www/sounds/podcast/ ./ep5.mp3
```

## 記事作成
* `_posts` 以下にある過去の記事を参考にして、ポッドキャスト配信用の記事を markdown で作成する
* `jekyll s ` で編集した記事が localhost で見れるようになる。 watch されているので、編集するたびに反映される。

mp3 の情報を記事に反映させる

| tag       | value    | comments                         |
| :---      | :---     | :---                             |
| duration: | "16:09"  | podcastfeed に必要               |
| length:   | 15499668 | podcastfeed に必要               |
| size:     | 15.5MB   | 記事内に記載するサイズとして扱う |

jekyll (静的サイトジェネレーター) を使ってる。 netlify を使ってみたいと思ってはいる。

## 配信
* git commit して git push するだけ

## 宣伝
* twitter で podcast 録ったよって言う
