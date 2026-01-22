.. note::

    こんにちは、SunFounderのRaspberry Pi & Arduino & ESP32ファンコミュニティへようこそ！Raspberry Pi、Arduino、ESP32に興味のある仲間たちと共に、さらに深く探求してみましょう。

    **なぜ参加するのか？**

    - **専門家のサポート**: 購入後の問題や技術的な課題をコミュニティやチームの助けを借りて解決できます。
    - **学びと共有**: スキルを向上させるためのヒントやチュートリアルを交換しましょう。
    - **限定プレビュー**: 新製品の発表や予告を早期に入手できます。
    - **特別割引**: 最新製品の限定割引を利用できます。
    - **お祭りプロモーションとギブアウェイ**: ギブアウェイやホリデープロモーションに参加しましょう。

    👉 一緒に探求し、創造する準備はできましたか？[|link_sf_facebook|]をクリックして今すぐ参加しましょう！

10. ON/OFFデスクランプ
====================================

このレッスンでは、調光可能なデスクランプにスイッチボタンを追加することで、前回のプロジェクトを拡張します。この改良により、実際のデスクランプのようにオンオフを切り替え、その後に明るさを調整する機能が追加され、日常の使用に近いシナリオをシミュレートします。

.. image:: img/10_desk_lamp_button.jpg
    :width: 500
    :align: center

* リアルタイムデータ表示のためのシリアルモニタの使用方法を学ぶ。
* ボタン入力を効率的に管理するための ``INPUT_PULLUP`` モードの実装。
* 状態の変化を検出する方法を理解する。
* デジタル信号とアナログ信号の特性を探る。
* 条件文（``if else``）の活用。

回路の構築
------------------------------------

**必要なコンポーネント**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * 赤色LED
     - 1 * 220Ω抵抗
     - 1 * ポテンショメータ
   * - |list_uno_r3| 
     - |list_red_led| 
     - |list_220ohm| 
     - |list_potentiometer| 
   * - 1 * ボタン
     - 1 * USBケーブル
     - 1 * ブレッドボード
     - ジャンパーワイヤー
   * - |list_button| 
     - |list_usb_cable| 
     - |list_breadboard| 
     - |list_wire| 


**構築手順**

1. 前回のレッスンのデスクランプ回路から始めます。

.. image:: img/9_dimmer_led1_pin9.png
    :width: 500
    :align: center

2. ボタンをブレッドボードの中央のギャップをまたいで挿入し、ピンを6E、8E、6J、8Jの穴に挿入します。

.. note::

    ボタンの挿入方法が不明な場合は、両方の向きを試してみてください。一方の向きでは、ピンの間隔が少し狭くて合わないかもしれません。

.. image:: img/10_desk_lamp_button_button.png
    :width: 500
    :align: center

3. ボタンの左下のピンを長いジャンパーワイヤーでArduino Uno R3のデジタルピン7に接続し、一方の端を8Jの穴に、もう一方の端をピン7に挿入します。

.. image:: img/10_desk_lamp_button_p7.png
    :width: 500
    :align: center

4. ボタンの右上のピンを短いジャンパーワイヤーでブレッドボードの負端子に接続し、一方の端を6Aの穴に、もう一方の端を負端子に挿入します。

.. image:: img/10_desk_lamp_button_gnd.png
    :width: 500
    :align: center


コードの作成
-----------------

**ボタンの状態を表示**

1. 以前保存したスケッチ ``Lesson9_Desk_Lamp`` を開き、「名前を付けて保存...」を選択して ``Lesson10_Desk_Lamp_Button`` に名前を変更し、「保存」をクリックします。

2. レッスン8では、10Kプルダウン抵抗を手動でGNDとボタンの間に接続しましたが、この回路では抵抗を接続していません。代わりに、Arduinoのソフトウェアプルアップ機能を使用します。ボタンに接続されたピンを入力に設定し、 ``PULLUP`` に設定する必要があります。

.. code-block:: Arduino
    :emphasize-lines: 6

    int potValue = 0;

    void setup() {
        // ここに初期設定コードを記述します。プログラムが開始すると1回だけ実行されます:
        pinMode(9, OUTPUT);        // ピン9を出力に設定
        pinMode(7, INPUT_PULLUP);  // ピン7を内部プルアップ抵抗で入力に設定
    }

3. シリアルモニタを利用するには、Arduino Uno R3でシリアル通信を開始するコマンドを含める必要があります。

