.. note::

    こんにちは、SunFounderのFacebookコミュニティ「Raspberry Pi & Arduino & ESP32 Enthusiasts」へようこそ！Raspberry Pi、Arduino、ESP32の世界を仲間と一緒に深く掘り下げましょう。

    **参加する理由**

    - **専門家のサポート**: アフターサポートや技術的な問題をコミュニティやチームの助けを借りて解決しましょう。
    - **学びと共有**: スキルを向上させるためのヒントやチュートリアルを交換しましょう。
    - **限定プレビュー**: 新製品発表や先行情報を早めに入手できます。
    - **特別割引**: 最新製品を特別価格で購入できます。
    - **フェスティブプロモーションとプレゼント**: ギブアウェイや季節のプロモーションに参加できます。

    👉 私たちと一緒に探求し、創造する準備はできましたか？今すぐ[|link_sf_facebook|]をクリックして参加しましょう！

12. 虹の色
=======================================
光で絵を描くことができたらどうでしょう？赤、緑、青を混ぜて、想像できるすべての色を作り出すことができます。まるでパレット上の絵の具を混ぜるように、光のビームで色を作り出すのです。

.. image:: img/12_rgb_mix.png
    :width: 300
    :align: center

このレッスンでは、RGB LEDの魅力的な世界を探求し、一次色の組み合わせがどのようにして鮮やかな色のスペクトラムを作り出すかを学びます。このハンズオンコースでは、RGB LEDの機能原理と、プログラミングと回路構築の実際の応用について説明します。

このレッスンで学ぶこと:

* RGB LEDの動作原理を理解する。
* タスクを簡略化し、コードの可読性を向上させるための関数の作成と利用方法を学ぶ。
* RGB LEDを操作することで、さまざまな色の組み合わせの影響を探る。


回路の構築
-----------------------

**必要なコンポーネント**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * RGB LED
     - 3 * 220Ω 抵抗
     - ジャンパーワイヤー
   * - |list_uno_r3| 
     - |list_rgb_led| 
     - |list_220ohm| 
     - |list_wire| 
   * - 1 * USBケーブル
     - 1 * ブレッドボード
     - 1 * マルチメーター
     -
   * - |list_usb_cable| 
     - |list_breadboard| 
     - |list_meter|
     -
     
**ステップバイステップの構築手順**

配線図または以下の手順に従って回路を構築してください。

.. image:: img/12_mix_color_bb_4.png
    :width: 500
    :align: center

1. RGB LEDから始めます。

RGB LEDは、赤、緑、青のLEDを1つのパッケージに統合することで、さまざまな色の光を放ちます。3つのピンへの電圧入力を変えることで、これらのLEDは組み合わせて16,777,216色まで作り出すことができます。

.. image:: img/12_mix_color_rgb.png
    :width: 400
    :align: center

設計によって、RGB LEDは共通アノードまたは共通カソードのいずれかです。このプロジェクトでは、3つのLEDが共通の負の接続を共有する **共通カソード** RGB LEDを使用します。

* 共通カソードRGB LEDは、共通の負の接続を持っています。
* 共通アノードRGB LEDは、共通の正の接続を持っています。

.. image:: img/12_rgb_cc_ca.jpg
    :width: 600
    :align: center

RGB LEDは通常4本のピンを持ち、最も長いピンがグラウンドです。RGB LEDを配置するときは、最も長いリードが左から2番目にくるように配置し、ピンを左から右に向かって赤、GND、緑、青に設定します。

.. image:: img/12_mix_color_rgb_1.jpg
    :width: 200
    :align: center

また、ダイオードテストモードのマルチメーターを使用して、各ピンが放つ色を確認することもできます。

マルチメーターを **導通** 設定にして、抵抗を測定します。

.. image:: img/multimeter_diode_measure.png
    :width: 300
    :align: center

