.. note::

    こんにちは、SunFounderのRaspberry Pi & Arduino & ESP32愛好家コミュニティへようこそ！Facebookで一緒にRaspberry Pi、Arduino、ESP32についてもっと深く学びましょう。

    **参加する理由**

    - **専門的なサポート**: コミュニティとチームの助けを借りて、販売後の問題や技術的な課題を解決しましょう。
    - **学びと共有**: スキルを向上させるためのヒントやチュートリアルを交換しましょう。
    - **独占プレビュー**: 新製品の発表や予告をいち早く手に入れましょう。
    - **特別割引**: 最新の製品を特別価格で楽しみましょう。
    - **お祭りプロモーションとギブアウェイ**: ギブアウェイや祝祭のプロモーションに参加しましょう。

    👉 さあ、私たちと一緒に探検し、創造しましょう！クリックして[|link_sf_facebook|]今すぐ参加！

25. 74HC595で数字を表示する
==================================

前のレッスンで、74HC595と7セグメントディスプレイが絶妙なペアであることに気付いたかもしれません。74HC595は8ビット信号を同時に出力でき、7セグメントディスプレイは8つの電気信号（小数点LEDセグメント、つまりdpセグメントを含む）で制御されます。

それでは、74HC595を使用して7セグメントディスプレイを制御できるでしょうか？答えは「はい」です。

このレッスンでは、74HC595を使用して7セグメントディスプレイを制御し、異なる数字を表示する方法を学びます。

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/25_show_number.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

このレッスンでは、以下を学ぶことができます：

* 74HC595シフトレジスタを使用して7セグメントディスプレイを駆動する方法を理解する。
* 数字0から9のバイナリ表現を学び、それらを10進数および16進数に変換する方法を理解する。
* シリアルモニタを使用してデータを入力し、それを7セグメントディスプレイに表示する方法を理解する。


回路の構築
--------------------------------

**必要なコンポーネント**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * 7セグメントディスプレイ
     - 1 * 220Ω抵抗
     - 1 * 74HC595
   * - |list_uno_r3| 
     - |list_7segment| 
     - |list_220ohm| 
     - |list_74hc595| 
   * - 1 * ブレッドボード
     - ジャンパーワイヤー
     - 1 * USBケーブル
     -
   * - |list_breadboard| 
     - |list_wire| 
     - |list_usb_cable| 
     -

**ステップバイステップの構築**

配線図または以下の手順に従って回路を構築します。

.. image:: img/25_show_number.png
    :width: 500
    :align: center

1. 小数点が右下にくるようにして、7セグメントディスプレイをブレッドボードに挿入します。

.. image:: img/25_show_number_7segment.png
    :width: 500
    :align: center

2. 7セグメントディスプレイの負極（-）端子をジャンパーワイヤーでブレッドボードのグランドレールに接続します。

.. image:: img/25_show_number_resistor.png
    :width: 500
    :align: center

3. 74HC595チップを見つけてブレッドボードに挿入します。チップが中央のギャップをまたぐように配置してください。

.. image:: img/25_show_number_74hc595.png
    :width: 500
    :align: center

4. 74HC595のVCCおよびMRピンをブレッドボードのプラスレールに接続します。

.. image:: img/25_show_number_vcc.png
    :width: 500
    :align: center

5. 74HC595のCEおよびGNDピンをブレッドボードのマイナスレールに接続します。

.. image:: img/25_show_number_gnd.png
    :width: 500
    :align: center

6. 74HC595のQ0を7セグメントディスプレイの'a'ピンに、Q1を'b'ピンに、Q2を'c'ピンに、Q3を'd'ピンに、Q4を'e'ピンに接続します。

.. image:: img/25_show_number_q0_q4.png
    :width: 500
    :align: center

7. 74HC595のQ5を7セグメントディスプレイの'f'ピンに、Q6を'g'ピンに、Q7を'dp'ピンに接続します。

.. image:: img/25_show_number_q5_q7.png
    :width: 500
    :align: center

8. 74HC595のDSピンをArduino Uno R3のピン11に接続します。

.. image:: img/25_show_number_pin11.png
    :width: 500
    :align: center

9. 74HC595のST_CPピンをArduino Uno R3のピン12に接続します。

.. image:: img/25_show_number_pin12.png
    :width: 500
    :align: center

