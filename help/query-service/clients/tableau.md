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

# Verbinden [!DNL Tableau] met de Dienst van de Vraag

Dit document bevat informatie over het tot stand brengen van een verbinding tussen [!DNL Tableau] en Adobe Experience Platform [!DNL Query Service] .

>[!NOTE]
>
> In deze handleiding wordt ervan uitgegaan dat u al toegang hebt tot [!DNL Tableau] en dat u bekend bent met de manier waarop u door de interface kunt navigeren. Meer informatie over [!DNL Tableau] kan in de [ officiële  [!DNL Tableau]  documentatie ](https://help.tableau.com/current/pro/desktop/en-us/default.htm) worden gevonden.

Instructies op hoe te [ met een server te verbinden PostgreSQL met Tableau ](https://help.tableau.com/current/pro/desktop/en-us/examples_postgresql.htm) zijn beschikbaar bij de officiële website van Tableau. Zodra het dialoogvenster voor verbindingsinstellingen wordt weergegeven, voert u uw Platformreferenties in in de parametervelden voor verbinding met Adobe Experience Platform. Hieronder wordt een lijst met de vereiste verbindingsparameters weergegeven.

| Verbindingsparameter | Beschrijving |
|---|---|
| **[!DNL Server]** | Het adres van uw opslagplaats SFTP. Gebruik de waarde van uw Experience Platform **[!UICONTROL Host]** referentie. |
| **[!DNL Port]:** | De poort voor [!DNL Query Service] . U moet haven **80** of **gebruiken 5432** om met [!DNL Query Service] te verbinden. |
| **[!DNL Database]** | De database(s) die u wilt openen. Gebruik de waarde van de referentie **[!UICONTROL Database]** van het Experience Platform: `prod:all` . |
| **[!DNL Authentication]:** | De gekozen methode om de identiteit van de gebruiker aan te tonen. U wordt aangeraden [!DNL Username and Password] te selecteren uit de beschikbare opties in het keuzemenu. |
| **[!DNL Username]** | Dit is uw organisatie-id voor het platform. Gebruik de waarde van uw Experience Platform **[!UICONTROL Username]** referentie. De id heeft de notatie `ORG_ID@AdobeOrg` . |
| **[!DNL Password]** | Deze alfanumerieke tekenreeks is de referentie voor het Experience Platform **[!UICONTROL Password]** . Als u niet-verlopen geloofsbrieven wilt gebruiken, is deze waarde de samengevoegde argumenten van `technicalAccountID` en `credential` gedownload in het configuratieJSON dossier. De wachtwoordwaarde heeft de vorm: {technicalAccountId}:{credential}. Het configuratieJSON dossier voor niet-vervallende geloofsbrieven is een eenmalig download tijdens hun initialisering die de Adobe geen exemplaar van houdt. |

Voor meer informatie bij het vinden van uw gebruikersbenaming, wachtwoord, en login geloofsbrieven, te lezen gelieve de [ gids van geloofsbrieven ](../ui/credentials.md). Als u uw referenties wilt zoeken, meldt u zich aan bij [!DNL Platform] en selecteert u **[!UICONTROL Queries]** , gevolgd door **[!UICONTROL Credentials]** .

>[!IMPORTANT]
>
>Als gebruiker van Tableau of van de Power BI, kunt u Customer Journey Analytics met uw hulpmiddelen van BI van de geloofsbrieven tabel van de Dienst van de Vraag verbinden. Zie de geloofsbrieven documentatie voor instructies op hoe te [ uw hulpmiddelen van BI aan Customer Journey Analytics ](../ui/credentials.md#connect-to-customer-journey-analytics) verbinden.

Controleer of u het selectievakje **[!UICONTROL Require SSL]** hebt ingeschakeld voordat u probeert verbinding te maken. Zie de [ SSL wijzedocumentatie ](./ssl-modes.md) om over SSL steun voor derdeverbindingen aan de Dienst van de Vraag van Adobe Experience Platform te leren.

>[!IMPORTANT]
>
>De genestelde gegevensstructuren in derdehulpmiddelen van BI kunnen worden afgevlakt om hun bruikbaarheid te verbeteren en de vereiste werkbelasting te verminderen om gegevens terug te winnen, te analyseren, om te zetten en te melden. Zie de documentatie op de [`FLATTEN` eigenschap ](../key-concepts/flatten-nested-data.md) voor instructies op hoe te om dit te activeren die wanneer het verbinden met een gegevensbestand plaatst.

Nadat u al uw referenties hebt ingevuld, bevestigt u uw instellingen om door te gaan. U hebt nu verbinding met Adobe Experience Platform.

## Volgende stappen

Nu u verbinding hebt met [!DNL Query Service], kunt u [!DNL Tableau] gebruiken om query&#39;s te schrijven. Voor meer informatie over hoe te om vragen te schrijven en in werking te stellen, te lezen gelieve de gids op [ lopende vragen ](../best-practices/writing-queries.md).
