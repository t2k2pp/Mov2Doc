# PC操作動画を分析する方法の検討

PC操作を記録した動画は準備済みであることを想定（MP4など）。  
そこからマニュアルや記録を目的にテキスト化することを目的とする。

## 目次
- [手法の検討](#手法の検討)
- [Tools](#Tools)

## 手法の検討
### 1. 動画を生成AIに渡して分析する

マルチモーダル対応の **ChatGPT 4o** などは入力データとして動画を利用することができる。  
それらの能力を検証する。

守谷市の児童クラブに提出する「[就労証明書](https://www.city.moriya.ibaraki.jp/kurashi_tetsuzuki/e-service/1001536/1006145/1006146.html)」をPC画面に表示し、それを Power Point で録画を行いスクロールした動画を撮影。
その内容を ChatGPT 4o にインプットした。結果、実際とは一切関連のない内容が生成 [0001](https://github.com/t2k2pp/Mov2Doc/blob/main/log/Evidence01_0001.md),[0002](https://github.com/t2k2pp/Mov2Doc/blob/main/log/Evidence01_0002.md) された（ハルシネーション）。

### 2. 動画を静止画にして分析×画像分生成されたテキストを時系列に並べて分析

守谷市の児童クラブに提出する「[就労証明書](https://www.city.moriya.ibaraki.jp/kurashi_tetsuzuki/e-service/1001536/1006145/1006146.html)」をPC画面に表示し、それを Power Point で録画を行いスクロールした動画を撮影。
その内容を [動画フレーム抽出アプリケーション](#動画フレーム抽出アプリケーション) で画像を抽出し、ChatGPT 4o にインプットした。
結果、単一の画像においてはフレームにあった内容の情報が生成 [0001](https://github.com/t2k2pp/Mov2Doc/blob/main/log/Evidence02_0001.md) された。

### 3. 動画を静止画にして４コマ漫画のようにつなげて分析
### 4. 動画をアニメーションGISにして分析



## Tools
### 動画フレーム抽出アプリケーション
- [セットアップと使用法](https://github.com/t2k2pp/Mov2Doc/blob/main/tools/ToolsDocs.md)
- [Pythonコード](https://github.com/t2k2pp/Mov2Doc/blob/main/tools/video-frame-extractor.py)
