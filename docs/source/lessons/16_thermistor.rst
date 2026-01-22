.. note::

    こんにちは、SunFounderのRaspberry Pi＆Arduino＆ESP32ファンのコミュニティへようこそ！Facebookで仲間と一緒にRaspberry Pi、Arduino、ESP32についてさらに深く掘り下げましょう。

    **参加のメリット**

    - **専門サポート**：購入後の問題や技術的な課題を、コミュニティやチームの助けを借りて解決します。
    - **学び＆共有**：スキルを向上させるためのヒントやチュートリアルを交換します。
    - **独占プレビュー**：新製品の発表や先行情報にいち早くアクセスできます。
    - **特別割引**：最新製品の特別割引をお楽しみいただけます。
    - **フェスティブプロモーションとプレゼント**：ギブアウェイやホリデープロモーションに参加できます。

    👉 準備はできましたか？[|link_sf_facebook|]をクリックして、今すぐ参加しましょう！

16. 温度アラーム
========================

このレッスンでは、食品安全における温度管理の重要な役割を探ります。すべての食品が冷蔵や冷凍を必要とするわけではありません。チップス、パン、特定の果物のような常温保存可能な食品でも、品質と安全性を維持するためには適切な温度で保存する必要があります。温度監視システムを構築することで、食品を安全な温度範囲内に保ち、その範囲を超えるとアラームを発するように学びます。この実践的なプロジェクトは、食品を保護するだけでなく、環境監視の現実世界での応用に良い導入となります。

.. .. image:: img/16_temperature.jpg
..     :width: 400
..     :align: center

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/16_temp_alarm.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

このレッスンの終わりには、以下のことができるようになります：

* 食品安全における温度管理の重要性を理解する。
* 温度変化を監視するためのサーミスタを使用した回路を構築する。
* サーミスタから温度データを読み取るArduinoプログラムを書く。
* プログラミングにおいて温度データに基づいてアクション（LEDの点灯やアラームの鳴動）をトリガーするロジックを使用する。
* 電気抵抗と温度変換の概念を実際のシナリオに適用する。

回路の構築
-----------------------

**必要な部品**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * RGB LED
     - 3 * 220Ω 抵抗
     - 1 * 10KΩ 抵抗
   * - |list_uno_r3| 
     - |list_rgb_led| 
     - |list_220ohm| 
     - |list_10kohm| 
   * - 1 * サーミスタ
     - 1 * ブレッドボード
     - ジャンパーワイヤー
     - 1 * USB ケーブル
   * - |list_thermistor| 
     - |list_breadboard| 
     - |list_wire| 
     - |list_usb_cable| 
   * - 1 * マルチメーター
     - 
     - 
     - 
   * - |list_meter| 
     - 
     - 
     - 

**手順ごとの構築**

この回路はレッスン12の回路にサーミスタを追加したものです。

.. image:: img/16_temperature_alarm.png
    :width: 500
    :align: center

1. レッスン12の回路に基づいて、Arduino Uno R3のGNDピンとRGB LEDのGNDピンを接続しているジャンパーワイヤーを取り外し、それをブレッドボードの負極端子に差し込みます。その後、負極端子からRGB LEDのGNDピンにジャンパーワイヤーを接続します。

.. image:: img/16_temperature_alarm_gnd.png
    :width: 500
    :align: center

2. サーミスタを6Eと8Eの穴に挿入します。ピンは方向性がなく、自由に挿入できます。

.. image:: img/16_temperature_alarm_thermistor.png
    :width: 500
    :align: center

サーミスタは温度によって抵抗値が変わる特殊な抵抗器です。このデバイスは温度を検出し測定するのに非常に便利で、さまざまな電子プロジェクトやデバイスで温度を制御するのに役立ちます。

ここにサーミスタの電子記号があります。

.. image:: img/16_thermistor_symbol.png
    :width: 300
    :align: center

サーミスタには2つの基本的な種類があります：

* **NTCサーミスタ**：温度が上昇すると抵抗が減少します。温度センサーや回路の突入電流制限器として一般的に使用されます。
* **PTCサーミスタ**：温度が上昇すると抵抗が増加します。回路のリセット可能なヒューズとして、過電流保護に使用されることがよくあります。

