# ■AI
<div style="text-align: right;">記述：2022/04/10</div>
<div style="text-align: right;">バージョン：UE5.0.0</div>

---
## ■注意事項
**<font color=red>※注意事項</font>**

---
## ■参考URL
[ビヘイビアツリーのクイックスタートガイド](https://docs.unrealengine.com/5.0/ja/behavior-tree-in-unreal-engine---quick-start-guide/)

---
## ■アセット概要
|アセット|説明|
|:--|:--|
|ブラックボード|ビヘイビアツリーからアクセス可能な変数の定義などを行う<br>※変数をActorとして定義する場合、「KeyType」を"Object"にしただけだとアクターとして使用できず、<br>折りたたまれている「BaseClass」を「Actor」に設定しないといけないので注意|
|ビヘイビアツリー|AIの試行順序などを決める|
|ビヘイビアツリータスク|ビヘイビアツリーエディタの「新規タスク」から作成できるアセット<br>ブループリント関数アセットのようなもの。<br>ビヘイビアツリーにビヘイビアツリータスクを配置する|

---
## ■AI作成手順

|手順|画像|説明|
|:--:|:--|:--|
|1||ブラックボードアセット作成|
|2||ビヘイビアツリーアセット作成|
|3||ビヘイビアツリーの「BlackboardAsset」に（1）で作成したブラックボードを設定|
|4||AIControllerアセット作成|
|5||AIControllerのグラフで「On Possese」関数をオーバーライドし「Run Behavia Tree」ノードを繋げる。<br>「RUn Behavia Tree」ノードの「BTAsset」に（2）で作成したビヘイビアツリーを設定|
|6||Characterアセット作成|
|7||Characterの「ポーン」-「AI Controller Class」に（4）で作成したAIcontrollerを設定|
|8||あとは、ビヘイビアツリータスクなどで処理を作成して、ビヘイビアツリーを組み上げていく|