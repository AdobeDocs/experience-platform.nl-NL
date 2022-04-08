---
keywords: Experience Platform;huis;populaire onderwerpen;vraagdienst;de dienst van de Vraag;de Studio van Gegevens Aqua;de gegevensstudio van Aqua;verbind met de vraagdienst;
solution: Experience Platform
title: Connect Aqua Data Studio aan de Dienst van de Vraag
topic-legacy: connect
description: Dit document doorloopt de stappen voor het verbinden van de Studio van Gegevens Aqua met de Dienst van de Vraag van Adobe Experience Platform.
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: a887c502213e96d6af90af0859da78c2984f89a7
workflow-type: tm+mt
source-wordcount: '464'
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

Na installatie [!DNL Aqua Data Studio], moet u de server eerst registreren. Selecteer in het hoofdmenu de optie **[!DNL Server]**, gevolgd door **[!DNL Register Server]**.

![Het vervolgkeuzemenu Server met registerserver gemarkeerd.](../images/clients/aqua-data-studio/register-server.png)

De **[!DNL Register Server]** wordt weergegeven. Onder de **[!DNL General]** tab, selecteert u **[!DNL PostgreSQL]** in de lijst aan de linkerkant. Geef in het dialoogvenster dat wordt weergegeven de volgende gegevens op voor de serverinstellingen.

- **[!DNL Name]**: De naam van de verbinding. U wordt aangeraden een vriendelijke naam op te geven om de verbinding te herkennen.
- **[!DNL Login Name]**: De aanmeldingsnaam is uw organisatie-id voor het Platform. Het heeft de vorm van `ORG_ID@AdobeOrg`.
- **[!DNL Password]**: Dit is een alfanumerieke tekenreeks die wordt gevonden op het tabblad [!DNL Query Service] verificatiedashboard.
- **[!DNL Host and Port]**: Het gastheereindpunt en zijn haven voor [!DNL Query Service]. U moet poort 80 gebruiken om verbinding te maken met [!DNL Query Service].
- **[!DNL Database]:** De database die wordt gebruikt. De waarde voor de gebruikersinterface van het Platform gebruiken `dbname`: `prod:all`.

![Het lusje van de Studio Algemeen van Gegevens Aqua met de vereiste benadrukte inputgebieden.](../images/clients/aqua-data-studio/register-server-general-tab.png)

### [!DNL Query Service] geloofsbrieven

Meld u aan bij de [!DNL Platform] UI en selecteer **[!UICONTROL Queries]** van de linkernavigatie, gevolgd door **[!UICONTROL Credentials]**. Voor volledige instructies voor het zoeken naar uw aanmeldingsgegevens, host, poort en databasenaam leest u de [aanmeldingsgids](../ui/credentials.md).

[!DNL Query Service] biedt ook niet-vervallende geloofsbrieven aan om voor eenmalig opstelling met derdecliënten toe te staan. Zie de documentatie voor [volledige instructies op hoe te om niet vervallende geloofsbrieven te produceren en te gebruiken](../ui/credentials.md#non-expiring-credentials).

### SSL-modus instellen

Selecteer vervolgens de **[!DNL Driver]** tab. Onder **[!DNL Parameters]**, stelt u de waarde in als `?sslmode=require`

![Het lusje van de Bestuurder van de Studio van Gegevens Aqua met het benadrukte gebied van Parameters.](../images/clients/aqua-data-studio/register-server-driver-tab.png)

Selecteer **[!DNL Test Connection]** om ervoor te zorgen dat uw gegevens correct werken. Selecteer **[!DNL Save]** om uw server te registreren. Er verschijnt een bevestigingsvenster waarin de verbinding wordt bevestigd en de verbinding wordt weergegeven op het dashboard. U kunt nu verbinding maken met de server en de bijbehorende schemaobjecten weergeven.

## Volgende stappen

Nu hebt u verbinding met [!DNL Query Service]kunt u de **[!DNL Query Analyzer]** binnen [!DNL Aqua Data Studio] om SQL-instructies uit te voeren en te bewerken. Lees voor meer informatie over het schrijven en uitvoeren van query&#39;s de [gids voor uitvoeren van query&#39;s](../best-practices/writing-queries.md).
