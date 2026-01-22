.. note::

    こんにちは！SunFounderのRaspberry Pi & Arduino & ESP32 Enthusiasts CommunityのFacebookページへようこそ！Raspberry Pi、Arduino、ESP32に関する情報を深く掘り下げ、仲間と共に楽しみましょう。

    **なぜ参加するのか？**

    - **専門サポート**: 購入後の問題や技術的な課題を、コミュニティやチームの助けを借りて解決します。
    - **学びと共有**: スキルを向上させるためのヒントやチュートリアルを交換します。
    - **独占プレビュー**: 新製品の発表やスニークピークにいち早くアクセスできます。
    - **特別割引**: 最新の製品に対する特別割引を楽しめます。
    - **イベントとプレゼント**: プレゼント企画やホリデープロモーションに参加できます。

    👉 一緒に探究し、創造しましょう！[|link_sf_facebook|]をクリックして、今すぐ参加してください！

13. 視覚のスペクトル
================================================================================
このレッスンへようこそ。ここでは、人間の色の知覚の謎を解き明かし、それを技術で再現する方法を学びます。このレッスンでは、目が数百万色を識別する方法と、RGB LEDを使ってこの驚異的な能力をデジタルでシミュレートする方法に触れます。私たちの目の光受容体とRGBカラーモデルの相互作用を探求することで、デジタル形式で世界の鮮やかさを再現する方法を学びます。

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/13_human_perception_color.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>


**概要**

人間の視覚システムは約1000万色を認識することができます。この能力は、網膜の錐体細胞と桿体細胞によって実現されています。色の知覚は線形ではなく、特定の色の変化に対してより敏感です。色に敏感な錐体細胞は、主に赤、緑、青の光に最も敏感な3種類に分けられます。

.. image:: img/13_mix_eyeballjpg.jpg

RGBカラーモデルは加法混色のモデルで、異なる強度の赤、緑、青の光を混ぜることで色が生成されます。このモデルでは、赤、緑、青が通常、主要な色チャンネルとみなされます。各チャンネルの強度（0から最大値、通常は8ビットカラー深度に対応する255まで）を調整することで、1600万以上の色を作り出すことが可能です。例えば、オレンジ色は赤を多めに、緑を少なめに混ぜることで実現できます。

.. image:: img/13_mix_orange.jpg

このインタラクティブなレッスンでは、これらの原理を適用してRGB LEDを制御し、正確な電子コマンドを使用してお好みの色を表示できるようにします。

**学習目標**

* このモデルが人間の色知覚を模倣する方法と、デジタルディスプレイでの応用を理解する。
* PWM（パルス幅変調）を使用してRGB LEDで微妙な色の混合を行う方法を学ぶ。
* パラメータを取る関数を作成することで、コーディングの効率と明確さを向上させる。
* 人間の色覚の複雑さを反映して、RGB値を調整してLEDの色をカスタマイズする。

回路の構築
-----------------------

**必要なコンポーネント**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * RGB LED
     - 3 * 220Ω抵抗
     - ジャンパーワイヤー
   * - |list_uno_r3| 
     - |list_rgb_led| 
     - |list_220ohm| 
     - |list_wire| 
   * - 1 * USBケーブル
     - 1 * ブレッドボード
     -
     -
   * - |list_usb_cable| 
     - |list_breadboard| 
     -
     -

このレッスンでは、レッスン12と同じ回路を使用します。

.. image:: img/12_mix_color_bb_4.png
    :width: 600
    :align: center


コード作成 - 色の表示
------------------------------------

RGB LEDの制御をマスターするための旅では、 ``digitalWrite()`` を使用して基本的な色を点灯させる方法を見てきました。次に、PWM（パルス幅変調）信号を送信するために ``analogWrite()`` を使用し、RGB LEDが生成できる色の全範囲を探求し、解放します。

コードを使ってこれをどのように実装できるか見てみましょう。

1. Arduino IDEを開き、「ファイル」メニューから「新しいスケッチ」を選択して新しいプロジェクトを開始します。
2. スケッチを ``Lesson13_PWM_Color_Mixing`` として保存します。 ``Ctrl + S`` を押すか、「保存」をクリックします。

