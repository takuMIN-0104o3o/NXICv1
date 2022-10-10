# NXIC
NX Input Converterとは,キーボード・マウスの入力をRaspberry piを通じてPro Controllerの入力に変換するPythonプログラムです.
<!-- マウスの動きでジャイロ操作の他,ボトル・パブロ用の連打も実装しています. -->

## 本家を元にマウス G403 向けに変更しています。
- xy_offset を 0 から 3 に変更等
- 65535 以上の感度を検知した時の挙動修正

## 操作方法
デフォルトでは以下の操作に変換されます.

![image](https://user-images.githubusercontent.com/20591351/194798467-49783a53-4885-420e-9c14-cc8621d646ff.png)![2022-10-10_12h58_52](https://user-images.githubusercontent.com/20591351/194797893-f78976f2-d0f7-45a0-a9e1-5deb4ae73451.png)

## 使い方
1. ラズパイ4 に RasberryPi OS (64bit) をインストールします。

2. セットアップ

2.1 ログインして以下コマンドを実行
```
echo "dtoverlay=dwc2" | sudo tee -a /boot/config.txt
echo "dwc2" | sudo tee -a /etc/modules
echo "libcomposite" | sudo tee -a /etc/modules
sudo python -m pip install joycon-python hid pyglm keyboard
sudo apt install git -y
sudo git clone https://github.com/sakkuntyo/NXIC.git /root/NXIC
```

3. 起動方法

3.1 ラズパイを Switch からの電源で起動する

3.2 マウス、キーボードの順番で接続

3.3 次のコマンドを実行
```
sudo /root/NXIC/add_procon_gadget.sh
sudo /usr/bin/python /root/NXIC/NXIC.py
```
4. マウスで操作できる様になっているハズ

## 自動起動
1. 次のコマンドを実行
```
echo "@reboot root /root/NXIC/add_procon_gadget.sh;/usr/bin/python /root/NXIC/NXIC.py" | sudo tee /etc/crontab
```

2. ラズパイ4 を 黒い USB ジャック(USB2.0) が左に来る様に置いた状態で

青い USB ジャック (USB3.0) に上がマウス、下がキーボードとなる様に接続

3. Switch から給電され、OS が起動すると自動的にマウスとキーボードがコントローラになります。
OS の起動に時間がかかるのでうまくいっても20秒程度要します。

## 接続例
![2022-10-10_13h53_51](https://user-images.githubusercontent.com/20591351/194801434-8db6e71b-c764-47fd-9e91-8558aec67ea0.png)

## 注意点
ラズベリーパイ 3 では非対応 (USB Gadget API に非対応)

ラズベリーパイ 4 を使っています

### DEMO
![demo](https://github.com/sakkuntyo/NXIC/blob/main/nxic-sakkuntyo.gif)
https://www.youtube.com/watch?v=p048VY5oUCk
#### すぺしゃるさんくす
[mzyy94](https://www.mzyy94.com/blog/2020/03/20/nintendo-switch-pro-controller-usb-gadget/)

[Bokuchin](https://qiita.com/Bokuchin/items/7fee2c6a04c97dde29b4)

[mizuyoukanao](https://note.com/gamewagashi/n/n47ee6a6cf337)