マルチメーターの黒いリードをRGB LEDの最も長いピンに触れ、赤いリードを他のピンに個別に触れます。これにより、RGB LEDが赤、緑、または青に点灯するのがわかります。

.. image:: img/12_mix_color_measure_pin.png
    :width: 500
    :align: center

2. RGB LEDをブレッドボードに挿入し、最も長いピンを17Cの穴に、他の3つのピンをそれぞれ18C、16C、15Dの穴に挿入します。

.. image:: img/12_mix_color_bb_1.png
    :width: 500
    :align: center

3. 220Ωの抵抗を、15Eから15G、16Eから16G、18Eから18Gに挿入します。

.. image:: img/12_mix_color_bb_2.png
    :width: 500
    :align: center

4. これらの抵抗をジャンパーワイヤーでArduino Uno R3のピン9、10、11に接続します。

.. image:: img/12_mix_color_bb_3.png
    :width: 500
    :align: center

5. RGB LEDの最も長いピンをジャンパーワイヤーでGNDに接続します。

.. image:: img/12_mix_color_bb_4.png
    :width: 500
    :align: center

コード作成 - RGB LEDを点灯させる
----------------------------------------

1. Arduino IDEを開き、「ファイル」メニューから「新しいスケッチ」を選択して新しいプロジェクトを開始します。
2. スケッチを ``Lesson12_Rainbow_Color`` として保存します。 ``Ctrl + S`` を押すか、「保存」ボタンをクリックしてください。

3. 回路内のLEDはArduino Uno R3のデジタルピンに接続されています。LEDは出力デバイスであるため、デジタルピン9、10、11を ``OUTPUT`` として設定する必要があります。

.. code-block:: Arduino
    :emphasize-lines: 3-5


    void setup() {
        // put your setup code here, to run once:
        pinMode(9, OUTPUT);   // Set Blue pin of RGB LED as output
        pinMode(10, OUTPUT);  // Set Green pin of RGB LED as output
        pinMode(11, OUTPUT);  // Set Red pin of RGB LED as output
    }

    void loop() {
        // put your main code here, to run repeatedly:
    }

4. 次に、 ``void loop()`` 内でRGB LEDの赤ピンを ``HIGH`` に設定し、他の2つのピンを ``LOW`` に設定します。

.. note::

    PWMピン9、10、11を使用しているため、 ``digitalWrite()`` または ``analogWrite()`` のいずれかを使用して、高または低のレベルを出力することができます。
    
    このレッスンでは、ピンを単に高または低に設定するため、 ``digitalWrite()`` を使用します。



.. code-block:: Arduino
    :emphasize-lines: 10-12

    void setup() {
        // ここに一度だけ実行するセットアップコードを記述:
        pinMode(9, OUTPUT);   // RGB LEDの青ピンを出力に設定
        pinMode(10, OUTPUT);  // RGB LEDの緑ピンを出力に設定
        pinMode(11, OUTPUT);  // RGB LEDの赤ピンを出力に設定
    }

    void loop() {
        // ここに繰り返し実行するメインコードを記述:
        digitalWrite(9, LOW);    // RGB LEDの青ピンをオフ
        digitalWrite(10, LOW);   // RGB LEDの緑ピンをオフ
        digitalWrite(11, HIGH);  // RGB LEDの赤ピンをオン
    }

5. コードを保存し、「アップロード」ボタンをクリックしてArduino Uno R3に送信します。どうなるか見てみましょう。

6. RGB LEDが赤色に点灯するのがわかります。しかし、緑色と青色も点灯させたい場合はどうすればよいでしょうか？コードをどのように変更すればよいでしょうか？

今度は、3つの ``digitalWrite()`` コマンドを2回コピーします。表示したいピンを ``HIGH`` に設定し、他のピンを ``LOW`` に設定します。各色を1秒間表示させます。

