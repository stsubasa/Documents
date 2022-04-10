# ■WorldPartition
<div style="text-align: right;">記述：2022/04/10</div>
<div style="text-align: right;">バージョン：UE5.0.0</div>

---
## ■概要
自動データ管理および距離ベースのレベルストリーミングシステム

---
## ■参考URL
[ワールドパーティション](https://docs.unrealengine.com/5.0/en-US/world-partition-in-unreal-engine/)

[UE5移行ガイド - ワールドパーティションへの変換](https://dev.epicgames.com/community/learning/talks-and-demos/J5q/upgrading-your-project-to-ue5)

---
## ■ワールドパーティションの設定手順
|手順|画像|説明|
|:--:|:--|:--|
|1|![](.\image\WorldPartition_00.png)|レベルアセットを作成する|
|2|![](.\image\WorldPartition_01.png)|Unrealエディターのメニューから「ツール」→「レベルを変換」を選択|
|3|![](.\image\WorldPartition_02.png)|「アセットダイアログ」で変換したいレベルアセットを選択|
|4|![](.\image\WorldPartition_03.png)|変換設定を行い「OK」を選択<br>**<font color=red>設定項目については、後述する■レベル変換の設定一覧を参照</font>**|
|5|![](.\image\WorldPartition_04.png)|メッセージウィンドウが表示され「変換完了」となっていれば変換成功|
|6|![](.\image\WorldPartition_05.png)|レベルのワールドパーティションを有効にする為、Unrealエディターのメニューから「ウィンドウ」→「ワールドセッティング」を選択|
|7|![](.\image\WorldPartition_06.png)|ワールドセッティングの「ワールドパーティション」→「Enable Streaming」を有効にする|

---
### ■レベル変換の設定一覧
|項目|説明|
|--:|:--|
|InPlace|デフォルトは無効<br>・無効の場合、変換したレベルアセットは"元アセット名_WP"として別アセットが作成される<br>例）"LV_World.umap"→"LV_World_WP.umap"<br>・有効の場合、変換対象のレベルアセットをそのまま上書きする|
|Commandlet Class||
|Delete Source Levels||
|Generate Ini||
|Report Only|変換は行わず、変換した際のワーニングやエラーを表示する|
|Verbose||
|Skip Stable GUIDValidation||
|Only Merge Sub levels||
|Save Foliage Type to Content Folder||