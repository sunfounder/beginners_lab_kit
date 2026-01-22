.. note::

    Hallo und herzlich willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Community auf Facebook! Tauche gemeinsam mit anderen Enthusiasten tiefer in die Welt von Raspberry Pi, Arduino und ESP32 ein.

    **Warum beitreten?**

    - **Expertenunterstützung**: Löse nach dem Kauf auftretende Probleme und technische Herausforderungen mit Hilfe unserer Community und unseres Teams.
    - **Lernen & Teilen**: Tausche Tipps und Anleitungen aus, um deine Fähigkeiten zu erweitern.
    - **Exklusive Vorschauen**: Erhalte frühzeitigen Zugang zu neuen Produktankündigungen und exklusiven Einblicken.
    - **Spezielle Rabatte**: Profitiere von exklusiven Rabatten auf unsere neuesten Produkte.
    - **Festliche Aktionen und Verlosungen**: Nimm an Verlosungen und Feiertagsaktionen teil.

    👉 Bereit, gemeinsam mit uns zu entdecken und zu erschaffen? Klicke auf [|link_sf_facebook|] und tritt noch heute bei!


4. Ohmsches Gesetz: Eine Reise durch die Grundlagen elektrischer Schaltkreise
===================================================================================

Jedes elektronische Gerät basiert auf Prinzipien, die durch Schaltkreise und Leiterplatten geregelt werden. Um sicherzustellen, dass diese Geräte einwandfrei funktionieren, müssen Elektroingenieure den Stromfluss tiefgehend verstehen und kontrollieren. Ein zentrales Konzept in diesem Bereich ist das Ohmsche Gesetz, das eine grundlegende Beziehung zwischen Spannung, Strom und Widerstand in elektrischen Schaltkreisen beschreibt. In dieser Lektion tauchen wir in das Ohmsche Gesetz ein und erkunden seine Implikationen und Anwendungen.

Diese Lektion beleuchtet die grundlegenden Prinzipien, die jedem modernen elektronischen Gerät zugrunde liegen. Das Verständnis dieser Prinzipien, insbesondere des Ohmschen Gesetzes, ist für Elektroingenieure unerlässlich, um das Verhalten von Schaltkreisen effektiv zu kontrollieren und vorherzusagen.



Der Funke der Elektrizität
-------------------------------

Die Geschichte der Elektrizität beginnt mit frühen Experimenten und bahnbrechenden Erkenntnissen. Benjamin Franklin entfachte mit seinem Drachenexperiment zwar nicht die Elektrizität, weckte aber das Interesse und inspirierte weitere Forschungen zu elektrischen Ladungen und deren Kräften.

.. image:: img/2_electronic.webp
    :width: 600
    :align: center

Seine Experimente legten den Grundstein für das Verständnis, dass Elektrizität mit der Bewegung positiver und negativer Ladungen zusammenhängt, vergleichbar mit dem natürlichen Phänomen des Blitzes. Inspiriert von Franklin zeigte der französische Wissenschaftler Thomas-François Dalibard praktische Beispiele dafür, wie elektrische Ströme auf natürliche Weise entstehen können.

Diese Ära erlebte auch die Rivalität und die kollektiven Errungenschaften von Nikola Tesla und Thomas Edison, deren Bemühungen unsere moderne elektrische Infrastruktur geprägt haben. Teslas Entwicklung des Wechselstroms (AC) und Edisons Einführung der Glühbirne sind Beispiele für den rasanten Fortschritt in der Elektroingenieurwissenschaft.

.. image:: img/2_lamp.webp
    :width: 400
    :align: center

Die Erfindung des Transistors im Jahr 1947, eines grundlegenden Bauteils für alle modernen Elektronikgeräte, führte zu weiteren Fortschritten. Dieses kleine, aber leistungsstarke Bauteil ermöglichte die Entwicklung von Mikrochips und elektronischen Schaltern, die in der heutigen technikgetriebenen Welt von entscheidender Bedeutung sind.

.. image:: img/2_transistor.jpg
    :width: 300
    :align: center
    

Georg Ohm und sein Gesetz
------------------------------

Mitten in diesen technologischen Fortschritten führte der deutsche Physiker Georg Ohm Experimente durch, die die Grundprinzipien elektrischer Schaltkreise definierten. Zu einer Zeit, als Elektrizität noch ein neues wissenschaftliches Feld war, untersuchte Ohm, wie sich elektrische Ströme unter verschiedenen Bedingungen verhalten, indem er einfache, aber effektive Aufbauten mit Drähten, Batterien und selbstgemachten Widerständen verwendete.

Ohms sorgfältige Experimente enthüllten eine konstante proportionale Beziehung zwischen Spannung, Strom und Widerstand, die in der Formel V=IR festgehalten ist – heute bekannt als das Ohmsche Gesetz. Diese Entdeckung lieferte nicht nur eine mathematische Beschreibung von Elektrizität, sondern ermöglichte auch das planbare Design und den Betrieb elektrischer Geräte.

