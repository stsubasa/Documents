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
## ■ワールドパーティションレベルの作り方

<details><summary>新規レベルをワールドパーティションレベルとして作成</summary>

|手順|画像|説明|
|:--:|:--|:--|
|1|![](.\image\WorldPartition_Create_00.png)|Unrealエディターのメニューから「ファイル」→「新規レベル」を選択|
|1|![](.\image\WorldPartition_Create_01.png)|「新規レベル」ウィンドウで、「Open World」か「オープンワールドを空にします」を選択して「作成」<br>【オープンワールドを空にします】<br>ワールドパーティションに必要な「WorldDataLayers」と「WorldPartitionMiniMap」のみが配置されたレベルを作成します。<br>【Open World】<br>「オープンワールドを空にします」に加えて「ランドスケープ」も配置されたレベルを作成します。|

</details>

<details><summary>既存のレベルをワールドパーティションレベルに変換</summary>

|手順|画像|説明|
|:--:|:--|:--|
|1|![](.\image\WorldPartition_00.png)|レベルアセットを作成する|
|2|![](.\image\WorldPartition_01.png)|Unrealエディターのメニューから「ツール」→「レベルを変換」を選択|
|3|![](.\image\WorldPartition_02.png)|「アセットダイアログ」で変換したいレベルアセットを選択|
|4|![](.\image\WorldPartition_03.png)|変換設定を行い「OK」を選択<br>**<font color=red>設定項目については、後述する[■レベル変換の設定一覧](#■レベル変換の設定一覧)を参照</font>**|
|5|![](.\image\WorldPartition_04_0.png)<br>![](.\image\WorldPartition_04_1.png)|メッセージウィンドウが表示され「変換完了」となっていれば変換成功<br>変換したレベルのアウトライナーに下記の2つのアクターが追加されます<br>・WorldDataLayers<br>・WorldPartitionMiniMap|
|6|![](.\image\WorldPartition_05.png)|レベルのワールドパーティションを有効にする為、Unrealエディターのメニューから「ウィンドウ」→「ワールドセッティング」を選択|
|7|![](.\image\WorldPartition_06.png)|ワールドセッティングの「ワールドパーティション」→「Enable Streaming」を有効にする|
|8|![](.\image\WorldPartition_07.png)|ワールドセッティングの「ワールドパーティション」→「Cell Size」と「Loading Range」を設定する<br><br>【Cell Size】<br>1セルのサイズ（X,Y）。単位はcm。<br>画像の場合は128平方メートルとなる<br><br>【Loading Range】<br>ロードを始める距離。こちらも単位はcm<br><br>**<font color=red>※それぞれの値はゲームにあった数値を設定する必要があります</color>**|

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
</details>

---
## ■ワールドパーティションの設定

---
## ■アクターの配置とセル割り当て

<details><summary>アクターの配置</summary>

|手順|画像|説明|
|:--:|:--|:--|
|1|![](.\image\WorldPartition_PlaceAndCells_00_00.png)<br>![](.\image\WorldPartition_PlaceAndCells_00_01.png)|Unrealエディターのメニューから「ウィンドウ」→「ワールドパーティションエディタ」を選択|
|2|![](.\image\WorldPartition_PlaceAndCells_01_00.png)<br>![](.\image\WorldPartition_PlaceAndCells_01_01.png)|レベルに適当なアクターを座標（0,0）に配置して保存すると、「ワールドパーティション」ウィンドウにセルが追加されます<br><font color=red>赤</font>と<font color=Green>緑</font>の十字の交差地点が座標（0,0）となります<br>今回は座標（0,0）に配置したため、セルが4つ追加されています|
|3|![](.\image\WorldPartition_PlaceAndCells_02_00.png)|レベルにもう一つ適当なアクターを座標（200,200）に配置して保存します<br>この時点では「ワールドパーティション」に変化はないハズです|
|4|![](.\image\WorldPartition_PlaceAndCells_03_00.png)|次に「ワールドパーティション」ウィンドウで、右下のセルを選択した状態で右クリックし、「選択したセルをアンロード」を選択します|
|5|![](.\image\WorldPartition_PlaceAndCells_04_00.png)|すると、右下のセルに含まれている（3）で追加したアクターがアウトライナー上で「アンロード済み」となり、レベルビュー上でも非表示になります|
|6|![](.\image\WorldPartition_PlaceAndCells_05_00.png)|（5）でアンロードしたセルを再び右クリックメニューからロードしたら、（3）で追加したアクターを座標（13000,200）に移動させて保存してください。<br>すると「ワールドパーティション」ウィンドウにセルが追加されたかと思います|

</details>