このキットでは **NTC** タイプを使用します。

今、マルチメーターを使用してこのサーミスタの抵抗を測定し、温度が上昇するにつれて抵抗が減少するかどうかを確認します。

3. サーミスタの定格抵抗が10Kであるため、マルチメーターを20キロオーム（20K）レンジに設定します。

.. image:: img/multimeter_20k.png
    :width: 300
    :align: center

4. 次に、マルチメーターの赤と黒のテストリードでフォトレジスタの2つのピンに触れます。

.. image:: img/16_temperature_alarm_test.png
    :width: 500
    :align: center

5. 現在の温度下での抵抗値を読み取り、以下の表に記録します。

.. list-table::
   :widths: 20 20
   :header-rows: 1

   * - 環境
     - 抵抗値 (キロオーム)
   * - 現在の温度
     - *9.37*
   * - 高温時
     -
   * - 低温時
     -

6. まず友人にサーミスタを持ってもらうか、他の方法でサーミスタ周囲の温度を上げます（水や火は使用しないでください、安全第一です）。このときのサーミスタの抵抗値を表に記録します。

.. list-table::
   :widths: 20 20
   :header-rows: 1

   * - 環境
     - 抵抗値（キロオーム）
   * - 現在の温度
     - *9.37*
   * - 高温時
     - *6.10*
   * - 低温時
     -

7. サーミスタを屋外に置くか、扇いで周囲の温度を下げます。このときのサーミスタの抵抗値を表に記録します。

.. list-table::
   :widths: 20 20
   :header-rows: 1

   * - 環境
     - 抵抗値（キロオーム）
   * - 現在の温度
     - *9.37*
   * - 高温時
     - *6.10*
   * - 低温時
     - *12.49*

これらの測定から、周囲温度が高くなると抵抗値が低くなることがわかります。

8. 次に回路の構築を続けます。サーミスタの一端を10K抵抗に接続し、10K抵抗のもう一端をブレッドボードの負端子に接続します。

.. image:: img/16_temperature_alarm_resistor.png
    :width: 500
    :align: center

9. ブレッドボードの他端をArduino Uno R3の5Vピンに接続します。

.. image:: img/16_temperature_alarm_5v.png
    :width: 500
    :align: center

10. 最後に、フォトレジスタと10K抵抗の共通ピンをArduino Uno R3のA0ピンに接続します。

.. image:: img/16_temperature_alarm.png
    :width: 500
    :align: center

温度計算の理解
----------------------------------------
**温度公式について**

NTCサーミスタの抵抗は温度によって変化します。この関係は通常、Steinhart-Hart方程式で正確に記述されます。

.. image:: img/16_format_steinhart.png
    :width: 400
    :align: center

ここで、a、b、およびcはSteinhart-Hartパラメータと呼ばれ、各デバイスに対して指定する必要があります。Tは絶対温度であり、Rは抵抗です。

Steinhart-Hart方程式に加えて、多くの実用的なアプリケーションでは、ベータパラメータモデルに基づく簡略化された公式も使用して温度を迅速に計算します。このモデルでは、抵抗と温度の関係をより簡単な指数関数的関係で近似し、計算プロセスを簡素化し、エンジニアリングアプリケーションでの迅速な温度監視に適しています。

.. image:: img/16_format_3.png
    :width: 400
    :align: center

* **T**: サーミスタの温度（ケルビン）。
* **T0**: 基準温度、通常は25°C（ケルビンでは273.15 + 25）。
* **B**: 材料のベータパラメータ、このキットに使用されているNTCサーミスタのベータ係数は3950です。
* **R**: 測定した抵抗値。
* **R0**: 基準温度T0での抵抗、このキットに使用されているNTCサーミスタの25°Cでの抵抗は10キロオームです。

上記の公式を変換すると、ケルビン温度は次のように計算されます: ``T=1/(ln(R/R0)/B+1/T0)`` , 273.15を引くと摂氏に変換されます。