10. 74HC595のSH_CPピンをArduino Uno R3のピン8に接続します。

.. image:: img/25_show_number_pin8.png
    :width: 500
    :align: center

11. 最後に、Arduino Uno R3のGNDピンと5Vピンをそれぞれブレッドボードのマイナスおよびプラスレールに接続します。

.. image:: img/25_show_number.png
    :width: 500
    :align: center

12. 次の表は、74HC595、Arduino Uno R3、および7セグメントディスプレイの間のピン接続を示しています。

.. list-table::
    :widths: 20 20
    :header-rows: 1

    *   - 74HC595
        - Arduino UNO R3
    *   - VCC
        - 5V
    *   - DS
        - 11
    *   - CE
        - GND
    *   - ST_CP
        - 12
    *   - SH_CP
        - 8
    *   - MR
        - 5V
    *   - GND
        - GND

.. list-table::
    :widths: 20 20
    :header-rows: 1

    *   - 74HC595
        - 7セグメントディスプレイ
    *   - Q0
        - a
    *   - Q1
        - b 
    *   - Q2
        - c
    *   - Q3
        - d
    *   - Q4
        - e
    *   - Q5
        - f
    *   - Q6
        - g
    *   - Q7
        - dp

数字0から9のバイナリ数
------------------------------------

このプロジェクトでは、74HC595シフトレジスタを使用して7セグメントディスプレイに異なる数字を表示させます。しかし、74HC595はバイナリ数を受け取るため、プログラミングの前に、数字0から9の対応するバイナリ数を知る必要があります。

7セグメントディスプレイに数字2を表示させたいと仮定します。セグメントfとcをオフにし、他のセグメントをオンにする必要があります。

.. image:: img/23_segment_2.png
    :align: center
    :width: 200

配線図によると、74HC595の出力ピンQ0からQ7は、図に示すように7セグメントディスプレイの対応するピンに対応しています。バイナリでは、0はオフ（閉）、1はオン（開）を表します。数字2を表示するには、dp、f、およびcを0にし、他のセグメントを1にする必要があり、結果としてバイナリ数「B01011011」になります。

.. image:: img/25_display_2_binary.png
    :align: center
    :width: 600

.. note::

    1つの7セグメントディスプレイしかない場合、DPピンは常に0に設定されます。複数の7セグメントディスプレイをデイジーチェーン構成で使用する場合、DPピンを使用して小数点を示すことができます。

数字0を表示するには、dpとgを0にし、他のすべてのセグメントを1にします。これにより、バイナリ数「B00111111」が得られます。

**質問**

数字0と2のバイナリ表現がわかったので、以下の表に残りの数字のバイナリ数を記入してください。

.. list-table::
    :widths: 20 20
    :header-rows: 1

    *   - 数字
        - バイナリ
    *   - 0
        - B00111111
    *   - 1
        -
    *   - 2
        - B01011011
    *   - 3
        -
    *   - 4
        -
    *   - 5
        -
    *   - 6
        -
    *   - 7
        -
    *   - 8
        -
    *   - 9
        -        


コード作成 - 数字の表示
------------------------------------------
1. 以前保存したスケッチ ``Lesson24_Flowing_Light`` を開きます。

2. 「ファイル」メニューから「名前を付けて保存」を選択し、名前を ``Lesson25_Show_Number_Binary`` に変更します。「保存」をクリックします。

3. 「datArray[]」を、数字0から9に対応するバイナリ数に変更します。

.. code-block:: Arduino
    :emphasize-lines: 5

    const int STcp = 12;  //Pin connected to ST_CP of 74HC595
    const int SHcp = 8;   //Pin connected to SH_CP of 74HC595
    const int DS = 11;    //Pin connected to DS of 74HC595
    //display 0,1,2,3,4,5,6,7,8,9
    int datArray[] = { B00111111, B00000110, B01011011, B01001111, B01100110, B01101101, B01111101, B00000111, B01111111, B01101111 };


4. ``datArray[]`` 配列には10個の要素が含まれているため、変数 ``num`` の範囲を ``num <= 9`` に修正します。

