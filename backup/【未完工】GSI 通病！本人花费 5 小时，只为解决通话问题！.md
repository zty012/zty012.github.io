## 前言

本人使用 Redmi 13G 5G，因为 MIUI 太卡，刷了 PixelOS GSI（GSI 是因为所有 ROM 都没有适配我的机型 air）。

刷完了发现能给别人打电话，但是别人打不进来电话，丸辣！

找了移动客服，无果。

## Google

搜不到。

## 学习

通过[百度百科](https://baike.baidu.com/item/%E7%BD%91%E7%BB%9C%E5%88%B6%E5%BC%8F/2677928#3-1)了解到，中国的三网都使用了 `TD-LTE` 制式。

## 实践

拨号盘输入 `*#*#4636#*#*` 进入网络设置，找到网络类型，诶？列表里怎么没有 `TD-LTE`？

## 退一步

中国移动 3G 使用 `TD-SCDMA`，正好列表里面有，改成这个试试！

## 移动网络被谁吃了？

卧槽，我 5G 摇身一边，变成 3G 了！？？

原来，网络类型里面，斜杠划分了多个制式，优先级从前往后，系统检测到了通话的 `TD-SCDMA` 但是没有检测到网络的 `LTE` 等类型，具体可以看列表上面的 `数据服务类型` 和 `语音网络类型`

## 突破口找到了！如何解决？

打开 MT，在 `/system` 中搜索文件内容 `GSM/WCDMA/LTE`，显然 `TeleService.apk` 符合各项条件，打开 dex 文件，显然在 `TelephonyShellCommand` 14687 行，写了一些通话类型的 bitmask 示例，在第二条注释中写道 `Reference the NetworkTypeBitMask`，继续在 dex 中搜索 `NetworkTypeBitMask`……搜不到？

## 已经不是 apk 里的问题了

接下来请出 唯 一 真 神——AOSP 源代码！

https://cs.android.com/