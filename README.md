# facedetect-on-tao-toolkit
facedetect-on-tao-toolkit は、NVIDIA TAO TOOLKIT を用いて FaceDetect の AIモデル最適化を行うマイクロサービスです。  

## 動作環境
- NVIDIA 
    - TAO TOOLKIT
- FaceDetect
- Docker
- TensorRT Runtime

## FaceDetectについて
FaceDetect は、画像内の人の顔を検出し、カテゴリラベルを返すAIモデルです。  

## 動作手順

### engineファイルの生成
FaceDetect のAIモデルをデバイスに最適化するため、 FaceDetect の .etlt ファイルを engine file に変換します。  
現時点におけるNVIDIAの仕様では、GPUのアーキテクチャごとに engine file の生成が必要です。  
つまり、あるサーバで生成した engine file を別のサーバーにそのまま適用することはできません。  
本レポジトリに格納された facedetect.engine は、実際に生成される engine file の参考例です。  
engine fileへの変換は、Makefile に記載された以下のコマンドにより実行できます。
```
tao-convert:
	docker exec -it facedetect-tao-toolkit tao-converter -k nvidia_tlt -d 3,416,736 -e /app/src/facedetect.engine /app/src/facedetect.etlt
```

## 相互依存関係にあるマイクロサービス  
本マイクロサービスで最適化された FaceDetect の AIモデルを Deep Stream 上で動作させる手順は、[facedetect-on-deepstream](https://github.com/latonaio/facedetect-on-deepstream)を参照してください。  

## engineファイルについて
engineファイルである facedetect.engine は、[facedetect-on-deepstream](https://github.com/latonaio/facedetect-on-deepstream)と共通のファイルであり、本レポジトリで作成した engineファイルを、当該リポジトリで使用しています。  
