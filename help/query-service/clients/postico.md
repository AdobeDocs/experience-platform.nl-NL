---
keywords: Experience Platform;home;populaire onderwerpen;Query-service;query-service;postico;Postico;connect to query service;
solution: Experience Platform
title: Connect Postico aan de Dienst van de Vraag
description: Dit document bevat de koppeling voor de installatie van de back-upclient Postico for Adobe Experience Platform Query Service.
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# Verbinden [!DNL Postico] met de Dienst van de Vraag (Mac)

In dit document worden de stappen beschreven voor het maken van een verbinding tussen [!DNL Postico] en Adobe Experience Platform [!DNL Query Service] .

>[!NOTE]
>
> In deze handleiding wordt ervan uitgegaan dat u al toegang hebt tot [!DNL Postico] en dat u bekend bent met de manier waarop u door de interface kunt navigeren. Meer informatie over [!DNL Postico] kan in de [&#x200B; officiële  [!DNL Postico]  documentatie &#x200B;](https://eggerapps.at/postico/docs) worden gevonden.
> 
> Bovendien, [!DNL Postico] is **slechts** beschikbaar op de apparaten van macOS.

Als u [!DNL Postico] wilt verbinden met Query Service, opent u [!DNL Postico] en selecteert u **[!DNL New Favorite]** . Het dialoogvenster voor verbindingsinstellingen wordt weergegeven. Vanaf hier kunt u parameterwaarden invoeren om verbinding te maken met Adobe Experience Platform. Voer de hieronder vermelde verbindingsinstellingen in. De instructies op hoe te [&#x200B; met een server te verbinden PostgreSQL met Postico &#x200B;](https://eggerapps.at/postico/docs/v1.5.21/favorite-window.html) zijn ook beschikbaar bij de officiële website van Postico.

| Verbindingsparameter | Beschrijving |
|---|---|
| **[!DNL Host]:** | De hostnaam van de PostSQL-server. |
| **[!DNL Port]:** | De poort voor [!DNL Query Service] . U moet haven **80** of **gebruiken 5432** om met [!DNL Query Service] te verbinden. |
| **[!DNL User]** | Maak een naam voor uw specifieke verbinding. Laat het veld leeg om uw Mac-aanmeldnaam te gebruiken. |
| **[!DNL Password]** | Deze alfanumerieke tekenreeks is uw Experience Platform **[!UICONTROL Password]** referentie. Als u niet-verlopen geloofsbrieven wilt gebruiken, is deze waarde de samengevoegde argumenten van `technicalAccountID` en `credential` gedownload in het configuratieJSON dossier. De wachtwoordwaarde heeft de vorm: {technicalAccountId}:{credential}. Het configuratie-JSON-bestand voor niet-vervallende gegevens is een eenmalige download tijdens de initialisatie waarbij Adobe geen kopie van het bestand bewaart. |
| **[!DNL Database]** | Gebruik uw Experience Platform **[!UICONTROL Database]** -referentie: `prod:all` . |

Voor meer informatie bij het vinden van uw gegevensbestandnaam, gastheer, haven, en login geloofsbrieven, te lezen gelieve de [&#x200B; gids van geloofsbrieven &#x200B;](../ui/credentials.md). Als u uw referenties wilt zoeken, meldt u zich aan bij [!DNL Experience Platform] en selecteert u **[!UICONTROL Queries]** , gevolgd door **[!UICONTROL Credentials]** .

Nadat u uw referenties hebt ingevoegd, selecteert u **[!DNL Connect]** om verbinding te maken met Query Service.

Na het verbinden met Experience Platform, zult u een lijst van alle die betrekkingen kunnen zien eerder met de Dienst van de Vraag worden gemaakt.

## SQL-instructies maken

Als u een nieuwe SQL-query wilt maken, selecteert u **[!DNL SQL Query]** in de zijbalk. U kunt ook de sneltoets ( ⇧ ⌘ T) gebruiken om naar de queryweergave te navigeren en de query in te voeren die u wilt uitvoeren. Selecteer **[!DNL Execute Statement]** als u klaar bent om de query uit te voeren. Er wordt een tabel weergegeven met de resultaten van de voltooide query.

Zie de officiële documentatie van Postico voor meer informatie over [&#x200B; gebruikend de vraagmening &#x200B;](https://eggerapps.at/postico/docs/v1.3.1/sql-query-view.html).

## Volgende stappen

Nu u verbinding hebt met [!DNL Query Service], kunt u [!DNL Postico] gebruiken om query&#39;s te schrijven. Voor meer informatie over hoe te om vragen te schrijven en in werking te stellen, te lezen gelieve de [&#x200B; lopende vraaggids &#x200B;](../best-practices/writing-queries.md).
