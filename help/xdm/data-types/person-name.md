---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schemas;fullName;xdm:fullName;person name;name;datatype;data-type;data-type; data-type;
solution: Experience Platform
title: Gegevenstype naam persoon
description: Meer informatie over het XDM-gegevenstype Personaam.
exl-id: 5cf55fb1-b6b0-4d1c-93c3-7e2b7766599e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# [!UICONTROL Person name] gegevenstype

[!UICONTROL Person name] is een standaard XDM gegevenstype dat de volledige naam van een persoon beschrijft. Aangezien de conventies voor naamstructuren sterk verschillen tussen talen en culturen, moeten namen altijd worden gemodelleerd met dit gegevenstype.

Daarnaast biedt het gegevenstype een aantal optionele eigenschappen die kunnen worden gebruikt in situaties die alleen een fragment met de volledige naam vereisen, zoals het maken van een formele of informele begroeting.

<img src="../images/data-types/person-name.png" width="500" /><br />

| Eigenschap | Beschrijving |
| --- | --- |
| `courtesyTitle` | Een afkorting van de titel, de eerlijkheid of de aanhef van een persoon (zoals `Mr.` , `Miss.` of `Dr.` ). |
| `firstName` | Het eerste segment van de naam in de schrijfvolgorde wordt meestal geaccepteerd in de taal van de naam. |
| `fullName` | De volledige naam van de persoon, in de schrijfvolgorde die het meest wordt aanvaard in de taal van de naam. |
| `lastName` | Het laatste segment van de naam in de schrijfvolgorde dat het meest wordt geaccepteerd in de taal van de naam. |
| `middleName` | Midden-, alternatieve of aanvullende namen opgegeven tussen de voornaam en achternaam. |
| `suffix` | Een groep letters die na de naam van een persoon wordt opgegeven voor aanvullende informatie (zoals `Jr.` , `Sr.` , `M.D.` , `PhD` , `I` , `II` , `III` , enzovoort). |

{style="table-layout:auto"}

Voor meer details over het gegevenstype van de persoonnaam, verwijs naar de openbare bewaarplaats XDM:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.schema.json)