.. code-block:: Arduino
    :emphasize-lines: 2

    void loop() {
        for (int num = 0; num <= 9; num++) {
            digitalWrite(STcp, LOW);                      // Ground ST_CP and hold low while transmitting
            shiftOut(DS, SHcp, MSBFIRST, datArray[num]);  // Shift out the data, MSB first
            digitalWrite(STcp, HIGH);                     // Pull ST_CP high to save the data
            delay(1000);                                  // Wait for a second
        }
    }

5. 完成したコードは次のようになります。この時点で、コードをArduino Uno R3にアップロードすると、7セグメントディスプレイに数字0から9が順番に表示されるのが見えます。

.. code-block:: Arduino

    const int STcp = 12;  //Pin connected to ST_CP of 74HC595
    const int SHcp = 8;   //Pin connected to SH_CP of 74HC595
    const int DS = 11;    //Pin connected to DS of 74HC595
    //display 0,1,2,3,4,5,6,7,8,9
    int datArray[] = { B00111111, B00000110, B01011011, B01001111, B01100110, B01101101, B01111101, B00000111, B01111111, B01101111 };

    void setup() {
        //set pins to output
        pinMode(STcp, OUTPUT);
        pinMode(SHcp, OUTPUT);
        pinMode(DS, OUTPUT);
    }

    void loop() {
        for (int num = 0; num <= 9; num++) {
            digitalWrite(STcp, LOW);                      // Ground ST_CP and hold low while transmitting
            shiftOut(DS, SHcp, MSBFIRST, datArray[num]);  // Shift out the data, MSB first
            digitalWrite(STcp, HIGH);                     // Pull ST_CP high to save the data
            delay(1000);                                  // Wait for a second
        }
    }

バイナリ変換
------------------

実際のアプリケーションでは、バイナリ数を書くことでデータ内の各ビットの状態を明確に表現できます。しかし、一般的な数値表現には、10進数を書く方が便利です。

.. note::

    バイナリ、10進数、または16進数を書くことは、プログラムの結果に影響を与えることはなく、コードの可読性にのみ影響します。たとえば、10進数の ``91`` を書いても、内部ではバイナリ形式の ``B01011011`` に変換されます。

バイナリ数を10進数に変換する方法を見てみましょう。

**10進数への変換**

バイナリシステムでは、各ビットは対応する位の値を表します。位の値は2の累乗で、2^0、2^1、2^2…のようになります。各ビットを対応する位の値で掛け合わせ、その結果をすべて足し合わせることで、10進数を得ることができます。

たとえば、バイナリ数 ``B01011011`` は10進数の91に変換されます。

.. image:: img/25_binary_dec.png
    :align: center
    :width: 600
 
**電卓の使用**

実際のアプリケーションでは、コンピュータの電卓を使用できます。プログラマモードに切り替えると、バイナリ、10進数、および16進数の間で簡単に変換できます。

コンピュータで "Calculator" を検索し、 **Programmer** モードに切り替えます。

.. image:: img/25_calculator_programmer.png
    :align: center

2. すでにバイナリ数を知っていて、それを他の基数に変換したい場合は、 **BIN** を選択します。

.. image:: img/25_calculator_binary.png
    :align: center

3. ここで、バイナリ数を入力し始めます。

* バイナリの有効ビットは、最も重要なビット（左端の非ゼロビット）から最も重要でないビット（右端の非ゼロビット）までの範囲を指します。
* したがって、バイナリ数 ``B00111111`` の場合、有効ビットは ``111111`` です。
* ここで、電卓に ``111111`` を入力して、対応する10進数および16進数を取得します。

.. image:: img/25_calculator_binary_0.png
    :align: center
    :width: 300

**質問**

バイナリ数を表す数字0から9を10進数および16進数に変換し、表に記入してください。これにより、基数変換のクイックリファレンスガイドが得られます。

.. list-table::
    :widths: 20 40 30 30
    :header-rows: 1

    *   - 数字
        - バイナリ
        - 10進数
        - 16進数
    *   - 0
        - B00111111
        - 63
        - 0x3F
    *   - 1
        - B00000110
        -
        -
    *   - 2
        - B01011011
        -
        -
    *   - 3
        - B01001111
        -
        -
    *   - 4
        - B01100110
        -
        -
    *   - 5
        - B01101101
        -
        -
    *   - 6
        - B01111101
        -
        -
    *   - 7
        - B00000111
        -
        -
    *   - 8
        - B01111111
        -
        -
    *   - 9
        - B01101111
        -
        -

