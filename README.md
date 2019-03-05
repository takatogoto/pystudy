# pystudy
Ubuntu 16.04のクリーンインストールする


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




----Anacondaのセットアップ----------------------------------------------------------------------
ダウンロードして、zipファイルを解凍。 https://www.anaconda.com/download/#linux
install.shを実行。
sudo sh 'shfilepath'

処理の最後に.bashrcを編集するかと聞かれるので、yesとタイプする。
忘れたら、以下を追記。
# added by Anaconda3 installer
export PATH="/home/bridgestone-forest/anaconda3/bin:$PATH"

conda update --all
conda upgrade --all
**定期的に実行!!

**
https://stackoverflow.com/questions/49092807/when-conda-install-django-permissionerror13-permission-denied



----CUDAインストール-> 9.0を強く推奨----------------------------------------------------------------
**NVIDIA-HPからlocal(deb)を選択する、netowrkを選ぶと既に9.1に移行しているため注意！！
必要ファイルはNASにあります。


****別バージョンがあってuninstallする場合*****
sudo apt purge cuda*
sudo apt purge nvidia-cuda-*
sudo apt purge libcuda*
sudo apt autoremove
sudo rm -R /usr/local/cuda-9.1
------------------------


--順番大事 最初cuda-repo-<distro>_<version>_<architecture>.deb

sudo dpkg -i cuda-repo-ubuntu1604-9-0-local_9.2.0.176-1_amd64.deb
sudo apt-get update
sudo apt-get install cuda
**sudo dpkg -i /path_to_file/***.deb


.bashrcに以下を追記。
export PATH=/usr/local/cuda-9.0/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda-9.0/lib64\
                       ${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}

----ターミナル再起動、本体も再起動したほうがいいかも


------> 以下のコマンドで、GPU稼働率が2秒毎に可視化できる。
watch nvidia-smi

---if error
https://devtalk.nvidia.com/default/topic/1025694/cuda-setup-and-installation/error-when-running-nvidia-smi-with-vidia-smi-couldn-t-find-libnvidia-ml-so-library-/



------->サンプルプログラムを動かしてみたいときには、以下を実行
/usr/local/cuda-9.0/bin/cuda-install-samples-9.0.sh ~
cd
cd NVIDIA_CUDA-9.0_Samples/
---- -j　のあとにコア数を入力すると早い
make -j 12



/bin以下にあるお好みのアプリを実行してみる。



----cuDNNインストール-> 7.0を強く推奨-------------------------------------------------------------------------------

**NVIDIA-HPで個人情報を登録してから、３つのファイルをダウンロードし、dpkg実行 (NASに保存してある。)
sudo dpkg -i /path_to_file/***.deb
sudo dpkg -i /path_to_file/***dev.deb
sudo dpkg -i /path_to_file/***doc.deb



-->サンプルプログラムによる動作検証
cp -r /usr/src/cudnn_samples_v7/ $HOME
cd  $HOME/cudnn_samples_v7/mnistCUDNN
make clean && make
./mnistCUDNN





----tensorflowをインストール(anacondaとの連携環境)---------------------------------------------------

sudo apt-get update
sudo apt-get install libcupti-dev

conda create -n tensorflow anaconda
source activate tensorflow

**opencvは、引き継がれないので、以下のコマンドで仮想環境に個別インストール
conda install opencv

python --version       
**pythonのバージョンを調べておく。

pip install --ignore-installed --upgrade 'tfBinaryURL'

**'tfBinaryURL'の在り処については、tensorflow.orgのHPから、自分の環境にあわせて選択。たとえばpython3.6の場合は???
https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-1.3.0-cp35-cp35m-linux_x86_64.whl

'https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-1.6.0-cp36-cp36m-linux_x86_64.whl'






----object detection APIのインストール-----------------------------------------------------------

sudo apt-get update
sudo apt-get install git
cd ~
mkdir tensorflow
cd tensorflow
git clone https://github.com/tensorflow/models.git
cd ~/tensorflow/models/research
protoc object_detection/protos/*.proto --python_out=.
export PYTHONPATH=$PYTHONPATH:`pwd`:`pwd`/slim


以下を.bashrcに追記
# From tensorflow/models/research/
export PYTHONPATH=$PYTHONPATH:~/tensorflow/models/research:~/tensorflow/models/research/slim


-->動作確認方法
python ~/tensorflow/models/research/object_detection/builders/model_builder_test.py





-----APC社製UPSの接続------------------------------------------------------------------------

1.ドライバのインストール
sudo apt-get install apcupsd
y/nと聞かれるので、yを選択。

2.ドライバの環境設定
sudo vi /etc/apcupsd/apcupsd.conf

    (1)ケーブルタイプの指定を変更 29行目
    UPSCABLE smart
       ↓
    UPSCABLE usb

    (2)UPSタイプとデバイスファイルの指定を変更　82行目
    UPSTYPE apcsmart
    DEVICE /dev/ttyS0
       ↓
    UPSTYPE usb
    DEVICE

    (3)タイムアウトの設定変更　157行目
    TIMEOUT 0
       ↓
    TIMEOUT 300

sudo vi /etc/default/apcupsd

    ISCONFIGURED=no
       ↓
    ISCONFIGURED=yes

3.再起動
sudo /etc/init.d/apcupsd restart




