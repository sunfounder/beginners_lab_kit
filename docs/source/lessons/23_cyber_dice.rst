.. note::

    こんにちは、SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts Community on Facebook へようこそ！ここでラズベリーパイ、アルドゥイーノ、ESP32の世界をより深く探求し、他の愛好者と交流しましょう。

    **なぜ参加するのか？**

    - **専門的なサポート**: 購入後の問題や技術的な課題を、コミュニティやチームの助けを借りて解決できます。
    - **学びと共有**: 技術の向上に役立つヒントやチュートリアルを交換できます。
    - **限定プレビュー**: 新製品の発表やプレビューをいち早く入手できます。
    - **特別割引**: 最新の製品を特別価格で購入できます。
    - **フェスティバルプロモーションとプレゼント**: プレゼントやホリデープロモーションに参加できます。

    👉 私たちと一緒に探求し創造する準備はできましたか？今すぐ[|link_sf_facebook|]をクリックして参加しましょう！

23. サイバーダイス
=======================

このレッスンでは、デジタルエレクトロニクスとプログラミングに関する2つのプロジェクトに取り組みます。

.. image:: img/23_dice.jpg
    :align: center
    :width: 500

まず、7セグメントディスプレイの動作について学び、数字を順番に表示する方法を学びます。その後、電子ダイスを作成します。ボタンを押すだけで、1から6までのランダムな数字が7セグメントディスプレイに表示され、従来のダイスにデジタルなひねりを加えます。

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/23_cycle_dice.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

このレッスンで学ぶこと:

* 7セグメントディスプレイの原理とその機能
* switch-case文を使用してコードロジックを簡素化する方法
* whileループを使用して状態を保持し、変更が必要になるまで維持する方法
* シンプルなエレクトロニクスとインタラクティブなプログラミングを統合して、実際に使用できるサイバーダイスプロジェクトを構築する方法

ダイスの起源
-----------------------

ダイスは世界最古のギャンブルツールの一つで、紀元前数千年に遡る歴史を持っています。紀元前3000年頃、古代エジプトで誕生し、主に骨や象牙などの自然素材で作られていました。初期のダイスは形が不規則で、必ずしも完全に対称ではありませんでした。

.. image:: img/23_dice.png
    :width: 500
    :align: center

同時期に古代メソポタミア（現代のイラク）でもダイスが発見されました。古代の占い師や宗教指導者は、決定を下したり未来を予言したりするためにダイスを使用しており、宗教的および神秘的な儀式において重要な役割を果たしていました。

時が経つにつれて、ダイスの形状と製造技術は標準化されました。紀元前1世紀までには、ローマ帝国全土でダイスが広く使用されるようになり、ギャンブルだけでなく、社会的および娯楽的な目的でも使用されていました。

アジアでは、特にインドにおいて、古代の叙事詩『マハーバーラタ』にダイスの使用が記録されており、物語の中で重要な役割を果たしています。

ルネサンス期には、ダイスの生産がより洗練され、木、骨、象牙、さらには金属など、さまざまな素材が使用されるようになりました。今日では、ダイスは単なる娯楽やギャンブルの道具ではなく、教育、意思決定支援、さまざまなテーブルトップゲームなどでも使用されています。その歴史と多様性は、人類の文化と技術の進化を反映しており、チャンスと運を探求する魅力的な窓を提供しています。



7セグメントディスプレイの理解
-------------------------------------------

1. 7セグメントディスプレイを見つけます。

7セグメントディスプレイは、7つのLEDをパッケージ化した8の字型のコンポーネントです。ディスプレイ内の各LEDは位置セグメントが割り当てられており、その接続ピンの一つが長方形のプラスチックパッケージから引き出されています。これらのLEDピンは、各LEDを表す「a」から「g」までのラベルが付けられています。
他のLEDピンは一つの共通ピンに接続されています。同じパッケージ内で追加の8番目のLEDが使用されるため、2つ以上の7セグメントディスプレイを接続して10以上の数字を表示する際に、小数点（DP）を示すことができます。

.. image:: img/23_7_segment.png
    :width: 300
    :align: center

ディスプレイの共通ピンは通常、そのタイプを示します。ピン接続には、カソードが接続されたものとアノードが接続されたものの2種類があり、共通カソード（CC）と共通アノード（CA）を示します。名前が示すように、CCディスプレイは7つのLEDのカソードがすべて接続されており、CAディスプレイは7つのセグメントのアノードがすべて接続されています。

