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