**スケッチの修正**

次に、Arduino IDEで ``Lesson25_Show_Number_Binary`` スケッチを開きます。「ファイル」 -> 「名前を付けて保存」をクリックし、ファイル名を ``Lesson25_Show_Number_Decimal`` に変更します。「保存」をクリックします。

``datArray[]`` のすべての要素を10進数に変更します。修正後、コードをArduino Uno R3にアップロードして効果を確認します。

.. code-block:: Arduino

    const int STcp = 12;  //Pin connected to ST_CP of 74HC595
    const int SHcp = 8;   //Pin connected to SH_CP of 74HC595
    const int DS = 11;    //Pin connected to DS of 74HC595
    //display 0,1,2,3,4,5,6,7,8,9
    int datArray[] = { 63, 6, 91, 79, 102, 109, 125, 7, 127, 111 };

    void setup() {
        //set pins to output
        pinMode(STcp, OUTPUT);
        pinMode(SHcp, OUTPUT);
        pinMode(DS, OUTPUT);
    }

    void loop() {
        for (int num = 0; num <= 9; num++) {
            digitalWrite(STcp, LOW);                      // Ground ST_CP and hold low while transmitting
            shiftOut(DS, SHcp, MSBFIRST, datArray[num]);  // Shift out the data, MSB first
            digitalWrite(STcp, HIGH);                     // Pull ST_CP high to save the data
            delay(1000);                                  // Wait for a second
        }
    }

コード作成 - シリアル入力
---------------------------------

シリアルモニタは、Arduino IDEが提供する強力なツールで、Arduinoボードとの通信に使用されます。私たちはこれを使って、フォトレジスタからのアナログ値を読み取るなど、Arduinoからのデータ出力を監視しました。また、シリアルモニタを使用してArduinoにデータを送信し、受信したデータに基づいてアクションを実行させることもできます。

このアクティビティでは、シリアルモニタに0から9の数字を入力して、7セグメントディスプレイに表示します。


1. Arduino IDEで ``Lesson25_Show_Number_Decimal`` スケッチを開きます。「ファイル」->「名前を付けて保存」をクリックし、ファイル名を ``Lesson25_Show_Number_Serial`` とします。「保存」をクリックします。

2. ``void setup()`` でシリアルモニタを開始し、そのボーレートを9600に設定します。

.. code-block:: Arduino
    :emphasize-lines: 6

    void setup() {
        // ピンを出力に設定
        pinMode(STcp, OUTPUT);
        pinMode(SHcp, OUTPUT);
        pinMode(DS, OUTPUT);
        Serial.begin(9600);  // シリアル通信の設定（9600ボーレート）
    }

3. シリアルモニタを使用する際には、Arduinoコードを通じて入力されたデータを読み取ることができます。ここでは、次の2つの関数を理解する必要があります：

* ``Serial.available()``: シリアルポートから読み取ることができるバイト（文字）の数を取得します。これはすでに到着してシリアル受信バッファ（64バイト保持）に格納されたデータです。
* ``Serial.read()``: シリアル入力経由で受信した文字のASCIIコードを返します。

次に、 ``void loop()`` でデータがポートから読み取られたかどうかを確認し、それを表示するために ``if`` 文を使用します。

.. note::

    印刷プロセスに影響を与えないように、7セグメントディスプレイに文字を表示するための ``void loop()`` のfor文を一時的にコメントアウトしてください。

.. code-block:: Arduino
    :emphasize-lines: 2-5

    void loop() {
        if (Serial.available() > 0) {
            // シリアルポートから受信した文字を表示
            Serial.println(Serial.read());
        }

        // for (int num = 0; num <= 9; num++) {
        //   digitalWrite(STcp, LOW);                      // ST_CPをグランドに接続し、送信中は低く保持
        //   shiftOut(DS, SHcp, MSBFIRST, datArray[num]);  // データをMSBから先にシフトアウト
        //   digitalWrite(STcp, HIGH);                     // ST_CPを高くしてデータを保存
        //   delay(1000);                                  // 1秒待機
        // }
    }

4. 完全なコードは以下の通りです。この時点で、コードをArduino Uno R3にアップロードできます。

