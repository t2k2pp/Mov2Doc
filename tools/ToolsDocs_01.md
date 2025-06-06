# 動画フレーム抽出アプリケーションのセットアップと使用法

作成したプログラムは、マウスカーソル程度の小さな変化を無視し、実質的な動きのあるフレームのみを抽出するtkinterベースのアプリケーションです。では、環境構築から実行までの手順を説明します。

## 1. 環境構築

### 必要なライブラリ

以下のライブラリが必要です：

```bash
pip install opencv-python numpy scikit-image pillow
```

- **opencv-python**: 動画および画像処理用
- **numpy**: 数値計算用
- **scikit-image**: フレーム間の類似度比較用
- **pillow**: TkinterでのGUI画像表示用

tkinterはPythonの標準ライブラリなので、追加インストールは不要です。

## 2. プログラム構成

プログラムは単一のPythonファイルで、以下の2つの主要クラスで構成されています：

1. **VideoFrameExtractor**: 動画処理のコアロジックを担当
    
    - フレーム抽出
    - 差分検出
    - 画像保存
2. **VideoFrameExtractorApp**: Tkinter UIを実装
    
    - ファイル選択インターフェース
    - パラメータ設定UI
    - 進捗表示
    - プレビュー機能

## 3. 使用方法

1. プログラムを実行すると、以下の機能を持つGUIが表示されます：
    
    - **入力動画ファイル選択**: 動画ファイルを参照ボタンから選択
    - **出力フォルダ選択**: 抽出された静止画の保存先を指定
    - **変化検出感度**: 値が小さいほど小さな変化に敏感（0.01～0.2）
    - **最小変化領域**: マウスカーソルなどの小さな変化を無視するための閾値（100～2000 px²）
    - **サンプリング間隔**: すべてのフレーム、0.1秒、0.5秒、1秒、2秒、5秒、10秒から選択
    - **出力サイズ設定**: 元のサイズのまま、または指定サイズに変更可能
2. パラメータを設定したら「抽出開始」ボタンをクリックして処理を開始します。
    
3. 処理中は以下の情報が表示されます：
    
    - 処理の進捗状況（%表示とプログレスバー）
    - 現在の処理時間/総時間
    - 抽出済みのフレーム数
    - 現在のフレームのプレビュー（サンプリング）
4. 処理が完了すると、結果が表示されます。
    

## 4. アルゴリズムの概要

このアプリケーションは以下のアルゴリズムを使用して動きのあるフレームを抽出します：

1. フレームを順番に読み込む（サンプリング間隔に従って）
2. 連続するフレーム間の構造的類似性（SSIM）を計算
3. 差分画像から変化領域を検出（輪郭抽出）
4. 変化領域のサイズが閾値を超え、かつフレーム全体の類似度が閾値を下回る場合のみフレームを保存
5. 保存する画像には時間情報とフレーム番号を付加

## 5. パラメータ調整のポイント

- **変化検出感度**: 0.05が一般的な設定。値を小さくすると小さな変化も検出します。
- **最小変化領域**: マウスカーソルのサイズは通常500px²以下。それ以上の値を設定すると、マウスカーソル程度の変化は無視されます。
- **サンプリング間隔**: 長時間の動画では、処理時間短縮のために1秒以上の間隔を選ぶと効率的です。

## 6. 出力ファイル

抽出されたフレームは以下の命名規則で保存されます：

```
frame_[フレーム番号6桁]_[時間].jpg
```

例: `frame_000123_0-00-05.jpg`（5秒時点の123フレーム目）

---

このアプリケーションは、画面録画から重要なシーンだけを抽出したり、動画から効率的にサムネイルを生成したりするのに役立ちます。サンプリング間隔やサイズ変更機能を活用することで、様々な用途に対応可能です。

必要に応じてパラメータを調整して、最適な結果を得てください。