.. code-block:: Arduino
    :emphasize-lines: 14-21

    void setup() {
        // put your setup code here, to run once:
        pinMode(9, OUTPUT);   // Set Blue pin of RGB LED as output
        pinMode(10, OUTPUT);  // Set Green pin of RGB LED as output
        pinMode(11, OUTPUT);  // Set Red pin of RGB LED as output
    }

    void loop() {
        // put your main code here, to run repeatedly:
        digitalWrite(9, LOW);    // Turn off the Blue pin of RGB LED
        digitalWrite(10, LOW);   // Turn off the Green pin of RGB LED
        digitalWrite(11, HIGH);  // Turn on the Red pin of RGB LED
        delay(1000);              //Wait for 1 second
        digitalWrite(9, LOW);    // Turn off the Blue pin of RGB LED
        digitalWrite(10, HIGH);  // Turn on the Green pin of RGB LED
        digitalWrite(11, LOW);   // Turn off the Red pin of RGB LED
        delay(1000);              //Wait for 1 second
        digitalWrite(9, HIGH);   // Turn on the Blue pin of RGB LED
        digitalWrite(10, LOW);   // Turn off the Green pin of RGB LED
        digitalWrite(11, LOW);   // Turn off the Red pin of RGB LED
        delay(1000);              //Wait for 1 second
    }

7. コードを再度アップロードして、効果を確認してください。RGB LEDが赤、緑、青と順番に点灯するのがわかります。

**質問**:

1. 他の色を作りたい場合はどうすればよいでしょうか？以下の図を参照して、アイデアをハンドブックに記入してください。

.. image:: img/12_rgb_mix.png
    :width: 300
    :align: center

.. list-table::
   :widths: 20 20 20 20
   :header-rows: 1

   * - 色
     - 赤ピン
     - 緑ピン
     - 青ピン
   * - 赤
     - *HIGH*
     - *LOW*
     - *LOW*
   * - 緑
     - *LOW*
     - *HIGH*
     - *LOW*
   * - 青
     - *LOW*
     - *LOW*
     - *HIGH*
   * - 黄色
     -
     -
     -
   * - ピンク
     -
     -
     -
   * - シアン
     - 
     -
     -
   * - 白
     -
     -
     -

コード作成 - 関数を作成する
--------------------------------------

RGB LEDに異なる色を順番に表示するためには、多くの同様のコードを記述する必要があることに気付いたかもしれません。例えば、RGB LEDに7つの異なる色を表示するには、次のようなコードを書くことになります。

.. code-block:: Arduino

    void setup() {
        // 一度だけ実行するセットアップコードを記述:
        pinMode(9, OUTPUT);   // RGB LEDの青ピンを出力に設定
        pinMode(10, OUTPUT);  // RGB LEDの緑ピンを出力に設定
        pinMode(11, OUTPUT);  // RGB LEDの赤ピンを出力に設定
    }

    void loop() {
        // 繰り返し実行するメインコードを記述:
        digitalWrite(9, LOW);    // RGB LEDの青ピンをオフ
        digitalWrite(10, LOW);   // RGB LEDの緑ピンをオフ
        digitalWrite(11, HIGH);  // RGB LEDの赤ピンをオン
        delay(1000);             // 1秒待つ
        digitalWrite(9, LOW);    // RGB LEDの青ピンをオフ
        digitalWrite(10, HIGH);  // RGB LEDの緑ピンをオン
        digitalWrite(11, LOW);   // RGB LEDの赤ピンをオフ
        delay(1000);             // 1秒待つ
        digitalWrite(9, HIGH);   // RGB LEDの青ピンをオン
        digitalWrite(10, LOW);   // RGB LEDの緑ピンをオフ
        digitalWrite(11, LOW);   // RGB LEDの赤ピンをオフ
        delay(1000);             // 1秒待つ
        digitalWrite(9, LOW);    // RGB LEDの青ピンをオフ
        digitalWrite(10, HIGH);  // RGB LEDの緑ピンをオン
        digitalWrite(11, HIGH);  // RGB LEDの赤ピンをオン
        delay(1000);             // 1秒待つ
        digitalWrite(9, HIGH);   // RGB LEDの青ピンをオン
        digitalWrite(10, LOW);   // RGB LEDの緑ピンをオフ
        digitalWrite(11, HIGH);  // RGB LEDの赤ピンをオン
        delay(1000);             // 1秒待つ
        digitalWrite(9, HIGH);   // RGB LEDの青ピンをオン
        digitalWrite(10, HIGH);  // RGB LEDの緑ピンをオン
        digitalWrite(11, LOW);   // RGB LEDの赤ピンをオフ
        delay(1000);             // 1秒待つ
        digitalWrite(9, HIGH);   // RGB LEDの青ピンをオン
        digitalWrite(10, HIGH);  // RGB LEDの緑ピンをオン
        digitalWrite(11, HIGH);  // RGB LEDの赤ピンをオン
        delay(1000);             // 1秒待つ
    }

