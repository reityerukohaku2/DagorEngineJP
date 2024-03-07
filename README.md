## 本リポジトリの目的
本リポジトリでは、Dagor Engineの日本語ドキュメントを充実させることを目的としています。

## 環境構築
Dagor Engineツールキットの使用に関する要件は以下の通りです。
- Windows10 (x64)
- 16GB以上のRAM容量
- 200GB以上のHDD/SDD容量

また、以下のソフトウェアが必要です。

* Git: https://git-scm.com/download/win
* 7-Zip: https://www.7-zip.org/
* Python 3
* FMOD soundライブラリを利用する場合、FMOD Studio SDK 2.02.15のインストールが必要です。

任意のドライブのルートディレクトリに、プロジェクトフォルダを作成します（フォルダ名は英数字のみを使用すること、スペースを含めてはいけません）。

```
md X:\develop && cd X:\develop
```

以下のコマンドで、DagorEngineをクローンしてください。
```
git clone https://github.com/GaijinEntertainment/DagorEngine.git
cd DagorEngine
```

次に、`make_devtoold.py`を実行します。これは、ビルドツールキットをダウンロード、インストール、構成を行うツールです。<br>
実行の際には、ビルドツールキットをインストールするフォルダへのパスを引数としてしているす必要があります。<br>
指定されたフォルダが存在しない場合は、自動的に作成されます。

以下は、`make_devtoods.py`の実行コマンドです。
インストール先フォルダの例として、`X:\develop\devtools`を指定しています。

```
python3 make_devtools.py X:\develop\devtools
```

実行時に以下のエラーが発生した場合、再度`make_devtools.py`を実行することで、解消する場合があります。

```
ERROR: Windows 8.1 SDK is required but not found at
```

また、管理者権限で実行しなかった場合、特定のプログラムのインストーラがインストールの許可を要求する場合があり、その際は許可する必要があります。

3ds Max SDKを利用するか尋ねられた際に、3ds Maxを利用する予定があるのであれば「y」を押してください。

また、スクリプトを実行すると `インストール先フォルダ\devtools` が環境変数PATHに追加されます。
そして、変数 `GDEVTOOL` がこのフォルダを指すように設定するよう要求します。

スクリプトの実行が完了すると、`インストール先フォルダ\devtools` フォルダが、以下のSDKとツールで構成されます。

* FidelityFX_SC - 画質向上用のライブラリ
* fmod-studio-2.xx.xx [optional] - FMOD sound のライブラリ
* LLVM-15.0.7 - C/C++ コンパイラおよびライブラリ (Clang)
* nasm - アセンブラ
* max2024.sdk - 3ds Max 2004 SDK
* openxr-1.0.16 - AR/VR用ライブラリ
* vc2019_16.10.3 - C/C++ コンパイラとライブラリ (MSVC)
* win.sdk.100 - Windows 10 SDK
* win.sdk.81 - Windows 8.1 SDK
* ducible.exe - ポータブル実行ファイルおよびPDBファイルのビルドを可能にするツール
* pdbdump.exe - PDbファイルの内容をダンプするツール
* jam.exe - Makeの代わりに利用可能な小規模ビルドツール

その後、新しい環境変数を有効にするためにコマンドラインツールを再起動してください。

## ビルド済みバイナリの準備
以下のリポジトリからビルド済みバイナリをダウンロードし、展開する必要があります。
[https://github.com/GaijinEntertainment/DagorEngine/releases](https://github.com/GaijinEntertainment/DagorEngine/releases)

ダウンロードしたビルド済みバイナリは、`DagorEngine` フォルダに展開してください。

ダウンロードするビルド済みバイナリを以下に示します。
* samples-base.7z - ゲームにロードされるバイナリファイルでコンパイルされる初期アセットが含まれています。
* samples-prebuilt-game.7z - ビルド済みアセットが含まれています。
* tools-prebuilt.7z - ビルド済みエンジンツールキットが含まれています。

ここまで準備が完了すると、ディレクトリ構造は以下のようになります。
なお、`DagorEngine`のインストール先は`X:\develop\`であると仮定しています。

```
X:\develop\DagorEngine\tools\...

X:\develop\DagorEngine\samples\skiesSample\game
                              \skiesSample\develop
                              \skiesSample\prog

X:\develop\DagorEngine\samples\testGI\game
                              \testGI\develop
                              \testGI\prog
```

* prog - ゲームソースコード
* develop - 初期アセット
* game - ビルド後にアセットが配置されるディレクトリ。また、ゲームの実行可能ファイルも配置されます。

## ソースコードを元にビルド

`testGI` サンプルをビルドするには、`インストール先フォルダ\samples\testGI\prog`フォルダに移動し、`jam`コマンドを実行します。<br>
ビルド後、実行可能ファイルが`testGI\game`フォルダに配置されます。

そして、ソースコードを元にプロジェクトツールキット全体をビルドするために `DagorEngine\build_all.cmd` を実行します。この作業には多くの時間がかかる場合があります。

> [!WARNING]
> 現在、ソースコードの一部にキリル文字が含まれており、日本人開発者の多くの環境で `DagorEngine\build_all.cmd` によるビルドが失敗する可能性があります。<br>
> この現象の解消方法は現在調査中です。<br>

## オープンソースロードマップ
さらに多くのエンジンとツールがオープンソース化される予定です。<br>
これは2023年時点の計画であり、変更される可能性もあります。

### ドキュメント
* Dagor レンダリング
* Dagor アセットの利用方法
* Dagor レベルエディタ
* Dagor リアクティブGUIフレームワーク

### Dagorの基本的なサンプル
- 基本的なレンダリングとゲームサンプルのバイナリとアセットソース。ゲームサンプルには以下のものがあります。
    - 地形
    - 雲
    - 水
    - 草
    - 入力とコントロール
- 基本的なゲームサンプルのソースコード

### 多数のゲームフレームワーク
DaslangとDagorをベースにした、サンプルとドキュメント付きのフレームワーク。<br>
詳細については今後公開予定です。