**抵抗の測定方法**

サーミスタと10K抵抗を直列に接続します。

.. image:: img/16_thermistor_sch.png
    :width: 200
    :align: center

A0ピンで測定した電圧を直列抵抗（10K抵抗）で割ると、回路を流れる電流がわかります。この電流は、全電圧を回路全体の抵抗（直列抵抗+サーミスタ）で割ることで得られます。

.. image:: img/16_format_1.png
    :width: 400
    :align: center

* **Vsupply**: 回路に供給される電圧。
* **Rseries**: 直列抵抗の抵抗値。
* **Vmeasured**: 10K抵抗の両端の電圧、つまりA0ピンでの電圧。

これらから、サーミスタの抵抗を求めるために公式を再配置できます。

.. image:: img/16_format_2.png
    :width: 400
    :align: center

コードでは、 ``analogRead()`` 関数を使用してA0ピンでの電圧を読み取ります。電圧 **Vmeasured** と読み取ったアナログ値との関係は次の通りです:

.. code-block::

    (A0のアナログ値) / 1023.0 = Vmeasured / Vsupply

上記の公式を使用して、サーミスタの抵抗を計算します:

.. code-block::

    R_thermistor = R_series x (1023.0 / (A0のアナログ値) - 1)
.. note::

    もしこれらの数式が複雑に感じる場合は、ここに示した最終的な式だけを覚えておけば大丈夫です。

    サーミスタの抵抗値は次の式で求められます：

    .. code-block::

        R_thermistor =R_series x (1023.0 / (Analog value at A0) - 1)

    次に、次の式を使ってケルビン温度を計算します：

    .. code-block::

        T=1/(ln(R/R0)/B+1/T0)

    * **T0**: 273.15 + 25
    * **B**: 3950
    * **R**: 測定した抵抗値
    * **R0**: 10キロオーム

    最後に、次の式を使って摂氏温度に変換します：

    .. code-block::

        Tc = T - 273.15

    
コード作成
---------------

**温度の取得**

1. Arduino IDEを開き、「ファイル」メニューから「新しいスケッチ」を選択して新しいプロジェクトを開始します。
2. スケッチを ``Ctrl + S`` を押すか「保存」をクリックして ``Lesson16_Temperature_Alarm`` として保存します。

3. 前のレッスンでは、RGB LEDのピンを直接コード内で参照していましたが、ここではそれらを定数として定義します。

.. code-block:: Arduino
    :emphasize-lines: 2-5

    // ピンの設定
    const int tempSensorPin = A0;  // NTCサーミスタのアナログ入力ピン
    const int redPin = 11;         // 赤色LEDのデジタルピン
    const int greenPin = 10;       // 緑色LEDのデジタルピン
    const int bluePin = 9;         // 青色LEDのデジタルピン

    void setup() {
        // 初期設定コードをここに記述します。一度だけ実行されます。
    }

変数ではなく定数を使用することで、プログラム全体で変更されない値を明確にし、保守を簡素化できます。これにより、数字の代わりに意味のある名前を使用でき、コード全体で変更が必要な場合は宣言部だけを修正すれば済みます。定数は変数と同じ命名規則に従い、Arduino IDEの予約語やコマンドを避ける必要があります。

4. サーミスタを使用する前に、回路に関連するパラメータを格納するための定数をさらに定義する必要があります。

.. note::
 
    ``int`` 型定数と ``float`` 型定数があることに気づくでしょう。それでは、これら二つの型の定数の違いは何でしょうか？

  * ``const int`` : ``int`` （整数）は、整数値を保持します。この型は小数点や分数をサポートしません。システムに依存しますが、通常は16ビットまたは32ビットのメモリを使用します。
  * ``const float`` : ``float`` （浮動小数点数）は、小数部分を持つ数値を保持します。測定値や計算で小数点以下の精度が必要な場合に使用します。 ``float`` は通常32ビットのメモリを使用し、 ``int`` よりも広い範囲の数値を表すことができます。

