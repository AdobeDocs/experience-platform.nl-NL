---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schemas;fullName;xdm:fullName;person name;name;datatype;data-type;data-type; data-type;
solution: Experience Platform
title: Gegevenstype naam persoon
topic: overview
description: Dit document biedt een overzicht van het XDM-gegevenstype Personnaam.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---


# [!UICONTROL Persoon ] met naam gegevenstype

[!UICONTROL Persoon ] noemt een standaard XDM gegevenstype dat de volledige naam van een persoon beschrijft. Aangezien de conventies voor naamstructuren sterk verschillen tussen talen en culturen, moeten namen altijd worden gemodelleerd met dit gegevenstype.

Daarnaast biedt het gegevenstype een aantal optionele eigenschappen die kunnen worden gebruikt in situaties die alleen een fragment met de volledige naam vereisen, zoals het maken van een formele of informele begroeting.

<img src="../images/data-types/person-name.png" width="500" /><br />

| Eigenschap | Beschrijving |
| --- | --- |
| `courtesyTitle` | Een afkorting van de titel, de eerlijkheid of de aanhef van een persoon (zoals `Mr.`, `Miss.` of `Dr.`). |
| `firstName` | Het eerste segment van de naam in de schrijfvolgorde dat het meest wordt geaccepteerd in de taal van de naam. |
| `fullName` | De volledige naam van de persoon, in de schrijfvolgorde die het meest wordt aanvaard in de taal van de naam. |
| `lastName` | Het laatste segment van de naam in de schrijfvolgorde dat het meest wordt geaccepteerd in de taal van de naam. |
| `middleName` | Midden-, alternatieve of aanvullende namen opgegeven tussen de voornaam en achternaam. |
| `suffix` | Een groep letters die na de naam van een persoon wordt opgegeven voor aanvullende informatie (zoals `Jr.`, `Sr.`, `M.D.`, `PhD`, `I`, `II`, `III`, enzovoort). |

Voor meer details over het gegevenstype van de persoonnaam, verwijs naar de openbare bewaarplaats XDM:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/person-name.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/person-name.schema.json)