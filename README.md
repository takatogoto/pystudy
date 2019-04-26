# pystudy
編集するために参考にしたページ
https://gist.github.com/mignonstyle/083c9e1651d7734f84c99b8cf49d57fa
https://gist.github.com/wate/7072365  
https://qiita.com/Qiita/items/c686397e4a0f4f11683d

## Install Ubuntu on Virtual Box
### Windows に Virtual Boxをインストール
参考：https://eng-entrance.com/virtualbox-install  
[公式ページ](https://www.virtualbox.org/)からダウンロードしてインストール。

### Ubuntu をインストール
http://releases.ubuntu.com/  
からお好みのバージョン（18.04 or 16.04 とか32 or 64とか）のISOファイルをダウンロード。

----システムセットアップ->定期的に実行!------------------------------------------------------------  
`sudo apt-get update`  
`sudo apt-get upgrade`

----Vimをアップデートしないと、入力が色々ややこしいので、下記を実行やっておく -------------------------  
`sudo apt-get install vim`

----.bashrcの編集方法 (パスの通し方)------------------------------------------------------  
`cd ~`  
`sudo vim ~/.bashrc`  
aを押す　→　編集モードに入る  

編集がおわったら、escを押してコマンドモードへ、  
`:q!` → 保存せずに終了。  
`:wq!` →　保存して終了。  


**万が一、謎の症状に見舞われた場合、以下のおまじないを唱えて、bashrcを復活させる。  
パス情報を含めて、すべての設定がリセットされる。  
`sudo /bin/cp /etc/skel/.bashrc ~/`  
`source ~/.bashrc`  
参考：https://qiita.com/hide/items/5bfe5b322872c61a6896

----共有フォルダの設定（結構厄介、まだできてない）------------------------------------------------------------  
https://web-dev.hatenablog.com/entry/etc/virtualbox/ubuntu16-shared-folder  
https://www.tecmint.com/install-virtualbox-guest-additions-in-ubuntu/  
https://qiita.com/haseken/items/982c5369988636991a4a  
https://qiita.com/SUZUKI_Masaya/items/3444a010cf9903a088b3  
https://unofficialtokyo.com/2018/12/virtualbox-ubuntu1804-on-windows/  
https://www.souichi.club/technology/virtualbox-share/  
https://note.mu/gkz74/n/n774da4725f7e  
https://www.hiroom2.com/2016/05/11/ubuntu-16-04%E3%81%ABsamba%E3%82%92%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB%E3%81%97%E3%81%A6windows-10%E3%81%A8%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E5%85%B1%E6%9C%89%E3%81%99%E3%82%8B/  
`sudo apt-get install -y samba`  

## Anacondaでいろいろ
----プロジェクト毎に仮想環境を作るとライブラリの依存関係が便利------------------------------------------------------------ 
https://qiita.com/tackey/items/a5e1ab29c8152fcc5da6  
https://qiita.com/caad1229/items/325ca5c8ad198b0ebce7  
https://qiita.com/fiftystorm36/items/b2fd47cf32c7694adc2e  

https://www.anaconda.com/tensorflow-in-anaconda/

`conda create -n env_name tensorflow`or 
`conda create -n env_name tensorflow-gpu` 
`conda activate env_name`  
`conda install -c anaconda jupyter`

## Nvidia
------> 以下のコマンドで、GPU稼働率が2秒毎に可視化できる。  
`watch nvidia-smi`  

---if error  
https://devtalk.nvidia.com/default/topic/1025694/cuda-setup-and-installation/error-when-running-nvidia-smi-with-vidia-smi-couldn-t-find-libnvidia-ml-so-library-/

---CUDA、cuDNN、tensorflowの互換性  
https://www.tensorflow.org/install/source#tested_build_configurations  
---CUDAのバージョン確認
`nvcc --version`  
https://medium.com/@changrongko/nv-how-to-check-cuda-and-cudnn-version-e05aa21daf6c  
`cat /usr/include/cudnn.h | grep CUDNN_MAJOR -A 2`  


## Tensorflow
バージョン確認
`python -c 'import tensorflow as tf; print(tf.__version__)'`  

# Music Album Cover Generation from Music Track with Conditional Generative Adversarial Network
Go Deep or Go home  
Anna Nadtochiy, Iordanis Fostiropoulos, Syamil Mohd Razak, Takato Goto  
University of Southern California, Los Angeles, CA, USA  
{nadtochi, fostirop, mohdraza, tgoto}@usc.edu  
## Introduction
### Goals
- Learn the relationship between the songs and the album covers as the visual  
- Generate album covers conditioned to a music track
![Samples of cover albums from two distinct groups genre show similarities of features and styles within each genre. Death metal music and jazz music are undeniably distinct.](https://user-images.githubusercontent.com/42685217/56783671-b96f8580-67a1-11e9-9ded-6a0b57aa3a73.png)
### Problem Formulation
![02](https://user-images.githubusercontent.com/42685217/56784100-d60cbd00-67a3-11e9-86f5-8c2dda3901fb.png)

## Framework
### Encoding function &Phi;  
- Extract features from music track to be used as conditional data
### Conditional GAN
- Condition on music track features  
- Generate complex and diverse album covers  
![03](https://user-images.githubusercontent.com/42685217/56784170-179d6800-67a4-11e9-9048-efe36271e073.png)

## Encoding functions
### Various dimensionality reduction techniques are used to identify groups/genres in music tracks
1. Reduce the dimension of music spectral and rhythm features using PCA  
2. Using RNN as a feature extraction method to account for temporal variation in music tracks  
3. Reduce the dimension of music spectral and rhythm features using auto-encoder  
4. Converting music tracks to spectrogram and using CNN as a feature extraction (CNN was trained to classify the music genre)   
![music tracks](https://user-images.githubusercontent.com/42685217/56784466-7b746080-67a5-11e9-9e90-c54d5469ef15.png)
![album covers](https://user-images.githubusercontent.com/42685217/56784471-7ca58d80-67a5-11e9-9e38-c978bd28203c.png)  
Samples of album covers from two distinct groups of genre show similarities of features and styles within each genre (different colors). Death metal (dark blue) and jazz (red) music are undeniably distinct, but album covers are not.  
![06](https://user-images.githubusercontent.com/42685217/56784691-bb881300-67a6-11e9-988a-f71bc4bf0efc.png)
![07](https://user-images.githubusercontent.com/42685217/56784693-bd51d680-67a6-11e9-92cc-0e90c2e42531.png)
Raw mp3 files encoded in lower dimension as a compact representation of the music track. Different genres are shown in different colors.  
![08](https://user-images.githubusercontent.com/42685217/56784762-09048000-67a7-11e9-9972-b9be9cbbe5eb.png)
![09](https://user-images.githubusercontent.com/42685217/56784763-0ace4380-67a7-11e9-82cb-045b5be37038.png)
Features extracted by LibROSA are reduced in dimension using an auto-encoder. Features can be split into 4 clusters (different color).  
![10](https://user-images.githubusercontent.com/42685217/56784831-64367280-67a7-11e9-8c0b-76e29602767e.png)
![11](https://user-images.githubusercontent.com/42685217/56784833-66003600-67a7-11e9-97b1-72521930f838.png)
Music track, represented as spectrogram, classified into 8 distinct genres using CNN.  
## GAN Architectures
### Various GANs have been tested to see if they have the capacity to represent and generate complex unstructured images
[![Style Gan on Album Covers](https://img.youtube.com/vi/8a0zIEanp6A&feature=youtu.be/.jpg)](https://www.youtube.com/watch?v=8a0zIEanp6A&feature=youtu.be)

### Conditional GAN

## Discussion & Conclusion



