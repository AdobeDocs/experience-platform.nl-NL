---
title: Bot Filtreren in de Dienst van de Vraag met het Leren van de Machine
description: Dit document biedt een overzicht van het gebruik van Query Service en het leren van computers om zowel de activiteit te bepalen als hun acties te filteren van echt verkeer van websitebezoekers.
source-git-commit: 7b223b4917e6bdb3f4a05238cbaf66261d80660e
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 5%

---

# Bot filteren in [!DNL Query Service] met leren van machines

Beide activiteiten kunnen invloed hebben op de meetwaarden van de analyse en de gegevensintegriteit schaden. Adobe Experience Platform [!DNL Query Service] kan worden gebruikt om uw gegevenskwaliteit te handhaven door beide te filtreren.

Door het beide filteren kunt u de gegevenskwaliteit behouden door gegevensverontreiniging die het gevolg is van niet-menselijke interactie met uw website, grotendeels te verwijderen. Dit proces wordt bereikt door de combinatie van SQL-query&#39;s en het leren van machines.

Beide activiteiten kunnen op verschillende manieren worden geïdentificeerd. De in dit document gevolgde aanpak richt zich op activiteitspikes, in dit geval, het aantal acties die een gebruiker in een bepaalde periode neemt. Aanvankelijk, plaatst een SQL vraag willekeurig een drempel voor het aantal acties die over een periode worden genomen om als beide activiteit te kwalificeren. Deze drempel wordt vervolgens dynamisch verfijnd met behulp van een machinaal leermodel om de nauwkeurigheid van deze verhoudingen te verbeteren.

Dit document biedt een overzicht en gedetailleerde voorbeelden van de SQL bot filtering query&#39;s en de machine learningmodellen die nodig zijn om het proces in uw omgeving in te stellen.

## Aan de slag

Als onderdeel van dit proces moet u een model voor machinaal leren trainen, wordt in dit document uitgegaan van een praktische kennis van een of meer computerleeromgevingen.