.. note::

    通常、7セグメントディスプレイの側面には、xxxAxまたはxxxBxというラベルがあります。一般に、xxxAxは共通カソード、xxxBxは共通アノードを示します。私たちのキットに含まれているディスプレイは共通カソードです。

.. image:: img/23_segment_cathode_1.png
    :align: center
    :width: 600

7セグメントディスプレイが共通カソードか共通アノードかを判別するには、マルチメータを使用します。また、ディスプレイの各セグメントが正常に動作しているかどうかをテストするためにもマルチメータを使用できます。以下の手順に従います：

1. マルチメータをダイオードテストモードに設定します。ダイオードテストは、ダイオードや類似の半導体デバイス（LEDなど）の順方向導通をチェックするためのマルチメータの機能です。マルチメータはダイオードに小さな電流を流します。ダイオードが無事であれば、電流が流れます。

.. image:: img/multimeter_diode.png
    :width: 300
    :align: center

2. 7セグメントディスプレイをブレッドボードに挿入し、小数点が右下にあることを確認し、中央のギャップを跨いでいることを確認します。ディスプレイのピン1と同じ列にワイヤを挿入し、マルチメータの赤いリードで触れます。ディスプレイの任意の「-」ピンと同じ列に別のワイヤを挿入し、黒いリードで触れます。

.. image:: img/23_7_segment_test.png
    :align: center
    :width: 500

3. いずれかのLEDセグメントが点灯するかどうかを確認します。点灯する場合、ディスプレイが共通カソードであることを示します。点灯しない場合は、赤と黒のリードを入れ替えます。入れ替え後にセグメントが点灯する場合は、ディスプレイが共通アノードであることを示します。

4. セグメントが点灯する場合、この図を参照して、ハンドブックの表にセグメントのピン番号と大まかな位置を記録します。

.. image:: img/23_segment_2.png
    :align: center

.. list-table::
    :widths: 20 20 40
    :header-rows: 1

    *   - ピン
        - セグメント番号
        - 位置
    *   - 1
        - a
        - 上部セグメント
    *   - 2
        -
        - 
    *   - 3
        -
        - 
    *   - 4
        -
        - 
    *   - 5
        -
        - 
    *   - 6
        -
        - 
    *   - 7
        -
        - 
    *   - 8
        -
        -     

5. 上記の手順を繰り返し、「-」ピンに黒のリードを接続したまま、他のピンに赤のリードを接続して、ディスプレイのLEDセグメントに対応する制御ピンを確認します。


**質問**

前述のテストから、キットのディスプレイは共通カソードであることがわかります。つまり、共通ピンをGNDに接続し、他のピンに高電圧を供給するだけで対応するセグメントを点灯できます。ディスプレイに数字2を表示させるには、どのピンに高電圧を供給すればよいでしょうか？その理由を説明してください。

.. image:: img/23_segment_2.png
    :align: center



回路の構築
--------------------------------

**必要な部品**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * 7セグメントディスプレイ
     - 1 * 220Ω抵抗
     - 1 * 10KΩ抵抗
   * - |list_uno_r3| 
     - |list_7segment| 
     - |list_220ohm| 
     - |list_10kohm| 
   * - 1 * ボタン
     - 1 * ブレッドボード
     - ジャンパーワイヤ
     - 1 * USBケーブル
   * - |list_button| 
     - |list_breadboard| 
     - |list_wire| 
     - |list_usb_cable| 
   * - 1 * マルチメータ
     - 
     - 
     - 
   * - |list_meter| 
     - 
     - 
     - 





**ステップバイステップの構築手順**

配線図に従うか、以下の手順に従って回路を構築します。

.. image:: img/23_segment_5v.png
    :align: center
    :width: 500

1. 7セグメントディスプレイをブレッドボードに挿入し、小数点が右下にあることを確認します。

.. image:: img/23_segment_segment.png
    :align: center
    :width: 500

2. 220Ω抵抗の一端を7セグメントディスプレイの負端子（「-」）に挿入し、もう一端をブレッドボードの負レールに挿入します。その後、ブレッドボードの負レールをジャンパーワイヤでArduino Uno R3のGNDピンに接続します。

.. image:: img/23_segment_resistor_gnd.png
    :align: center
    :width: 500

3. LEDのa、b、cセグメントを制御するピンをArduino Uno R3のピン2、3、4に接続します。

.. image:: img/23_segment_abc.png
    :align: center
    :width: 500

4. LEDのd、e、f、gセグメントを制御するピンをArduino Uno R3のピン5、6、7、8に接続します。

