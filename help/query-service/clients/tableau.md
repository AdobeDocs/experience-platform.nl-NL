---
keywords: Experience Platform;thuis;populaire onderwerpen;tableau;Tableau;queryservice;Query-service;Verbinden met queryservice;
solution: Experience Platform
title: Connect Tableau naar Query Service
description: Dit document doorloopt de stappen voor het verbinden van Tableau met de Dienst van de Vraag van Adobe Experience Platform.
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# Verbinden [!DNL Tableau] aan de Dienst van de Vraag

Dit document bevat informatie over het verbinden van [!DNL Tableau] met Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Deze handleiding gaat ervan uit dat u al toegang hebt tot [!DNL Tableau] en zijn vertrouwd met hoe te om zijn interface te navigeren. Meer informatie over [!DNL Tableau] kunt u vinden in het dialoogvenster [ambtenaar [!DNL Tableau] documentatie](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

Instructies over hoe [Verbinding maken met een PostgreSQL-server met Tableau](https://help.tableau.com/current/pro/desktop/en-us/examples_postgresql.htm) zijn beschikbaar op de officiële website van Tableau. Zodra het dialoogvenster voor verbindingsinstellingen wordt weergegeven, voert u uw Platform-gegevens in de parametervelden in om verbinding te maken met Adobe Experience Platform. Hieronder wordt een lijst met de vereiste verbindingsparameters weergegeven.

| Verbindingsparameter | Beschrijving |
|---|---|
| **[!DNL Server]** | Het adres van uw opslagplaats SFTP. De waarde van uw Experience Platform gebruiken **[!UICONTROL Host]** referentie. |
| **[!DNL Port]:** | De poort voor [!DNL Query Service]. U moet poort gebruiken **80** of **5432** om te verbinden met [!DNL Query Service]. |
| **[!DNL Database]** | De database(s) die u wilt openen. De waarde van uw Experience Platform gebruiken **[!UICONTROL Database]** referentie: `prod:all`. |
| **[!DNL Authentication]:** | De gekozen methode om de identiteit van de gebruiker aan te tonen. U wordt aangeraden [!DNL Username and Password] met de beschikbare opties in het keuzemenu. |
| **[!DNL Username]** | Dit is de organisatie-id van uw Platform. De waarde van uw Experience Platform gebruiken **[!UICONTROL Username]** referentie. De id heeft de notatie `ORG_ID@AdobeOrg`. |
| **[!DNL Password]** | Deze alfanumerieke tekenreeks is uw Experience Platform **[!UICONTROL Password]** referentie. Als u niet-vervallende geloofsbrieven wilt gebruiken, is deze waarde de samengevoegde argumenten van `technicalAccountID` en de `credential` gedownload in de configuratie JSON-bestand. De wachtwoordwaarde heeft de vorm: {technicalAccountId}:{credential}. Het configuratieJSON dossier voor niet-vervallende geloofsbrieven is een eenmalig download tijdens hun initialisering die Adobe geen exemplaar van houdt. |

Voor meer informatie over het zoeken naar uw gebruikersnaam, wachtwoord, en login geloofsbrieven, gelieve te lezen [aanmeldingsgids](../ui/credentials.md). Meld u aan om uw referenties te zoeken [!DNL Platform]selecteert u vervolgens **[!UICONTROL Queries]**, gevolgd door **[!UICONTROL Credentials]**.

Controleer of u de **[!UICONTROL Require SSL]** voordat u probeert verbinding te maken. Zie de [Documentatie over SSL-modi](./ssl-modes.md) voor meer informatie over SSL-ondersteuning voor verbindingen van derden met Adobe Experience Platform Query Service.

>[!IMPORTANT]
>
>De genestelde gegevensstructuren in derdehulpmiddelen van BI kunnen worden afgevlakt om hun bruikbaarheid te verbeteren en de vereiste werkbelasting te verminderen om gegevens terug te winnen, te analyseren, om te zetten en te melden. Zie de documentatie op de[`FLATTEN` functie](../essential-concepts/flatten-nested-data.md) voor instructies over het activeren van deze instelling wanneer u verbinding maakt met een database.

Nadat u al uw referenties hebt ingevuld, bevestigt u uw instellingen om door te gaan. U hebt nu verbinding met Adobe Experience Platform.

## Volgende stappen

Nu hebt u verbinding met [!DNL Query Service]kunt u [!DNL Tableau] om query&#39;s te schrijven. Lees voor meer informatie over het schrijven en uitvoeren van query&#39;s de handleiding op [uitvoeren, query&#39;s](../best-practices/writing-queries.md).
