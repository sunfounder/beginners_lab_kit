.. note::

    こんにちは、SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts Community（Facebook）へようこそ！Raspberry Pi、Arduino、ESP32の世界を仲間と一緒に深く掘り下げましょう。

    **参加する理由**

    - **専門サポート**：コミュニティとチームの助けを借りて、販売後の問題や技術的な課題を解決します。
    - **学びと共有**：スキルを向上させるためのヒントやチュートリアルを交換しましょう。
    - **限定プレビュー**：新製品の発表やスニークピークをいち早く入手できます。
    - **特別割引**：最新の製品に対する限定割引を楽しめます。
    - **フェスティブプロモーションとプレゼント**：プレゼントやホリデープロモーションに参加できます。

    👉 探索と創造の準備はできましたか？こちらをクリックして [|link_sf_facebook|] 参加しましょう！

19. リバースパーキングアラームシステム
===========================================

.. image:: img/19_packing.png
    :width: 600
    :align: center

車をバックさせる際には、特に視界が限られている状況で、車両の後ろの障害物に注意を払うことが重要です。
安全性を向上させるために、多くの現代の車両にはバック警告システムが装備されています。

このプロジェクトでは、Arduino、超音波センサー、アクティブブザーを使用してこのようなシステムをシミュレートします。
超音波センサーは車両の後ろの障害物までの距離を検出し、この距離が短すぎる場合にはアクティブブザーが警告音を鳴らしてドライバーに知らせます。

このプロジェクトを通じて、超音波センサーの動作原理を理解し、Arduinoを使って実際に機能するバック警告機能をプログラムおよび制御する方法を学びます。

.. raw:: html

    <video controls style = "max-width:90%">
        <source src="_static/video/19_reverse_parking_system.mp4" type="video/mp4">
        お使いのブラウザはビデオタグをサポートしていません。
    </video>
  

**超音波モジュール**

暗い部屋にいて、周りの物体が見えない状況を想像してください。この場合、手を叩いて音を出すことで音が外に伝わります。この音が壁や他の物体に当たると、反射してエコーとして戻ってきます。注意深く聞けば、このエコーを聞くことができます。音が外に伝わり、エコーが戻ってくるまでの時間を計算することで、壁や物体までの距離を大まかに推定することができます。超音波センサーも同じような方法で周囲を「見る」ことができます。

.. image:: img/19_ultrasonic_pic.png
    :width: 400
    :align: center

超音波センサーは主に送信部と受信部の2つの部分で構成されています。これはちょうど口と耳のようなものです。

1. 音波の送信:

超音波センサーが作動すると、送信部は一連の急速な音波を発信します。これはちょうど手を叩くようなものです。これらの音波は非常に高い周波数を持っているため、私たちの耳には聞こえません。

2. 音波の伝播と戻り:

音波は前方に伝わり、壁やテーブルのような物体に当たると反射して戻ってきます。

3. 音波の受信:

超音波センサーの受信部は、これらのエコーを「聞く」役割を果たします。これはちょうど耳が物体から反射して戻ってくる音波をキャッチするようなものです。

4. 距離の計算:

センサーは音波が出てから戻ってくるまでの時間を記録します。
音速は既知であるため（空気中では約340メートル毎秒）、
この時間を音速で掛けることで音波が伝わった総距離を求めることができます。
私たちが必要とするのは物体までの片道の距離だけなので、
総距離を2で割って最終的な結果を得ます。
この技術により、超音波センサーは多くの状況で非常に有用になります。
例えば、ロボットが障害物を避けるのを助けたり、
車がバックする際に車両の後ろの物体までの距離を示すことでドライバーを支援したりします。

.. image:: img/19_ultrasonic_ms.png
    :width: 500
    :align: center


**超音波のタイミング**

以下にタイミング図を示します。
トリガー入力に短い10usのパルスを供給するだけで測距を開始できます。
モジュールは40kHzで8サイクルの超音波バーストを送信し、エコーを上げます。
トリガー信号の送信とエコー信号の受信の間の時間間隔を通じて距離を計算できます。

式: us / 58 = センチメートルまたは us / 148 = インチ; または: 距離 = 高レベル時間 * 速度 (340M/S) / 2;
トリガー信号とエコー信号の衝突を防ぐために、測定サイクルを60ms以上に設定することをお勧めします。

