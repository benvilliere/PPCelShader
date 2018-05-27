Unreal Engine 4 ポストプロセス セルシェーダー
=======================================================
対応Ver UE 4.19.2


解説
------
UE4上でポストプロセスを使ってのセルシェーダー実装です。

過去に存在したポストプロセスによるその他のシェーダーと比較すると、


1.セルシェーディングに特化(セルルックらしさを追求)

2.余計な機能はほぼ持たない

3.柔軟な4種類のアウトライン描画

4.UE4標準のライトだけで調整可能(カラーもしっかり反映)

5.シャドウカラーやハイライトカラーの指定

6.Unlitマテリアルと遠距離メッシュは自動的にセルシェーダーから除外

7.Custom Depthで対象メッシュのみにセルシェーダーを適用するスイッチ

8.オプションとしてディフュージョンフィルターシェーダー


など、セルシェーダーとして必要最低限の機能を持ち合わせていながら、

誰でも非常に簡単に導入可能で、すぐにセルシェーダーが使えます。


基本的な使用方法
------------------
『PPI_CelShader』をPostprocessマテリアルとして追加してください。

https://docs.unrealengine.com/ja-JP/Engine/Rendering/PostProcessEffects/PostProcessMaterials

『PPI_CelShader』には様々なパラメーターが公開されていますので、自由に調整してください。
全てのパラメーターにポップアップ時の解説がついています。
『PPI_Diffusion』は必要に応じて追加してください。

実際に開いてもらうと、セルシェーダーが適用されたレベルを確認できますので、参考にしてください。


キャラクター側の調整
--------------------
キャラクターやアクター側のマテリアルではハイライトを検出する際には『スペキュラー』の値を使います。

テクスチャーマップでハイライト用のスペキュラー値が入ったものを用意すれば指定の場所のみにハイライトを出すことも可能です。

シャドウの場合にはマテリアルの『エミッシブ』の値を使うことで影の入る位置を調整することもできます。

エミッシブが1以上であればそこに影が落ちることはありません。上手く影を落としたい場合にはテクスチャーマップで影が落ちる位置を調整してください。


アウトライン
------------
4種類のアウトライン描画があります。

まず、『Depth Line』と『Normal Line』はメッシュのカメラ距離に関係なく一環したライン描画が行われます。

その分、細かいライン調整を行うことはできませんが、安定したライン描画を行うことができるようになっています。

『Edge Line』と『Crease Line』はメッシュのカメラ距離に大きく依存しますが、『Depth Line』や『Normal Line』では描画できない部分が調整可能です。

それぞれを必要に応じて使わない選択肢も可能ですので、調整してみて好みに応じて利用してください。


制限と注意事項
--------------
ポストプロセスによる実装なので、個別で適用するシェーダーと比較し、それなりに制限があります。

1.個別のシャドウカラーやハイライトカラーは調整できない

2.輝度が低いものは検出することができず、ライトにもある程度の強さが必要

3.煙のような半透明物は一切検出できないので、不透明で作成の必要あり

4.G-Bufferを利用したポストプロセスなので、モバイルなどのフォワードレンダリングでは使用不可

5.ゲーム向けに軽量化は考慮していない


ライセンス
-------------------------
完全なパブリックドメインとして公開します。

https://github.com/alwei/PPCelShader/blob/master/LICENSE


連絡先
------------------
Twitter : @aizen76

mail : altaizen76@gmail.com
