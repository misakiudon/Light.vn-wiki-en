---
title: 20. マルチプラットフォーム展開
description: 
published: true
date: 2025-07-17T21:19:27.068Z
tags: 
editor: markdown
dateCreated: 2025-07-17T21:19:27.068Z
---

## マルチプラットフォーム展開用ツール

Python

- https://www.python.org/downloads/
- <img alt="image" src="https://github.com/user-attachments/assets/0a0d0596-f8db-44bd-a299-233d1d8ec177" />
  - **Add Python 3.9 to PATH をチェックいれること！**
- <img alt="image" src="https://github.com/user-attachments/assets/ca8b1ddc-3aa3-4857-b9bc-567a8d4d3335" />
  - Disable path length limitもおす
- Close押してインストール終了

Cmder

- cmder (https://cmder.app/)をダウンロードする (Download Full)

## Web版

### 配布完了までの流れ

- [(User Wiki 資料)](https://wikiwiki.jp/lightvn/packaging)
- [参考：解説動画](https://youtu.be/778d4NgP2ZY?si=hppinVjEg5weKxPD)
  - こちらの方をみながら一緒に手順を踏んだ方が、多分楽かと思いますー
- Light.vnのBrowser(WebGL)版は、現在エディターからの配布後、ユーザー側で最終的にリソースを圧縮する手順を踏む必要があります。（改善対策模索中）
- 環境準備を行う (一度のみ必要)
  - python3
  - cmder
  - emsdk_directory.txtの更新
    - emsdkを設置したいフォルダーにいく。(作品の配布先以外)
    - 作品の配布先/scripts/setup_emscripten.shをそこにペースト。
    - cmderを該当フォルダーに開いて、以下を実行：
      - `sh setup_emscripten.sh`
      - 最後に出てくるPaste: のパスを、emsdk_directory.txtの1行めにペースト。
        - (LightEditor.exeのおかれた、_export/webgl/scripts/emsdk_directory.txtも)
          - <img alt="image" src="https://github.com/user-attachments/assets/dfff00cb-f6d2-4311-ab80-f314a182b01b" />
            - (この場合、`/c/Users/daego/Desktop/Light.vn_Sample/emsdk`)
- テストプレイを行う (配布先にて)
  - 開始：`sh ./scripts/run.sh`
    - すると、
      - browser向けに素材が圧縮 (loader.js, project.dataファイル作成)
      - ブラウザーが自動で開き、プレイが開始される。
  - 終了：`ctrl + c`
- 配布サイトにアップロードする：
  - data/, 
  - scripts/
  - フォルダー以外の全て。

### 動作環境

- 以下をサポートするブラウザー：
  - WebAssembly: https://webassembly.org/
  - WebGL 2: https://caniuse.com/webgl2 
    - (現状Safariの場合WebGL2に対応していない）

### C++版との違い・未実装機能

- (以下の他にもC++版との違いがあればバグなので、Discordを通してご連絡お願いします)
- 未実装機能・機能変更・留意点
  - テキスト入力
  - 開く、コマンドの実行はurlに制限される。
  - LuaがWindows上で実行することを前提としている場合問題の可能性あり。
  - ページをクリックするまでは音楽が再生されない。
- 違い
  - 作品をプレイするタブを閉じると、セーブデータは消える。（永久保存されない）
  - Wasmを裏で使っているため、サーバーから作品を配信する際には
    - Response Headerを：
      - "Cross-Origin-Opener-Policy", "same-origin"
      - "Cross-Origin-Embedder-Policy", "require-corp"
      - に設定する必要がある。
        - (server.pyを参考)
  - 画面を押すまでには音楽は流れない。
  - 作品ロード時に作品の全リソースを読み込むため：
    - ネット回線などの遅い環境だと最初のロードに時間がかかる。
    - + その分のメモリが使用される。
      - => 軽量化大事。
  - **最大FPSは60前後。**
    - Light.vn C++版は、OS内で実行されるのであれば。
    - WebGL版は、OS内のブラウザー内で実行される為の違い。

### 配布時の設定

- Light vn で作品をブラウザー用に配布する際に、
- settings.xml
    - disallowOpenをtrue
      - （開くコマンドの無効化）
    - disallowPopupsをtrue
      - （エラーアラムの無効化）
- の状態として配布されます。
  - disallowOpenをtrueにするのは、ふりーむ！などの外部配布サイトに作品を登校する場合、外部リンクを開く動作を行おうとすると、作品が停止することになり。
    - （原因：サーバーの`Content-Security-Policy`設定）
  - disallowPopupsをtrueにするのは、PC作品とは違ってブラウザーで作品をプレイする場合ユーザーがエラーがでるだけですぐ作品を閉じてしまう傾向が強いため。
- 個人サイトなどに配布する場合、或いはこういった動作を望まない場合は、
- 配布後、上記二つの設定を調整してください。

### リソースの最適化

- ブラウザーを通してプレイされるため、WebGL版はリソースの最適化が特に重要です。いくつかの理由をあげると：
  - **ユーザーがネット回線を通じて作品のダウンロードをするため、**
    - ファイルサイズが大きければ大きいほど、作品のロードに時間がかかってしまい、重く感じられる
    - ネット通信が遅いだけでなく、不安定な環境の場合、素材のファイルサイズが大きいと、途中でダウンロードに失敗してしまう可能性もある。
- なので、短い作品でない場合は、画質が若干落ちても画像素材のファイルサイズをより小さくしたりなど、工夫する必要があるかと思われます。
- **モバイルブラウザーへの対応：**
  - モバイルブラウザーはPCブラウザーと比べメモリー限界が遥かに低いです。
  - 対応を望まれる場合は：
    - 画像の解像度をさげ（大きくても800 x 600くらいに）、
    - 背景音楽のファイルサイズが1MB未満
    - になるようにして、
      - 作品全体のデーターが90MB以下になるようにすることを推奨します。
    - (こうやってもユーザーの形態のブラウザーメモリー限界を突破し、作品が停止することもあるので、モバイルブラウザー対応は最適化が多少面倒なほど重要です）