このコマンドは通常、スケッチの ``void setup()`` セクションに配置されます。 ``Serial.begin(baud)`` コマンドはシリアル通信を開始し、 ``baud`` はコンピュータとArduino Uno R3間の1秒あたりのデータ転送速度を表します。一般的なボーレートは9600ビット/秒と115200ビット/秒です。

.. code-block:: Arduino
    :emphasize-lines: 7

    int potValue = 0;

    void setup() {
        // put your setup code here, to run once:
        pinMode(9, OUTPUT);        // Set pin 9 as output
        pinMode(7, INPUT_PULLUP);  // Set pin 7 as input with an internal pull-up resistor
        Serial.begin(9600);        // Serial communication setup at 9600 baud
    }


4. ``void loop()`` に入る前に、ボタンとLEDの状態を初期化するための変数を2つ作成する必要があります。ボタンが押されていないときにLEDが消灯している状態に設定し、ボタンは内部プルアップ抵抗を使用しているため、押されていないときはHIGHとして読み取られます。

.. code-block:: Arduino
    :emphasize-lines: 2,3

    int potValue = 0;  // Variable to store the value read from the potentiometer
    int ledState = LOW;          // Initial state of the LED
    int lastButtonState = HIGH;  // the previous reading from the input pin

    void setup() {
        pinMode(9, OUTPUT);        // Set pin 9 as output
        pinMode(7, INPUT_PULLUP);  // Set pin 7 as input with an internal pull-up resistor
        Serial.begin(9600);        // Serial communication setup at 9600 baud
    }

5. 次に、 ``void loop()`` 内で最初にボタンの状態を ``digitalRead()`` を使用して読み取り、その値を ``buttonState`` 変数に格納します。

.. code-block:: Arduino
    :emphasize-lines: 2

    void loop() {
        int buttonState = digitalRead(7);  // Read the state of the button
    }
    
6. シリアルモニタを使用してデータを表示する準備が整いました。 ``Serial.print()`` を利用してデータやテキストを表示します。

使い方は以下の通りです：


    * ``Serial.print(val)`` または ``Serial.print(val, format)``: データをシリアルポートに人間が読み取れるASCIIテキストとして出力します。

    **パラメータ**
        - ``Serial``: シリアルポートオブジェクト。
        - ``val``: 出力する値。許容データ型：任意のデータ型。

    **戻り値**
        ``print()`` は書き込まれたバイト数を返しますが、その数を読み取るのは任意です。データ型：size_t。

このコマンドは様々なデータ型やフォーマットを表現できます。例えば：

.. code-block:: Arduino

    Serial.print(78);                // "78"と出力
    Serial.print(78, BIN);           // "1001110"と出力
    Serial.print(1.23456);           // "1.23"と出力
    Serial.print(1.23456, 0);        // "1"と出力
    Serial.print('N');               // "N"と出力
    Serial.print("Hello world.");    // "Hello world."と出力

7. 次に、表示するデータについてのプロンプトを表示するコマンドを使用します。これは複数のデータを一度に区別するのに役立ちます。

.. code-block:: Arduino
    :emphasize-lines: 3

    void loop() {
        int buttonState = digitalRead(7);  // Read the state of the button
        Serial.print("Button State: ");
    }

8. 次に、 ``buttonState`` 変数に格納されている値を表示します。シリアルモニタで各出力を新しい行に表示するには、 ``Serial.println()`` を使用して、印刷文の末尾に改行文字を追加します。

.. note::

    文字や文字列（引用符で囲む必要があります）を印刷する場合と、変数を直接挿入する場合の違いに注意してください。
    
.. code-block:: Arduino
    :emphasize-lines: 14

    int potValue = 0;  // Variable to store the value read from the potentiometer
    int ledState = LOW;          // Initial state of the LED
    int lastButtonState = HIGH;  // the previous reading from the input pin

    void setup() {
        pinMode(9, OUTPUT);        // Set pin 9 as output
        pinMode(7, INPUT_PULLUP);  // Set pin 7 as input with an internal pull-up resistor
        Serial.begin(9600);        // Serial communication setup at 9600 baud
    }

    void loop() {
        int buttonState = digitalRead(7);  // Read the state of the button
        Serial.print("Button State: ");
        Serial.println(buttonState);  // Print the current button state
    }

9. ここで、コードは本質的に完成です。「アップロード」をクリックしてコードをArduino Uno R3にアップロードします。

    .. note::

        ボードからコンピュータにデータが送信されるたびに、Arduino Uno R3のTX LEDが点滅するはずです。

10. その後、Arduino IDEの右上にある「シリアルモニタ」ボタンをクリックします。

    .. image:: img/10_dimmer_led_serial.png
        :align: center

