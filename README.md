# Wirkung von Hitze- (und Trockenperioden) auf Ackerflächen 

  
## Motivation und Relevanz
Hitze- und Trockenperioden können Nutzpflanzen erheblich schädigen, besonders während empfindlicher Phasen wie der Blüte oder des vegetativen Wachstums. Dieser Schaden wirkt sich häufig negativ auf den späteren Ernteertrag aus. Besonders schädlich sind dabei Perioden, in denen Hitze und Trockenheit gemeinsam auftreten, da sich ihre Wirkung gegenseitig verstärkt. Wir konzentrieren uns deshalb auf heiß-trockene Perioden während der Wachstumszeit einer ausgewählten Kultur, statt Hitze und Trockenheit isoliert zu betrachten.
Die Gesundheit und Vitalität von Pflanzen lässt sich über Satellitenbilder mit dem Normalized Difference Vegetation Index (NDVI) quantitativ erfassen – dem am häufigsten genutzten Vegetationsindex der Fernerkundung. Er macht sich zunutze, dass gesunde Pflanzen rotes Licht stark aufnehmen (für die Photosynthese), nahes Infrarotlicht dagegen stark zurückwerfen; aus dem Verhältnis beider Werte ergibt sich der NDVI. 
<img width="860" height="584" alt="image" src="https://github.com/user-attachments/assets/cd2e8479-3be9-4bcc-8f3a-54fc0938a065" />

Grobe Richtwerte zur Einordnung:
- −1 bis 0: Wasser, Schnee oder Wolken
- 0 bis 0,2: kahle Flächen, Fels, Sand oder stark gestresste Vegetation
- 0,2 bis 0,5: spärliche Vegetation, Gräser oder Vegetation unter Dürrestress
- 0,6 bis 1,0: dichte, gesunde und aktive Vegetation (z. B. Wälder oder ertragreiche Felder)
- Klassische amtliche Ertragsstatistiken sind für eine datengetriebene Untersuchung dieses Zusammenhangs wenig geeignet, da sie nur jährlich und auf grober räumlicher Ebene (Kreis) vorliegen und von vielen weiteren Faktoren (Sorte, Düngung, Bodenqualität) überlagert werden. Der NDVI reagiert dagegen innerhalb weniger Wochen auf Hitze- und Trockenstress und erlaubt damit einen direkteren, dichter aufgelösten Blick auf den Zusammenhang.
<img width="560" height="373" alt="image" src="https://github.com/user-attachments/assets/b6ae47a3-2245-4745-87c3-6579f4ccc73e" />


## Fragestellung (Business Problem)
Wie stark und mit welcher zeitlichen Verzögerung reagiert der Vegetationszustand (NDVI) von Ackerflächen auf heiß-trockene Perioden während der Wachstumszeit? Da zwischen einer solchen Stressperiode und ihrer sichtbaren Wirkung auf den NDVI erfahrungsgemäß mehrere Wochen liegen, soll der NDVI-Wert nach Ablauf dieses Zeitfensters vorhergesagt und mit dem für diese Jahreszeit üblichen, saisonbereinigten NDVI-Wert verglichen werden.
Diese Vorhersage hat einen konkreten praktischen Nutzen: Deutet der vorhergesagte NDVI-Wert auf eine beeinträchtigte Pflanzengesundheit hin, können Landwirte frühzeitig abschätzen, ob sich eine künstliche Bewässerung finanziell lohnt, um den drohenden Ernteverlust zu begrenzen.

## Daten und Werkzeuge
- Vegetationsindex (NDVI): MODIS MOD13Q1 (250 m Auflösung, 16-Tage-Komposite, seit 2000), abgerufen über NASA AppEEARS. Die 16-Tage-Komposite sind bereits wolkenbereinigt.
- Wetterdaten: Open-Meteo Historical-Weather-API – liefert ERA5-Reanalysedaten
- Pflanzenarten auf den Feldern: EuroCrop 2.0 Daten
- Python-Werkzeuge: pandas zum Einlesen der AppEEARS-CSV und der Open-Meteo-JSON-Antworten, requests für den Open-Meteo-Abruf, scikit-learn für die Modellierung, matplotlib/seaborn für Visualisierungen.

## Methodik & Vorgehen
Eine Kultur festlegen und Wachstumsphase festlegen ( z.B. Weizen von April bis Juli).
Testflächen mit dieser Kultur über min. 5 Jahre festlegen
NDVI-Zeitreihen für diese Testflächen runterladen
Open-Meteo-Abruf für dieselben Koordinaten aufsetzen; 
Hitze- und Trockenheitskennzahlen einfach definieren
Prüfen, mit welchem zeitlichen Abstand die NDVI-Werte eine Reaktion auf eine hitzetrockene Periode  zeigen. Aus fachlicher Literatur beträgt diese Differenz etwa 4 bis 16 Wochen. Da dies ein sehr großer Zeitraum ist, möchten wir am Anfang selber Trockenperioden und NDVI-Werte modellieren, um unsere eigene zeitliche Differenz festzulegen. 
Mit Hilfe der Daten Normalwerte für NDVI für den Zeitraum modellieren
Datensatz zusammenstellen
Modelle vergleichen ( LR, RF..)
NDVI-Effekt anhand von Literaturwerten grob in einen Ertrags-/Geldwert übersetzen; 

## Erwartetes Ergebnis
Ein trainiertes Regressionsmodell, das den NDVI-Abfall aus Hitze- und Trockenheitsmerkmalen sowie Beregnungsstatus vorhersagt, sowie eine daraus abgeleitete, einfache Handlungsempfehlung: ab welcher Stress-Intensität sich eine Beregnung in der untersuchten Region tendenziell lohnt.

## Daten
### Daten für Crop Type:
https://jeodpp.jrc.ec.europa.eu/ftp/jrc-opendata/DRLL/EuroCropsV2/gpqtv201/ 
https://github.com/Martincccc/EuroCropsV2/blob/main/data/cropcodemapping/eurocrops.csv 

### Daten für NDVI: 
https://appeears.earthdatacloud.nasa.gov/ 

### Daten für Wetter: 
https://openweathermap.org/ 

## Literature
- https://www.sciencedirect.com/science/article/pii/S2214662826000472 
- https://www.frontiersin.org/journals/plant-science/articles/10.3389/fpls.2017.01147/full 
- https://pmc.ncbi.nlm.nih.gov/articles/PMC5489704/
