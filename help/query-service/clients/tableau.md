---
keywords: Experience Platform;thuis;populaire onderwerpen;tableau;Tableau;queryservice;Query-service;Verbinden met queryservice;
solution: Experience Platform
title: Connect Tableau naar Query Service
description: Dit document doorloopt de stappen voor het verbinden van Tableau met de Dienst van de Vraag van Adobe Experience Platform.
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: 26f0725f0f239707bd719ed46929648f8d557155
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# Verbinden [!DNL Tableau] aan de Dienst van de Vraag

Dit document bevat informatie over het verbinden van [!DNL Tableau] met Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> In deze handleiding wordt ervan uitgegaan dat u al toegang hebt tot [!DNL Tableau] en zijn vertrouwd met hoe te om zijn interface te navigeren. Meer informatie over [!DNL Tableau] kunt u vinden in het dialoogvenster [ambtenaar [!DNL Tableau] documentatie](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

Instructies over hoe [Verbinding maken met een PostgreSQL-server met Tableau](https://help.tableau.com/current/pro/desktop/en-us/examples_postgresql.htm) zijn beschikbaar op de officiële website van Tableau. Zodra het dialoogvenster voor verbindingsinstellingen wordt weergegeven, voert u uw Platformreferenties in in de parametervelden voor verbinding met Adobe Experience Platform. Hieronder wordt een lijst met de vereiste verbindingsparameters weergegeven.

| Verbindingsparameter | Beschrijving |
|---|---|
| **[!DNL Server]** | Het adres van uw opslagplaats SFTP. De waarde van uw Experience Platform gebruiken **[!UICONTROL Host]** referentie. |
| **[!DNL Port]:** | De poort voor [!DNL Query Service]. U moet poort gebruiken **80** of **5432** om te verbinden met [!DNL Query Service]. |
| **[!DNL Database]** | De database(s) die u wilt openen. De waarde van uw Experience Platform gebruiken **[!UICONTROL Database]** referentie: `prod:all`. |
| **[!DNL Authentication]:** | De gekozen methode om de identiteit van de gebruiker aan te tonen. U wordt aanbevolen [!DNL Username and Password] met de beschikbare opties in het keuzemenu. |
| **[!DNL Username]** | Dit is uw organisatie-id voor het platform. De waarde van uw Experience Platform gebruiken **[!UICONTROL Username]** referentie. De id heeft de notatie `ORG_ID@AdobeOrg`. |
| **[!DNL Password]** | Deze alfanumerieke tekenreeks is uw Experience Platform **[!UICONTROL Password]** referentie. Als u niet-vervallende geloofsbrieven wilt gebruiken, is deze waarde de samengevoegde argumenten van `technicalAccountID` en de `credential` gedownload in de configuratie JSON-bestand. De wachtwoordwaarde heeft de vorm: {technicalAccountId}:{credential}. Het configuratieJSON dossier voor niet-vervallende geloofsbrieven is een eenmalig download tijdens hun initialisering die de Adobe geen exemplaar van houdt. |

Voor meer informatie over het zoeken naar uw gebruikersnaam, wachtwoord, en login geloofsbrieven, gelieve te lezen [handleiding voor referenties](../ui/credentials.md). Meld u aan om uw referenties te zoeken [!DNL Platform]selecteert u vervolgens **[!UICONTROL Queries]**, gevolgd door **[!UICONTROL Credentials]**.

>[!IMPORTANT]
>
>Als gebruiker van Tableau of van de Power BI, kunt u Customer Journey Analytics met uw hulpmiddelen van BI van de geloofsbrieven tabel van de Dienst van de Vraag verbinden. Zie de documentatie bij de referenties voor instructies over hoe u [Sluit uw hulpmiddelen van BI aan Customer Journey Analytics aan](../ui/credentials.md#connect-to-customer-journey-analytics).

Controleer of u de **[!UICONTROL Require SSL]** voordat u probeert verbinding te maken. Zie de [Documentatie over SSL-modi](./ssl-modes.md) voor meer informatie over SSL-ondersteuning voor verbindingen van derden met Adobe Experience Platform Query Service.

>[!IMPORTANT]
>
>De genestelde gegevensstructuren in derdehulpmiddelen van BI kunnen worden afgevlakt om hun bruikbaarheid te verbeteren en de vereiste werkbelasting te verminderen om gegevens terug te winnen, te analyseren, om te zetten en te melden. Zie de documentatie op de[`FLATTEN` functie](../key-concepts/flatten-nested-data.md) voor instructies over het activeren van deze instelling wanneer u verbinding maakt met een database.

Nadat u al uw referenties hebt ingevuld, bevestigt u uw instellingen om door te gaan. U hebt nu verbinding met Adobe Experience Platform.

## Volgende stappen

Nu hebt u verbinding met [!DNL Query Service]kunt u [!DNL Tableau] om vragen te schrijven. Lees voor meer informatie over het schrijven en uitvoeren van query&#39;s de handleiding op [uitvoeren, query&#39;s](../best-practices/writing-queries.md).