.. image:: img/23_segment_defg.png
    :align: center
    :width: 500

5. 次に、ブレッドボードにボタンを挿入します。

.. image:: img/23_segment_button.png
    :align: center
    :width: 500

6. ボタンの右下ピンをワイヤでR3のピン9に接続します。

.. image:: img/23_segment_pin9.png
    :align: center
    :width: 500

7. 10Kプルダウン抵抗をボタンに接続し、ボタンが押されていないときにピン9が低レベルのままでバウンスしないようにします。

.. image:: img/23_segment_10k_resistor.png
    :align: center
    :width: 500

8. ボタンの左下ピンをArduino Uno R3の5Vに接続します。

.. image:: img/23_segment_5v.png
    :align: center
    :width: 500

.. list-table::
    :widths: 20 20
    :header-rows: 1

    *   - 7セグメントディスプレイ
        - Arduino UNO R3
    *   - a
        - 2
    *   - b
        - 3 
    *   - c
        - 4
    *   - d
        - 5
    *   - e
        - 6
    *   - f
        - 7
    *   - g
        - 8

コード作成 - 数字の表示
-------------------------------------
1. Arduino IDEを開き、「ファイル」メニューから「新規スケッチ」を選択して新しいプロジェクトを開始します。
2. スケッチを ``Lesson23_Show_Number`` として保存するには、 ``Ctrl + S`` を押すか、「保存」をクリックします。

3. 7セグメントディスプレイに接続されたピンを定義し、すべてのピンを出力として設定します。

.. code-block:: Arduino

    // 7セグメントディスプレイに接続されたピンを定義
    int pinA = 2;
    int pinB = 3;
    int pinC = 4;
    int pinD = 5;
    int pinE = 6;
    int pinF = 7;
    int pinG = 8;

    void setup() {
        // すべてのピンを出力として設定
        pinMode(pinA, OUTPUT);
        pinMode(pinB, OUTPUT);
        pinMode(pinC, OUTPUT);
        pinMode(pinD, OUTPUT);
        pinMode(pinE, OUTPUT);
        pinMode(pinF, OUTPUT);
        pinMode(pinG, OUTPUT);
    }

4. 次に、7セグメントディスプレイに数字を表示するコードを書きます。例えば、数字2を表示するには、セグメントFとCをLOW（オフ）、他のセグメントをHIGH（オン）に設定します。

.. code-block:: Arduino
  :emphasize-lines: 22-29

    // 7セグメントディスプレイに接続されたピンを定義
    int pinA = 2;
    int pinB = 3;
    int pinC = 4;
    int pinD = 5;
    int pinE = 6;
    int pinF = 7;
    int pinG = 8;

    void setup() {
        // すべてのピンを出力として設定
        pinMode(pinA, OUTPUT);
        pinMode(pinB, OUTPUT);
        pinMode(pinC, OUTPUT);
        pinMode(pinD, OUTPUT);
        pinMode(pinE, OUTPUT);
        pinMode(pinF, OUTPUT);
        pinMode(pinG, OUTPUT);
    }

    void loop() {
        // セグメントFとCをLOW（オフ）、他のセグメントをHIGH（オン）に設定
        digitalWrite(pinA, HIGH);
        digitalWrite(pinB, HIGH);
        digitalWrite(pinC, LOW);
        digitalWrite(pinD, HIGH);
        digitalWrite(pinE, HIGH);
        digitalWrite(pinF, LOW);
        digitalWrite(pinG, HIGH);
    }

5. このコードをArduino Uno R3にアップロードすると、7セグメントディスプレイに数字2が表示されます。

6. 他の数字を表示する場合、例えば1から6までをサイクリングするには、各セグメントを ``digitalWrite()`` で設定するのはコードが非常に長くなり、論理が不明瞭になります。ここでは、関数作成の方法を使用します。

7. パラメータを持つ関数 - ``displayDigit()`` を作成し、まず7セグメントディスプレイのすべてのLEDセグメントをオフにします。

.. code-block:: Arduino

    void displayDigit(int digit) {
        // すべてのセグメントをオフにする
        digitalWrite(pinA, LOW);
        digitalWrite(pinB, LOW);
        digitalWrite(pinC, LOW);
        digitalWrite(pinD, LOW);
        digitalWrite(pinE, LOW);
        digitalWrite(pinF, LOW);
        digitalWrite(pinG, LOW);
    }

