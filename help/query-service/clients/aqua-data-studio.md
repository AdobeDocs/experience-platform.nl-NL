---
keywords: Experience Platform;home;populaire onderwerpen;queryservice;Query-service;Aqua Data Studio;Aqua-gegevensstudio;Verbind met queryservice;
solution: Experience Platform
title: Connect Aqua Data Studio aan de Dienst van de Vraag
description: Dit document doorloopt de stappen voor het verbinden van de Studio van Gegevens Aqua met de Dienst van de Vraag van Adobe Experience Platform.
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# Verbinden [!DNL Aqua Data Studio] met de Dienst van de Vraag

In dit document worden de stappen beschreven voor het maken van een verbinding tussen [!DNL Aqua Data Studio] en Adobe Experience Platform [!DNL Query Service] .

## Aan de slag

Voor deze handleiding moet u al toegang hebben tot [!DNL Aqua Data Studio] en vertrouwd zijn met de navigatie in de interface. Meer informatie over [!DNL Aqua Data Studio] kan in de [&#x200B; officiële  [!DNL Aqua Data Studio]  documentatie &#x200B;](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1) worden gevonden.

>[!NOTE]
>
>Er zijn [!DNL Windows] en [!DNL macOS] versies van [!DNL Aqua Data Studio] . In deze handleiding zijn schermafbeeldingen gemaakt met de bureaubladtoepassing van [!DNL macOS] . Er kunnen kleine discrepanties in UI tussen de versies zijn.

U hebt toegang tot de [!UICONTROL Queries] -werkruimte in de gebruikersinterface van Experience Platform nodig om de vereiste gegevens voor het verbinden van [!DNL Aqua Data Studio] met Experience Platform te verkrijgen. Neem contact op met uw organisatiebeheerder als u momenteel geen toegang hebt tot de werkruimte van [!UICONTROL Queries] .

## De server registreren {#register-server}

Nadat u [!DNL Aqua Data Studio] hebt geïnstalleerd, moet u de server eerst registreren. Zie de officiële documentatie van de Studio van Gegevens Aqua voor instructies op hoe te [&#x200B; de  [!DNL Register Server]  dialoog &#x200B;](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#launching_the_register_server_dialog) lanceren en [&#x200B; de server &#x200B;](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#steps_to_register_a_server_in_aqua_data_studio) registreren.

Wanneer het dialoogvenster **[!DNL Register Server]** voor een PostgresSQL-server wordt weergegeven, geeft u de volgende gegevens op voor de serverinstellingen.

- **[!DNL Name]**: De naam van de verbinding. U wordt aangeraden een vriendelijke naam op te geven om de verbinding te herkennen.
- **[!DNL Login Name]**: De aanmeldingsnaam is uw Experience Platform-organisatie-id. De notatie heeft de vorm van `ORG_ID@AdobeOrg` .
- **[!DNL Password]**: dit is een alfanumerieke tekenreeks die u vindt op het dashboard met referenties [!DNL Query Service] .
- **[!DNL Host and Port]**: Het eindpunt van de host en de bijbehorende poort voor [!DNL Query Service] . U moet poort 80 gebruiken om verbinding te maken met [!DNL Query Service] .
- **[!DNL Database]:** De database die wordt gebruikt. Gebruik de waarde voor de Experience Platform UI-referentie `dbname` : `prod:all` .

### [!DNL Query Service] referenties

Meld u aan bij de gebruikersinterface van [!DNL Experience Platform] en selecteer **[!UICONTROL Queries]** in de linkernavigatie, gevolgd door **[!UICONTROL Credentials]** om uw referenties te zoeken. Voor volledige richtingen om uw login geloofsbrieven, gastheer, haven, en gegevensbestandnaam te vinden, te lezen gelieve de [&#x200B; gids van geloofsbrieven &#x200B;](../ui/credentials.md).

[!DNL Query Service] biedt ook niet-vervallende referenties, zodat een eenmalige installatie met externe clients mogelijk is. Zie de documentatie voor [&#x200B; volledige instructies op hoe te om niet-het verlopen geloofsbrieven &#x200B;](../ui/credentials.md#non-expiring-credentials) te produceren en te gebruiken.

### SSL-modus instellen

Vervolgens moet u de waarde van de SSL-modus instellen op `?sslmode=require` . Dit gebeurt op het tabblad [!DNL Driver] van het dialoogvenster [!DNL Edit Server Properties] . Zie de officiële documentatie van de Studio van Gegevens Aqua voor instructies op hoe te [&#x200B; geef bestuurderseigenschappen uit &#x200B;](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation13/page/116/PostgreSQL#drivers) en [&#x200B; vorm SSL voor  [!DNL PostgreSQL] &#x200B;](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation20/page/SSL-Configuration/SSL-Configuration). Gebruik de zoekbalk om de eigenschap `sslmode` te zoeken.

>[!IMPORTANT]
>
>Zie de [[!DNL Query Service]  SSL documentatie &#x200B;](./ssl-modes.md) om over SSL steun voor derdeverbindingen aan de Dienst van de Vraag van Adobe Experience Platform te leren, en hoe te om het gebruiken van `verify-full` SSL wijze te verbinden.

Nadat u de verbindingsgegevens hebt ingevoerd, schakelt u op hetzelfde tabblad de optie **[!DNL Test Connection]** in om ervoor te zorgen dat uw referenties naar behoren werken. Als de verbindingstest succesvol is, selecteert u **[!DNL Save]** om uw server te registreren. Er verschijnt een bevestigingsvenster waarin de verbinding wordt bevestigd en het verbindingspictogram wordt weergegeven op het dashboard. U kunt nu verbinding maken met de server en de bijbehorende schemaobjecten weergeven.

## Volgende stappen

Nu u verbinding hebt gemaakt met [!DNL Query Service] , kunt u de instructies **[!DNL Query Analyzer]** within [!DNL Aqua Data Studio] gebruiken om SQL-instructies uit te voeren en te bewerken. Voor meer informatie over hoe te om vragen te schrijven en in werking te stellen, te lezen gelieve de [&#x200B; lopende vraaggids &#x200B;](../best-practices/writing-queries.md).
