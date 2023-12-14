# ローカルでの実行手順
以下手順によりローカル環境でのサンプルアプリ実行が可能です。

## 事前準備
1. [Azure Function Core Tools](https://learn.microsoft.com/en-us/azure/azure-functions/functions-run-local?tabs=windows%2Cisolated-process%2Cnode-v4%2Cpython-v2%2Chttp-trigger%2Ccontainer-apps&pivots=programming-language-csharp) のインストールします。
1. [Node.js](https://nodejs.org/en/download)のインストールします。
1. 本レポジトリのソースコードをフォーク、またはダウンロードします。

## 依存関係のインストール
1. Visual Studio Code でターミナルを開き、プロジェクトフォルダーに移動します。
    ```Bash
    cd POC-BlobUpload
    ```
1. /app ディレクトリに移動し、依存関係をインストールします。
    ```Bash
    cd app
    npm install
    ```
1. /app ディレクトリに移動し、依存関係をインストールします。
    ```Bash
    cd api
    npm install
    ```

## 設定ファイルの構成
1. /api ディレクトリに local.settings.json ファイルを作成し内容を貼り付け、以下環境値を入力します。

    | プロパティ | 値 | 説明 |
    | --- | --- | --- | --- |
    | Azure_Storage_AccountName | Azure Storage Account 名 | ストレージリソースへの接続に利用 |
    | Azure_Storage_AccountKey	| Azure Storage Account のキー | ストレージリソースへの接続に利用 |
    | AzureWebJobsStorage | Azure Storage Account の接続文字列 | Azure Function ランタイムのステートとログ保管用 |

    ```
    {
      "IsEncrypted": false,
      "Values": {
        "AzureWebJobsStorage": "Azure Storage Account の接続文字列",
        "FUNCTIONS_WORKER_RUNTIME": "node",
        "AzureWebJobsFeatureFlags": "EnableWorkerIndexing",
        "Azure_Storage_AccountName": "Azure Storage Account 名",
        "Azure_Storage_AccountKey":"Azure Storage Account のキー"
      },
      "Host": {
        "CORS": "*"
      }
    }
    ```

## アプリケーションの実行
1. /api ディレクトリでのアプリケーション実行
    ```Bash
    cd api
    npm run start
    ```

1. /app ディレクトリでのアプリケーション実行(別のターミナルウィンドウで実行)
    ```Bash
    cd app
    npm run dev
    ```

## 動作確認
1. /app ディレクトリでアプリケーション実行時に出力される URL にアクセスし、任意のファイルが Azure Blob Storage にアップロード完了すれば動作確認完了です。