3. 最初に、RGB LEDの3つのピンを出力として設定します。

.. code-block:: Arduino
    :emphasize-lines: 3-5

    void setup() {
        // Set up code to run once:
        pinMode(9, OUTPUT);   // Set Blue pin of RGB LED as output
        pinMode(10, OUTPUT);  // Set Green pin of RGB LED as output
        pinMode(11, OUTPUT);  // Set Red pin of RGB LED as output
    }

4. ``analogWrite()`` を使用して、RGB LEDにPWM値を送信します。レッスン9から、PWM値がLEDの明るさを変えることができること、PWM範囲が0-255であることを学びました。赤を表示するには、RGB LEDの赤ピンのPWM値を255に、他の2つのピンを0に設定します。

.. code-block:: Arduino
    :emphasize-lines: 10-12

    void setup() {
        // Set up code to run once:
        pinMode(9, OUTPUT);   // Set Blue pin of RGB LED as output
        pinMode(10, OUTPUT);  // Set Green pin of RGB LED as output
        pinMode(11, OUTPUT);  // Set Red pin of RGB LED as output
    }

    void loop() {
        // Main code to run repeatedly:
        analogWrite(9, 0);    // Set the PWM value of Blue pin to 0
        analogWrite(10, 0);   // Set the PWM value of Green pin to 0
        analogWrite(11, 255);  // Set the PWM value of Red pin to 255
    }

5. このセットアップで、コードをArduino Uno R3にアップロードすると、RGB LEDが赤色を表示します。

6. ``analogWrite()`` 関数を使用すると、RGB LEDは7つの基本色だけでなく、他の多くの色も表示できるようになります。9、10、11ピンの値をそれぞれ調整し、観察した色をハンドブックに記録します。

.. list-table::
    :widths: 20 20 20 40
    :header-rows: 1

    *   - 赤ピン    
        - 緑ピン  
        - 青ピン
        - 色
    *   - 0
        - 128
        - 128
        - 
    *   - 128
        - 0
        - 255
        - 
    *   - 128
        - 128
        - 255
        - 
    *   - 255
        - 128
        - 0
        -     

コード作成 - パラメータ化された関数
------------------------------------------------

異なる色を表示するために ``analogWrite()`` 関数を使用すると、多くの色を同時に表示したい場合、コードが長くなることがあります。そのため、関数を作成する必要があります。

前のレッスンとは異なり、今回はパラメータを持つ関数を作成します。

パラメータ化された関数を使用すると、特定の値を関数に渡し、その値を使用してタスクを実行できます。これは、色の強度などのプロパティを動的に調整するのに非常に便利です。これにより、コードが柔軟で読みやすくなります。

パラメータ化された関数を定義するとき、関数名の後の括弧内に必要な値（パラメータ）を指定します。これらのパラメータは、関数が呼び出されたときに実際の値に置き換えられます。

以下に、RGB LEDの色を設定するためのパラメータ化された関数を定義する方法を示します：


1. 以前に保存したスケッチ ``Lesson13_PWM_Color_Mixing`` を開きます。

2. 「ファイル」メニューから「名前を付けて保存」を選択し、スケッチを ``Lesson13_PWM_Color_Mixing_Function`` として保存します。「保存」をクリックします。

3. ``void loop()``の後に、キーワード ``void`` を使用して関数を宣言し、関数名と括弧内にパラメータを記述します。 ``setColor`` 関数では、RGB LEDの各色成分の強度を表す ``red`` 、 ``green`` 、 ``blue`` の3つのパラメータを使用します。

.. code-block:: Arduino
    :emphasize-lines: 5,6

    void loop() {
        // 繰り返し実行するメインコードを記述:
    }

    void setColor(int red, int green, int blue) {
    }

4. 関数の本文内で、 ``analogWrite()`` コマンドを使用してRGB LEDのピンにPWM信号を送信します。 ``setColor`` に渡された値は各色の明るさを決定します。ここでは、パラメータ ``red`` 、 ``green`` 、 ``blue`` を使用して、各LEDピンの強度を直接制御します。