.. code-block:: Arduino
    :emphasize-lines: 2-5

    // ピンの設定
    const int tempSensorPin = A0;  // NTCサーミスタのアナログ入力ピン
    const int redPin = 10;         // 赤色LEDのデジタルピン
    const int greenPin = 11;       // 緑色LEDのデジタルピン
    const int bluePin = 12;        // 青色LEDのデジタルピン

    // 温度計算のための定数
    const float beta = 3950.0;               // NTCサーミスタのベータ値
    const float seriesResistor = 10000;      // 直列抵抗の値（オーム）
    const float roomTempResistance = 10000;  // 25°CでのNTC抵抗値
    const float roomTemp = 25 + 273.15;      // 室温（ケルビン）

5. ``void setup()`` 内で、RGB LEDピンを出力として設定し、シリアル通信のボーレートを9600に設定します。

.. code-block:: Arduino
    :emphasize-lines: 2-5

    void setup() {
        // Initialize LED pins as outputs
        pinMode(redPin, OUTPUT);
        pinMode(greenPin, OUTPUT);
        pinMode(bluePin, OUTPUT);
        
        // Start serial communication at 9600 baud
        Serial.begin(9600);
    }

6. まず、 ``void loop()`` 内でA0ピンのアナログ値を読み取る必要があります。

.. code-block:: Arduino
    :emphasize-lines: 2

    void loop() {
        int adcValue = analogRead(tempSensorPin);  // サーミスタの値を読み取る
    }

7. 次に、アナログ値を電圧に変換するために導き出された式を使用してサーミスタの抵抗を計算します。

.. code-block:: Arduino
    :emphasize-lines: 3

    void loop() {
        int adcValue = analogRead(tempSensorPin);                     // サーミスタの値を読み取る
        float resistance = (1023.0 / adcValue - 1) * seriesResistor;  // サーミスタの抵抗を計算
    }

8. その後、以下の式を使ってケルビン温度を計算します。

.. code-block:: Arduino
    :emphasize-lines: 6

    void loop() {
        int adcValue = analogRead(tempSensorPin);                     // サーミスタの値を読み取る
        float resistance = (1023.0 / adcValue - 1) * seriesResistor;  // サーミスタの抵抗を計算

        // ベータパラメータ方程式を使用してケルビン温度を計算
        float tempK = 1 / (log(resistance / roomTempResistance) / beta + 1 / roomTemp);
    }
    
9. ケルビン温度から273.15を引いて摂氏温度に変換し、結果を ``Serial.println()`` 関数を使ってシリアルモニタに表示します。

.. code-block:: Arduino
    :emphasize-lines: 8,9

    void loop() {
        int adcValue = analogRead(tempSensorPin);                     // サーミスタの値を読み取る
        float resistance = (1023.0 / adcValue - 1) * seriesResistor;  // サーミスタの抵抗を計算

        // ベータパラメータ方程式を使用してケルビン温度を計算
        float tempK = 1 / (log(resistance / roomTempResistance) / beta + 1 / roomTemp);
    
        float tempC = tempK - 273.15;  // 摂氏に変換
        Serial.println(tempC);         // 摂氏温度をシリアルモニタに表示
    }

10. この時点で、コードをArduino Uno R3にアップロードし、現在の摂氏温度を取得できます。

.. code-block::

    26.28
    26.19
    26.19
    26.28
    26.28

**RGB LEDの色を変更する**

次に、サーミスタで測定した温度に基づいてRGB LEDの色を変更します。

例えば、次のような温度範囲を設定します：

* 10度未満では、RGB LEDは緑色を表示し、快適な温度を示します。
* 10度から20度の間では、RGB LEDは黄色を表示し、現在の温度に注意を促します。
* 21度以上では、RGB LEDは赤色を表示し、高温であることを示し、対策が必要です。

11. RGB LEDを制御するために、前のレッスンで作成した ``setColor()`` 関数を使用します。

.. code-block:: Arduino

    // RGB LEDの色を設定する関数
    void setColor(int red, int green, int blue) {
        // PWM値を赤、緑、青の各LEDに書き込み
        analogWrite(11, red);
        analogWrite(10, green);
        analogWrite(9, blue);
    }

