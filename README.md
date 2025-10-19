https://github.com/user-attachments/assets/da629734-6ea7-4b88-82e1-12630bc480f9

※GUIのスライダーからキャラのサイズや走る速度、立方体の重さや大きさを変更している

※UMGは共通だが、キャラと立方体それぞれのBPからUIコンポーネントは生成されている

# 実現したいこと

PJ毎のUMGを準備なしで、プラグアンドプレイな感じで簡単にGUIを追加

（Touch DesignerやOpenFrameworksのように、UIを強く意識せずにゲーム内でパラメータをコントロールしたい）

※ユースケースとしてはVJやAudioVisualのような映像表現の場を想定しています

※将来的にはlevel variantやOSCと連動させたい

# できること

- 機能１：表示やコントロールしたいBP内にいくつかノードを追加するだけで利用できる
- 機能２：異なるBPから共通のUMGにGUIを追加できる
- 機能３：BP内のテキスト情報や変数をGUIとして表示できる
- 機能４：BP内の変数をコントロールするスライダーを表示しインタラクションできる

# 使い方

1. プラグイン「UMG Viewmodel」をインポート
    
    ※Beta版のためdependencyとして設定できませんでした。必ず事前にインストールしてください
    
2. プラグイン「EasyGUI」をインポート
3. BP_EasyGUIをレベル上に配置（以降は触らない）
4. GUIでコントロールしたいActorにInterfaceを設定
    - ClassSettingsからBPI_EZG_ReflectValueFromUIを追加
      
        <img width="673" height="701" alt="image" src="https://github.com/user-attachments/assets/f5669a37-13d0-453b-a95a-50595921573a" />
 
5. EventBeginPlayで表示したいGUIを呼び出して変数化
    - テキストを表示する場合はEZG_Textを利用：
        1. 初期化：
            - Easy_GUI_Textを呼び出し初期値を設定する（更新する場合は変数化しておく）
              
                <img width="769" height="185" alt="image1" src="https://github.com/user-attachments/assets/8ee5d84e-48bd-49da-8c72-89cad0d7c719" />

        2. 更新：
            - 変数を呼び出しSet Stringから文字列を設定する
              
                <img width="540" height="246" alt="image4" src="https://github.com/user-attachments/assets/e07cbab9-d289-4e9f-8519-8e578c6eb4f6" />
                
    - 数値を表示する場合はEZG_Float:を利用
        1. 初期化：
            - Easy_GUI_Floatを呼び出し初期値を設定し、変数化する
              
                <img width="791" height="221" alt="image5" src="https://github.com/user-attachments/assets/813df6ff-eb24-4204-8841-8fbebc5aaa6a" />
               
        3. 更新：
            - 変数を呼び出しSet Floatから値を格納

                <img width="567" height="244" alt="image8" src="https://github.com/user-attachments/assets/a97083e8-b6ea-4f58-a304-193df5365110" />
                
    - スライダーを表示する場合はEZG_Sliderを利用:
        1. 初期化：
            - Easy_GUI_Sliderを呼び出し初期値を設定し、変数化する
              
                <img width="783" height="273" alt="image9" src="https://github.com/user-attachments/assets/43cfb1e7-ff21-441a-910b-e0072b67ec0b" />
                
        2. 更新：
            - インターフェースのイベント「ReflectFloat」をダブルクリックするとノードが追加されるので、変更したい変数をアサイン
            ※BPに対してSliderが１個の場合は、BPVM EZG Sliderノードは何も繋がなくて良い
                <img width="566" height="386" alt="image10" src="https://github.com/user-attachments/assets/e231be49-d91b-4d78-bb8c-d847163263cd" />

                <img width="816" height="288" alt="image11" src="https://github.com/user-attachments/assets/bb6ef46d-ca91-4584-b6a1-fdf2e3a6da8a" />
                    

# 環境
UE5.5.4で作成。他のバージョンでは未確認

もう少し詳しいことは以下にもまとめています。

https://www.notion.so/Plugin-EasyGUI-29140f731aea80bcbd6bc60cceb35564?source=copy_link