.. code-block:: Arduino

    // Function to set the color of the RGB LED
    void setColor(int red, int green, int blue) {
        // Write PWM value for red, green, and blue to the RGB LED
        analogWrite(11, red);
        analogWrite(10, green);
        analogWrite(9, blue);
    }

5. 新しく作成した ``setColor()`` 関数を ``void loop()`` 内で呼び出します。パラメータを持つ関数を作成したので、 ``()`` 内に引数を埋める必要があります。例えば ``(255, 0, 0)`` のようにします。コメントを忘れずに記述してください。

.. code-block:: Arduino
    :emphasize-lines: 3

    void loop() {
        // put your main code here, to run repeatedly:
        setColor(255, 0, 0); // Display red color
    }

    // Function to set the color of the RGB LED
    void setColor(int red, int green, int blue) {
        // Write PWM value for red, green, and blue to the RGB LED
        analogWrite(11, red);
        analogWrite(10, green);
        analogWrite(9, blue);
    }

6. 既に、RGB LEDの3つのピンに異なる値を提供することで、異なる色の光を点灯させることができることを知っています。では、RGB LEDを正確に希望の色に点灯させるにはどうすればよいでしょうか？これには、カラーパレットの助けが必要です。Windowsに付属の **Paint** （または任意の描画ソフトウェア）を開きます。

.. image:: img/13_mix_color_paint.png

7. 好きな色を選択し、そのRGB値を記録します。

.. note::

    色を選択する前に、明度を適切な位置に調整することを忘れないでください。

.. image:: img/13_mix_color_paint_2.png

8. 選択した色を ``void loop()`` 内の ``setColor()`` 関数に入力し、 ``delay()`` 関数を使用して各色の表示時間を指定します。

.. code-block:: Arduino

    void loop() {
        // put your main code here, to run repeatedly:
        setColor(255, 0, 0);      // Display red color
        delay(1000);              // Wait for 1 second
        setColor(0, 128, 128);    // Display teal color
        delay(1000);              // Wait for 1 second
        setColor(128, 0, 255);    // Display purple color
        delay(1000);              // Wait for 1 second
        setColor(128, 128, 255);  // Display Light blue color
        delay(1000);              // Wait for 1 second
        setColor(255, 128, 0);    // Display orange color
        delay(1000);              // Wait for 1 second
    }

9. 以下は完全なコードです。クリックして「アップロード」し、Arduino Uno R3にコードを転送して効果を確認します。

.. code-block:: Arduino

    void setup() {
        // put your setup code here, to run once:
        pinMode(9, OUTPUT);   // Set Blue pin of RGB LED as output
        pinMode(10, OUTPUT);  // Set Green pin of RGB LED as output
        pinMode(11, OUTPUT);  // Set Red pin of RGB LED as output
    }

    void loop() {
        // put your main code here, to run repeatedly:
        setColor(255, 0, 0);      // Display red color
        delay(1000);              // Wait for 1 second
        setColor(0, 128, 128);    // Display teal color
        delay(1000);              // Wait for 1 second
        setColor(128, 0, 255);    // Display purple color
        delay(1000);              // Wait for 1 second
        setColor(128, 128, 255);  // Display Light blue color
        delay(1000);              // Wait for 1 second
        setColor(255, 128, 0);    // Display orange color
        delay(1000);              // Wait for 1 second
    }

    // Function to set the color of the RGB LED
    void setColor(int red, int green, int blue) {
        // Write PWM value for red, green, and blue to the RGB LED
        analogWrite(11, red);
        analogWrite(10, green);
        analogWrite(9, blue);
    }

10. 最後に、コードを保存し、作業スペースを整理することを忘れないでください。

**まとめ**

今日の色の知覚に関する探求は、生物学と電子応用の橋渡しをし、プログラミングの力が抽象的な概念を現実にする方法を強調しました。RGB値を調整してLEDを制御することで、目が色を認識する方法を模倣し、人間の生物学への深い理解と電子制御の高度なスキルを習得しました。