8. 次に、異なるLEDセグメントを制御して数字を表示します。ここでは ``if-else`` 文を使うこともできますが、それは面倒です。そのため、複数の ``if-else`` 文よりも明確で整理された方法を提供する ``switch`` 文を使用します。

プログラミングにおいて、 ``switch`` 文は、変数の値に基づいて異なるコードセグメントを実行するための制御構造です。

スイッチ文の基本構文は通常次のようになります：

.. code-block:: Arduino

    switch (expression) {
        case value1:
            // code
            break;
        case value2:
            // code
            break;
        default:
            // code
    }

* ``expression``: 通常、整数または文字を返す式で、これに基づいてスイッチ文はどの ``case`` を実行するかを決定します。
* ``case``: 各 ``case`` キーワードには、 ``expression`` の結果と一致する値が続きます。一致が成功すると、その時点から ``break`` 文に出会うまでのコードが実行されます。
* ``break``: ``break`` 文は、スイッチブロックを終了するために使用されます。 ``break`` がない場合、プログラムは一致に関係なく次のcaseのコードを実行し続けます。これを「フォールスルー」と呼びます。
* ``default``: ``default`` 部分はオプションで、どの ``case`` とも一致しない場合に実行されます。 ``if-else`` 構造の ``else`` に似ています。

.. image:: img/23_flow_swtich.png
    :align: center
    :width: 600

9. ``displayDigit()`` 関数内で ``switch-case`` 文を使用して、7セグメントディスプレイに数字を表示します。例えば、1を表示するにはBとCのセグメントのみをHIGHにします。2を表示するには、FとCのセグメントをLOWにし、他のセグメントをHIGHにします。

.. code-block:: Arduino

    void displayDigit(int digit) {
        // すべてのセグメントをオフにする
        digitalWrite(pinA, LOW);
        digitalWrite(pinB, LOW);
        digitalWrite(pinC, LOW);
        digitalWrite(pinD, LOW);
        digitalWrite(pinE, LOW);
        digitalWrite(pinF, LOW);
        digitalWrite(pinG, LOW);

        // 必要なセグメントをオンにするためにHIGHに設定
        switch (digit) {
            case 1:
                digitalWrite(pinB, HIGH);
                digitalWrite(pinC, HIGH);
                break;
            case 2:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinB, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinE, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 3:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinB, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 4:
                digitalWrite(pinB, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinF, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 5:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinF, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 6:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinE, HIGH);
                digitalWrite(pinF, HIGH);
                digitalWrite(pinG, HIGH);
                break;
        }
    }

10. ``void loop()`` で ``displayDigit()`` を呼び出して特定の数字を表示し、1秒間隔で3と6を交互に表示します。

.. code-block:: Arduino

    void loop() {
        displayDigit(3);  // 7セグメントディスプレイに3を表示
        delay(1000);
        displayDigit(6);  // 7セグメントディスプレイに6を表示
        delay(1000);
    }

11. 以下が完全なコードです。これをArduino Uno R3にアップロードすると、7セグメントディスプレイが3と6を交互に表示するのが見えます。

.. code-block:: Arduino

    // 7セグメントディスプレイに接続されたピンを定義
    int pinA = 2;
    int pinB = 3;
    int pinC = 4;
    int pinD = 5;
    int pinE = 6;
    int pinF = 7;
    int pinG = 8;

    void setup() {
        // すべてのピンを出力として設定
        pinMode(pinA, OUTPUT);
        pinMode(pinB, OUTPUT);
        pinMode(pinC, OUTPUT);
        pinMode(pinD, OUTPUT);
        pinMode(pinE, OUTPUT);
        pinMode(pinF, OUTPUT);
        pinMode(pinG, OUTPUT);
    }

    void loop() {
        displayDigit(3);  // 7セグメントディスプレイに3を表示
        delay(1000);
        displayDigit(6);  // 7セグメントディスプレイに6を表示
        delay(1000);
    }

    void displayDigit(int digit) {
        // すべてのセグメントをオフにする
        digitalWrite(pinA, LOW);
        digitalWrite(pinB, LOW);
        digitalWrite(pinC, LOW);
        digitalWrite(pinD, LOW);
        digitalWrite(pinE, LOW);
        digitalWrite(pinF, LOW);
        digitalWrite(pinG, LOW);

        // 必要なセグメントをオンにする（共通カソードの場合、HIGHがセグメントをオンにする）
        switch (digit) {
            case 1:
                digitalWrite(pinB, HIGH);
                digitalWrite(pinC, HIGH);
                break;
            case 2:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinB, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinE, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 3:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinB, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 4:
                digitalWrite(pinB, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinF, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 5:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinF, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 6:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinE, HIGH);
                digitalWrite(pinF, HIGH);
                digitalWrite(pinG, HIGH);
                break;
        }
    }

