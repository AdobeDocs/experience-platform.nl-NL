---
keywords: Experience Platform;home;populaire onderwerpen;queryservice;Query-service;Power BI;power bi;connect to query service;
solution: Experience Platform
title: Power BI verbinden met Query Service
description: Dit document doorloopt de stappen voor het verbinden van Power BI met de Dienst van de Vraag van Adobe Experience Platform.
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 0%

---

# Verbinden [!DNL Power BI] met de Dienst van de Vraag

In dit document worden de stappen beschreven voor het verbinden van [!DNL Power BI] Desktop met Adobe Experience Platform Query Service.

## Aan de slag

Deze handleiding vereist dat u al toegang hebt tot de bureaubladtoepassing van [!DNL Power BI] en dat u bekend bent met de manier waarop u door de interface kunt navigeren. Om [!DNL Power BI] Desktop of voor meer informatie te downloaden, zie de [&#x200B; officiële  [!DNL Power BI]  documentatie &#x200B;](https://docs.microsoft.com/en-us/power-bi/).

>[!IMPORTANT]
>
> De [!DNL Power BI] Desktoptoepassing is **slechts** beschikbaar op de apparaten van Vensters.

U hebt toegang tot de werkruimte Query&#39;s in de gebruikersinterface van Experience Platform nodig om de referenties te verkrijgen waarmee u [!DNL Power BI] kunt verbinden met Experience Platform. Neem contact op met uw organisatiebeheerder als u momenteel geen toegang hebt tot de werkruimte met query&#39;s.

## Verbinden [!DNL Power BI] met de Dienst van de Vraag {#connect-power-bi}

Als u [!DNL Power BI] wilt verbinden met Query Service, opent u [!DNL Power BI] en selecteert u **[!DNL Get Data]** in het bovenste menribbon. Daarna, ga &quot;[!DNL PostgreSQL]&quot;in de onderzoeksbar in om de lijst van gegevensbronnen te beperken. Selecteer in de weergegeven resultaten **[!DNL PostgreSQL database]** , gevolgd door **[!DNL Connect]** .

Het databasedialoogvenster [!DNL PostgreSQL] wordt geopend waarin waarden voor uw server en database worden aangevraagd. De extra instructies op hoe te [&#x200B; verbinden met een gegevensbestand PostgreSQL van de Desktop van de Vraag van de Macht &#x200B;](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-to-a-postgresql-database-from-power-query-desktop) kunnen in de officiële [!DNL PowerBI] documentatie worden gevonden.

Deze vereiste waarden zijn afkomstig van je Adobe Experience Platform-gebruikersgegevens. Meld u aan bij de gebruikersinterface van Experience Platform en selecteer **[!UICONTROL Queries]** in de linkernavigatie, gevolgd door **[!UICONTROL Credentials]** om uw referenties te zoeken. Voor meer informatie bij het vinden van uw gegevensbestandnaam, gastheer, haven, en login geloofsbrieven, te lezen gelieve de [&#x200B; gids van geloofsbrieven &#x200B;](../ui/credentials.md).

>[!IMPORTANT]
>
>Als Power BI- of Tableau-gebruiker kunt u Customer Journey Analytics verbinden met uw BI-gereedschappen via het tabblad Inloggegevens van Query Service. Zie de geloofsbrieven documentatie voor instructies op hoe te [&#x200B; uw hulpmiddelen van BI met Customer Journey Analytics &#x200B;](../ui/credentials.md#connect-to-customer-journey-analytics) verbinden.

![&#x200B; de werkruimte van Vragen van Experience Platform met het lusje van Referenties en het Verlopen van benadrukte geloofsbrieven.](../images/clients/power-bi/query-service-credentials-page.png)

Voer in het veld **[!DNL Server]** van het dialoogvenster [!DNL PostgreSQL database] de waarde in voor de host die u vindt in de sectie Query Service [!UICONTROL Credentials] . Voeg voor productie poort `:80` toe aan het einde van de hosttekenreeks. Bijvoorbeeld `made-up.platform-query.adobe.io:80` .

Het veld **[!DNL Database]** kan &quot;all&quot; of een tabelnaam van een gegevensset zijn. Bijvoorbeeld `prod:all` .

>[!IMPORTANT]
>
>De genestelde gegevensstructuren in derdehulpmiddelen van BI kunnen worden afgevlakt om hun bruikbaarheid te verbeteren en de vereiste werkbelasting te verminderen om gegevens terug te winnen, te analyseren, om te zetten en te melden. Zie de documentatie op de [`FLATTEN` eigenschap &#x200B;](../key-concepts/flatten-nested-data.md) voor instructies op hoe te om dit te activeren die wanneer het verbinden met een gegevensbestand plaatst.

### De modus Gegevensconnectiviteit {#data-connectivity-mode}

Vervolgens kunt u uw **[!DNL Data Connectivity mode]** selecteren. Selecteer in het dialoogvenster [!DNL PostgreSQL database] de optie **[!DNL Import]** gevolgd door **[!DNL OK]** om een lijst met alle beschikbare tabellen weer te geven of selecteer **[!DNL DirectQuery]** om rechtstreeks een query op de gegevensbron uit te voeren zonder gegevens te importeren of rechtstreeks naar [!DNL Power BI] te kopiëren.

Om meer over de **[!DNL Import]** wijze te leren, te lezen gelieve de sectie op [&#x200B; invoerend een lijst &#x200B;](#import). Meer over **[!DNL DirectQuery]** wijze leren, te lezen gelieve de sectie over [&#x200B; het vragen van een dataset zonder gegevens &#x200B;](#direct-query) in te voeren.

Selecteer **[!DNL OK]** nadat u de databasedetails hebt bevestigd.

### Verificatie {#authentication}

Nadat u de gegevensconnectiviteitsmodus hebt bevestigd, verschijnt er een vraag om uw gebruikersnaam, wachtwoord en toepassingsinstellingen. De gebruikersnaam is in dit geval uw organisatie-id en het wachtwoord is uw verificatietoken. Beide zijn te vinden op de pagina van de geloofsbrieven van de Dienst van de Vraag.

Vul deze details in en selecteer vervolgens **[!DNL Connect]** om door te gaan naar de volgende stap.

## Een tabel importeren {#import}

Als u **[!DNL Import]** [!DNL Data Connectivity mode] selecteert, wordt de volledige gegevensset geïmporteerd, zodat u de geselecteerde tabellen en kolommen in de bureaubladtoepassing van [!DNL Power BI] ongewijzigd kunt gebruiken.

>[!IMPORTANT]
>
>Als u gegevenswijzigingen wilt zien die zich hebben voorgedaan sinds de eerste importbewerking, moet u de gegevens binnen [!DNL Power BI] vernieuwen door de volledige gegevensset opnieuw te importeren.

Om een lijst in te voeren, ga de server en gegevensbestanddetails [&#x200B; in zoals hierboven beschreven &#x200B;](#connect-power-bi) en selecteer **[!DNL Import]** [!DNL Data Connectivity mode], die door **[!DNL OK]** wordt gevolgd. Het dialoogvenster [!DNL Navigator] wordt weergegeven met een lijst van alle beschikbare tabellen. Selecteer de tabel die u wilt voorvertonen, gevolgd door **[!DNL Load]** om de gegevensset over te brengen naar Power BI. De tabel wordt nu geïmporteerd in [!DNL Power BI] .

[&#x200B; Algemene informatie bij het verbinden met gegevens in de Desktop PowerBi &#x200B;](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-quickstart-connect-to-data#connect-to-data) app kan in de officiële documentatie worden gevonden.

### Tabellen importeren met behulp van aangepaste SQL

[!DNL Power BI] en andere hulpmiddelen van derden zoals [!DNL Tableau] staan gebruikers momenteel niet toe geneste objecten, zoals XDM-objecten in Experience Platform, te importeren. Om dit te verklaren, [!DNL Power BI] staat u toe om douaneSQL te gebruiken om tot deze genestelde gebieden toegang te hebben en een samengevoegde mening van de gegevens tot stand te brengen. [!DNL Power BI] laadt vervolgens deze samengevoegde weergave van de eerder geneste gegevens als een normale tabel.

Selecteer **[!DNL Advanced options]** in het dialoogvenster [!DNL PostgreSQL database] om een aangepaste SQL-query in te voeren in de sectie **[!DNL SQL statement]** . Deze aangepaste query moet worden gebruikt om de naam-waardeparen van JSON af te vlakken in een tabelindeling. De officiële documentatie verstrekt ook informatie over hoe te [&#x200B; PowerBI verbinden gebruikend een SQL verklaring in de geavanceerde opties &#x200B;](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-using-advanced-options).

Nadat u de aangepaste query hebt ingevoerd, selecteert u **[!DNL OK]** om door te gaan met het verbinden van uw database. Zie de [&#x200B; authentificatie &#x200B;](#authentication) sectie hierboven voor begeleiding bij het verbinden van een gegevensbestand van dit deel van het werkschema.

Zodra de verificatie is voltooid, wordt een voorvertoning van de samengevoegde gegevens als een tabel weergegeven in het dashboard voor het bureaublad van [!DNL Power BI] . De server- en databasenaam worden boven in het dialoogvenster weergegeven. Selecteer **[!DNL Load]** om het importproces te voltooien.

De visualisaties kunnen nu worden bewerkt en geëxporteerd vanuit de [!DNL Power BI] Desktop-app.

## Vraag de dataset zonder gegevens in te voeren {#direct-query}

De **[!DNL DirectQuery]** [!DNL Data Connectivity mode] vraagt de gegevensbron rechtstreeks op zonder gegevens te importeren of te kopiëren naar het bureaublad van [!DNL Power BI] . Met deze verbindingsmodus kunt u alle visualisaties met de huidige gegevens vernieuwen via de gebruikersinterface. De tijd die nodig is om de visualisatie te produceren of te vernieuwen, is echter afhankelijk van de prestaties van de onderliggende gegevensbron.

Meer informatie over [&#x200B; het gebruik van  [!DNL DirectQuery] &#x200B;](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-use-directquery) evenals een uitvoerige bespreking over zijn [&#x200B; connectiviteitsopties, gebruiksgevallen, en beperkingen &#x200B;](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-directquery-about) kan in de officiële [!DNL PowerBI] documentatie worden gevonden.

Als u deze [!DNL Data Connectivity mode] wilt gebruiken, selecteert u **[!DNL DirectQuery]** vervolgens **[!DNL Advanced options]** om een aangepaste SQL-query in te voeren in de sectie **[!DNL SQL statement]** . Zorg ervoor dat **[!DNL Include relationship columns]** is geselecteerd. Nadat u de query hebt uitgevoerd, selecteert u **[!DNL OK]** om door te gaan.

Er wordt een voorbeeld van de query weergegeven. Selecteer **[!DNL Load]** om de resultaten van de query weer te geven.

## Volgende stappen

Door dit document te lezen, moet u nu weten hoe u verbinding maakt met de bureaubladtoepassing van [!DNL Power BI] en de verschillende beschikbare gegevensverbindingsmodi. Voor meer informatie over hoe te om vragen te schrijven en in werking te stellen, verwijs naar de [&#x200B; begeleiding voor vraaguitvoering &#x200B;](../best-practices/writing-queries.md).