.. image:: img/19_ultrasonic_timing.png
    :width: 600
    :align: center

回路の構築
--------------------------------

**必要なコンポーネント**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * 超音波モジュール
     - 1 * アクティブブザー
     - ジャンパーワイヤー
   * - |list_uno_r3| 
     - |list_ultrasonic| 
     - |list_active_buzzer| 
     - |list_wire| 
   * - 1 * USBケーブル
     - 1 * ブレッドボード
     - 1 * マルチメーター
     - 
   * - |list_usb_cable| 
     - |list_breadboard| 
     - |list_meter|
     - 



**ステップバイステップでの構築**

配線図または以下の手順に従って回路を構築します。



.. image:: img/19_reversing_aid_bb.png
    :width: 600
    :align: center


コード作成
-------------

1. Arduino IDEを開き、「ファイル」メニューから「新しいスケッチ」を選択して新しいプロジェクトを開始します。
2. スケッチを ``Ctrl + S`` を押すか「保存」をクリックして ``Lesson19_reversin_alarm`` として保存します。

3. まず、超音波センサーとブザーに接続されているArduinoのピンを定義する必要があります。このステップは、ハードウェアインターフェイスの基礎を設定するために重要です。

* **TRIGGER_PIN** と **ECHO_PIN** は、超音波センサーからの信号を送信および受信するために使用されます。
* **BUZZER_PIN** はブザーに接続されているピンです。

.. code-block:: Arduino

  #define TRIGGER_PIN  10
  #define ECHO_PIN     9
  #define BUZZER_PIN   2


4. setup() 関数内で、各ピンのモードを設定します。Trigピンは信号を送信するために出力に設定し、Echoピンは信号を受信するために入力に設定し、ブザーピンも音を出すために出力に設定します。

.. code-block:: Arduino

  void setup() {
    pinMode(TRIGGER_PIN, OUTPUT);
    pinMode(ECHO_PIN, INPUT);
    pinMode(BUZZER_PIN, OUTPUT);
    Serial.begin(9600); // Start serial communication for debugging and distance viewing
  }

5. measureDistance() 関数の作成:

measureDistance() 関数は、超音波センサーをトリガーしてエコーを受信し、距離を測定するロジックをカプセル化します。

a. 超音波パルスのトリガー

  * 初めに TRIGGER_PIN を低に設定してクリーンパルスを確保します。
  * ラインがクリアになるまでの短い遅延として2マイクロ秒待ちます。
  * TRIGGER_PIN に10マイクロ秒の高パルスを送信します。このパルスはセンサーに超音波を発信するよう指示します。
  * TRIGGER_PIN を再び低に設定してパルスを終了します。

  .. code-block:: Arduino

    long measureDistance() {
      digitalWrite(TRIGGER_PIN, LOW);  // パルスの前にTrigピンを低に設定
      delayMicroseconds(2);
      digitalWrite(TRIGGER_PIN, HIGH); // 高パルスを送信
      delayMicroseconds(10);           // パルスの持続時間は10マイクロ秒
      digitalWrite(TRIGGER_PIN, LOW);  // 高パルスを終了
    }

.. note::

  以前のレッスンでは、 ``int``  および ``float`` 型の変数や定数を扱いました。今回は、long と unsigned long 型の変数について理解しましょう。

  * ``long``: ``long`` 整数は、 ``int`` の拡張版です。標準の ``int`` の容量を超える大きな整数値を格納するために使用されます。通常、32ビットまたは64ビットのメモリを占有し、非常に大きな値（正および負の両方）を保持できます。
  * ``unsigned long``: ``unsigned long`` は ``long`` に似ていますが、非負の値のみを表現できます。符号用に予約されているビットを使用して保持できる値の範囲を拡張しますが、正の値に限定されます。



b. エコーの読み取り

  * pulseIn() 関数を ECHO_PIN で使用して、入力パルスの持続時間を測定します。この関数はピンが HIGH になるのを待ち、HIGH のままでいる時間を計り、その持続時間をマイクロ秒で返します。
  * この持続時間は、超音波パルスが物体に到達し、戻ってくるまでの時間です。

  .. code-block:: Arduino
    :emphasize-lines: 7

    long measureDistance() {
      digitalWrite(TRIGGER_PIN, LOW);  // パルスの前にTrigピンを低に設定
      delayMicroseconds(2);
      digitalWrite(TRIGGER_PIN, HIGH); // 高パルスを送信
      delayMicroseconds(10);           // パルスの持続時間は10マイクロ秒
      digitalWrite(TRIGGER_PIN, LOW);  // 高パルスを終了
      long duration = pulseIn(ECHO_PIN, HIGH);  // Echoピンの高レベルの持続時間を測定
    }