11. データが文字化けして表示される場合は、コードで設定したボーレートに合わせてボーレートを調整する必要があります。

    .. image:: img/10_dimmer_led_serial_baud.png
        :align: center

12. ボタンが押されていないときは「1」が連続して表示され、ボタンが押されると「0」が連続して表示されることがわかります。これは、デジタル信号の特徴で、状態が「0」と「1」のみであることを示しています。

**ボタン状態の変化を検出**

このセクションでは、簡単なボタンでLEDのオンオフを切り替える方法を学びます。これは、ボタンの状態が変化した瞬間を検出することを含みます。

1. ボタンの押下を監視するコア機能から始めましょう。

以前に、ボタンが押されたかどうかをその状態が ``HIGH`` または ``LOW`` で読み取る方法を学びました。しかし、このレッスンではボタンを押し続ける必要がないように、単一の押下に応答することを目指します。これには、ボタンの状態が変化したことを検出する必要があります。

これを達成するために、ボタンの前回の状態（ ``lastButtonState`` ）を現在の状態（ ``buttonState`` ）と比較する ``if`` 文を使用します。論理演算子 ``&&`` をここで使用して、両方の条件が真である場合に ``if`` 文内のコードブロックが実行されるようにします。

.. code-block:: Arduino
    :emphasize-lines: 7,8

    void loop() {
        int buttonState = digitalRead(7);  // Read the state of the button
        Serial.print("Button State: ");
        Serial.println(buttonState);  // Print the current button state
            
        // Check if button state has changed from the last loop iteration
        if (lastButtonState == HIGH && buttonState == LOW) {  // Button press detected
        }
    }

2. ボタンが押されたと検出されたとき、LEDの状態を切り替えます。つまり、LEDが消灯していた場合は点灯し、点灯していた場合は消灯します。 ``!`` 演算子を使用してledState変数の状態を反転させます。

.. code-block:: Arduino
    :emphasize-lines: 8

    void loop() {
        int buttonState = digitalRead(7);  // Read the state of the button
        Serial.print("Button State: ");
        Serial.println(buttonState);  // Print the current button state
        
        // Check if button state has changed from the last loop iteration
        if (lastButtonState == HIGH && buttonState == LOW) {  // Button press detected
            ledState = !ledState;                               // Toggle LED state
        }
    }

3. ボタンの状態を確認してLEDを更新した後、ボタンの現在の状態を新しい「最後に知られている状態」として記録する必要があります。このステップは次の状態変化を検出するために重要です。

.. code-block:: Arduino
    :emphasize-lines: 10,11

    void loop() {
        int buttonState = digitalRead(7);  // ボタンの状態を読み取る
        Serial.print("Button State: ");
        Serial.println(buttonState);  // 現在のボタン状態を出力
        
        // ボタン状態が前回のループの反復から変化したかどうかを確認
        if (lastButtonState == HIGH && buttonState == LOW) {  // ボタン押下が検出された
            ledState = !ledState;                               // LEDの状態を切り替え
        }
        lastButtonState = buttonState;  // lastButtonStateを現在の状態に更新
        delay(200);                     // オプション：簡単なソフトウェアデバウンス
    }

**ポテンショメータで明るさを調整**

``ledState`` が ``HIGH`` の場合、LEDを点灯させるだけでなく、ポテンショメータで明るさを調整できるようにします。これを実装する方法は次の通りです：

1. ボタン押下でLEDの状態を切り替える ``if`` 文の直後に、 ``ledState`` が ``HIGH`` であるかどうかを確認する別の ``if`` 文を追加します。もしそうであれば、ポテンショメータの値に基づいてLEDの明るさを調整します。

.. code-block:: Arduino
    :emphasize-lines: 10,12

    void loop() {
        int buttonState = digitalRead(7);  // Read the state of the button
        Serial.print("Button State: ");
        Serial.println(buttonState);  // Print the current button state
        
        // Check if button state has changed from the last loop iteration
        if (lastButtonState == HIGH && buttonState == LOW) {  // Button press detected
            ledState = !ledState;                               // Toggle LED state
        }
        if (ledState == HIGH) {

        }
        lastButtonState = buttonState;  // Update lastButtonState to the current state
        delay(200);                     // Optional: Simple software debouncing
    }

2. ``if (ledState == HIGH)``ブロックの中で、ポテンショメータの値を読み取って明るさレベルを決定します。次に、 ``analogWrite()`` を使用してこの値を適用し、LEDの明るさを調整します。また、シリアルモニタにこの値をリアルタイムでフィードバックするために出力します。

