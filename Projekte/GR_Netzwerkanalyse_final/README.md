# Wie kooperationsbereit ist die linke Mehrheit im Zürcher Gemeinderat?

Im Frühjahr 2018 ist eine linke Mehrheit ins Zürcher Stadtparlament gewählt worden. Seither ist vor allem von der unterlegenen Seite (aber nicht nur) immer wieder zu hören, dass die Zusammenarbeit über Parteien und Blöcke hinweg gelitten habe, wie sie früher üblich gewesen sei. Dies macht sich vor allem an populären linken Vorhaben fest, die die Mehrheit nach eigenem Gutdünken realisiert, wie zum Beispiel am angekündigten Parkplatzabbau in der Innenstadt. Die Linke sagt, es sei genau umgekehrt: Man arbeite mehr zusammen als früher. 

### Publizierter Artikel
Online-Version mit mehreren Grafiken - [Von wegen rot-grüner Alleingang](http://www.tagesanzeiger.ch/zuerich/region/von-wegen-rotgruener-alleingang/story/20271652)

Grafisch abgespeckte Print-Version - [Von wegen rot-grüner Alleingang](https://github.com/Supermarius/cas-ddj-hub/blob/master/Projekte/GR_Netzwerkanalyse_final/ta_20200205_0_0_17.pdf)

### Ausgangsthese

Zürichs Linke arbeitet entgegen ihrer Behauptungen weniger oft als früher mit Vertretern aus anderen Blöcken zusammen, seit sie die Mehrheit hat. Dies lässt sich anhand der eingereichten Vorstöse nachzeichnen.

### Idee

Die Idee entstand in der Klasse beim Experimentieren mit dem Netzwerkanalyse-Tool Network X: Da viele der Vorstösse im Zürcher Gemeinderat jeweils von zwei Politikern/Politikerinnen eingereicht werden – oft auch von solchen unterschiedlicher Parteien – müsste sich anhand solcher Paare ein Netzwerk für jede Legislatur zeichnen lassen. Wenn man die Metamorphose dieser Netze auf einer dynamischen Zeitachse darstellt, lässt sich anschaulich zeigen, wann und wie sich bestimmte Parteien aus diesem Netz verabschiedet haben. 

Ich habe die Idee bewusst so zurechtgelegt, dass ich dabei im Rahmen dieser Arbeit mehrere Techniken anwenden kann:
1. Einen Scraper mit Selenium bauen
2. Die gesprapten Daten auslesen und zu einem Pandas-Dataframe verarbeiten
3. Die verarbeiteten Daten einer Netzwerkanalyse mit NetworkX unterziehen

Anhand dieser Daten erhoffte ich folgende Fragen zu beantworten:
1. Veränderungen der Anzahl partei-/blockübergreifenden Vorstösse im zeitlichen Verlauf?
2. Trends bei Paarbildungen: Vertreter welcher Parteien schliessen sich öfter/seltener zusammen?
3. Analyse thematischer Schwerpunkte: Welche Departemente betreffen die partei-/blockübergreifenden Vorstösse?
4. Netzwerkanalyse: Welche Personen spielen im Netz der "Brückenbauer" eine wichtige Rolle?
5. Konfrontieren der Politiker/Politikerinnen mit den Resultaten: Wie reagieren sie darauf?

Die Ergebnisse wollte ich mit Datawrapper- und Gephi-Grafiken (für die NetworkX-Analyse) darstellen und in einem Online-Artikel erläutern. 

### Abschätzen von Aufwand / Ertrag

Ich ging davon aus, dass sich der Scraper mit überschaubarem Aufwand realisieren lassen sollte, da ich dabei auf bereits gemachte Erfahrungen mkt Selenium zurückgreifen konnte. Beim Auslesen und Strukturieren der Daten rechnete ich – ebenfalls aufgrund von Erfahrungen – bei über 7000 Files mit mehr Schwierigkeiten, wegen Sonderfällen und dergleichen. Überhaupt nicht abschätzbar war der Aufwand, der bei der NetworkX-Analys anfällt. Die grundlegende Datenstruktur schien gegeben, aber wie leicht sich meine Idee mit Gephi in eine brauchbare Grafik übersetzen liess, war offen. Bei der Visualisierung für den Artikel rechnete ich mit überschaubarem Aufwand.

### Knackpunkt

Entscheidend würde erstens sein, ob sich anhand der Daten überhaupt eine brauchbare Aussage ablesen liesse. Und zweitens, ob es mir gelingen würde, die Netzwerke wie gewünscht darzustellen.

### Briefing-Personen

Ich habe mich des Themas vor einem Jahr schon einmal angenommen. Damals vertrat SP-Gemeinderat Jean-Daniel Strub den Standpunkt, dass seine Partei konsensorientierter sei als behauptet. Vor den Wahlen habe man namentlich mit der FDP in einigen relevanten Themen, etwa im Schulbereich, gemeinsame Positionen gefunden. Seitdem die Linke eine Mehrheit im Rat hat, habe sich dieser Trend nicht etwas abgeschwächt, im Gegenteil: «Wir haben noch nie so viel überparteilich zusammengearbeitet wie seit den Wahlen».

Vertreter andere Parteien stützten diese Ansicht. Es falle  auf, dass die SP sich mitunter selbst dann um Schulterschlüsse über die Mitte hinaus bemühe, wenn sie dies rechnerisch gar nicht nötig hätte. 

Im Vorfeld der Datenarbeit habe ich verschiedene Gemeinderäte darauf angesprochen, ob die Auswertung überparteilicher Vorstösse im Gemeinderat ein brauchbares Indiz sein könnte, um die Intensität solcher Kooperationen über die eigene Partei/den eigenen Block hinaus zu messen. Sie äuserten sich positiv: Auch wenn dies nicht die gesamte Arbeit des Gemeinderats abbilde, komme in den Vorstössen sicher eine Grundtendenz zum Ausdruck.


### Arbeitsprotokoll

**1. Scraper für die Vorstösse bauen (ca. 1/2 Tag)**

Knackpunkte: 
- Genügend Pausen einbauen, um den von Selenium gesteuerten Browser nicht zu überfordern
- Nachträglich erfuhr ich, dass es inzwischen auch eine API-Schnittstelle gäbe. (Lehre: Die Datenquelle erst einmal sauber explorieren, bevor man mit seinem Plan loslegt. Wobei es mir in diesem Fall aber nichts ausmachte, weil ich sowieso mit Selenium üben wollte.)

**2. Daten auslesen und zu Dataframe strukturieren (ca. 3 Tage)**

Dies war aufwändiger als erwartet, weil immer wieder neue Fehler in den Daten auftraten; nicht nur beim Auslesen, sondern auch danach, beim Prüfen des Dataframes. Dazu musste ich immer wieder Loops bauen, die mir die fehlerhaften Files anzeigen, und diese dann gezielt ansteuern, um die Probleme zu lokalisieren und zu beheben.

Knackpunkte:
- Daten und Departemente liessen sich nicht in allen 7000 Files sauber lokalisieren, musste mühsam mit Regex nachhelfen.
- Es stellte sich heraus, dass im Datenarchiv bei manchen Gemeinderäten keine Parteibezeichnung erfasst ist, obwohl sie einer angehörten. (Zum Beispiel, weil sie später einen Job im Ratsbüro übernommen haben.) Es kostete mich viel Zeit, die fehlenden Daten einzeln zu recherchieren und eine Reparatur-Funktion zu bauen, die sie in den Dataframe einbaut.
- Aufgrund dieser nachträglichen Ergänzungen war mein Dataframe verfälscht: Es befanden sich nun plötzlich Paare drin, die gar nicht unterschiedlichen Parteien angehörten. Um diese rauszusieben, musste ich einen Korrektur-Duchlauf bauen.
- Es gab diverse Probleme dabei, einen Datetime-Timestamp als Index zu verwenden, weil die Ursprungsdaten in den Files zum Teil korrumpiert waren (Leerschläge, nur zwei Ziffern bei der Jahreszahl etc.)
- Ich musste eine weitere Funktion bauen, die die Parteien nach Blöcken (Links / Mitte / Rechts) ordnet und jene Paare rausfiltert, die dem gleichen Block angehören

**3. Daten mit NetworkX analysieren (ca. 3 Tage)**

Dies war aufgrund mangelnder Erfahrung wie erwartet ein ziemlicher Brocken, obwohl das Netz mit NetworkX relativ schnell gebaut war.

Knackpunkte:
- Beim Import der gefx-Dateien in Gephi wurden zunächst weder die Departemente noch die Parteien noch die Timestamps eingelesen. Dies klappte später wundersamerweise beim x-ten Anlauf plötzlich. Keine Ahnung, warum.
- Gephi verweigerte mir, wie gewünscht ein dynamisches Netzwerk im mehrjährigen Vergleich darzustellen. Ich musste deshalb einen Plan B entwickeln: Separate Netzwerke für jede Legislatur bauen und diese miteinander vergleichen.
- Beim Experimentieren mit den Visualisierungsmöglichkeiten von Gephi ergab sich die Frage, welche Daten für den Leser überhaupt vermittelbar sind (Network Centrality?) und was ich grafisch überhaupt darstellen kann, so dass das Netz noch lesbar bleibt. Dabei reduzierte ich meine anfänglichen Ideen zusehends und entschied mich am Ende sogar, nur ein einziges von zahlreichen Netzen zu zeigen.

**Recherche und Schreiben (ca. 2 Tage)**
Knackpunkt:
- Das Problem bestand hier vor allem darin, dass die Gephi-Grafiken sich nicht sauber integrieren liessen; ich musste Hilfe von einem Inforgrafiker organisieren. 


### Datensatz / Programmiercode
- [Kompletter dokumentierter Code: Scraper / Datenauslesen / Netzwerkanalyse](http://localhost:8888/notebooks/Documents/maz-datenjournalismus/cas-ddj-hub/Projekte/GR_Netzwerkanalyse_final/Code_Komplett.ipynb)
- [Beispiel eines fertig geputzten Dataframes als csv (blockübergreifende Vorstösse)](https://github.com/Supermarius/cas-ddj-hub/blob/master/Projekte/GR_Netzwerkanalyse_final/Dataframe_bereinigt_blockuebergreifend.csv)
- [Strukturierte Daten für Visualisierung in Datawrapper (Apple-Numbers-File)](https://github.com/Supermarius/cas-ddj-hub/blob/master/Projekte/GR_Netzwerkanalyse_final/Aufbereitet%20f%C3%BCr%20Datawrapper.numbers)
- [Netzwerkanalyse in Gephi](https://github.com/Supermarius/cas-ddj-hub/blob/master/Projekte/GR_Netzwerkanalyse_final/gemeinderat.gephi)