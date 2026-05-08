# RSNA Intracranial Aneurysm Detection

## 概要
このコンペティションでは、CTA/MRA/MRIによって撮影された脳の画像を使い、脳腫瘍を検知するモデルの精度を競うものである。  

私は[RSNA-IAD | Ensemble | LB #1](https://www.kaggle.com/code/zshashz/rsna-iad-ensemble-lb-1)を~~パクり~~参考にし、3つのモデルのアンサンブルで推論させた。

大まかなプロセスは次の5つ： 

1. `dicom`ファイルを`npy`ファイルに変換 ― `utilities/dicom_to_npy.ipynb`
2. `npy`ファイルのPathをcsvファイルに記述 ― `utilities/npy_path_to_df.ipynb`
3. 3つのモデルを学習させる。
4. 3つのモデルの出力に基づいて、アンサンブルの比率を計算する。
5. アンサンブルによる推論を行う。
   
## 4つのプロセスの詳細

### dicomファイルをnpyファイルに変換
windowing、resizeなどを行ってdicomからsliceを取り出し、npyファイルに出力。  
また、このときSeriesInstanceUIDごとのメタデータをcsvファイルに保存している。

### npyファイルのpathをpd.DataFrameに保存