.. code-block:: Arduino

    const int STcp = 12;  // 74HC595のST_CPに接続されたピン
    const int SHcp = 8;   // 74HC595のSH_CPに接続されたピン
    const int DS = 11;    // 74HC595のDSに接続されたピン
    // 0,1,2,3,4,5,6,7,8,9を表示
    int datArray[] = { 63, 6, 91, 79, 102, 109, 125, 7, 127, 111 };

    void setup() {
        // ピンを出力に設定
        pinMode(STcp, OUTPUT);
        pinMode(SHcp, OUTPUT);
        pinMode(DS, OUTPUT);
        Serial.begin(9600);  // シリアル通信の設定（9600ボーレート）
    }

    void loop() {
        if (Serial.available() > 0) {
            // シリアルポートから受信した文字を表示
            Serial.println(Serial.read());
        }

        // for (int num = 0; num <= 9; num++) {
        //   digitalWrite(STcp, LOW);                      // ST_CPをグランドに接続し、送信中は低く保持
        //   shiftOut(DS, SHcp, MSBFIRST, datArray[num]);  // データをMSBから先にシフトアウト
        //   digitalWrite(STcp, HIGH);                     // ST_CPを高くしてデータを保存
        //   delay(1000);                                  // 1秒待機
        // }
    }

5. アップロード後、シリアルモニタを開きます。入力ボックスに数字 ``0`` （または0-9の任意の数字）を入力し、エンターキーを押します。この時点で、シリアルモニタに ``48`` という数字が表示されるのを確認できます。

.. note::

    * シリアルモニタの行末オプションで「Newline」が選択されている場合、 ``10`` も表示されます。
    * ``10`` は改行文字（LF - Line Feed）のASCIIコードです。

.. image:: img/25_serial_read.png
    :align: center
    :width: 600

では、入力した ``0`` はどこに行ったのでしょうか？ ``48`` はどこから来たのでしょうか？ ``0`` が ``48`` である可能性はあるのでしょうか？

これは、シリアルモニタに入力した ``0`` が「数値」ではなく「文字」として扱われるためです。

文字の転送は、ASCII（American Standard Code for Information Interchange）という標準コードに従います。

ASCIIには、大文字（A-Z）、小文字（a-z）、数字（0-9）、句読点（ピリオド、カンマ、感嘆符など）などの一般的な文字が含まれています。また、デバイスや通信プロトコルを制御するために使用されるいくつかの制御文字も定義されています。これらの制御文字は通常画面に表示されませんが、プリンターや端末などのデバイスの動作を制御するために使用されます。例として、改行、バックスペース、キャリッジリターンなどがあります。

以下はASCII表です：

.. image:: img/25_ascii_table.png
    :align: center
    :width: 800

シリアルモニタに文字 ``0`` を入力すると、文字 ``0`` のASCIIコードがArduinoに送信されます。
ASCIIでは、文字 ``0`` のコードは10進数で ``48`` です。
6. コードを続ける前に、以下のコードが干渉しないように、前回のASCIIコードを表示するコードをコメントアウトする必要があります。

.. code-block:: Arduino
    :emphasize-lines: 4

    void loop() {
        if (Serial.available() > 0) {
            // シリアルポートから受信した文字を表示
            // Serial.println(Serial.read());
        }

        // for (int num = 0; num <= 9; num++) {
        //   digitalWrite(STcp, LOW);                      // ST_CPをグランドに接続し、送信中は低く保持
        //   shiftOut(DS, SHcp, MSBFIRST, datArray[num]);  // データをMSBから先にシフトアウト
        //   digitalWrite(STcp, HIGH);                     // ST_CPを高くしてデータを保存
        //   delay(1000);                                  // 1秒待機
        // }
    }

7. シリアルモニタから読み取った文字を格納するために、新しい ``char`` 変数を作成する必要があります。

.. code-block:: Arduino
    :emphasize-lines: 6,7

    void loop() {
        if (Serial.available() > 0) {
            // シリアルポートから受信した文字を表示
            // Serial.println(Serial.read());

            // シリアルポートから受信した文字を読み取る
            char receivedChar = Serial.read();
        }
    }

8. 次に、文字を数字に変換します。ASCIIでは、文字 ``'0'`` の値は ``48`` 、 ``'1'`` は ``49`` となります。そのため、文字 ``'0'`` のASCIIコードを引くことで、対応する数値を得ることができます。

