---
keywords: Experience Platform;huis;populaire onderwerpen;vraagdienst;de dienst van de Vraag;de Studio van Gegevens Aqua;de gegevensstudio van Aqua;verbind met de vraagdienst;
solution: Experience Platform
title: Connect Aqua Data Studio aan de Dienst van de Vraag
description: Dit document doorloopt de stappen voor het verbinden van de Studio van Gegevens Aqua met de Dienst van de Vraag van Adobe Experience Platform.
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: 3ffb535e9a6648f037678acebba0de5f2088e79e
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# Verbinden [!DNL Aqua Data Studio] aan de Dienst van de Vraag

In dit document worden de stappen beschreven voor het verbinden [!DNL Aqua Data Studio] met Adobe Experience Platform [!DNL Query Service].

## Aan de slag

Voor deze handleiding hebt u al toegang tot [!DNL Aqua Data Studio] en vertrouwd zijn met hoe te om zijn interface te navigeren. Meer informatie over [!DNL Aqua Data Studio] kunt u vinden in het dialoogvenster [ambtenaar [!DNL Aqua Data Studio] documentatie](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1).

>[!NOTE]
>
>Er zijn [!DNL Windows] en [!DNL macOS] versies van [!DNL Aqua Data Studio]. Screenshots in deze gids werden genomen gebruikend [!DNL macOS] bureaubladtoepassing. Er kunnen kleine discrepanties in UI tussen de versies zijn.

Om de vereiste geloofsbrieven te verkrijgen voor het verbinden [!DNL Aqua Data Studio] aan Experience Platform, moet u toegang hebben tot [!UICONTROL Queries] in de gebruikersinterface van het Platform. Neem contact op met uw IMS-systeembeheerder als u momenteel geen toegang hebt tot de [!UICONTROL Queries] werkruimte.

## De server registreren {#register-server}

Na installatie [!DNL Aqua Data Studio], moet u de server eerst registreren. Zie de officiële documentatie van de Studio van Gegevens van Aqua voor instructies over hoe te [start de [!DNL Register Server] dialoogvenster](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#launching_the_register_server_dialog) en [de server registreren](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#steps_to_register_a_server_in_aqua_data_studio).

Wanneer de **[!DNL Register Server]** wordt weergegeven voor een PostgresSQL-server. Geef de volgende gegevens op voor de serverinstellingen.

- **[!DNL Name]**: De naam van de verbinding. U wordt aangeraden een vriendelijke naam op te geven om de verbinding te herkennen.
- **[!DNL Login Name]**: De aanmeldingsnaam is uw organisatie-id voor het Platform. Het heeft de vorm van `ORG_ID@AdobeOrg`.
- **[!DNL Password]**: Dit is een alfanumerieke tekenreeks die wordt gevonden op het tabblad [!DNL Query Service] verificatiedashboard.
- **[!DNL Host and Port]**: Het gastheereindpunt en zijn haven voor [!DNL Query Service]. U moet poort 80 gebruiken om verbinding te maken met [!DNL Query Service].
- **[!DNL Database]:** De database die wordt gebruikt. De waarde voor de gebruikersinterface van het Platform gebruiken `dbname`: `prod:all`.

### [!DNL Query Service] geloofsbrieven

Meld u aan bij de [!DNL Platform] UI en selecteer **[!UICONTROL Queries]** van de linkernavigatie, gevolgd door **[!UICONTROL Credentials]**. Voor volledige instructies voor het zoeken naar uw aanmeldingsgegevens, host, poort en databasenaam leest u de [aanmeldingsgids](../ui/credentials.md).

[!DNL Query Service] biedt ook niet-vervallende geloofsbrieven aan om voor eenmalig opstelling met derdecliënten toe te staan. Zie de documentatie voor [volledige instructies op hoe te om niet vervallende geloofsbrieven te produceren en te gebruiken](../ui/credentials.md#non-expiring-credentials).

### SSL-modus instellen

Vervolgens moet u de waarde van de SSL-modus instellen als `?sslmode=require`. Dit wordt gedaan van [!DNL Driver] tabblad van het dialoogvenster [!DNL Edit Server Properties] . Zie de officiële documentatie van de Studio van Gegevens van Aqua voor instructies over hoe te [bestuurderseigenschappen bewerken](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation13/page/116/PostgreSQL#drivers) en [SSL configureren voor [!DNL PostgreSQL]](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation20/page/SSL-Configuration/SSL-Configuration). Gebruik de zoekbalk om de `sslmode` eigenschap.

>[!IMPORTANT]
>
>Zie de [[!DNL Query Service] SSL-documentatie](./ssl-modes.md) voor meer informatie over SSL-ondersteuning voor verbindingen van derden met Adobe Experience Platform Query Service en over het maken van verbindingen met deze service `verify-full` SSL-modus.

Na het invoeren van uw verbindingsdetails, van het zelfde lusje, selecteer **[!DNL Test Connection]** om ervoor te zorgen dat uw gegevens correct werken. Selecteer **[!DNL Save]** om uw server te registreren. Er verschijnt een bevestigingsvenster waarin de verbinding wordt bevestigd en het verbindingspictogram wordt weergegeven op het dashboard. U kunt nu verbinding maken met de server en de bijbehorende schemaobjecten weergeven.

## Volgende stappen

Nu hebt u verbinding met [!DNL Query Service]kunt u de **[!DNL Query Analyzer]** binnen [!DNL Aqua Data Studio] om SQL-instructies uit te voeren en te bewerken. Lees voor meer informatie over het schrijven en uitvoeren van query&#39;s de [gids voor uitvoeren van query&#39;s](../best-practices/writing-queries.md).
