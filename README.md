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

## How to Build: Prebuilt Binaries

You will need to download and extract additional binary files from the repository [https://github.com/GaijinEntertainment/DagorEngine/releases](https://github.com/GaijinEntertainment/DagorEngine/releases) into the X:\develop\DagorEngine folder:

* samples-base.7z - contains initial assets that will be compiled into binary files that will be loaded the game
* samples-prebuilt-game.7z - contains precompiled assets
* tools-prebuilt.7z - contains the prebuilt engine toolkit

The directory structure should look like this:
```
X:\develop\DagorEngine\tools\...

X:\develop\DagorEngine\samples\skiesSample\game
                              \skiesSample\develop
                              \skiesSample\prog

X:\develop\DagorEngine\samples\testGI\game
                              \testGI\develop
                              \testGI\prog
```

* prog - game source code
* develop - initial assets
* game - directory where assets are placed after building and game executable files are located

## How to Build: Build from Source Code

To build the "testGI" sample, navigate to the X:\develop\DagorEngine\samples\testGI\prog folder and run the "jam" command. After building, the executable file will be placed in the testGI\game folder.

Run DagorEngine/build_all.cmd to build the entire project toolkit from the source code. This process may take a considerable amount of time.

## Open-source roadmap

We are going to open-source more parts of our Engine and tools.
These are general and broad plans for next year, can be changed.

### Documentation

* dagor render
* how to work with dagor assets
* dagor level editor
* dagor reactive gui framework

### Basic dagor samples

* Binaries of basic render and game samples (terrain, clouds, water, grass; inputs and controls) with assets sources
* Sources of basic game samples

### The Pretty Games framework

Framework with samples and documentation, based on daslang and dagor.
Details yet to come.
