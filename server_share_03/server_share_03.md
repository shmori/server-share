# 第3回：Vagrant
* Vagrantの説明
* Vagrantのインストール
* 既存のBoxから起動
* 既存のBoxに手を加えてBoxを再生成
* Vagrantfileでのプロビジョニング

## Vagrantの説明
> 仮想環境の雛形を作成し、どこでも簡単に同じ環境を再現できるようにするソフトウェア。  
> <a href="http://e-words.jp/w/Vagrant.html" target="_blank">http://e-words.jp/w/Vagrant.html</a>

プロバイダ<sup>※1</sup>のフロントエンドとして動作します。  
プロバイダとして下記のものを選択できます。

* デフォルト  
`VirtualBox`
* 他の選択肢（要プラグイン追加）  
`VMware Fusion, AWS, Rackspace Cloud`

特にこだわりがなければデフォルトのままで問題ありません。

```
※1
Vagrantでは、バックエンドとして指定できる仮想化ソフトやIaaSのことをプロバイダと呼んでいます。  
```

## Vagrantのインストール
```
"Virtual Box" がすでに導入されている前提で進めます。
まだインストールが終わっていない場合は、ダウンロードしてインストールを行ってください。
2015/04現在ではMac, Windowsともにデフォルト設定で問題ありません。
```

### 必要なものを取得
下記サイトよりVagrantをダウンロード  
<a href="https://www.vagrantup.com/downloads.html" target="_blank">https://www.vagrantup.com/downloads.html</a>  

Windowsの場合は下記サイトから Git for Windows をダウンロード  
<a href="https://msysgit.github.io/" target="_blank">https://msysgit.github.io/</a>  

### インストール
#### Macの場合
##### Vagrantのインストール
1. ダウンロードしたdmgファイルを起動  
2. インストーラーに従ってインストール  
（2015/04現在では全てデフォルトでインストールしてOK）

1<img src="./img/mv_install01.jpg" width="30%">
2<img src="./img/mv_install02.jpg" width="30%">
3<img src="./img/mv_install03.jpg" width="30%">  
4<img src="./img/mv_install04.jpg" width="30%">

#### Windowsの場合
```
Vagrantを使うにはUnixライクなシェルがあったほうが便利です。  
しかしWindowsには標準でUnixライクなシェルが備わっていません。  
 Git for Windows をインストールすると、手軽にUnixライクなシェルが手に入るので  
先にこちらを導入します。
```
##### Git for Windows のインストール  
1. ダウンロードしたexeファイルを起動
2. インストーラーに従ってインストール  
今回は2箇所だけデフォルトから変更します。  
「画像4で On the Desktop にチェック」「画像6で2番目を選択」


1<img src="./img/g_install01.jpg" width="30%">
2<img src="./img/g_install02.jpg" width="30%">
3<img src="./img/g_install03.jpg" width="30%">  
4<img src="./img/g_install04.jpg" width="30%">
5<img src="./img/g_install05.jpg" width="30%">
6<img src="./img/g_install06.jpg" width="30%">  
7<img src="./img/g_install07.jpg" width="30%">
8<img src="./img/g_install08.jpg" width="30%">

3. 日本語の文字化けを修正  
下記サイトを参照   
<a href="http://qiita.com/kumazo@github/items/2169e1ee7be278f82b94" target="_blank">msysgit で日本語を使いたい - Qiita</a>

##### Vagrantのインストール
1. ダウンロードしたmsiファイルを起動
2. インストーラーに従ってインストール  
（2015/04現在では全てデフォルトでインストールしてOK）

1<img src="./img/v_install01.jpg" width="30%">
2<img src="./img/v_install02.jpg" width="30%">
3<img src="./img/v_install03.jpg" width="30%">  
4<img src="./img/v_install04.jpg" width="30%">
5<img src="./img/v_install05.jpg" width="30%">
6<img src="./img/v_install06.jpg" width="30%">

## 既存のBoxから起動
### Boxとは？
OSが予めインストールされた仮想マシンのイメージファイルです。  
VagrantではこのイメージファイルのことをBoxと呼んでいます。  
VagrantではBase Boxと呼ばれる起点のBoxをテンプレートとして、いくつもの仮想マシンを作成できます。