12. 次に、 ``if else if`` 文を使って、異なる温度に応じてRGB LEDの色を制御します。

.. code-block:: Arduino
    :emphasize-lines: 12-18

    void loop() {
        int adcValue = analogRead(tempSensorPin);                     // サーミスタの値を読み取る
        float resistance = (1023.0 / adcValue - 1) * seriesResistor;  // サーミスタの抵抗を計算

        // ベータパラメータ方程式を使用してケルビン温度を計算
        float tempK = 1 / (log(resistance / roomTempResistance) / beta + 1 / roomTemp);
    
        float tempC = tempK - 273.15;  // 摂氏に変換
        Serial.println(tempC);         // 摂氏温度をシリアルモニタに表示

        // 温度に応じてLEDの色を調整
        if (tempC < 10) {
            setColor(0, 0, 255);  // Cold: blue
        } else if (tempC >= 10 && tempC <= 21) {
            setColor(0, 255, 0);  // Comfortable: green
        } else if (tempC > 21) {
            setColor(255, 0, 0);  // Hot: red
        }
        delay(1000);  // 次の読み取りまで1秒待つ
    }

13. これでコードが完成しました。コードをArduino Uno R3にアップロードし、効果を確認してください。

.. code-block:: Arduino

    // ピンの設定
    const int tempSensorPin = A0;  // NTCサーミスタのアナログ入力ピン
    const int redPin = 10;         // 赤色LEDのデジタルピン
    const int greenPin = 11;       // 緑色LEDのデジタルピン
    const int bluePin = 12;        // 青色LEDのデジタルピン

    // 温度計算のための定数
    const float beta = 3950.0;               // NTCサーミスタのベータ値
    const float seriesResistor = 10000;      // 直列抵抗の値（オーム）
    const float roomTempResistance = 10000;  // 25°CでのNTC抵抗値
    const float roomTemp = 25 + 273.15;      // 室温（ケルビン）

    void setup() {
        // LEDピンを出力として初期化
        pinMode(redPin, OUTPUT);
        pinMode(greenPin, OUTPUT);
        pinMode(bluePin, OUTPUT);

        // シリアル通信を9600ボーレートで開始
        Serial.begin(9600);
    }

    void loop() {
        int adcValue = analogRead(tempSensorPin);                     // サーミスタの値を読み取る
        float resistance = (1023.0 / adcValue - 1) * seriesResistor;  // サーミスタの抵抗を計算

        // ベータパラメータ方程式を使用してケルビン温度を計算
        float tempK = 1 / (log(resistance / roomTempResistance) / beta + 1 / roomTemp);

        float tempC = tempK - 273.15;  // 摂氏に変換
        Serial.println(tempC);         // 摂氏温度をシリアルモニタに表示

        // 温度に応じてLEDの色を調整
        if (tempC < 10) {
            setColor(0, 0, 255);  // 寒い：青色
        } else if (tempC >= 10 && tempC <= 21) {
            setColor(0, 255, 0);  // 快適：緑色
        } else if (tempC > 21) {
            setColor(255, 0, 0);  // 暑い：赤色
        }
        delay(1000);  // 次の読み取りまで1秒待つ
    }

    // RGB LEDの色を設定する関数
    void setColor(int red, int green, int blue) {
        // PWM値を赤、緑、青の各LEDに書き込み
        analogWrite(11, red);
        analogWrite(10, green);
        analogWrite(9, blue);
    }

14. 最後に、コードを保存し、作業スペースを整理することを忘れないでください。

**質問**

1. コードでは、ケルビン温度と摂氏温度が計算されています。もし華氏温度も知りたい場合、どうすればよいでしょうか？

2. 今日作成した温度監視システムが他にどのような状況や場所で役立つか考えてみてください。

**まとめ**

今日のレッスンでは、サーミスタを使って貯蔵エリアの温度を監視する温度警報システムを作成しました。サーミスタの抵抗値を読み取り、摂氏温度に変換する方法を学びました。さらに、温度に応じてRGB LEDの色を変更するプログラムを設定し、低温、適温、高温を視覚的に警告する方法を学びました。