void loop()が長くなり、ロジックがわかりにくくなっていることに気付くでしょう。このタイミングで、関数の概念を導入するのが理想的です。

コードの作成過程で、pinMode()、digitalWrite()、delay()などのArduinoの組み込み関数を使用してきました。ここでは、カスタム関数の作成に取り組みます。カスタム関数を使用すると、コードを簡素化し、より論理的で管理しやすくなります。

関数を作成するには、void loop()の括弧の後にスケッチの末尾に追加します。void setup()やvoid loop()のように、関数はvoidから始まり、その後に任意の名前を付けます。関数の名前の付け方は、変数や定数と同様で、Arduino IDEのキーワードではない名前を使用し、そのコマンドを中括弧で囲みます。

.. code-block:: Arduino
    :emphasize-lines: 9-11

    void setup() {
        ...
    }

    void loop() {
        ...
    }

    void lightRed(){
    
    }

1. スケッチの末尾、void loop()の括弧の直後に、7つの新しい関数を追加します。各関数には、RGB LEDに特定の色を表示するコードが含まれます。

.. code-block:: Arduino
    :emphasize-lines: 10-22

    void loop() {
        // put your main code here, to run repeatedly:
        digitalWrite(9, LOW);    // Turn off the Blue pin of RGB LED
        digitalWrite(10, LOW);   // Turn off the Green pin of RGB LED
        digitalWrite(11, HIGH);  // Turn on the Red pin of RGB LED
        delay(1000);             //Wait for 1 second
        ...
    }

    void lightRed(){
    
    }

    void lightGreen(){
    
    }

    ...

    void lightWhite(){
    
    }

2. 次に、void loop()から色特有のコードスニペットをカットして、それぞれの関数に貼り付けます。これにより、loop()関数には7つのdelay()呼び出しのみが残ります。

.. code-block:: Arduino

    ...

    void loop() {
        // 繰り返し実行するメインコードを記述:

        delay(1000);  //Wait for 1 second
        delay(1000);  //Wait for 1 second
        delay(1000);  //Wait for 1 second
        delay(1000);  //Wait for 1 second
        delay(1000);  //Wait for 1 second
        delay(1000);  //Wait for 1 second
        delay(1000);  //Wait for 1 second
    }

    void lightRed() {
        digitalWrite(9, LOW);    // Turn off the Blue pin of RGB LED
        digitalWrite(10, LOW);   // Turn off the Green pin of RGB LED
        digitalWrite(11, HIGH);  // Turn on the Red pin of RGB LED
    }
    ...

    void lightWhite() {
        digitalWrite(9, HIGH);   // Turn on the Blue pin of RGB LED
        digitalWrite(10, HIGH);  // Turn on the Green pin of RGB LED
        digitalWrite(11, HIGH);  // Turn on the Red pin of RGB LED
    }