c. 距離の計算

  * 空気中の音速（約340 m/s）を使用します。距離を計算する公式は (duration * speed of sound) / 2 です。音波は物体まで行って戻ってくるため、片道の距離のみを必要とするため、総距離を2で割ります。
  * コード内では、0.034 cm/us（音速の cm/マイクロ秒単位）が変換係数として使用されます。

  .. code-block:: Arduino
    :emphasize-lines: 8,9

    long measureDistance() {
      digitalWrite(TRIGGER_PIN, LOW);  // パルスの前にTrigピンを低に設定
      delayMicroseconds(2);
      digitalWrite(TRIGGER_PIN, HIGH); // 高パルスを送信
      delayMicroseconds(10);           // パルスの持続時間は10マイクロ秒
      digitalWrite(TRIGGER_PIN, LOW);  // 高パルスを終了
      long duration = pulseIn(ECHO_PIN, HIGH);  // Echoピンの高レベルの持続時間を測定
      long distance = duration * 0.034 / 2;     // 距離を計算（cm単位）
      return distance;
    }


6. メインループの実装
loop() 関数内で、measureDistance() 関数を使用して頻繁に距離を測定します。この距離に基づいて、ブザーを作動させるかどうかを判断します。

.. code-block:: Arduino

  void loop() {
    long distance = measureDistance(); // 距離を測定
    Serial.print("Distance: ");
    Serial.print(distance);
    Serial.println(" cm");

    if (distance > 0 && distance <= 50) {
      digitalWrite(BUZZER_PIN, HIGH);  // 距離が近ければブザーを作動
      delay(100);                      // ブザーが100ミリ秒鳴る
      digitalWrite(BUZZER_PIN, LOW);   // ブザーをオフにする
    } else {
      digitalWrite(BUZZER_PIN, LOW);   // ブザーをオフに保つ
    }

    delay(100);  // 測定間の遅延
  }


7. これが完全なコードです。これで「アップロード」をクリックしてコードをArduino Uno R3にアップロードできます。

.. code-block:: Arduino

  #define TRIGGER_PIN  10
  #define ECHO_PIN     9
  #define BUZZER_PIN   2

  void setup() {
    pinMode(TRIGGER_PIN, OUTPUT);  // Trigピンを出力に設定
    pinMode(ECHO_PIN, INPUT);      // Echoピンを入力に設定
    pinMode(BUZZER_PIN, OUTPUT);   // ブザーピンを出力に設定
    Serial.begin(9600);            // デバッグのためにシリアル通信を開始
  }

  void loop() {
    long distance = measureDistance(); // 距離を測定する関数を呼び出す
    Serial.print("Distance: ");
    Serial.print(distance);
    Serial.println(" cm");

    if (distance > 0 && distance <= 50) { // 距離が50センチ以内であれば
      digitalWrite(BUZZER_PIN, HIGH);     // ブザーをオンにする
      delay(100);                         // ブザーが100ミリ秒鳴る
      digitalWrite(BUZZER_PIN, LOW);      // ブザーをオフにする
    } else {
      digitalWrite(BUZZER_PIN, LOW);      // ブザーをオフに保つ
    }

    delay(100);  // 測定間の遅延
  }

  long measureDistance() {
    digitalWrite(TRIGGER_PIN, LOW);  // パルスの前にTrigピンを低に設定
    delayMicroseconds(2);
    digitalWrite(TRIGGER_PIN, HIGH); // 高パルスを送信
    delayMicroseconds(10);           // パルスの持続時間は10マイクロ秒
    digitalWrite(TRIGGER_PIN, LOW);  // 高パルスを終了

    long duration = pulseIn(ECHO_PIN, HIGH);  // Echoピンの高レベルの持続時間を測定
    long distance = duration * 0.034 / 2;     // 距離を計算（cm単位）
    return distance;
  }

8. 最後に、コードを保存し、作業スペースを整理することを忘れないでください。

**質問**

このデバイスが検出する距離を小数点までより正確にするには、コードをどのように変更すればよいでしょうか？