.. code-block:: Arduino
    :emphasize-lines: 6-9

    // Check if button state has changed from the last loop iteration
    if (lastButtonState == HIGH && buttonState == LOW) {  // Button press detected
        ledState = !ledState;                               // Toggle LED state
    }
    if (ledState == HIGH) {
        potValue = analogRead(A0);  // Continuously read value from potentiometer when LED is on
        analogWrite(9, potValue / 4);  // Adjust brightness continuously
        Serial.print("Pot Value: ");
        Serial.println(potValue);
    }
    lastButtonState = buttonState;  // Update lastButtonState to the current state
    delay(200);                     // Optional: Simple software debouncing

3. ``ledState`` が ``LOW`` の場合、LEDをオフにするための ``else`` 文を ``if`` ブロックの後に追加します。これにより、 ``if`` の条件が満たされない場合にLEDを完全にオフにします。

.. image:: img/if_else.png
    :width: 400
    :align: center

.. code-block:: Arduino
    :emphasize-lines: 6-8

    if (ledState == HIGH) {
        potValue = analogRead(A0);  // Continuously read value from potentiometer when LED is on
        analogWrite(9, potValue / 4);  // Adjust brightness continuously
        Serial.print("Pot Value: ");
        Serial.println(potValue);
    } else {
        analogWrite(9, 0);  // Adjust brightness continuously
    }
    
**コードの実行**

コードが完成したので、全体のリストは次のようになります：

.. code-block:: Arduino

    int potValue = 0;            // Variable to store the value read from the potentiometer
    int ledState = LOW;          // Initial state of the LED
    int lastButtonState = HIGH;  // the previous reading from the input pin

    void setup() {
        pinMode(9, OUTPUT);        // Set pin 9 as output
        pinMode(7, INPUT_PULLUP);  // Set pin 7 as input with an internal pull-up resistor
        Serial.begin(9600);        // Serial communication setup at 9600 baud
    }

    void loop() {
        int buttonState = digitalRead(7);  // Read the state of the button
        Serial.print("Button State: ");
        Serial.println(buttonState);

        // Check if button state has changed from the last loop iteration
        if (lastButtonState == HIGH && buttonState == LOW) {  // Button press detected
            ledState = !ledState;                               // Toggle LED state
        }

        if (ledState == HIGH) {
            potValue = analogRead(A0);  // Continuously read value from potentiometer when LED is on
            analogWrite(9, potValue / 4);  // Adjust brightness continuously
            Serial.print("Pot Value: ");
            Serial.println(potValue);
        } else {
            analogWrite(9, 0);  // Adjust brightness continuously
        }

        lastButtonState = buttonState;  // Update lastButtonState to the current state
        delay(200);                     // Optional: Simple software debouncing
    }

1. 正しいボードとポートを選択した後、「Upload」をクリックしてコードをArduinoにアップロードします。

2. シリアルモニタを開いて出力データを確認します。ボタンが押されていないときは「1」が連続して表示され、押された瞬間は「0」が表示されることがわかります。同時に、ポテンショメータからの値も表示されます。ポテンショメータを回すと、その値が高くなるほどLEDが明るくなり、逆に低くなると暗くなります。
    
.. image:: img/10_dimmer_led_serial_tool.png
    :align: center

.. note::

    これにより、以下が明確に理解できるはずです：

    - デジタル信号は0と1の2つの状態しか持たない。
    - アナログ信号は0から1023までの範囲を持つ。

3. 最後に、コードを保存して作業スペースを整理整頓しましょう。

**質問**

1. デジタルピン7を単にINPUTに設定した場合、何が起こるでしょうか？なぜですか？

.. code-block::
    :emphasize-lines: 3

    void setup() {
        pinMode(9, OUTPUT);        // Set pin 9 as output
        pinMode(7, INPUT);  // Set pin 7 as input with an internal pull-up resistor
        Serial.begin(9600);        // Serial communication setup at 9600 baud
    }

2. ピン7を ``INPUT`` に設定するだけの場合、回路にはどのような調整が必要ですか？

**まとめ**

このレッスンの終わりまでに、シンプルなユーザーインターフェースを介して制御される完全な機能を持つON/OFFデスクランプが完成します。さまざまな電子部品の統合とArduinoプログラミング技術を駆使して、実用的でインタラクティブな電子デバイスを作成する方法を習得します。このプロジェクトは、エレクトロニクスとプログラミングの基本概念を強化するだけでなく、DIYプロジェクトのコレクションに追加できる機能的な作品を提供します。
