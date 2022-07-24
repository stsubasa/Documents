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
|コンポジットノード|ビヘイビアツリーの「Selector」や「Sequence」といったノードの総称|
|ビヘイビアツリータスク|ビヘイビアツリーエディタの「新規タスク」から作成できるアセット<br>ブループリント関数アセットのようなもの。<br>ビヘイビアツリーにビヘイビアツリータスクを配置する|

---
## ■AI作成手順

|手順|画像|説明|
|:--:|:--|:--|
|1||ブラックボードアセット作成|
|2||ビヘイビアツリーアセット作成|
|3||ビヘイビアツリーの「BlackboardAsset」に（1）で作成したブラックボードを設定|
|4||AIControllerアセット作成|
|5||AIControllerのグラフで「On Possese」関数をオーバーライドして、下記のノードを繋いでいく<br><br>・「Use Blackboard」ノード<br>「Blackboard Asset」には、(1)で作成したブラックボードを設定<br>・「Run Behavia Tree」ノード<br>「BTAsset」には、（2）で作成したビヘイビアツリーを設定|
|6||Characterアセット作成|
|7||Characterの「ポーン」-「AI Controller Class」に（4）で作成したAIcontrollerを設定|
|8||あとは、ビヘイビアツリータスクなどで処理を作成して、ビヘイビアツリーを組み上げていく|

### ■ビヘイビアツリータスク
<details><summary>ビヘイビアツリータスクの作り方</summary>

|手順|画像|説明|
|:--:|:--|:--|
|1|![](.\image\BehaviorTreeTask_01.png)|ビヘイビアツリーエディターの「新規タスク」から「BTTask_BlueprintBase」を選択|
|2|![](.\image\BehaviorTreeTask_02.png)|ビヘイビアツリータスクの名前を入力して「決定」を押す|
|3|![](.\image\BehaviorTreeTask_03.png)|(2)で作成したビヘイビアツリータスクを開き、ブラックボードの変数と紐づける為のキー用の変数を作成する<br>変数の型は「Blackboard Key Selector」とし<br>「インスタンス編集可能」を有効にしておく<br>※編集可能にしておかないと、ビヘイビアツリーで変数にアクセスできません）|
|4|![](.\image\BehaviorTreeTask_04.png)|ビヘイビアツリータスクのグラフで「Recieve Execute AI」関数をオーバーライドし、このタスクの処理を書いていく<br>ブラックボードの値にアクセスする際は「Set Blackboard Value as XXX」や「Get Blackboard Value as XXX」を使用し<br>ノードの「Key」には(3)で作成した変数を繋ぐ|
|5|![](.\image\BehaviorTreeTask_05.png)|タスクの最後に「Finish Execute」ノードを接続する<br>「Success」がtrueを返すとビヘイビアツリーが次のタスクに進みます|
|6|![](.\image\BehaviorTreeTask_06.png)|再びビヘイビアツリーエディターに戻り、コンポジットノードの下側をドラッグして(2)で作成したビヘイビアツリータスクのノードを作成します|
|7|![](.\image\BehaviorTreeTask_07.png)|作成したビヘイビアツリータスクのノードを選択し、(3)で作成した変数にブラックボードの変数を設定する|

</details>

## ■トラブルシューティング
|不具合|試す事|
|:--|:--|
|ターゲットの位置に移動しない|ナビゲーションが途切れている可能性<br>接地している場合、ナビゲーションが埋まる程度に浮かせて移動するようになるか試す|