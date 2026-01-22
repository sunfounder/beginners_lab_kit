.. note::

    こんにちは、SunFounderのRaspberry Pi & Arduino & ESP32 Enthusiasts Communityへようこそ！Facebookで同じ趣味を持つ仲間と一緒に、Raspberry Pi、Arduino、ESP32についてさらに深く探求しましょう。

    **参加する理由**

    - **専門的なサポート**：購入後の問題や技術的な課題を、コミュニティとチームの助けを借りて解決します。
    - **学びと共有**：スキル向上のためのヒントやチュートリアルを交換します。
    - **独占プレビュー**：新製品発表や先行情報に早期アクセスできます。
    - **特別割引**：最新製品に対する特別割引を享受できます。
    - **イベントプロモーションとギブアウェイ**：ギブアウェイやホリデープロモーションに参加できます。

    👉 探索と創造の旅に出る準備はできましたか？[|link_sf_facebook|]をクリックして、今日参加しましょう！


7. 信号機を作ろう！
==============================

.. .. image:: img/5_traffic_light_pic.png
..     :width: 400
..     :align: center

このレッスンへようこそ。この魅力的なレッスンでは、理論的な概念と実際の応用を電子工学とプログラミングの両面で橋渡しします。私たちは、擬似コード（プログラミング言語の簡略化された形）を機能的なArduinoスケッチに変換するプロセスを探求します。この演習では、信号機の操作をシミュレートし、プログラミングと回路設計の実践的な経験を提供します。擬似コードを解釈し実装することで、コードを使用して電子デバイスを制御する背後にある論理を深く理解することができます。

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/7_traffic_light.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

このレッスンで学ぶこと:

* 電子回路の機能を計画するための擬似コードを書く方法と解釈する方法を学びます。
* 擬似コードをArduinoスケッチに変換して信号機のシミュレーションを制御します。
* LEDとArduinoボードを使用して信号機システムを構築し、プログラムします。

これらのスキルを習得することで、基本的な電子システムを設計、プログラム、トラブルシューティングする能力が身につき、より複雑なプロジェクトへの道が開かれます。

信号機の準備
------------------------------------------
こんにちは！Arduinoで自分だけの信号機を作る準備はできましたか？以下のものが必要です。

**必要なコンポーネント**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * 赤色LED
     - 1 * 黄色LED
     - 1 * 緑色LED
   * - |list_uno_r3| 
     - |list_red_led| 
     - |list_yellow_led| 
     - |list_green_led| 
   * - 1 * USBケーブル
     - 1 * ブレッドボード
     - 3 * 220Ω抵抗
     - ジャンパーワイヤー
   * - |list_usb_cable| 
     - |list_breadboard| 
     - |list_220ohm| 
     - |list_wire| 



**ステップバイステップの組み立て**

すべてをレゴセットのように組み立てましょう！

.. image:: img/7_traffic_light.png
    :width: 600
    :align: center

1. ブレッドボードに220Ω抵抗を接続します。片方の端を負極に、もう片方の端を1Bに差し込みます。

.. image:: img/7_traffic_light_resistor.png
    :width: 600
    :align: center

2. 緑色LEDをブレッドボードに追加します。LEDのアノード（長いリード）を1Fに、カソード（短いリード）を1Eに差し込みます。

.. image:: img/7_traffic_light_green.png
    :width: 600
    :align: center

3. 緑色LEDをジャンパーワイヤーでArduino Uno R3のピン3に接続します。ジャンパーワイヤーの一端を1Jに、もう一端をArduino Uno R3のピン3に差し込みます。

.. image:: img/7_traffic_light_pin3.png
    :width: 600
    :align: center

4. 別の220Ω抵抗を取り、片方の端を負極に、もう片方の端を6Bに接続します。

.. image:: img/7_traffic_light_yellow_resistor.png
    :width: 600
    :align: center

5. 黄色LEDを用意します。LEDのアノード（長いリード）を6Fに、カソード（短いリード）を6Eに差し込みます。

.. image:: img/7_traffic_light_yellow.png
    :width: 600
    :align: center

6. 黄色LEDをArduino Uno R3のピン4に接続します。

.. image:: img/7_traffic_light_pin4.png
    :width: 600
    :align: center

7. 赤色LEDを同じ方法で接続し、赤色LEDはArduino Uno R3のピン5に接続します。

.. image:: img/7_traffic_light_red.png
    :width: 600
    :align: center

8. うっかりしていましたが、回路をグラウンドに接続するのを忘れずに行いましょう。黒いワイヤーを使ってブレッドボードの負極側をArduino Uno R3のGNDピンに接続します。これで、すべてがセット完了です！

.. image:: img/7_traffic_light.png
    :width: 600
    :align: center

