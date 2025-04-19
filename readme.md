# YOLO11 Pose 居眠り検知システム

このプロジェクトはYOLO11のポーズ推定を使用した居眠り検知システムを実装しています。人間のポーズを画像から分析し、頭の位置が肩に対して下がっているかどうかに基づいて居眠り状態を判定します。

## 特徴

- YOLO11 ONNXモデルによる人間のポーズ検出
- 頭の位置に基づく居眠り検知（頭が肩よりも下がっている状態を検出）
- 骨格の可視化と居眠りアラートを含む視覚的な出力
- カスタムモデルと信頼度閾値のサポート

## 必要条件

- Python 3.6以上
- OpenCV (`opencv-python`)
- NumPy
- ONNX Runtime (`onnxruntime`)

必要なパッケージのインストール:

```bash
pip install opencv-python numpy onnxruntime
```

## 使用方法

スクリプトはデフォルト設定で直接実行できます:

```bash
python drowsiness_yolo_pose.py
```

デフォルトでは:
- `yolo11n-pose.onnx`をモデルとして使用
- `test.jpg`を入力画像として処理
- 結果を`drowsiness_output.jpg`に保存

### コマンドライン引数

様々なコマンドライン引数で実行をカスタマイズできます:

```
--model        ONNXモデルへのパス (デフォルト: yolo11n-pose.onnx)
--image        入力画像へのパス (デフォルト: test.jpg)
--size         モデルの入力サイズ (デフォルト: 640)
--conf         検出信頼度閾値 (デフォルト: 0.25)
--kpt-conf     キーポイント信頼度閾値 (デフォルト: 0.2)
--output       出力画像を保存するパス (デフォルト: drowsiness_output.jpg)
--show         結果をウィンドウに表示
```

### 例

```bash
python drowsiness_yolo_pose.py --model yolo11n-pose.onnx --image person.jpg --show
```

## 仕組み

1. **ポーズ検出**: システムはYOLO11ポーズ推定を使用して人体の17のキーポイント（COCOデータセットのキーポイント定義に従う）を検出します。

2. **居眠り検知ロジック**: 
   - システムは頭部キーポイント（鼻、目、耳）の平均Y座標を計算
   - 肩のキーポイントの平均Y座標も計算
   - 頭の位置が肩の位置よりも低い場合（つまり、頭が下がっている状態）、居眠りと判定

3. **視覚的出力**:
   - 人物の境界ボックスは緑色（正常）または赤色（居眠り検出）で色分け
   - キーポイント間に骨格線を描画
   - 居眠りが検出された場合は警告メッセージを表示

## 注意点

- 検出精度は入力画像の品質とYOLO11ポーズモデルのパフォーマンスに依存します
- 最適な結果を得るためには、人物の顔と上半身がはっきり見えていることを確認してください
- このシステムは単一画像の分析用に設計されています。リアルタイムモニタリングには追加のコードが必要です


## 参考
ポーズ推定のためのUltralytics YOLO11 使い方
https://www.ultralytics.com/ja/blog/how-to-use-ultralytics-yolo11-for-pose-estimation

トランジスタ技術2025年5月号
 居眠り検知エッジAIの製作 ～なんと最高26TOPS！ ラズパイ用AI拡張ボード「AI Kit」試用レポート～
https://toragi.cqpub.co.jp/download2025/