Dit voorbeeld gebruikt [!DNL Jupyter Notebook] als ontwikkelomgeving. Hoewel er veel opties beschikbaar zijn, [!DNL Jupyter Notebook] wordt aanbevolen omdat het een opensource webtoepassing is met lage computervereisten. Het kan [gedownload van de officiële site](https://jupyter.org/).

## Gebruiken [!DNL Query Service] om een drempel voor beide activiteit te bepalen

De twee kenmerken die worden gebruikt om gegevens voor beide detectie te extraheren, zijn:

* Marketing Cloud-id (MCID): Dit biedt een universele, permanente id die uw bezoekers identificeert voor alle Adobe-oplossingen.
* Tijdstempel: Dit geeft de tijd en datum in UTC-indeling wanneer een activiteit op de website is opgetreden.

De volgende SQL-instructie biedt een eerste voorbeeld om beide activiteiten te identificeren. De instructie gaat ervan uit dat als een bezoeker binnen één minuut 50 klikken uitvoert, de gebruiker een bot is.

```sql
SELECT * 
FROM   <YOUR_TABLE_NAME> 
WHERE  enduserids._experience.mcid NOT IN (SELECT enduserids._experience.mcid 
                                           FROM   <YOUR_TABLE_NAME> 
                                           GROUP  BY Unix_timestamp(timestamp) / 
                                                     60, 
                                                     enduserids._experience.mcid 
                                           HAVING Count(*) > 50);  
```

De expressie filtert de MCID&#39;s van alle bezoekers die aan de drempel voldoen, maar behandelt geen spikes in verkeer vanaf andere intervallen.

## De beide detectie verbeteren door machines te leren

De eerste SQL-instructie kan worden verfijnd tot een extractiequery voor functies voor machinaal leren. De verbeterde query zou meer functies moeten opleveren voor verschillende intervallen voor het trainen van modellen voor machinaal leren met hoge nauwkeurigheid.

De voorbeeldverklaring wordt uitgebreid van één minuut met maximaal 60 klikken, om vijf minuten en 30 minuten periodes met kliktellingen van respectievelijk 300, en 1800 te omvatten.

De voorbeeldverklaring verzamelt het maximumaantal kliks voor elke MCID over de diverse duur. De eerste instructie is uitgebreid met een minuut (60 seconden), 5 minuten (300 seconden) en een uur (1800 seconden).

```sql
SELECT table_count_1_min.mcid AS id, 
       count_1_min, 
       count_5_mins, 
       count_30_mins 
FROM   ( ( (SELECT mcid, 
                 Max(count_1_min) AS count_1_min 
          FROM   (SELECT enduserids._experience.mcid.id AS mcid, 
                         Count(*)                       AS count_1_min 
                  FROM 
       <YOUR_TABLE_NAME> 
                  GROUP  BY Unix_timestamp(timestamp) / 60, 
                            enduserids._experience.mcid.id) 
          GROUP BY mcid) AS table_count_1_min 
           LEFT JOIN (SELECT mcid, 
                             Max(count_5_mins) AS count_5_mins 
                      FROM   (SELECT enduserids._experience.mcid.id AS mcid, 
                                     Count(*)                       AS 
                                     count_5_mins 
                              FROM 
           <YOUR_TABLE_NAME> 
                              GROUP  BY Unix_timestamp(timestamp) / 300, 
                                        enduserids._experience.mcid.id) 
                      GROUP  BY mcid) AS table_count_5_mins 
                  ON table_count_1_min.mcid = table_count_5_mins.mcid ) 
         LEFT JOIN (SELECT mcid, 
                           Max(count_30_mins) AS count_30_mins 
                    FROM   (SELECT enduserids._experience.mcid.id AS mcid, 
                                   Count(*)                       AS 
                                   count_30_mins 
                            FROM 
         <YOUR_TABLE_NAME> 
                            GROUP  BY Unix_timestamp(timestamp) / 1800, 
                                      enduserids._experience.mcid.id) 
                    GROUP  BY mcid) AS table_count_30_mins 
                ON table_count_1_min.mcid = table_count_30_mins.mcid ) 
```

Het resultaat van deze expressie kan er ongeveer zo uitzien als in de onderstaande tabel.

| `id` | `count_1_min` | `count_5_min` | `count_30_min` |
|---|---|---|---|
| 4833075303848917832 | 1 | 1 | 1 |
| 1469109497068938520 | 1 | 1 | 1 |
| 504568251944554093 | 1 | 1 | 1 |
| 7148203816406620066 | 3 | 3 | 3 |
| 1013065429311352386 | 1 | 1 | 1 |
| 3077475871984695013 | 7 | 7 | 7 |
| 4151486040344674930 | 2 | 2 | 2 |
| 6563366098591762751 | 6 | 6 | 6 |
| 2403566105776993627 | 4 | 4 | 4 |
| 5710530640819698543 | 1 | 1 | 1 |
| 3675089655839425960 | 1 | 1 | 1 |
| 9091930660723241307 | 1 | 1 | 1 |

## Nieuwe spookdrempels identificeren aan de hand van computerleren

Daarna, voer de resulterende vraagdataset in formaat CSV uit en voer het in [!DNL Jupyter Notebook]. Vanuit die omgeving kun je een model voor machinetraining trainen met behulp van de huidige bibliotheken voor machinaal leren. Raadpleeg de handleiding voor probleemoplossing voor meer informatie over [hoe te om gegevens van uit te voeren [!DNL Query Service] in CSV-indeling](../troubleshooting-guide.md#export-csv)

De aanvankelijk vastgestelde ad-hocdrempels voor spinnen zijn niet gebaseerd op gegevens en zijn daarom niet nauwkeurig. De modellen van het leren van de machine kunnen worden gebruikt om parameters als drempels op te leiden. Dientengevolge, kunt u de vraagefficiency verhogen door het aantal te verminderen `GROUP BY` trefwoorden door overbodige functies te verwijderen.

In dit voorbeeld wordt de Scikit-Learn-bibliotheek voor machinaal leren gebruikt, die standaard met [!DNL Jupyter Notebook]. De pythonbibliotheek &quot;pandas&quot; wordt ook geïmporteerd voor gebruik hier. De volgende opdrachten worden ingevoerd in [!DNL Jupyter Notebook].

```shell
import pandas as ps

df = pd_read.csv('data/bot.csv')
df = df[df['count_1-min'] > 1]
df['is_bot'] = 0
df.loc[df['count_1_min'] > 50,'is_bot'] = 1
df
```

Daarna, moet u een classificator van de beslissingsboom op de dataset opleiden en de logica waarnemen die uit het model voortvloeit.

De bibliotheek Matplotlib wordt gebruikt om de indeling van de beslissingsboomstructuur in het onderstaande voorbeeld te visualiseren.

```shell
from sklearn.tree import DecisionTreeClassifier
from sklearn import tree
from matplotlib import pyplot as plt

X = df.iloc[:,:[1,3]]
y = df.iloc[:,-1]

clf = DecisionTreeClassifier(max_leaf_nodes=2, random_state=0)
clf.fit(X,y)

print("Model Accuracy: {:.5f}".format(clf.scre(X,y)))

tree.plot_tree(clf,feature_names=X.columns)
plt.show()
```

De waarden die door [!DNL Jupyter Notebook] voor dit voorbeeld zijn de volgende voorbeelden van toepassing.

```text
Model Accuracy: 0.99935
```

![Statistische output van [!DNL Jupyter Notebook] model voor machinaal leren.](../images/use-cases/jupiter-notebook-output.png)

De resultaten voor het model in het bovenstaande voorbeeld zijn meer dan 99% nauwkeurig.

Aangezien de klasser van de beslissingsboom kan worden getraind met behulp van gegevens van [!DNL Query Service] op een regelmatige ervaring die de geplande vragen gebruikt, kunt u gegevensintegriteit verzekeren door beide activiteit met een hoge graad van nauwkeurigheid te filtreren. Door de parameters te gebruiken die uit het machine het leren model worden afgeleid, kunnen de originele vragen met de hoogst nauwkeurige parameters worden bijgewerkt die door het model worden gecreeerd.

Het voorbeeldmodel bepaalde met een hoge mate van nauwkeurigheid dat om het even welke bezoekers met meer dan 130 interactie in vijf minuten bots zijn. Deze informatie kan nu worden gebruikt om uw bot te verfijnen die SQL vragen filtreren.

## Volgende stappen

Door dit document te lezen hebt u een beter inzicht in hoe u Query Service en het leren van machines kunt gebruiken om beide activiteiten te bepalen en te filteren.

Andere documenten die de voordelen van [!DNL Query Service] aan de strategische bedrijfsinzichten van uw organisatie zijn de verlaten browse use casevoorbeeld.