.. note::

    Arduino Uno R3にはGNDピンが3つあります。どのピンも同じように機能するので、どれでも使用できます。

これで、信号機のセットアップが完了しました！それぞれの色のライトは、R3上の独自のスイッチで制御され、車が止まる、待つ、または進むべきタイミングを教えてくれます。実際の信号機のように機能するものを作るのは素晴らしいことですよね！お疲れ様でした！

信号機のための擬似コードを書く
-------------------------------------------

LEDに役割を持たせる時が来ました。このアクティビティでは、交通量の多い交差点での交通の流れを制御する信号機としてプログラムします。

信号機は3色のライトを厳密な順序で切り替えるための正確な制御が必要であり、Arduinoプログラミングに取り組むための理想的なプロジェクトです。信号機を完璧にするためには、Arduinoにそのタスクを明確に指示する必要があります。

人間同士のコミュニケーションには、聞く、話す、読む、書く、ジェスチャー、または表情を使います。マイクロコントローラー（Arduinoボード上のもの）とのコミュニケーションには、コードを書くことが必要です。

自然言語で「信号機を作って」とArduinoに伝えることはできませんが、自然言語を使って「擬似コード」を書くことで、実際のArduinoコードの開発に役立てることができます。

.. note::
    
    擬似コードを書く際に正しい答えや間違った答えはありません。擬似コードが詳細であればあるほど、機能的なプログラムに変換するのが簡単になります。


回路が信号機のように機能するために必要なことを考えてみましょう。ログのスペースに、信号機がどのように動作するかを説明する擬似コードを書きましょう。

擬似コードを書く際のガイドとなる質問をいくつか示します：

* 複数のライトが同時に点灯する必要がありますか？
* ライトの順序はどうなっていますか？
* あるライトが点灯しているときに他のライトはどうなりますか？
* 3つ目のライトが消えた後はどうなりますか？
* 各ライトはどのくらいの時間点灯しますか？

擬似コードの例をいくつか示します：

.. code-block::

    1) すべてのLEDピンを出力に設定する。
    2) メインループを開始する。
    a) すべてのライトをオフにする。
    b) 緑色のライトを10秒間点灯する。
    c) すべてのライトをオフにする。
    d) 黄色のライトを3秒間点灯する。
    e) すべてのライトをオフにする。
    f) 赤色のライトを10秒間点灯する。
    3) ループの開始に戻る。

.. code-block::

    セットアップ：
        すべてのLEDピンを出力に定義する
    メインループ：
        緑色のライトを点灯する
        赤色と黄色のライトを消灯する
        10秒待つ
        黄色のライトを点灯する
        赤色と緑色のライトを消灯する
        3秒待つ
        赤色のライトを点灯する
        緑色と黄色のライトを消灯する
        10秒待つ

擬似コードには厳密な形式はなく、考えを明確にし、論理的に整理するためのものです。この論理的な順序はアルゴリズムと呼ばれます。
毎日、無意識のうちにアルゴリズムを使用しているかもしれません。レシピのようなもので、プログラミングではキーワードやコマンドが材料であり、調理手順がアルゴリズムです。
アルゴリズムは一連の手順や指示のことです。擬似コードからArduinoプログラミング言語に変換されると、Arduinoボードに具体的な指示を与えることができます。

.. note::
    
    擬似コードを書く際には、付箋やインデックスカードを使用することが便利です。アルゴリズムの各ステップを別々のメモに書き、それを並べ替えたり、挿入したり、削除したりすることが簡単になります。


擬似コードをArduinoスケッチに変換する
----------------------------------------------

これまでに書いたコードを洗練させ、必要に応じて ``digitalWrite()`` や ``delay()`` コマンドを追加します。コードの構造をガイドするために、 ``void loop()`` 関数には、緑色、黄色、赤色のLEDそれぞれのセグメントをカプセル化し、それぞれの後に一意の遅延期間を追加する必要があります。すべての遅延が同じ期間である必要はありません。各行が何を達成するかを明確にするために、コードコメントを更新します。

1. 以前保存したスケッチ ``Lesson6_Blink_LED`` を開きます。「ファイル」メニューから「名前を付けて保存」をクリックし、 ``Lesson7_Traffic_Light`` に名前を変更します。「保存」をクリックします。

2. 擬似コードに従って、 ``void setup()`` で3つのピンをすべて出力に設定します。 ``pinMode()`` コマンドを2回コピーして貼り付け、それぞれのピン番号を調整します。

    .. code-block:: Arduino
        :emphasize-lines: 4,5

        void setup() {
            // Setup code here, to run once:
            pinMode(3, OUTPUT); // set pin 3 as output
            pinMode(4, OUTPUT); // set pin 4 as output
            pinMode(5, OUTPUT); // set pin 5 as output
        }

