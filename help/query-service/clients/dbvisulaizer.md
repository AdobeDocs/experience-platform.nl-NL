---
keywords: Experience Platform;huis;populaire onderwerpen;de vraagdienst;de dienst van de Vraag;Db Visualizer;DbVisualizer;db visulaizer;verbind met de vraagdienst;
solution: Experience Platform
title: Connect DbVisualizer aan de Dienst van de Vraag
topic-legacy: connect
description: Dit document doorloopt de stappen voor het verbinden van DbVisualizer met de Dienst van de Vraag van Adobe Experience Platform.
exl-id: badb0d89-1713-438c-8a9c-d1404051ff5f
source-git-commit: 7d38488c204e28c9cfd8ea50c06f1ce781d76c59
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 0%

---

# Verbinden [!DNL DbVisualizer] tot [!DNL Query Service] {#connect-dbvisualizer}

In dit document worden de stappen beschreven voor het verbinden van het [!DNL DbVisualizer] databasegereedschap met Adobe Experience Platform [!DNL Query Service].

## Aan de slag

Voor deze handleiding hebt u al toegang tot de [!DNL DbVisualizer] bureaubladtoepassing en weet hoe u door de interface kunt navigeren. Als u het dialoogvenster [!DNL DbVisualizer] bureaubladtoepassing of raadpleeg voor meer informatie de [ambtenaar [!DNL DbVisualizer] documentatie](https://www.dbvis.com/download/).

>[!NOTE]
>
>Er zijn [!DNL Windows], [!DNL macOS], en [!DNL Linux] versies van [!DNL DbVisualizer]. Screenshots in deze gids werden genomen gebruikend [!DNL macOS] bureaubladtoepassing. Er kunnen kleine discrepanties in UI tussen de versies zijn.

Om de vereiste geloofsbrieven te verkrijgen voor het verbinden [!DNL  DbVisualizer] aan Experience Platform, moet u toegang tot de werkruimte van Vragen in Platform UI hebben. Neem contact op met de beheerder van de IMS-organisatie als u momenteel geen toegang hebt tot de werkruimte Query&#39;s.

## Een databaseverbinding maken {#connect-database}

Nadat u de bureaubladtoepassing op uw lokale computer hebt geïnstalleerd, start u de toepassing en selecteert u **[!DNL Create a Database Connection]** vanaf de eerste [!DNL DbVisualizer] -menu. Selecteer vervolgens **[!DNL Create a Connection]** in het deelvenster rechts.

![De [!DNL DbVisualizer] hoofdmenu met de markering &#39;Een databaseverbinding maken&#39;.](../images/clients/dbvisualizer/create-db-connection.png)

Gebruik de zoekbalk of selecteer [!DNL PostgreSQL] in de vervolgkeuzelijst met bestuurdersnaam. De werkruimte Databaseverbinding wordt weergegeven.

![Het vervolgkeuzemenu voor de bestuurdersnaam met [!DNL PostgreSQL] gemarkeerd.](../images/clients/dbvisualizer/driver-name.png)

### Eigenschappen instellen voor uw verbinding {#properties}

Selecteer in de werkruimte Databaseverbinding de optie **[!DNL Properties]** tab, gevolgd door de **[!DNL Driver Properties]** op de navigatiezijbalk.

![De werkruimte Databaseverbinding met Eigenschappen en Eigenschappen van stuurprogramma gemarkeerd.](../images/clients/dbvisualizer/driver-properties.png)

Voer vervolgens de stuurprogramma-eigenschappen in die in de onderstaande tabel worden beschreven.

>[!IMPORTANT]
>
>Om DBVisualizer met Adobe Experience Platform te verbinden, moet u het gebruik van SSL toelaten. Zie de [Documentatie over SSL-modi](./ssl-modes.md) voor meer informatie over SSL-ondersteuning voor verbindingen van derden met Adobe Experience Platform Query Service en over het maken van verbindingen met deze service `verify-full` SSL-modus.

| Eigenschap | Beschrijving |
| ------ | ------ |
| `PGHOST` | De hostnaam voor de [!DNL PostgreSQL] server. Deze waarde is uw Experience Platform **[!UICONTROL Host]geloofsbrieven**. |
| `ssl` | De SSL-waarde definiëren `1` om het gebruik van SSL in te schakelen. |
| `sslmode` | Hiermee bepaalt u het niveau van SSL-beveiliging. U wordt aangeraden de `require` SSL-modus bij het verbinden van clients van derden met Adobe Experience Platform. De `require` De wijze zorgt ervoor dat de encryptie op alle mededelingen wordt vereist en dat het netwerk wordt vertrouwd om met de correcte server te verbinden. ServerSSL-certificaatvalidatie is niet vereist. |
| `user` | De gebruikersnaam die aan de database is gekoppeld, is uw organisatie-id. Het is een alfanumerieke tekenreeks die eindigt in `@Adobe.Org`. Deze waarde is uw Experience Platform **[!UICONTROL Username]geloofsbrieven**. |

Gebruik de zoekbalk om elke eigenschap te zoeken en selecteer vervolgens de bijbehorende cel voor de waarde van de parameter. De cel wordt in blauw gemarkeerd. Voer de referentie van het Platform in het veld Waarde in en selecteer **[!DNL Apply]** om de bestuurderseigenschap toe te voegen.

![Het tabblad Eigenschappen van DBVisulaizer-stuurprogramma met een ingevoerde waarde en de optie Toepassen gemarkeerd.](../images/clients/dbvisualizer/apply-parameter-value.png)

>[!NOTE]
>
>Een seconde toevoegen `user` profiel, selecteren `user` Selecteer vervolgens in de parameterkolom het pictogram blauw + (plus) om referenties voor elke gebruiker toe te voegen. Selecteren **[!DNL Apply]** om de bestuurderseigenschap toe te voegen.

De [!DNL Edited] de kolom toont een controleteken om erop te wijzen dat de parameterwaarde is bijgewerkt.

### Invoer[!DNL Query Service] geloofsbrieven

Als u de referenties wilt zoeken die nodig zijn om BBVisualizer te verbinden met Query Service, meldt u zich aan bij de gebruikersinterface van het Platform en selecteert u **[!UICONTROL Queries]** van de linkernavigatie, gevolgd door **[!UICONTROL Credentials]**. Meer informatie over het zoeken naar uw **host**, **poort**, **database**, **gebruikersnaam**, en **password** referenties, lees de [aanmeldingsgids](../ui/credentials.md).

![De pagina Credentials van de werkruimte van de Vragen van het Experience Platform met Geloofsbrieven en de Vervalende Gemarkeerde Referenties.](../images/clients/dbvisualizer/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] biedt ook niet-vervallende geloofsbrieven aan om voor eenmalig opstelling met derdecliënten toe te staan. Zie de documentatie voor [volledige instructies op hoe te om niet vervallende geloofsbrieven te produceren en te gebruiken](../ui/credentials.md#non-expiring-credentials). U moet dit proces voltooien als u BDVisualizer wilt aansluiten als een eenmalige installatie. De `credential` en `technicalAccountId` De verkregen waarden omvatten de waarde voor DBVisualizer `password` parameter.

## Verificatie

Selecteer **[!DNL Authentication]** vanaf de navigatiezijbalk onder [!DNL PostgreSQL].

Controleer in het deelvenster Verbindingsverificatie beide de opties **[!DNL Require Userid]** en **[!DNL Require Password]** selectievakjes en selecteer vervolgens **[!DNL Apply]**.

![Het deelvenster Verificatie voor [!DNL PostgreSQL] Databaseverbinding met de selectievakjes Gebruiker vereisen en Wachtwoord gemarkeerd.](../images/clients/dbvisualizer/connection-authentication.png)

## Verbinding maken met Platform

U kunt een verbinding maken met vervallende of niet-vervallende gegevens. Als u een verbinding wilt maken, selecteert u de optie **[!DNL Connection]** in de werkruimte Databaseverbinding en voer uw gegevens voor het Experience Platform in voor de volgende instellingen.

>[!NOTE]
>
>Alle geloofsbrieven die door BDVisualizer in de lijst hieronder worden vereist zijn het zelfde voor het verlopen en niet-verlopen geloofsbrieven tenzij vermeld in de parameterbeschrijving.

| Verbindingsparameter | Beschrijving |
|---|---|
| **[!UICONTROL Name]** | Maak een naam voor de verbinding. U wordt geadviseerd om een mensvriendelijke naam te verstrekken om de verbinding te erkennen. |
| **[!UICONTROL Database Server]** | Dit is uw Experience Platform **[!UICONTROL Host]** referentie. |
| **[!UICONTROL Database Port]** | De poort voor [!DNL Query Service]. U moet poort gebruiken **80** om te verbinden met [!DNL Query Service]. |
| **[!UICONTROL Database]** | Uw Experience Platform gebruiken **[!UICONTROL Database]** referentie waarde: `prod:all`. |
| **[!UICONTROL Database Userid]** | Dit is uw organisatie-id voor Platform. Uw Experience Platform gebruiken **[!UICONTROL Username]** referentie. De id heeft de notatie `ORG_ID@AdobeOrg`. |
| **[!UICONTROL Database Password]** | Deze alfanumerieke tekenreeks is uw Experience Platform **[!UICONTROL Password]** credential.If you want non-expiring credentials, this value is the concatenated arguments from the `technicalAccountID` en de `credential` gedownload in de configuratie JSON-bestand. De wachtwoordwaarde heeft de vorm: {technicalAccountId}:{credential}. Het configuratieJSON dossier voor niet-vervallende geloofsbrieven is een eenmalig download tijdens hun initialisering die Adobe geen exemplaar van houdt. |

Nadat u alle relevante gegevens hebt ingevoerd, selecteert u **[!DNL Connect]**.

![De [!DNL PostgreSQL] De werkruimte Databaseverbinding met het tabblad Verbinding en de knop Verbinding gemarkeerd.](../images/clients/dbvisualizer/connect.png)

De [!DNL Connect] wordt bij de eerste gelegenheid van de sessie weergegeven.

![De verbinding: [!DNL PostgreSQL] met de gemarkeerde tekstvelden Database-gebruikersnaam en Database-wachtwoord.](../images/clients/dbvisualizer/connect-dialog.png)

Voer uw gebruikersnaam en wachtwoord in en selecteer **[!DNL Connect]**. Er verschijnt een bericht in het logbestand ter bevestiging van een geslaagde verbinding.

## Volgende stappen

Nu hebt u verbinding [!DNL DbVisualizer] with [!DNL Query Service]kunt u [!DNL DbVisualizer] om query&#39;s te schrijven. Lees voor meer informatie over het schrijven en uitvoeren van query&#39;s de [handleiding voor het uitvoeren van query&#39;s](../best-practices/writing-queries.md).