.. code-block::

    Voltage = Current x Resistance
    Or
    V = I • R

Ohms Durchhaltevermögen trotz anfänglicher Skepsis unterstreicht die Bedeutung seiner Erkenntnisse, die den Grundstein für zukünftige technologische Fortschritte legten und eine neue Ära der Elektroingenieurwissenschaft einläuteten.



Verständnis von Strom, Spannung und Widerstand
----------------------------------------------------

Um das Ohmsche Gesetz vollständig zu verstehen und anwenden zu können, ist es wichtig, die grundlegenden Konzepte von Strom, Spannung und Widerstand zu begreifen. Diese Komponenten sind unverzichtbare Elemente eines jeden Schaltkreises und können mit den Elementen eines fließenden Flusses verglichen werden.

- **Strom (I)**: Der Fluss von Elektronen durch einen Leiter, gemessen in Ampere (A).
- **Spannung (V)**: Die elektrische Kraft oder der Druck, der Elektronen durch einen Leiter treibt.
- **Widerstand (R)**: Der Widerstand gegen den Elektronenfluss, gemessen in Ohm (Ω), und wird oft durch den griechischen Buchstaben Omega dargestellt.

.. image:: img/2_resistance.png
    :width: 400
    :align: center

Die Analogie eines Gartenschlauchs hilft, diese Konzepte zu verdeutlichen:

- **Strom** ist vergleichbar mit dem Wasserfluss und gibt die Geschwindigkeit an, mit der sich Elektronen durch einen Leiter bewegen.
- **Spannung** ist wie der Wasserhahn, der die Kraft reguliert, die das Wasser antreibt.
- **Widerstand** ist vergleichbar mit Knicken oder Biegungen im Schlauch, die den Weg des Wassers behindern und den Fluss verlangsamen.

Diese Erklärung verbindet das theoretische Wissen des Ohmschen Gesetzes mit dem Verhalten realer Schaltkreise und legt die Grundlage für weiteres Lernen und die praktische Anwendung.

Erkundung des Ohmschen Gesetzes durch praktische Experimente
-----------------------------------------------------------------

Nun wenden wir das Ohmsche Gesetz in einem praktischen Experiment an, indem wir mit einem einfachen LED-Schaltkreis die Auswirkungen von verändertem Widerstand und Spannung beobachten.

**Versuchsaufbau**

1. Du beginnst mit einem einfachen Schaltkreis, der eine LED und einen 220-Ohm-Widerstand enthält.
   
   .. image:: img/2_uno_gnd.png
     :width: 600
     :align: center

2. Ersetze den 220-Ohm-Widerstand durch andere Widerstände mit verschiedenen Werten, die unten aufgeführt sind. Notiere die Helligkeitsveränderungen der LED bei jedem Austausch, um zu beobachten, wie der Widerstand den Strom und damit die Lichtausgabe beeinflusst.

   .. list-table::
      :widths: 25 100
      :header-rows: 1

      * - Widerstand
        - Beobachtungen
      * - 100Ω
        - 
      * - 1KΩ
        - 
      * - 10KΩ
        - 
      * - 1MΩ
        - 

  
  Du wirst feststellen, dass die LED nur beim 100Ω-Widerstand heller leuchtet als mit dem vorherigen 220Ω-Widerstand. Mit höheren Widerständen nimmt die Helligkeit der LED ab, bis sie bei 1MΩ vollständig erlischt. Warum ist das so?


  Laut dem Ohmschen Gesetz (I = V/R) verringert sich der Strom durch die LED, wenn der Widerstand bei konstanter Spannung steigt, wodurch die LED dunkler wird. Bei 1MΩ ist der Strom zu gering, um die LED zum Leuchten zu bringen.

3. Nachdem du die Auswirkungen des veränderten Widerstands beobachtet hast, belasse den Widerstand bei 220 Ohm und ändere die Spannungsversorgung des Stromkreises von 5V auf 3,3V. Notiere die Veränderungen in der Helligkeit der LED.

  Du wirst feststellen, dass die LED bei 3,3V etwas dunkler ist als bei 5V. Warum ist das so?

  Nach dem Ohmschen Gesetz sollte der Strom mit dem bekannten Widerstand und der neuen Spannung I = V/R sein. Mit einer Verringerung der Spannung bei gleichbleibendem Widerstand sinkt der Strom, was die LED dunkler erscheinen lässt.

**Zusammenfassung**

Durch diese Experimente hast du direkt beobachtet, wie das Ohmsche Gesetz das Verständnis und die Gestaltung von elektrischen Schaltkreisen grundlegend beeinflusst. Diese praktische Anwendung hilft, die zuvor besprochenen theoretischen Konzepte zu festigen und zeigt die realen Auswirkungen von Spannung, Strom und Widerstand in der Elektroingenieurwissenschaft.