3. ``void loop()`` 関数では、最初に緑色のLEDを点灯し、他の2つのLEDを消灯します。そのため、 ``digitalWrite()`` コマンドを2回コピーしてピン番号を4と5に変更し、消灯したいLEDの ``HIGH`` を ``LOW`` に変更し、コメントも現在のシナリオに合わせて更新します。修正後のコードは以下の通りです：

    .. code-block:: Arduino
        :emphasize-lines: 4,5

        void loop() {
            // ここにメインのコードを書き、繰り返し実行します：
            digitalWrite(3, HIGH);  // ピン3のLEDを点灯
            digitalWrite(4, LOW);   // ピン4のLEDを消灯
            digitalWrite(5, LOW);   // ピン5のLEDを消灯
            delay(3000);            // 3秒待つ
        }

4. 緑色のLEDをもっと長く点灯させたい場合があります。交通システムでは約1分かかるかもしれませんが、ここでは10秒でシミュレーションします。

    .. code-block:: Arduino
        :emphasize-lines: 6

        void loop() {
            // ここにメインのコードを書き、繰り返し実行します：
            digitalWrite(3, HIGH);  // ピン3のLEDを点灯
            digitalWrite(4, LOW);   // ピン4のLEDを消灯
            digitalWrite(5, LOW);   // ピン5のLEDを消灯
            delay(10000);           // 10秒待つ
        }

5. 次に黄色のLEDを点灯させ、他の2つのLEDを消灯します。再び ``void loop()`` から4行をコピーしてペーストし、ピン4をHIGHに設定し、他をLOWにします。黄色のLEDの遅延を3秒に変更します。

    .. code-block:: Arduino
        :emphasize-lines: 7-10

        void loop() {
            // ここにメインのコードを書き、繰り返し実行します：
            digitalWrite(3, HIGH);  // ピン3のLEDを点灯
            digitalWrite(4, LOW);   // ピン4のLEDを消灯
            digitalWrite(5, LOW);   // ピン5のLEDを消灯
            delay(10000);           // 10秒待つ
            digitalWrite(3, LOW);   // ピン3のLEDを消灯
            digitalWrite(4, HIGH);  // ピン4のLEDを点灯
            digitalWrite(5, LOW);   // ピン5のLEDを消灯
            delay(3000);            // 3秒待つ
        }

6. 最後に、赤色のLEDを10秒間点灯させ、他の2つのLEDを消灯します。完成したコードは以下の通りです：

    .. code-block:: Arduino

        void setup() {
            // Setup code here, to run once:
            pinMode(3, OUTPUT); // set pin 3 as output
            pinMode(4, OUTPUT); // set pin 4 as output
            pinMode(5, OUTPUT); // set pin 5 as output
        }
        
        void loop() {
            // put your main code here, to run repeatedly:
            digitalWrite(3, HIGH);  // Light up the LED on pin 3
            digitalWrite(4, LOW);   // Switch off the LED on pin 4
            digitalWrite(5, LOW);   // Switch off the LED on pin 5
            delay(10000);           // Wait for 10 seconds
            digitalWrite(3, LOW);   // Switch off the LED on pin 3
            digitalWrite(4, HIGH);  // Light up the LED on pin 4
            digitalWrite(5, LOW);   // Switch off LED on pin 5
            delay(3000);            // Wait for 3 seconds
            digitalWrite(3, LOW);   // Switch off the LED on pin 3
            digitalWrite(4, LOW);   // Switch off the LED on pin 4
            digitalWrite(5, HIGH);  // Light up LED on pin 5
            delay(10000);           // Wait for 10 seconds
        }

**質問**

自宅周辺の交差点を見てみましょう。通常、信号機はいくつありますか？それらはどのように連携していますか？

**まとめ**

レッスン7の完了おめでとうございます！擬似コードを完全に機能するArduino制御の信号機システムに翻訳することに成功しました。ここで達成したことを簡単に振り返ってみましょう：

* 擬似コードのマスター：電子システムの操作を概説するための擬似コードの使用を習得し、論理的思考と計画スキルを向上させました。
* 擬似コードから実際のコードへ：構造化されたアプローチを使用することで、効果的で正確なArduinoプログラミングが可能になりました。
* 実践的な応用：信号機システムの組み立てとプログラミングを通じて、知識の実践的な応用を示し、ソフトウェアがハードウェアを直接制御する方法を学びました。

このレッスンは、技術的な能力と分析的思考を磨き、エレクトロニクスとプログラミングにおけるより複雑なプロジェクトに備えるものです。これらのスキルを活かして、さらなる技術統合の可能性を探求し続けましょう！