コード作成 - サイバーサイコロ
-------------------------------------
これで、7セグメントディスプレイに1から6の数字を表示する方法が分かりました。では、どのようにしてサイバーサイコロの効果を実現できるでしょうか？

これは、ボタンを押してディスプレイに1から6までの数字を順番に表示し、ボタンを離すと安定した数字を表示するというものです。コードでこの効果を実現する方法を見てみましょう。

1. 前に保存したスケッチ ``Lesson23_Show_Number`` を開きます。

2. 「ファイル」メニューから「名前を付けて保存」を選択し、名前を ``Lesson23_Cyber_Dice`` に変更します。「保存」をクリックします。

3. ボタンピンを定義し、入力として設定します。

.. code-block:: Arduino
    :emphasize-lines: 10-11,23-24

    // 7セグメントディスプレイのセグメントに接続されたピンを定義
    int pinA = 2;
    int pinB = 3;
    int pinC = 4;
    int pinD = 5;
    int pinE = 6;
    int pinF = 7;
    int pinG = 8;

    // ボタンに接続されたピンを定義
    int buttonPin = 9;

    void setup() {
        // すべてのピンを出力として設定
        pinMode(pinA, OUTPUT);
        pinMode(pinB, OUTPUT);
        pinMode(pinC, OUTPUT);
        pinMode(pinD, OUTPUT);
        pinMode(pinE, OUTPUT);
        pinMode(pinF, OUTPUT);
        pinMode(pinG, OUTPUT);

        // ボタンピンを入力として設定
        pinMode(buttonPin, INPUT);
    }

4. ``void loop()`` 関数が実行されるときに、ボタンが押されているかどうかを確認します。ボタンが押されていない場合、 ``if`` ブロック内のコードはスキップされます。

.. code-block:: Arduino
    :emphasize-lines: 3,4

    void loop() {
        // ボタンが押されているか確認
        if (digitalRead(buttonPin) == HIGH) {
        }
    }

5. Arduinoや類似のマイクロコントローラープログラミングで、ボタン入力を処理する際の一般的な問題は、各押下が一回のアクションのみをトリガーするようにすることです。特にイベントやコマンドを生成する場合（例：乱数生成）。これに対処するために、「待ちリリース」技法を使用できます。

**待ちリリース**

この方法の核心は、ボタンが押されてアクションが実行された後、プログラムがループに入り、ボタンの状態が解除されるまで監視し続けることです。これは、ボタンのバウンスやユーザーがボタンを押し続けることによって引き起こされる追加のアクションを防ぐためです。

コード内でこれを ``while`` ループで実装できます。

.. image:: img/while_loop.png
    :width: 400
    :align: center

.. code-block:: Arduino
    :emphasize-lines: 4-6

    void loop() {
        // ボタンが押されているか確認
        if (digitalRead(buttonPin) == HIGH) {
            // ボタンが離されるのを待つ
            while (digitalRead(buttonPin) == HIGH) {
            }
        }
    }

6. 次に、 ``random()`` 関数を使用して1から6までの乱数を生成し、 ``displayDigit()`` を使用して7セグメントディスプレイにこの数字を表示します。ボタンを押し続けると、ディスプレイが異なる数字を高速で表示するのが見えます。

.. code-block:: Arduino
    :emphasize-lines: 6-12

    void loop() {
        // ボタンが押されているか確認
        if (digitalRead(buttonPin) == HIGH) {
            // ボタンが離されるのを待つ
            while (digitalRead(buttonPin) == HIGH) {
                // 1から6までの乱数を生成
                int num = random(1, 7);
                
                // 乱数を7セグメントディスプレイに表示
                displayDigit(num);
                // 表示の更新を見えるようにするため短い遅延を追加
                delay(100);
            }
        }
    }

7. 最後に、ボタンのデバウンスを行い、複数の迅速な入力を防ぐために遅延を追加します。

.. code-block:: Arduino
    :emphasize-lines: 15

    void loop() {
        // ボタンが押されているか確認
        if (digitalRead(buttonPin) == HIGH) {
            // ボタンが離されるのを待って続行
            while (digitalRead(buttonPin) == HIGH) {
                // 1から6までの乱数を生成
                int num = random(1, 7);
                
                // 乱数を7セグメントディスプレイに表示
                displayDigit(num);
                // 表示の更新を見えるようにするため短い遅延を追加
                delay(100);
            }
            // ボタンのデバウンスを行い、複数の迅速な入力を防ぐために遅延を追加
            delay(500);
        }
    }


