---
keywords: Experience Platform;huis;populaire onderwerpen;de vraagdienst;de dienst van de Vraag;Db Visualizer;DbVisualizer;db visulaizer;verbind met de vraagdienst;
solution: Experience Platform
title: Connect DbVisualizer aan de Dienst van de Vraag
topic-legacy: connect
description: Dit document doorloopt de stappen voor het verbinden van DbVisualizer met de Dienst van de Vraag van Adobe Experience Platform.
source-git-commit: 69e105b2c52a668ba708847795d4c92813aad0db
workflow-type: tm+mt
source-wordcount: '697'
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

Selecteer in de werkruimte Databaseverbinding de optie **[!DNL Properties]** tab, gevolgd door de **[!DNL Driver Properties]** op de navigatiezijbalk.

![De werkruimte Databaseverbinding met de tab Eigenschappen gemarkeerd.](../images/clients/dbvisualizer/driver-properties.png)

De drie vereiste bestuurderseigenschappen worden gezien in de onderstaande tabel.

| Eigenschap | Beschrijving |
| ------ | ------ |
| `PGHOST` | De hostnaam voor de [!DNL PostgreSQL] server. Deze waarde is uw Experience Platform [!UICONTROL Host] referentie. |
| `SSL` | Dit bepaalt het gebruik van SSL-vereisten. U **moet** Gebruik de waarde &quot;1&quot; om deze vereiste in te schakelen. |
| `user` | De gebruikersnaam die aan de database is gekoppeld, is uw organisatie-id. Het is een alfanumerieke tekenreeks die eindigt in `@adobe.org` |

### [!DNL Query Service] geloofsbrieven

De `PGHOST` en `user` worden waarden opgehaald uit uw Adobe Experience Platform-referenties. Meld u aan bij de gebruikersinterface van het Platform en selecteer **[!UICONTROL Queries]** van de linkernavigatie, gevolgd door **[!UICONTROL Credentials]**. Voor meer informatie over het vinden van uw gegevensbestandnaam, gastheer, haven, en login geloofsbrieven, gelieve te lezen [aanmeldingsgids](../ui/credentials.md).

![Experience Platform vraagt het Dashboard van Referenties met benadrukte geloofsbrieven.](../images/clients/dbvisualizer/query-service-credentials-page.png)

[!DNL Query Service] biedt ook niet-vervallende geloofsbrieven aan om voor eenmalig opstelling met derdecliënten toe te staan. Zie de documentatie voor [volledige instructies op hoe te om niet vervallende geloofsbrieven te produceren en te gebruiken](../ui/credentials.md#non-expiring-credentials).

Gebruik de zoekbalk om elke eigenschap te zoeken en selecteer vervolgens de bijbehorende cel voor de waarde van de parameter. De cel wordt in blauw gemarkeerd. Voer de referentie van het Platform in het veld Waarde in en selecteer **[!DNL Apply]** om de bestuurderseigenschap toe te voegen.

>[!NOTE]
>
>Een seconde toevoegen `user` profiel, selecteren `user` Selecteer vervolgens in de parameterkolom het pictogram blauw + (plus) om referenties voor elke gebruiker toe te voegen. Selecteren **[!DNL Apply]** om de bestuurderseigenschap toe te voegen.

De [!DNL Edited] de kolom toont een controleteken om erop te wijzen dat de parameterwaarde is bijgewerkt.

## Verificatie

Selecteer **[!DNL Authentication]** vanaf de navigatiezijbalk onder [!DNL PostgreSQL].

Controleer in het deelvenster Verbindingsverificatie beide de opties **[!DNL Require Userid]** en **[!DNL Require Password]** selectievakjes en selecteer vervolgens **[!DNL Apply]**.

![Het deelvenster Verbindingsverificatie met de selectievakjes Gebruiker en Wachtwoord gemarkeerd.](../images/clients/dbvisualizer/connection-authentication.png)

## Verbinding maken met Platform

Als u een verbinding wilt maken, selecteert u de optie **[!DNL Connection]** in de werkruimte Databaseverbinding en voer uw gegevens voor het Experience Platform in voor de volgende instellingen.

- **Naam**: U wordt aangeraden een vriendelijke naam op te geven om de verbinding te herkennen.
- **Databaseserver**: Dit is uw Experience Platform [!UICONTROL Host] referentie.
- **Databasepoort**: De poort voor [!DNL Query Service]. U moet poort 80 gebruiken om verbinding te maken met [!DNL Query Service].
- **Database**: De referentie gebruiken `dbname` value `prod:all`.
- **Database-gebruiker**: Dit is uw organisatie-id voor Platform. De gebruikersnaam heeft de notatie `ORG_ID@AdobeOrg`.
- **Wachtwoord database**: Dit is een alfanumerieke tekenreeks die wordt gevonden op het tabblad [!DNL Query Service] verificatiedashboard.

Nadat u alle relevante gegevens hebt ingevoerd, selecteert u **[!DNL Connect]**.

![De werkruimte Databaseverbinding met het tabblad Verbinding en de knop Verbinding gemarkeerd.](../images/clients/dbvisualizer/connect.png)

De [!DNL Connect] wordt bij de eerste gelegenheid van de sessie weergegeven.

![Het dialoogvenster Verbinding maken met de tekstvelden voor databasegebruikers en databasewachtwoorden wordt gemarkeerd.](../images/clients/dbvisualizer/connect-dialog.png)

Voer uw gebruikersnaam en wachtwoord in en selecteer **[!DNL Connect]**. Er verschijnt een bericht in het logbestand ter bevestiging van een geslaagde verbinding.

## Volgende stappen

Nu hebt u verbinding [!DNL DbVisualizer] with [!DNL Query Service]kunt u [!DNL DbVisualizer] om query&#39;s te schrijven. Lees voor meer informatie over het schrijven en uitvoeren van query&#39;s de [handleiding voor het uitvoeren van query&#39;s](../best-practices/writing-queries.md).
