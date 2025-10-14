---
keywords: Experience Platform;home;populaire onderwerpen;tableau;Tableau;query-service;Query-service;maak verbinding met queryservice;
solution: Experience Platform
title: Connect Tableau naar Query Service
description: Dit document doorloopt de stappen voor het verbinden van Tableau met de Dienst van de Vraag van Adobe Experience Platform.
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---

# Verbinden [!DNL Tableau] met de Dienst van de Vraag

Dit document bevat informatie over het tot stand brengen van een verbinding tussen [!DNL Tableau] en Adobe Experience Platform [!DNL Query Service] .

>[!NOTE]
>
> In deze handleiding wordt ervan uitgegaan dat u al toegang hebt tot [!DNL Tableau] en dat u bekend bent met de manier waarop u door de interface kunt navigeren. Meer informatie over [!DNL Tableau] kan in de [&#x200B; officiële  [!DNL Tableau]  documentatie &#x200B;](https://help.tableau.com/current/pro/desktop/en-us/default.htm) worden gevonden.

Instructies op hoe te [&#x200B; met een server te verbinden PostgreSQL met Tableau &#x200B;](https://help.tableau.com/current/pro/desktop/en-us/examples_postgresql.htm) zijn beschikbaar bij de officiële website van Tableau. Zodra het dialoogvenster voor verbindingsinstellingen wordt weergegeven, voert u uw Experience Platform-gegevens in de parametervelden in om verbinding te maken met Adobe Experience Platform. Hieronder wordt een lijst met de vereiste verbindingsparameters weergegeven.

| Verbindingsparameter | Beschrijving |
|---|---|
| **[!DNL Server]** | Het adres van uw opslagplaats SFTP. Gebruik de waarde van uw Experience Platform **[!UICONTROL Host]** -referentie. |
| **[!DNL Port]:** | De poort voor [!DNL Query Service] . U moet haven **80** of **gebruiken 5432** om met [!DNL Query Service] te verbinden. |
| **[!DNL Database]** | De database(s) die u wilt openen. Gebruik de waarde van uw Experience Platform **[!UICONTROL Database]** -referentie: `prod:all` . |
| **[!DNL Authentication]:** | De gekozen methode om de identiteit van de gebruiker aan te tonen. U wordt aangeraden [!DNL Username and Password] te selecteren uit de beschikbare opties in het keuzemenu. |
| **[!DNL Username]** | Dit is je Experience Platform-organisatie-id. Gebruik de waarde van uw Experience Platform **[!UICONTROL Username]** -referentie. De id heeft de notatie `ORG_ID@AdobeOrg` . |
| **[!DNL Password]** | Deze alfanumerieke tekenreeks is uw Experience Platform **[!UICONTROL Password]** referentie. Als u niet-verlopen geloofsbrieven wilt gebruiken, is deze waarde de samengevoegde argumenten van `technicalAccountID` en `credential` gedownload in het configuratieJSON dossier. De wachtwoordwaarde heeft de vorm: {technicalAccountId}:{credential}. Het configuratie-JSON-bestand voor niet-vervallende gegevens is een eenmalige download tijdens de initialisatie waarbij Adobe geen kopie van het bestand bewaart. |

Voor meer informatie bij het vinden van uw gebruikersbenaming, wachtwoord, en login geloofsbrieven, te lezen gelieve de [&#x200B; gids van geloofsbrieven &#x200B;](../ui/credentials.md). Als u uw referenties wilt zoeken, meldt u zich aan bij [!DNL Experience Platform] en selecteert u **[!UICONTROL Queries]** , gevolgd door **[!UICONTROL Credentials]** .

>[!IMPORTANT]
>
>Als gebruiker van Tableau of van Power BI, kunt u Customer Journey Analytics met uw hulpmiddelen van BI van het lusje van de geloofsbrieven van de Dienst van de Vraag verbinden. Zie de geloofsbrieven documentatie voor instructies op hoe te [&#x200B; uw hulpmiddelen van BI met Customer Journey Analytics &#x200B;](../ui/credentials.md#connect-to-customer-journey-analytics) verbinden.

Controleer of u het selectievakje **[!UICONTROL Require SSL]** hebt ingeschakeld voordat u probeert verbinding te maken. Zie de [&#x200B; SSL wijzedocumentatie &#x200B;](./ssl-modes.md) om over SSL steun voor derdeverbindingen aan de Dienst van de Vraag van Adobe Experience Platform te leren.

>[!IMPORTANT]
>
>De genestelde gegevensstructuren in derdehulpmiddelen van BI kunnen worden afgevlakt om hun bruikbaarheid te verbeteren en de vereiste werkbelasting te verminderen om gegevens terug te winnen, te analyseren, om te zetten en te melden. Zie de documentatie op de [`FLATTEN` eigenschap &#x200B;](../key-concepts/flatten-nested-data.md) voor instructies op hoe te om dit te activeren die wanneer het verbinden met een gegevensbestand plaatst.

Nadat u al uw referenties hebt ingevuld, bevestigt u uw instellingen om door te gaan. U hebt nu verbinding met Adobe Experience Platform.

## Volgende stappen

Nu u verbinding hebt met [!DNL Query Service], kunt u [!DNL Tableau] gebruiken om query&#39;s te schrijven. Voor meer informatie over hoe te om vragen te schrijven en in werking te stellen, te lezen gelieve de gids op [&#x200B; lopende vragen &#x200B;](../best-practices/writing-queries.md).
