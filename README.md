# Vorlesungsbegleitendes Projekt für die Vorlesung Strömungsmaschinen an der DHBW Karlsruhe

## Fünfstelliger Code zur Zuordnung der Leistung

46320

## Projektbeschreibung

Dieses Repository enthält das vorlesungsbegleitende Projekt für die Vorlesung "Strömungsmaschinen" an der DHBW Karlsruhe. Ziel des Projektes ist es, das Betriebsverhalten einer vorgegebenen Wasserpumpe mithilfe bestimmter Hilfsmittel zu analysieren und auszuwerten.
Diese Hilfsmittel sind:
1) Eine CSV Datei, welche die Werte für den Volumenstrom direkt nach der Pumpe im Abstand von je einer Minute beinhaltet
2) Das Datenblatt der Pumpe, welches neben den technischen Daten auch Kennlinien der Pumpe und deren Ausführungen enthält

## Anforderungen

Die Analyse und Auswertung soll mithilfe eines Python Skripts erfolgen.
Die Abgabe erfolgt in Form dieses GitHub Repositories, welches das Skript, die Beschreibung/Erläuterung dessen und alle notwendigen Dateien enthält.

## Aufgabenstellung

1) Die erste Aufgabe bezieht sich auf das ermitteln der insgesamt aufgenommenen Energie der elektrischen Pumpe. Dies soll über eine Abschätzung basierend auf den Volumenstromdaten der CSV Datei geschehen.

2) Die zweite Aufgabe beszieht sich auf die Bestimmung der durchschnittlichen Effizienz der Pumpe, also wie viel der elektrischen Leistung tatsächlich in hydraulische Leistung umgesetzt wird.

3) In der dritten Aufgabe soll das Delte beider Leistungen aufsummiert und somit die gesamte, ungenutzte Energie berechnet werden.

4) Die letzte Aufgabe bezieht sich auf Visualisierung. Mithilfe von Graphen sollen hilfreiche und sinnvolle Darstellungen aufgezeigt werden.

## Umsetzung der Aufgaben

1)
Zunächst muss die CSV Datei eingelesen werden. Diese enthält zwei Spalten.
Die erste Spalte beinhaltet die Zeitstempel der Messungen, die zweite Spalte die jeweiligen Messwerte für den Volumenstrom in m^3/h

Für die spätere Berechnung der hydraulischen Leistung werden die zu den Volumenströmen zugehörigen Förderhöhen benötigt. Dafür werden anhand der Kennlinien aus dem Datenblatt der Pumpe zwei Arrrays erstellt, welche Eckpunkte der Kennlinie für Förderhöhe in Abhängigkeit des Volumenstroms beinhalten. Mithilfe dieser Arrays kann im nächsten Schritt für jeden der Volumenstromwerte aus der CSV interpoliert und ein zugehöriges Array für die Förderhöhe erstellt werden.

Für die Berechnung notwendige Konstanten sind die Dichte roh = 969 kg/m^3 des Mediums, welche aus dem Datenblatt entnommen werden können, das Messintervall delta = 60s, sowie die Erdbeschleunigung g = 9,81 m/s^2. Zudem wird für die Abschätzung der elektrischen Energieaufnahme zunächst ein Wirkungsgrad der Pumpe mit 83,1% definiert, welcher ebenfalls aus dem Datenblatt entnommen wird.

Mit diesen Elementen kann nun für jeden Volumenstrom mit der Formel: 

"rho * g * Förderhöhe * Volumenstrom" 

die hydraulische Leistung in Watt [W] bestimmt werden. Über den angenommenen Wert für die Effizienz der Pumpe kann widerum die benötigte elektrische Energie in Kilowattstunden [kWh] berechnet und ausgegeben werden. Damit ist Aufgabe 1 erledigt.

2)
Für die Berechnung des tatsächlichen Pumpenwirkungsgrades für Aufgabe 2 werden erneut zwei Arrays für eine Interpolation aus der entsprechenden Kennlinie des Datenblattes erstellt.
Im Anschluss wird die Interpolation durchgeführt und zuletzt der Durchschnittswert für den Wirkungsgrad berechnet und ausgegeben. Zur Korrektur von Aufgabe 1 wird entsprechend der tatsächliche Energieaufwand berechnet und ausgegeben.

3)
Für Aufgabenteil 3 wird die gesamte hydraulische Leistung der Pumpe aufsummiert und somit die hydraulische Gesamtenergie berechnet. Diese wird im Anschluss mit der insgesamt aufgenommenen elektrischen Energie aus Aufgabenteil 2 (also dem korrigierten Wert aus Aufgabenteil 1) verrechnet und die Differenz ausgegeben.

4)
Für den letzten Aufgabenteil werden verschiedene Plots erstellt. Diese werden mithilfe der matplot library erstellt.

Der erste Plot enthält die Kurven für die elektrische Leistungsaufnahme (orange) und die hydraulische Leistungsabgabe (blau) der Pumpe. Dies soll in erster Linie zeigen, in welchem Verhältnis die beiden Größen zueinander stehen.

Der zweite Plot zeigt den Verlauf der Leistungsverlustkurve, also wie viel der elektrischen Energie nicht für den "Antrieb" des Mediums genutzt wird. Das kann für verschiedene Zwecke genutzt werden, wie beispielsweise das präventive Warten der Pumpe, wenn es Anzeichen für erhöhten Verschleiß und somit eine erhöhten Verlustleistung gibt.

Der dritte Plot zeigt die kumulierten Energiemengen für elektrische Energieaufnahme der Pumpe, hydraulische Energieabgabe der Pumpe, sowie die gesamte Verlustenergie über den Bemessungszeitraum an. Das kann genutzt werden, um Vergleichswerte für verschiedene Anlagen zu schaffen, wenn es beispielsweise um eine Neuanschaffung geht.
