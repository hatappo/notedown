---
layout: post
title: "Translation: inlein README.md"
categories: clojure
tags: clojure leiningen inlein translation
---

https://github.com/hyPiRion/inlein/README.mdを和訳しました。拙い和訳ですが。。  
このブログにコメントする機能が無いので、訂正や指摘など頂ける場合は[リポジトリ](https://github.com/hatappo/notedown)のほうへIssueかPullRequestしてもらえると幸いです。

原文(original)： [https://github.com/hyPiRion/inlein/blob/5e0de2442ec81bba5d5130fc02e0d29f73a60bec/README.md](https://github.com/hyPiRion/inlein/blob/5e0de2442ec81bba5d5130fc02e0d29f73a60bec/README.md)

----

----

# Inlein

クラスパスを設定する煩わしさなしに、Clojureのスクリプト（訳注：ClojureScriptのことではくて、比較的小規模な単一ファイルのプログラムの意味での「Clojureのスクリプト」）を依存性を解決して実行します。

## Installation

Inleinの完全な紹介とチュートリアルは、Wikiの[Getting Started](https://github.com/hyPiRion/inlein/wiki/Getting-Started)ページを見てください。
Leiningenのインストールと使い方を知っているなら、このREADMEのクイックスタートとインストール手順が十分理解できるでしょう。

Inleinは、`inlein`スクリプトの最初の実行において自身に必要なものをインストールします。そのため独立したインストール用のスクリプトはありません。
Inleinを手動でインストールするには、次の手順に従ってください。

1. JavaのJDKの**version 7**以上があることを確認。
2. [リリースされている最新の`inlein`プログラムをダウンロード](https://github.com/hyPiRion/inlein/releases/latest)
3. ダウンロードしたファイルをあなたの環境の`$PATH`上に配置。（`~/bin`がパスに含まれているならそこに置くのがいいでしょう。）
4. 実行権限を与える。（`chmod 755 ~/bin/inlein`）
5. 実行してください。

スクリプトの起動が最初の1回だけちょっと遅いかもしれないことに注意してください。
inleinのデーモンを取得し起動しなければならないためです。
`inlein --start-daemon`で呼び出すことによって、強制的にダウンロードとデーモンの起動を行うこともできます。
後続のスクリプトの実行における起動時間がより速くなります。（訳注：訳に自信なし）

## Quickstart

inleinは通常、実行するClojureのスクリプト・ファイルと、そのスクリプトに渡す引数を付けて呼び出されます。

```shell
inlein myscript.clj my args here
```

*nix系のOSなら、シバンの行を先頭に追記してスクリプト実行可能にすることで、inleinを直接呼び出すのを省略することができます。

```clj
#!/usr/bin/env inlein
```

スクリプトの先頭に書いてください。

### Sample Script

例として、0から数えて*nth（n番目の）*素数を計算するスクリプトを作ってみましょう。
依存ライブラリを追加するやり方を見ていくために、素数の探索には[私の素数用のライブラリ](https://github.com/hyPiRion/primes)を使用します。

以下をファイルに書き込んでください。書き込んだファイルは`primes.clj`という名前にします。

```clj
#!/usr/bin/env inlein

'{:dependencies [[org.clojure/clojure "1.8.0"]
                 [com.hypirion/primes "0.2.1"]]}

(require '[com.hypirion.primes :as p])

(when-not (first *command-line-args*)
  (println "Usage:" (System/getProperty "$0") "prime-number")
  (System/exit 1))

(-> (first *command-line-args*)
    (Long/parseLong)
    (p/get)
    println)
```

このスクリプトを実行可能（`chmod +x primes.clj`）にしたら、例えば`./primes.clj 10`を実行して試してみてください。

inleinのスクリプトでは、始めにクオートされたマップを書きます。このマップにはそのスクリプトの依存関係を記述します。

依存関係は、Leiningenと全く同じようにして指定されます。つまり、`:dependency`キーに紐付けられた、依存ライブラリのベクタとして指定します。

このクオートされたマップには、あなたが追加したいJVMのオプションも含めることができます（プログラムの起動スピードを上げるのによく使われます）。

inleinでは、実行しているファイル名が`$0`というシステム・プロパティに紐付けられます。shellっぽくスクリプトを書くのに役立ちます。

## Building from Source

パス上に`~/bin`があって、inleinのスナップショットのバージョンを実行したいとしたら、`test/install.sh`を呼び出すだけでOKです。
これを実行すると、`~/bin/inlein`にクライアントが配置され、適切なデーモンが必要な場所に配置されるでしょう。
改めてアップグレードやダウングレードをしたかったら、インストールされたinleinのバージョンを手動で上書きしなければならないことを忘れないでください。

手動でインストールしたりソースコードをいじったりするには、[CONTRIBUTING.md](https://github.com/hyPiRion/inlein/blob/master/CONTRIBUTING.md#bootstrapping)の中のBootstrappingの節を見てください。

## License

Copyright © 2016 Jean Niklas L'orange

Eclipse Public Licenseの1.0かあるいは（あなたの指定する）1.0以降のなんらかのバージョンにおいて配布されます。
詳細はLICENSEファイルを見てください。
