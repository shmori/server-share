#第2回：ホスト型VM
* ホスト型仮想化技術のおさらい
* VirtualBoxの説明
* VirtualBoxのインストールと設定
* VMの作成
* VM上にCentOSを単純にインストール
* RAID1ミラーリングの説明
* VM上にCentOSをRAID1でインストール
* RAID1のリカバリー作業

##ホスト型仮想化技術のおさらい
ホスト型仮想化技術は、OS上に仮想化ソフトウェアをインストールして、
さらにその上で仮想サーバを動作させる技術です。  
他の仮想化技術に比べると性能面では劣りますが、
サーバや私用PCなどの中で手軽にVMを作成することが出来ます。

<img src="./host_type.png" height="300px">

##Virtual Boxの説明
innotekによって開発されたホスト型仮想化ソフトです。  
innotekは2008年にサン・マイクロシステムズに買収されたため、  
現在はサン・マイクロシステムズによってメンテナンスがされています。  
ライセンスは：GPL2なので注意しましょう。

##VirtualBoxのインストールと設定
###VirtualBoxのダウンロード  
下記サイトよりダウンロード。  
<a href="https://www.virtualbox.org/wiki/Downloads" target="_blank">https://www.virtualbox.org/wiki/Downloads</a>  
<img src="./download_virtualbox.png" width="80%">

###CentOSのダウンロード  
下記サイトよりダウンロード。  
<a href="https://www.centos.org/download/" target="_blank">https://www.centos.org/download/</a>  
<img src="./download_centos.png" width="80%">

###インストール
2015/04現在では全てデフォルトのままインストールで大丈夫です。  
<img src="./v_install01.png" width="60%">
<img src="./v_install02.png" width="60%">
<img src="./v_install03.png" width="60%">
<img src="./v_install04.png" width="60%">
<img src="./v_install05.png" width="60%">
<img src="./v_install06.png" width="60%">
###設定  


##VMの作成
###HDDの種類と説明
###ネットワークの種類と説明
##VM上にCentOSを単純にインストール
##VM上にCentOSをRAID1でインストール
###RAID1ミラーリングの説明
###RAID1のリカバリー作業