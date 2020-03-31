---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Verbinding maken met Power BI
topic: connect
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# Verbinding maken met Power BI (PC)

Pc-gebruikers kunnen Power BI installeren vanaf [https://powerbi.microsoft.com/en-us/desktop/](https://powerbi.microsoft.com/en-us/desktop/).

## Power Bi instellen

Nadat u Power BI hebt geïnstalleerd, moet u de noodzakelijke componenten instellen om de PostgreSQL-connector te ondersteunen. Voer de volgende stappen uit:

- Zoek en installeer `npgsql`, een .NET stuurprogrammapakket voor PostgreSQL dat de officiële manier voor PowerBI is om verbinding te maken.

- Selecteer v4.0.10 (nieuwere versies resulteren momenteel in een fout).

- Onder &quot;Installatie van Npgsql GAC&quot;op het scherm van de Opstelling van de Douane, wordt de uitgezochte **Zal geïnstalleerd op lokale harde aandrijving**. Als u de GAC niet installeert, zal Power BI later mislukken.

- Start Windows opnieuw.

- De evaluatieversie van PowerBI Desktop vinden.

## Power BI aansluiten op Query Service

Na het uitvoeren van die voorbereidende stappen, kunt u Power BI aan de Dienst van de Vraag verbinden:

- Open Power BI.

- Klik op Gegevens **** ophalen in het bovenste menullint.

- Kies **PostgreSQL-database** en klik op **Connect**.

- Voer waarden in voor de server en database. **Server** is de host die onder de verbindingsgegevens wordt gevonden. Voor productie, voeg haven `:80` aan het eind van het koord van de Gastheer toe. **Het gegevensbestand** kan of &quot;allen&quot;of een naam van de datasetlijst zijn. (Probeer een van de gegevenssets die zijn afgeleid van CTAS.)

- Klik op **Geavanceerde opties** en schakel de optie **Relatiekolommen** opnemen uit. Schakel **Navigeren met volledige hiërarchie** niet in.

- *(Optioneel, maar aanbevolen wanneer &quot;all&quot; is gedeclareerd voor de database)* Voer een SQL-instructie in.

>[!NOTE] Als er geen SQL-instructie is opgegeven, geeft Power BI een voorvertoning weer van alle tabellen in de database. Voor hiërarchische gegevens moet een aangepaste SQL-instructie worden gebruikt. Als het tabelschema vlak is, werkt het met of zonder een aangepaste SQL-instructie. Samengestelde typen worden nog niet ondersteund door Power BI. Als u primitieve typen wilt ophalen uit samengestelde typen, moet u SQL-instructies schrijven om deze af te leiden.

```sql
SELECT web.webPageDetails.name AS Page_Name, 
SUM(web.webPageDetails.pageviews.value) AS Page_Views 
FROM _TABLE_ 
WHERE _ACP_YEAR=2018 AND _ACP_MONTH=11 AND _ACP_DAY=20 
GROUP BY web.webPageDetails.name 
ORDER BY SUM(web.webPageDetails.pageviews.value) DESC 
LIMIT 10
```

- Selecteer de **modus DirectQuery** of **Importeren** . In de modus **Importeren** worden de gegevens geïmporteerd in power BI. In de modus **DirectQuery** worden alle query&#39;s ter uitvoering naar de Query-service verzonden.

- Klik op **OK**. Power BI maakt nu verbinding met de Query Service en geeft een voorvertoning als er geen fouten zijn. Er is een bekend probleem met de weergave Voorvertoning van numerieke kolommen. Ga verder met de volgende stap.

- Klik **Lading** om de dataset in Power BI te brengen.