### 実際に起動してみる。
#### プロジェクトフォルダの作成
適当にプロジェクトフォルダを作成していきます。  
```bash
$ mkdir ~/vagrant/centos6/ && cd ~/vagrant/centos6/
```
Vagrantを開発した企業（HashiCorp）がBase Boxの公開リポジトリを提供しています。
公開リポジトリにアクセスして使いたいBase Boxを探します。   
<a href="https://atlas.hashicorp.com/boxes/search" target="_blank">https://atlas.hashicorp.com/boxes/search</a>   
今回はChef社が作成したCentosのBoxを利用します。
<img src="./img/box_search.jpg" width="80%">  
```bash
# Vagrantfileを作成する。
$ vagrant init chef/centos-6.5
A `Vagrantfile` has been placed in this directory. You are now
ready to `vagrant up` your first virtual environment! Please read
the comments in the Vagrantfile as well as documentation on
`vagrantup.com` for more information on using Vagrant.

# 仮想マシンを起動する。初回のみローカルにBaseBoxのダウンロードを行います。
$ vagrant up
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Box 'chef/centos-6.5' could not be found. Attempting to find and install...
    default: Box Provider: virtualbox
    default: Box Version: >= 0
==> default: Loading metadata for box 'chef/centos-6.5'
    default: URL: https://atlas.hashicorp.com/chef/centos-6.5
==> default: Adding box 'chef/centos-6.5' (v1.0.0) for provider: virtualbox
    default: Downloading: https://atlas.hashicorp.com/chef/boxes/centos-6.5/versions/1.0.0/providers/virtualbox.box
==> default: Successfully added box 'chef/centos-6.5' (v1.0.0) for 'virtualbox'!
==> default: Importing base box 'chef/centos-6.5'...
==> default: Matching MAC address for NAT networking...
==> default: Checking if box 'chef/centos-6.5' is up to date...
==> default: Setting the name of the VM: centos6_default_1428464976181_88242
==> default: Clearing any previously set network interfaces...
==> default: Preparing network interfaces based on configuration...
    default: Adapter 1: nat
==> default: Forwarding ports...
    default: 22 => 2222 (adapter 1)
==> default: Booting VM...
==> default: Waiting for machine to boot. This may take a few minutes...
    default: SSH address: 127.0.0.1:2222
    default: SSH username: vagrant
    default: SSH auth method: private key
    default: Warning: Connection timeout. Retrying...
    default: 
    default: Vagrant insecure key detected. Vagrant will automatically replace
    default: this with a newly generated keypair for better security.
    default: 
    default: Inserting generated public key within guest...
    default: Removing insecure key from the guest if its present...
    default: Key inserted! Disconnecting and reconnecting using new SSH key...
==> default: Machine booted and ready!
==> default: Checking for guest additions in VM...
==> default: Mounting shared folders...
    default: /vagrant => /Users/shota/Vagrant/centos6

# マシンのステータスを確認します。
$ vagrant status
Current machine states:

default                   running (virtualbox)

The VM is running. To stop this VM, you can run `vagrant halt` to
shut it down forcefully, or you can run `vagrant suspend` to simply
suspend the virtual machine. In either case, to restart it again,
simply run `vagrant up`.

# 仮想マシンにアクセスします。
$ vagrant ssh

# いろいろ遊びます。

# マシンを出ます。
[vagrant@localhost ~]$ exit

# マシンを停止します。
$ vagrant halt
==> default: Attempting graceful shutdown of VM...

#削除したかったら削除します。
$ vagrant destroy
    default: Are you sure you want to destroy the 'default' VM? [y/N] y
==> default: Destroying VM and associated drives...

#

```


## 既存のBoxに手を加えてBoxを再生成
## Vagrantfileでのプロビジョニング
## webサーバとdbサーバを同時に作成、起動する
## 自分でBase Boxを作成する
	- Base Box を自分で作る理由
	- 作り方
		マニュアル
			http://momijiame.tumblr.com/post/77460699382/vagrant-virtualbox-base-box
		Box作成ツールを利用（VeeWee, Packer）
	- Packerを使ってBoxを作成してみる
			http://technica.speee.jp/480
## Atlasについて

ドキュメント

本家
https://docs.vagrantup.com/v2/
翻訳
https://github.com/shmori/server-share