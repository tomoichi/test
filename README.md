# 本ソースのビルド方法（伊藤様側と今後合わせる）
## 1. debianイメージのビルド
[Varisciteのサイト](https://variwiki.com/index.php?title=Debian_Build_Release&release=mx8mm-debian-bullseye-5.4-2.1.x-v1.3)を参考に実施

#### 1. 実行に必要なパッケージをaptを使ってインストール。
```
sudo apt-get install binfmt-support qemu qemu-user-static debootstrap kpartx \ 
lvm2 dosfstools gpart binutils bison git lib32ncurses5-dev libssl-dev gawk wget \ 
git-core diffstat unzip texinfo gcc-multilib build-essential chrpath socat \
libsdl1.2-dev autoconf libtool libglib2.0-dev libarchive-dev xterm sed cvs \
subversion kmod coreutils texi2html bc docbook-utils help2man make gcc g++ \ 
desktop-file-utils libgl1-mesa-dev libglu1-mesa-dev mercurial automake groff curl \ 
lzop asciidoc u-boot-tools mtd-utils device-tree-compiler flex cmake zstd udisks2 \ 
python3-git python3-m2crypto python3-pyelftools
```
#### 2. Gitを使用してソースを取得。※gitは本プロジェクト用から取得する
```
git clone https://github.com/projectlucas/lucas_device_os
```
#### 3. 以下のコマンドでビルドが開始される(2H以上かかる場合がある)。
```
cd cd lucas_device_os/debian_imx8mm-var-dart-lucas/
```
#### 4. ソースをダウンロードする。
```
MACHINE=imx8mm-var-dart ./var_make_debian.sh -c deploy
```
#### 5. いずれかでビルド
```
開発用rootfsでビルド（今まで通り）
sudo MACHINE=imx8mm-var-dart ./var_make_debian.sh -c all |& tee build.log
```
または

```
ターゲット用rootfsでビルド
sudo MACHINE=imx8mm-var-dart ./var_make_debian.sh -c all -t target |& tee build.log
```

## 2. 開発用とターゲット用の呼び出しスクリプトの違い
開発用　　　：variscite/weston_rootfs.sh

ターゲット用：variscite/weston_rootfs_runtime.sh