3. 関数が設定されたので、次はvoid loop()内でそれらを呼び出します。関数を呼び出すには、その名前の後に丸括弧を2つ付け、行の終わりにセミコロンを付けるだけです。

.. code-block:: Arduino
    :emphasize-lines: 7-22

    void setup() {
        // put your setup code here, to run once:
        pinMode(9, OUTPUT);   // Set Blue pin of RGB LED as output
        pinMode(10, OUTPUT);  // Set Green pin of RGB LED as output
        pinMode(11, OUTPUT);  // Set Red pin of RGB LED as output
    }

    void loop() {
        // put your main code here, to run repeatedly:
        lightRed();
        delay(1000);  //Wait for 1 second
        lightGreen();
        delay(1000);  //Wait for 1 second
        lightBlue();
        delay(1000);  //Wait for 1 second
        lightYellow();
        delay(1000);  //Wait for 1 second
        lightPink();
        delay(1000);  //Wait for 1 second
        lightCyan();
        delay(1000);  //Wait for 1 second
        lightWhite();
        delay(1000);  //Wait for 1 second
    }

    void lightRed() {
        digitalWrite(9, LOW);    // Turn off the Blue pin of RGB LED
        digitalWrite(10, LOW);   // Turn off the Green pin of RGB LED
        digitalWrite(11, HIGH);  // Turn on the Red pin of RGB LED
    }

    void lightGreen() {
        digitalWrite(9, LOW);    // Turn off the Blue pin of RGB LED
        digitalWrite(10, HIGH);  // Turn on the Green pin of RGB LED
        digitalWrite(11, LOW);   // Turn off the Red pin of RGB LED
    }
    void lightBlue() {
        digitalWrite(9, HIGH);  // Turn on the Blue pin of RGB LED
        digitalWrite(10, LOW);  // Turn off the Green pin of RGB LED
        digitalWrite(11, LOW);  // Turn off the Red pin of RGB LED
    }
    void lightYellow() {
        digitalWrite(9, LOW);    // Turn off the Blue pin of RGB LED
        digitalWrite(10, HIGH);  // Turn on the Green pin of RGB LED
        digitalWrite(11, HIGH);  // Turn on the Red pin of RGB LED
    }
    void lightPink() {
        digitalWrite(9, HIGH);   // Turn on the Blue pin of RGB LED
        digitalWrite(10, LOW);   // Turn off the Green pin of RGB LED
        digitalWrite(11, HIGH);  // Turn on the Red pin of RGB LED
    }
    void lightCyan() {
        digitalWrite(9, HIGH);   // Turn on the Blue pin of RGB LED
        digitalWrite(10, HIGH);  // Turn on the Green pin of RGB LED
        digitalWrite(11, LOW);   // Turn off the Red pin of RGB LED
    }
    void lightWhite() {
        digitalWrite(9, HIGH);   // Turn on the Blue pin of RGB LED
        digitalWrite(10, HIGH);  // Turn on the Green pin of RGB LED
        digitalWrite(11, HIGH);  // Turn on the Red pin of RGB LED
    }


4. 関数がすべて設定され、loop()内で呼び出されると、コードは完成です。"Upload"ボタンをクリックして、コードをArduino Uno R3に転送します。RGB LEDが赤、緑、青、黄色、ピンク、シアン、白に順番に変わるのが見えるでしょう。

.. note::

    RGB LEDの明るさは非常に強いため、長時間直視しないようにして目の疲れを防ぎましょう。

    ティッシュや曇りガラスのような素材で光を拡散させ、明るさを和らげることも検討してください。

**まとめ**

一連のコーディング演習を通じて、LEDの色を動的に変えるスケッチを書きます。各色を制御する基本的なコマンドから始め、コードを関数を使用してリファクタリングし、セットアップをよりモジュール化し、管理しやすくします。このアプローチはコードをクリーンにするだけでなく、プログラミングにおける関数の重要性も教えてくれます。
