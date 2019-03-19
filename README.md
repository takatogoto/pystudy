# pystudy

## Install Ubuntu on Virtual Box
----システムセットアップ->定期的に実行!------------------------------------------------------------

sudo apt-get update

sudo apt-get upgrade



----Vimをアップデートしないと、入力が色々ややこしいので、下記を実行やっておく -------------------------
sudo apt-get install vim


----.bashrcの編集方法 (パスの通し方)------------------------------------------------------
cd ~
sudo vim ~/.bashrc
aを押す　→　編集モードに入る

編集がおわったら、escを押して、
:q! → 保存せずに終了。
:wq! →　保存して終了。


**万が一、謎の症状に見舞われた場合、以下のおまじないを唱えて、bashrcを復活させる。
パス情報を含めて、すべての設定がリセットされる。
sudo /bin/cp /etc/skel/.bashrc ~/
source ~/.bashrc
