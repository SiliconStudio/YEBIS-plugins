# YEBIS for Unity Document

[![](http://www.siliconstudio.co.jp/en/products-service/yebis/images/index_il001b.png)](http://www.siliconstudio.co.jp/middleware/yebis/en/)

- [YEBIS for Unity Document](#yebis-for-unity-document)
- [概要](#abstruct)
- [YEBISプラグインの適用](#YEBIS_apply)
- [YEBISプラグインのパラメータ設定](#YEBIS_setting)
	- [YEBISプラグインの機能全般の設定](#YEBIS_setting_general)
	- [トーンマップの設定](#YEBIS_setting_Tonemap)
	- [グレアの設定](#YEBIS_setting_Tonemap)
	- [被写界深度の設定](#YEBIS_setting_DoF)
	- [レンズシミュレーションの設定](#YEBIS_setting_LensSim)
	- [モーションブラーの設定](#YEBIS_setting_MotionBlur)
	- [SSAO（Screen Space Ambient Occlusion）の設定](#YEBIS_setting_SSAO)
	- [色調変換の設定](#YEBIS_setting_ColorCorrection)
	- [フィードバックエフェクトの設定](#YEBIS_setting_FeedbackEffect)


# <a name="abstruct"> 概要
|YEBIS適用前|YEBIS適用後|
|---|---|
|![](figure/beforeYEBIS.png)|![](figure/afterYEBIS.png)|

YEBIS for Unityは、ポストエフェクトライブラリ「YEBIS」を利用したUnity用のプラグインです。  
Unityでレンダリングしたシーンに「YEBIS」のポストエフェクトをかけることができます。

> 「YEBIS」の光の効果やピンボケ等の高品質な画像処理エフェクトをポストエフェクトと呼びます。

# <a name="YEBIS_apply"> YEBISプラグインの適用
## Componentの追加
1. プロジェクトにYEBIS.unitypackageをインポート  
"Assets" > "Inport Package" > "Custom Package..." > "YEBIS.unitypackage"  
[<img src="figure/applyYEBIS_add1.png" width="200pt">](figure/applyYEBIS_add1.png)
1. HierarchyよりMainCameraを選択
1. Yebisプラグインを追加  
"Component" > "YEBIS" > "YebisPostEffects"  
[<img src="figure/applyYEBIS_add2.png" width="200pt">](figure/applyYEBIS_add2.png)
1. InspectorからYebisPostEffectsのチェックボックスをONにする

## Graphics APIの設定
YEBIS for Unity 評価版では利用可能なGraphics APIは以下の通りです。
- OpenGL2 (WindowsPC)
- OpenGLES3 (Android/iOS)
- OpenGLES2 (Android/iOS)

### Windows版でのGraphics APIの設定
1. PlayerSettingsを開く  
"Edit" > "Project Settings" > "Player"
1. "Auto Graphics API for Windows"のチェックボックスを外す  
”PC, Mac & Linux　Standalone Settings” > "Auto Graphics API for Windows"
1. ”＋”を押して”OpenGL2”を選択し,ドラッグをしてGraphics API上部に配置  
[<img src="figure/applyYEBIS_GL2.png" width="300pt">](figure/applyYEBIS_GL2.png)

### Android,iOS版でのGraphics APIの設定
1. PlayerSettingsを開く  
"Edit" > "Project Settings" > "Player"
1. "Auto Graphics APIs"のチェックボックスを外す  
”Android Settings” or "iOS Settings" > "Auto Graphics APIs"
1. ”＋”を押して”OpenGLES3”,もしくは”OpenGLES2”を選択し,ドラッグをしてGraphics API上部に配置  
[<img src="figure/applyYEBIS_GLES.png" width="300pt">](figure/applyYEBIS_GLES.png)

> OpenGLES2を利用した場合,一部ポストエフェクトが制限されています。  

## HDRレンダリング
![](figure/applyYEBIS_HDR.png)
- UnityのMain CameraのHDRが有効化されていると,YEBIS内部のポストエフェクトもHDRモードとなり,クォリティが向上します。
- OpenGLES2ではYEBIS内部のHDRモードは無効化されます。
	- OpenGLES3でも16bit浮動小数点テクスチャに未対応のデバイスの場合はYEBISのHDRモードは無効化されます。
- HDRモードとLDRモードではポストエフェクトの値(例:グレアの明るさ)の表現が異なるものとなります。  
そのため,利用するデバイスに合わせてMain CameraのHDRを有効化してからYEBISのパラメータを設定してください。

# <a name="YEBIS_setting"> YEBISプラグインのパラメータ設定
[<img src="figure/UI_all.png" width="300pt">](figure/UI_all.png)
## <a name="YEBIS_setting_general"> YEBISプラグインの機能全般の設定
![](figure/UI_general.png)
### YEBISプラグインのポストエフェクトの有効化
- 「YEBISの有効化（Enable YEBIS）」をチェックしてYEBISプラグインのポストエフェクトを有効化します。

### フルスクリーンアンチエイリアスの有効化
- 「FXAAの有効化（Enable FXAA）」をチェックしてフルスクリーンアンチエイリアスを有効化します。

## <a name="YEBIS_setting_Tonemap"> トーンマップの設定
![](figure/UI_Tonemap.png)
### 露出値の設定
- 「自動露出調整（Auto Exposure）」のチェックをはずします。
- 「露出値（Exposure）」の値を変更して、露出値を直接設定できます

### 自動露出調整の有効化
- シーンのレンダリング画像の明るさを自動調節することができます。
- 「自動露出調整（Auto Exposure）」をチェックして自動露出調整を有効化します。
- 「自動露出の明るさ（Middle Gray）」の値を変更して、自動露出調整の目標とする画面の明るさを設定できます。
- **GLES2では無効**


## <a name="YEBIS_setting_Glare"> グレアの設定
![](figure/UI_Glare.png)
### グレアの有効化
- 「グレアの有効化（Enable Glare）」をチェックしてグレアを有効化します。
- 「品質（Quality）」の値を高くするほど品質の高いグレア表現が可能になります

### グレアの形状の変更
- 「形状（Shape）」からプリセットされたグレア形状を選択します。

                            タイプ | グレア形状
 --------------------------------- | ----------------------------------------------------------------------------------
 PFXGS_DISABLE                     | グレア無効
 PFXGS_BLOOM                       | ブルームのみ
 PFXGS_LENSFLARE                   | ブルーム,ゴースト（レンズフレア）,残像を含んだタイプ<br/>_**GLES2では無効**_
 PFXGS_STANDARD                    | 基本的な要素を全てバランス良く含んだタイプ
 PFXGS_CHEAPLENS                   | くっきりしたゴーストを含む、安価なレンズの表現
 PFXGS_FILTER_CROSSSCREEN          | クロススクリーンフィルタ. 十字型の光芒発生器を装着したレンズ
 PFXGS_FILTER_CROSSSCREEN_SPECTRAL | 分散の強いクロススクリーンフィルタ. 分散の強い十字型の光芒発生器を装着したレンズ
 PFXGS_FILTER_SNOWCROSS            | スノークロスフィルタ. 六方向の光条発生器を装着したレンズ<br/>_**GLES2では無効**_
 PFXGS_FILTER_SNOWCROSS_SPECTRAL   | 分散の強いスノークロスフィルタ. 分散の強い六方向の光条発生器を装着したレンズ<br/>_**GLES2では無効**_
 PFXGS_FILTER_SUNNYCROSS           | サニークロスフィルタ. 八方向の光条発生器を装着したレンズ<br/>_**GLES2では無効**_
 PFXGS_FILTER_SUNNYCROSS_SPECTRAL  | 分散の強いサニークロスフィルタ. 分散の強い八方向の光条発生器を装着したレンズ<br/>_**GLES2では無効**_
 PFXGS_HORIZONTALSTREAK            | 水平フレア. 水平方向に強い光条を持つタイプ. アナモルフィックレンズの簡易表現
 PFXGS_VERTICALSTREAK              | 垂直フレア. 垂直方向に強い光条を持つタイプ. CCDカメラのスミア表現

### グレアの明るさの変更
- 「輝度（Luminance）」の値を変更して、グレア全体の輝度を設定することができます。

### グレアの発生源の制御
- 「高輝度抽出の閾値（Threshold）」で指定した値よりも明るいピクセルのみ抽出され、グレアを発生します。
- **GLES2では無効**

### グレアの効果の強調
- 「非線形マッピング（RemapFactor）」の値を変更して、グレアの輝度成分を非線形に伸張（または圧縮）マッピングすることができます。
- 自然な輝度の計算ではありませんが、見た目の効果を強調することができます。
- **GLES2では無効**

### ライトシャフトの有効化
- 「グレアの有効化（Enable Glare）」と「ライトシャフトの有効化（Light Shaft）」をチェックしてライトシャフト（ゴッドレイとも呼ばれます）を有効化します。
- **GLES2では無効**

### ライトシャフトの光源位置の制御
- 「ライトシャフトの位置(Position)」で光源にしたいオブジェクトのTransformを選択します。
- 接続したオブジェクトのスクリーン上の位置を光源とするライトシャフトが表示されます。
- **GLES2では無効**

### ライトシャフトの効果の制御
- 以下のパラメータでライトシャフトの見た目を調整することができます。
- パラメータリファレンスの各パラメータの説明も参照してください。
    - 光源の色（Color）
    - 光芒の長さ（Length）
    - グレアの影響度（Glare Ratio）
    - 遮蔽マスクの距離（Mast Threshold）
    - 角度減衰率（Angle Attenuation）
    - 乱数マスクの強さ（Noise Mask）
    - 乱数マスクの細かさ（Noise Frequency）
    - 回折リングの強さ（Diffraction Ring）
    - 回折リングの角度（Diffraction Ring Radius）
    - 回折リングの減衰率（Diffraction Ring Attenuation）
    - 回折リングの方向（Diffraction Ring Order）
    - リング以外の色（Outer Color）
- **GLES2では無効**

## <a name="YEBIS_setting_DoF"> 被写界深度の設定
![](figure/UI_DoF.png)
### 被写界深度エフェクト（ピンボケ）の有効化
- 「被写界深度エフェクト（Enable Dof）」をチェックして被写界深度効果を有効化します。
- 「品質（Quality）」の値を高くするほど品質の高いボケ表現が可能になります。
- デバイスによって品質の上限値は異なります。
- 「絞り羽根フィルタ（Aperture Shape）」からカメラの絞りフィルタの種別を選択します。
	- **GLES2では無効**

### ボケ具合の制御
- 「フィルムサイズ（Film Size）」の値を変更して感光素子（フィルム、デジタルカメラのイメージセンサに相当）の縦サイズを設定します。
- 「フィルムサイズ（Film Size）」の値はシーンの作業単位で設定します。
    - Unityでは物理係数やモデルデータのデフォルト設定の作業単位として一般に1メートルが利用されます。
    - Unityの作業単位（スケール）はユーザーが自由に設定できますので、作業中のシーンの縮尺に合わせて換算した値を設定します。
    - 例えば35mmフィルムの縦サイズである24mmを設定する場合、シーンの作業単位がcmであれば2.4(cm)を設定します。
- 「絞りのＦナンバー（Aperture F-number）」の値を変更して絞りのＦナンバーを設定します。

### オートフォーカスの有効化
- 「オートフォーカス（Auto Focus）」をチェックしてオートフォーカスを有効化します。
- **GLES2では無効**

### フォーカス距離の手動設定
- 「オートフォーカス（Auto Focus）」のチェックをはずします。
- 「フォーカス距離（Focus Distance）」の値を変更して、フォーカス距離を直接設定することができます。

## <a name="YEBIS_setting_LensSim"> レンズシミュレーションの設定
![](figure/UI_LensSim.png)
- **GLES2では無効**  

### レンズディストーションの有効化
- 「歪曲収差（Lens Distortion）」をチェックしてレンズディストーションを有効化します。

### アナモルフィックレンズ効果の有効化
- 「アナモルフィックレンズ（Anamorphic Lens）」をチェックしてアナモルフィックレンズの効果を有効化します。
- 画面の歪みやグレアの形状など、アナモルフィックレンズ特有の効果が有効になります。

### 擬似的な周辺減光エフェクトの設定
- 「周辺減光エフェクト（Vignette Mode）」を「Vignette Effect」に設定します。
- 「光量低下の強度（Vignette Intensity）」の値を変更して、画面中央から離れるほど露出が落ちる周辺光量低下エフェクトの強さを設定します。

### 周辺減光の光学的なシミュレーションの設定
- 「周辺減光エフェクト（Vignette Mode）」を「Vignette Simulation」に設定します。
- 「コサインn乗（Power of Cosine）」の値を変更して、コサイン4乗則による減光シミュレーションを設定します。一般的なレンズでは0.5～1.0の値を設定します。
- 「イメージサークル（Image Circle）」の値を変更して、画像が明るく映る範囲のおおよその直径を設定します。画面の高さを1.0とした比率で設定します。
    - （より正確な説明）口径食を原因とする周辺減光により、輝度が半分まで落ちる円の直径を設定します。
- 「半影の広さ（Penumbra Width）」の値を変更して、イメージサークルで明るい領域と暗い領域の境界にできる半影部分の帯の広さを設定します。1.0を設定すると半影部分は画面の中央まで届く幅になります。
- 「ピンボケに対する口径食（Optical Vignetting）」をチェックして口径食のシミュレーションを有効化します。レモンボケ、キャッツアイエフェクト等とも呼ばれます。

## <a name="YEBIS_setting_MotionBlur"> モーションブラーの設定
![](figure/UI_MotionBlur.png)
- **GLES2では無効**  

### モーションブラーの有効化
- 「モーションブラーの有効化（Enable Motion Blur）」をチェックしてモーションブラーを有効化します。

### モーションブラーのシャッター角度の設定
- 「時間比（Blur Time Ratio）」の値を変更して、1フレームあたりのシャッター開放時間の比率を設定します。1.0を設定すると、シャッター角度360度に相当するモーションブラーが発生します。

### モーションブラーの長さの調節
- 「最大の長さ（Max Blur Length）」の値を変更して、モーションブラーの最大の長さを制限することができます。画面の高さを1.0とした比率で設定します。

## <a name="YEBIS_setting_SSAO"> SSAO（Screen Space Ambient Occlusion）の設定
![](figure/UI_SSAO.png)
- **GLES2では無効**

### SSAOの有効化
- 「SSAOの有効化（Enable SSAO）」をチェックしてSSAOを有効化します。

### SSAOの効果の設定
- 「サンプル数（Samples）」の値を変更して、SSAOのサンプル数を設定します。値を大きくするとSSAOの品質は高くなります。16～25程度の値が高速で無難な結果になります。
- 「サンプル半径（Sample Radius）」の値を変更して、SSAOのサンプルの物理半径を設定します。
- 「サンプル半径（Sample Radius）」の値はシーンの作業単位で設定します。
- 大きな値を設定するほど広い範囲を解析しますが、サンプリングはその分まばらになるため正確な判定が難しくなります。
- 「強さ（Scale）」の値を変更して、SSAOのかかり方の強さを設定します。0.0を指定するとSSAOは無効になります。
- 「コントラスト（Contrast）」の値を変更して、SSAOのかかり方のコントラストを設定します。0.0を指定するとSSAOは無効になります。

## <a name="YEBIS_setting_ColorCorrection"> 色調変換の設定
![](figure/UI_ColorCorrection.png)
### 色相の設定
- 「色相（Hue）」の値を変更して色相変換を設定します。

### 彩度の設定
- 「彩度（Saturation）」の値を変更して彩度変換を設定します。

### コントラストの設定
- 「コントラスト（Contrast）」の値を変更してコントラスト変換を設定します。

### 明度の設定
- 「明度（Brightness）」の値を変更して明度変換を設定します。

### セピア調の効果
- 「セピア調変換（ToneEffect）」の値を変更してセピア調変換のかかり方の強さを設定します。

### 色温度の設定
- 「色温度（Temperature）」の値を変更して色温度をケルビン度で設定します。

### ホワイトバランスの設定
- 「ホワイトバランス（White Balance）」の値を変更してホワイトバランスの補正目標の色温度をケルビン度で設定します。

### ガンマ補正の設定
- 「ガンマ補正（Gamma Value）」の値を変更してガンマ補正を設定します。
- **GLES2では無効**


## <a name="YEBIS_setting_FeedbackEffect"> フィードバックエフェクトの設定
![](figure/UI_FeedbackEffect.png)
- フィードバック画像（前フレームまでの残像）を利用したエフェクトを設定することができます。
- **GLES2では無効**

### フィードバックエフェクトの有効化
- 「フィードバックエフェクトの有効化（Feedback Effects）」をチェックしてフィードバックエフェクトを有効化します。

### フィードバックエフェクトの強さの設定
- 「強さ（Feedback Weight）」の値を変更して、フィードバック画像の重みを設定します。

### フィードバックエフェクトの回転の設定
- 「回転（Feedback Rotation）」の値を変更して、フィードバック画像の回転を設定します。

### フィードバックエフェクトのスケーリングの設定
- 「スケーリング（Feedback Scaling）」の値を変更して、フィードバック画像のスケーリングを設定します。

### フィードバックエフェクトの色相の設定
- 「色相（Feedback Hue）」の値を変更して、フィードバック画像の色相変換を設定します。

### フィードバックエフェクトの彩度の設定
- 「彩度（Feedback Saturation）」の値を変更して、フィードバック画像の彩度変換を設定します。

### フィードバックエフェクトのコントラストの設定
- 「コントラスト（Feedback Contrast）」の値を変更して、フィードバック画像のコントラスト変換を設定します。

### フィードバックエフェクトの明度の設定
- 「明度（Feedback Brightness）」の値を変更して、フィードバック画像の明度変換を設定します。


-----

<div align="center">

    <a href="http://www.siliconstudio.co.jp/en/" target="_blank">
    <img src="http://www.siliconstudio.co.jp/common/images/logo001.svg" width="200" border="0" alt="yebis_logo" hspace="5" /></a><br>

<br>
(c)Silicon Studio Corp., all rights reserved.
</div>