.. code-block:: Arduino
    :emphasize-lines: 8,9

    void loop() {
        if (Serial.available() > 0) {
            // シリアルポートから受信した文字を表示
            Serial.println(Serial.read());

            // シリアルポートから受信した文字を読み取る
            char receivedChar = Serial.read();
            // 文字を数字に変換する
            int digit = receivedChar - '0';
        }
    }

9. この例では、入力が数値文字 ``'0'`` から ``'9'`` であることを前提としています。したがって、入力文字がこの範囲内にあるかどうかだけを気にします。このため、数値が有効な範囲内にあるかどうかを確認する必要があります。

* 前にコメントアウトした ``for`` ループ文を選択し、 ``Ctrl + /`` を押してコメントを解除します。
* 次に、 ``for`` 文を ``if`` 文に変更して、入力文字が ``'0'`` から ``'9'`` の範囲内であるかどうかを確認します。範囲内であれば、7セグメントディスプレイに対応する数字を表示させます。

.. code-block:: Arduino
    :emphasize-lines: 9

    void loop() {
        if (Serial.available() > 0) {
            // シリアルポートから受信した文字を表示
            // Serial.println(Serial.read());

            // シリアルポートから受信した文字を読み取る
            char receivedChar = Serial.read();
            // 文字を数字に変換する
            int digit = receivedChar - '0';

            if (digit >= 0 && digit <= 9) {
                digitalWrite(STcp, LOW);                        // ST_CPをグランドに接続し、送信中は低く保持
                shiftOut(DS, SHcp, MSBFIRST, datArray[digit]);  // データをMSBから先にシフトアウト
                digitalWrite(STcp, HIGH);                       // ST_CPを高くしてデータを保存
                delay(1000);                                    // 1秒待機
            }
        }
    }

10. 完全なコードは以下の通りです。これで、コードをArduino Uno R3にアップロードし、シリアルモニタを開くことができます。0から9までの任意の数字を入力して、7セグメントディスプレイに対応する数字が表示されるか確認してください。

.. code-block:: Arduino

    const int STcp = 12;  // 74HC595のST_CPに接続されたピン
    const int SHcp = 8;   // 74HC595のSH_CPに接続されたピン
    const int DS = 11;    // 74HC595のDSに接続されたピン
    // 0,1,2,3,4,5,6,7,8,9を表示
    int datArray[] = { 63, 6, 91, 79, 102, 109, 125, 7, 127, 111 };

    void setup() {
        // ピンを出力に設定
        pinMode(STcp, OUTPUT);
        pinMode(SHcp, OUTPUT);
        pinMode(DS, OUTPUT);
        Serial.begin(9600);  // シリアル通信の設定（9600ボーレート）
    }   

    void loop() {
        if (Serial.available() > 0) {
            // シリアルポートから受信した文字を表示
            // Serial.println(Serial.read());

            // シリアルポートから受信した文字を読み取る
            char receivedChar = Serial.read();
            // 文字を数字に変換する
            int digit = receivedChar - '0';

            if (digit >= 0 && digit <= 9) {
                digitalWrite(STcp, LOW);                        // ST_CPをグランドに接続し、送信中は低く保持
                shiftOut(DS, SHcp, MSBFIRST, datArray[digit]);  // データをMSBから先にシフトアウト
                digitalWrite(STcp, HIGH);                       // ST_CPを高くしてデータを保存
                delay(1000);                                    // 1秒待機
            }
        }
    }

11. 最後に、コードを保存し、作業スペースを整理することを忘れないでください。

**まとめ**

このレッスンでは、74HC595シフトレジスタを使用して7セグメントディスプレイを駆動し、Arduino Uno R3に必要なピンの数を減らす方法を学びました。また、表示する数字のバイナリ表現を探り、バイナリ数を10進数や16進数形式に変換する方法を理解し、コードをより読みやすくしました。

さらに、シリアルモニタを使用してシリアル入力を行い、入力文字が内部でASCIIコードに変換される方法を学びました。この変換を理解することで、文字を対応する数値にマッピングし、7セグメントディスプレイに正確に表示することができました。

全体として、このレッスンではシフトレジスタの使用方法、7セグメントディスプレイの制御方法、およびインタラクティブなプロジェクトのためのシリアル通信の取り扱いについて、包括的な理解を提供しました。