8. 以下が完全なコードです。これをArduino Uno R3にアップロードすると、ボタンを押し続けるとディスプレイの数字が高速で変わり、ボタンを離すと一つの数字が表示されます。

.. code-block:: Arduino

    // 7セグメントディスプレイのセグメントに接続されたピンを定義
    int pinA = 2;
    int pinB = 3;
    int pinC = 4;
    int pinD = 5;
    int pinE = 6;
    int pinF = 7;
    int pinG = 8;

    // ボタンに接続されたピンを定義
    int buttonPin = 9;

    void setup() {
        // すべてのピンを出力として設定
        pinMode(pinA, OUTPUT);
        pinMode(pinB, OUTPUT);
        pinMode(pinC, OUTPUT);
        pinMode(pinD, OUTPUT);
        pinMode(pinE, OUTPUT);
        pinMode(pinF, OUTPUT);
        pinMode(pinG, OUTPUT);

        // ボタンピンを入力として設定
        pinMode(buttonPin, INPUT);
    }

    void loop() {
        // ボタンが押されているか確認
        if (digitalRead(buttonPin) == HIGH) {
            // ボタンが離されるのを待って続行
            while (digitalRead(buttonPin) == HIGH) {
                // 1から6までの乱数を生成
                int num = random(1, 7);

                // 乱数を7セグメントディスプレイに表示
                displayDigit(num);
                // 表示の更新を見えるようにするため短い遅延を追加
                delay(100);
            }
            // ボタンのデバウンスを行い、複数の迅速な入力を防ぐために遅延を追加
            delay(500);
        }
    }


    void displayDigit(int digit) {
        // すべてのセグメントをオフにする
        digitalWrite(pinA, LOW);
        digitalWrite(pinB, LOW);
        digitalWrite(pinC, LOW);
        digitalWrite(pinD, LOW);
        digitalWrite(pinE, LOW);
        digitalWrite(pinF, LOW);
        digitalWrite(pinG, LOW);

        // 必要な番号のセグメントをオンにする (LOWがセグメントをオンにする)
        switch (digit) {
            case 1:
            digitalWrite(pinB, HIGH);
            digitalWrite(pinC, HIGH);
            break;
            case 2:
            digitalWrite(pinA, HIGH);
            digitalWrite(pinB, HIGH);
            digitalWrite(pinD, HIGH);
            digitalWrite(pinE, HIGH);
            digitalWrite(pinG, HIGH);
            break;
            case 3:
            digitalWrite(pinA, HIGH);
            digitalWrite(pinB, HIGH);
            digitalWrite(pinC, HIGH);
            digitalWrite(pinD, HIGH);
            digitalWrite(pinG, HIGH);
            break;
            case 4:
            digitalWrite(pinB, HIGH);
            digitalWrite(pinC, HIGH);
            digitalWrite(pinF, HIGH);
            digitalWrite(pinG, HIGH);
            break;
            case 5:
            digitalWrite(pinA, HIGH);
            digitalWrite(pinC, HIGH);
            digitalWrite(pinD, HIGH);
            digitalWrite(pinF, HIGH);
            digitalWrite(pinG, HIGH);
            break;
            case 6:
            digitalWrite(pinA, HIGH);
            digitalWrite(pinC, HIGH);
            digitalWrite(pinD, HIGH);
            digitalWrite(pinE, HIGH);
            digitalWrite(pinF, HIGH);
            digitalWrite(pinG, HIGH);
            break;
        }
    }

9. 最後に、コードを保存して作業スペースを整理するのを忘れないでください。

**まとめ**

このレッスンでは、サイバーサイコロプロジェクトを無事に完成させました。これで、友達と一緒にサイコロを転がして最高の数字を競い合うことができます。このレッスンを通じて、7セグメントディスプレイの動作について学び、効果的に駆動する方法を理解しました。switch-caseステートメントを使用してコードを簡素化し、可読性と効率を向上させました。

さらに、ボタン押下の状態に基づいてランダムな数字を7セグメントディスプレイに表示するロジックを実装し、プロジェクトに動的なインタラクションを追加しました。この実践的な経験は、基本的な電子部品とコーディング戦略に慣れ親しむだけでなく、これらのスキルを使用して魅力的でインタラクティブなプロジェクトを作成する実用的な応用例を示しています。
