---
keywords: Experience Platform;home;popular topics;query service;Query service;Power BI;power bi;connect to query service;
solution: Experience Platform
title: Verbinding maken met Power BI
topic: connect
translation-type: tm+mt
source-git-commit: f9749dbc5f2e3ac15be50cc5317ad60586b2c07e
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---


# Verbinding maken met [!DNL Power BI] (pc)

Pc-gebruikers kunnen installeren [!DNL Power BI] via [https://powerbi.microsoft.com/en-us/desktop/](https://powerbi.microsoft.com/en-us/desktop/).

## Set up [!DNL Power BI]

Nadat u hebt [!DNL Power BI] geïnstalleerd, moet u opstelling de noodzakelijke componenten om de schakelaar te steunen PostgreSQL. Voer de volgende stappen uit:

- Zoek en installeer `npgsql`, een .NET stuurprogrammapakket voor PostgreSQL dat de officiële manier voor PowerBI is om verbinding te maken.

- Selecteer v4.0.10 (nieuwere versies resulteren momenteel in een fout).

- Onder &quot;Installatie van Npgsql GAC&quot;op het scherm van de Opstelling van de Douane, wordt de uitgezochte **[!UICONTROL Zal geïnstalleerd op lokale harde aandrijving]**. Als u de GAC niet installeert, mislukt de Power BI later.

- Start Windows opnieuw.

- Zoek de evaluatieversie van [!DNL PowerBI] Desktop.

## Verbinden [!DNL Power BI] met [!DNL Query Service]

Nadat u deze voorbereidende stappen hebt uitgevoerd, kunt u verbinding maken [!DNL Power BI] met [!DNL Query Service]:

- Open [!DNL Power BI].

- Klik op Gegevens **** ophalen in het bovenste menullint.

- Kies **[!UICONTROL PostgreSQL-database]** en klik op **[!UICONTROL Connect]**.

- Voer waarden in voor de server en database. **[!UICONTROL Server]** is de host die onder de verbindingsgegevens wordt gevonden. Voor productie, voeg haven `:80` aan het eind van het koord van de Gastheer toe. **[!UICONTROL Het gegevensbestand]** kan of &quot;allen&quot;of een naam van de datasetlijst zijn. (Probeer een van de gegevenssets die zijn afgeleid van CTAS.)

- Klik op **[!UICONTROL Geavanceerde opties]** en schakel de optie **[!UICONTROL Relatiekolommen]** opnemen uit. Schakel **[!UICONTROL Navigeren met volledige hiërarchie]** niet in.

- *(Optioneel, maar aanbevolen wanneer &quot;all&quot; is gedeclareerd voor de database)* Voer een SQL-instructie in.

>[!NOTE]
>
>Als er geen SQL-instructie wordt geleverd, [!DNL Power BI] worden alle tabellen in de database voorvertoond. Voor hiërarchische gegevens moet een aangepaste SQL-instructie worden gebruikt. Als het tabelschema vlak is, werkt het met of zonder een aangepaste SQL-instructie. Samengestelde typen worden nog niet ondersteund door [!DNL Power BI] - als u primitieve typen wilt ophalen uit samengestelde typen, moet u SQL-instructies schrijven om deze af te leiden.

```sql
SELECT web.webPageDetails.name AS Page_Name, 
SUM(web.webPageDetails.pageviews.value) AS Page_Views 
FROM _TABLE_ 
WHERE TIMESTAMP >= to_timestamp('2018-11-20')
GROUP BY web.webPageDetails.name 
ORDER BY SUM(web.webPageDetails.pageviews.value) DESC 
LIMIT 10
```

- Selecteer de **[!UICONTROL modus DirectQuery]** of **[!UICONTROL Importeren]** . In de modus **[!UICONTROL Importeren]** worden gegevens geïmporteerd in [!DNL Power BI]. In de **[!UICONTROL modus DirectQuery]** worden alle query&#39;s ter uitvoering verzonden [!DNL Query Service] .

- Klik op **[!UICONTROL OK]**. Maakt nu [!DNL Power BI] verbinding met de toepassing [!DNL Query Service] en produceert een voorvertoning als er geen fouten zijn. Er is een bekend probleem met de weergave Voorvertoning van numerieke kolommen. Ga verder met de volgende stap.

- Klik **[!UICONTROL Lading]** om de dataset in te brengen [!DNL Power BI].
