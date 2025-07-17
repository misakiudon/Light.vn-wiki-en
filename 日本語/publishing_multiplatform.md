---
title: 20. 作品配布
description: 
published: true
date: 2025-07-17T23:32:42.520Z
tags: 
editor: markdown
dateCreated: 2025-07-17T21:19:27.068Z
---

## C++版

C++版の場合、どの環境でも最適の動作を保証できるように、細かく設定することが出来ます。  
  
データー保存先の指定

- Light.vnは、セーブデーターを含め、ユーザーPC上でのデーターの保存先を柔軟に指定することが出来ます。
- Settings.xmlを開いてみると
- <img alt="image" src="https://github.com/user-attachments/assets/4833ffe6-e73a-461f-a01c-d7bdf994b044" />
- 「writeDirectoryType」が
  - 「0」に設定
    - 実行プログラムと同じフォルダー内にデーターを保存します
  - 「1」に設定
    - ユーザーPC上のAppDataフォルダ内（例：C:\Users\ユーザー名\AppData\Roaming\）に、プロジェクトフォルダー名（sysProjectFolder）のフォルダーを作成し、その中でデーターを保存します。
      - <img alt="image" src="https://github.com/user-attachments/assets/131b7034-f580-49d4-870a-3cc5152758f3" />
      - （フォルダー名は「ノベル設定」に指定されたフォルダー名として作成されます。これもユーザーPCの設定などによるエラーを回避するため、英数字の方での作成をお勧めします）
- PC設定などにもよりますが、ユーザーPC上に「書き込み不可」となっているフォルダーもあります。
  - （例：Program Files, Program Files (x86))
- そういう書き込み不可となっているフォルダー内にユーザーが作品をインストールし、「writeDirectoryType=”0”」（フォルダー内に保存）になっている場合、
  - 書き込み不可によりデーターの書き込みが出来なくなり、以下等のエラーが発生する事になります：
  - <img src="https://github.com/user-attachments/assets/000d336a-4e77-47b4-97bb-70e4e96c7c87" />
  - こうした場合、ユーザーの方で書き込み可能なフォルダー（例：Desktop, C: などは大抵書き込み可能になっております）に移すか、
  - 「writeDirectoryType=”1”」に変更すると解決できます。
- ちなみに、「writeDirectoryType=”1”」として配布すると、CDからの直接起動も出来るかもしれません（現在未確認）

パッチ配布

- 作品公開の前より、ある意味作品公開後がより重要とも言えます。
- 公開後のユーザー意見や誤字などにも早速対応できるように、Light.vn では作品公開後のパッチ作成も簡単にできるようにしてあります。
- 詳しくは、Light.vn Wikiの「[作品パッチ](https://wikiwiki.jp/lightvn/tutorial#Ent03_02_02)」をご参考ください。

メモリー管理

- 作品中に使用されるすべての素材は、実行中にPCの「メモリー」というところに一時保存されます。それ以上使うとすると急にエラーを吐くような仕組みになっております。
  - 例：<img alt="image" src="https://github.com/user-attachments/assets/6d92945e-482d-44d0-8bb6-f8bccfb639a1" />
    - （素材が存在しているにも読み込みに失敗したというエラーなど、急に理解できないエラーが出始めると大抵これです）
- こうならないように防止するには、作品中のシーン転換等の際に
  - ケース１：
    - 「未使用素材開放」コマンドを入れることをお勧めします。
    - （特にファイルサイズの大きい画像や音楽素材を使用する作品の場合これが重要になるので、所々適切な所に置くことをお勧めします）
  - ケース２：
    - 「何もかもわからない！　面倒！」という方は、settings.xml内の「sysMemoryManagementType」を「2」に変えてみてください。(現在のLight.vnのデフォルト)
    - Light.vnが自動的に管理してくれます。
      - あくまで自動管理なので、ケース１ほど細密な調整はできないのですが、リソースをものすごくすごくすごく使用する作品でなければこれでも問題ありません。
- 注：ユーザーPCによっては、作品実行途中にメモリー開放をしようとするとエラーを吐く環境があります。これはLight.vnの問題ではなく、ユーザー環境の他メモリー管理のできてないバグの入ってあるプログラム、またOS (Windows)破損などが原因となります。
  - こういう場合、厳密に言えばそのプログラムを特定し、終了、或いはOSを再インストール、（たまにはRAM破損により新規のものに変える）などの必要がありますが、
とりあえず、
    - ユーザー側のsettings.xml内の「sysMemoryManagementType」を「1」に変えてみてください。
    - <img alt="image" src="https://github.com/user-attachments/assets/3e276eca-1028-40c7-865a-70bf9c6d9aa8" />
    - デフォルト「0」の場合、メモリー開放をちゃんと行うようにする設定で、「1」の場合、実行中にメモリー開放をしないようにする設定です。
    - ただ、「1」にした場合、メモリー開放による問題は消えますが、上記に書いたみたいな、「メモリー開放をしない」事による問題が発生する可能性があります。
      - （プロジェクト全体サイズが2GB / 2 = 1 GB以下であれば大丈夫ではあります）

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
