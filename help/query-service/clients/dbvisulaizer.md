---
keywords: Experience Platform;home;populaire onderwerpen;queryservice;Query-service;Db Visualizer;DbVisualizer;db visulaizer;connect to query service;
solution: Experience Platform
title: Connect DbVisualizer aan de Dienst van de Vraag
description: Dit document doorloopt de stappen voor het verbinden van DbVisualizer met de Dienst van de Vraag van Adobe Experience Platform.
exl-id: badb0d89-1713-438c-8a9c-d1404051ff5f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 0%

---

# Verbinden [!DNL DbVisualizer] met [!DNL Query Service] {#connect-dbvisualizer}

In dit document worden de stappen beschreven voor het verbinden van het databasehulpprogramma [!DNL DbVisualizer] met Adobe Experience Platform [!DNL Query Service] .

## Aan de slag

Deze handleiding vereist dat u al toegang hebt tot de bureaubladtoepassing van [!DNL DbVisualizer] en dat u bekend bent met de manier waarop u door de interface kunt navigeren. Om [!DNL DbVisualizer] Desktop app of voor meer informatie te downloaden, zie de [ officiële  [!DNL DbVisualizer]  documentatie ](https://www.dbvis.com/download/).

U hebt toegang tot de werkruimte Query&#39;s in de gebruikersinterface van Experience Platform nodig om de referenties te verkrijgen waarmee u [!DNL &#x200B; DbVisualizer] kunt verbinden met Experience Platform. Neem contact op met uw organisatiebeheerder als u momenteel geen toegang hebt tot de werkruimte Query&#39;s.

## Een databaseverbinding maken {#connect-database}

Zodra u Desktop app op uw lokale machine hebt geïnstalleerd, volg de officiële instructies BDVisualizer om [ een nieuwe gegevensbestandverbinding ](https://confluence.dbvis.com/display/UG130/Create+a+New+Database+Connection) tot stand te brengen.

Nadat u **[!DNL PostgreSQL]** in de lijst [!DNL Connections] hebt geselecteerd, wordt een tabblad [!DNL Object View] voor de nieuwe [!DNL PostgreSQL] -verbinding weergegeven.

### Eigenschappen van stuurprogramma instellen voor uw verbinding {#properties}

Selecteer op het tabblad objectweergave van [!DNL PostgreSQL] de tab **[!DNL Properties]** , gevolgd door de **[!DNL Driver Properties]** in het navigatiezijpaneel. Meer informatie over [ bestuurderseigenschappen ](https://confluence.dbvis.com/display/UG130/Configuring+Connection+Properties#ConfiguringConnectionProperties-DriverProperties) kan in de officiële documentatie worden gevonden.

Voer vervolgens de stuurprogramma-eigenschappen in die in de onderstaande tabel worden beschreven.

>[!IMPORTANT]
>
>Om DBVisualizer met Adobe Experience Platform te verbinden, moet u het gebruik van SSL toelaten. Zie de [ SSL wijzedocumentatie ](./ssl-modes.md) om over SSL steun voor derdeverbindingen aan de Dienst van de Vraag van Adobe Experience Platform te leren, en hoe te om het gebruiken van `verify-full` SSL wijze te verbinden.

| Eigenschap | Beschrijving |
| ------ | ------ |
| `PGHOST` | De hostnaam voor de [!DNL PostgreSQL] -server. Deze waarde is uw Experience Platform **[!UICONTROL Host]referentie** . |
| `ssl` | Definieer de SSL-waarde `1` om het gebruik van SSL in te schakelen. |
| `sslmode` | Hiermee bepaalt u het niveau van SSL-beveiliging. U wordt aangeraden de SSL-modus van `require` te gebruiken wanneer u clients van derden verbindt met Adobe Experience Platform. De `require` wijze zorgt ervoor dat de encryptie op alle mededelingen wordt vereist en dat het netwerk wordt vertrouwd om met de correcte server te verbinden. ServerSSL-certificaatvalidatie is niet vereist. |
| `user` | De gebruikersnaam die aan de database is gekoppeld, is uw organisatie-id. Het is een alfanumerieke tekenreeks die eindigt in `@Adobe.Org` . Deze waarde is uw Experience Platform **[!UICONTROL Username]referentie** . |

Gebruik de zoekbalk om elke eigenschap te zoeken en selecteer vervolgens de bijbehorende cel voor de waarde van de parameter. De cel wordt in blauw gemarkeerd. Voer in het waardeveld uw Experience Platform-referentie in en selecteer **[!DNL Apply]** om de eigenschap driver toe te voegen.

>[!NOTE]
>
>Als u een tweede `user` -profiel wilt toevoegen, selecteert u `user` in de parameterkolom en selecteert u vervolgens het pictogram blauw + (plus) om referenties voor elke gebruiker toe te voegen. Selecteer **[!DNL Apply]** om de eigenschap driver toe te voegen.

In de kolom [!DNL Edited] staat een vinkje waarmee wordt aangegeven dat de parameterwaarde is bijgewerkt.

### Invoerquery-servicegegevens {#query-service-credentials}

Als u de gegevens wilt zoeken die nodig zijn om BBVisualizer te verbinden met Query Service, meldt u zich aan bij de gebruikersinterface van Experience Platform en selecteert u **[!UICONTROL Queries]** in de linkernavigatie, gevolgd door **[!UICONTROL Credentials]** . Voor meer informatie bij het vinden van uw **gastheer**, **haven**, **gegevensbestand**, **gebruikersbenaming**, en **wachtwoord** geloofsbrieven, te lezen gelieve de [ geloofsbrieven gids ](../ui/credentials.md).

![ de pagina van Geloofsbrieven van de werkruimte van de Vragen van Experience Platform met Geloofsbrieven en de Verpletterende Gemaakte Referenties.](../images/clients/dbvisualizer/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] biedt ook niet-vervallende referenties, zodat een eenmalige installatie met externe clients mogelijk is. Zie de documentatie voor [ volledige instructies op hoe te om niet-het verlopen geloofsbrieven ](../ui/credentials.md#non-expiring-credentials) te produceren en te gebruiken. U moet dit proces voltooien als u BDVisualizer wilt aansluiten als een eenmalige installatie. De verkregen waarden `credential` en `technicalAccountId` vormen de waarde voor de parameter DBVisualizer `password` .

## Verificatie {#authentication}

Als u telkens wanneer een verbinding tot stand wordt gebracht, een gebruikers-id en op een wachtwoord gebaseerde verificatie wilt vereisen, navigeert u naar het tabblad [!DNL Properties] en selecteert u **[!DNL Authentication]** in het navigatiezijpaneel onder [!DNL PostgreSQL] .

Schakel in het deelvenster Verbindingsverificatie de selectievakjes **[!DNL Require Userid]** en **[!DNL Require Password]** in en selecteer **[!DNL Apply]** . Meer informatie over [ plaatsende authentificatieopties ](https://confluence.dbvis.com/display/UG140/Setting+Common+Authentication+Options) kan in de officiële documentatie worden gevonden.

## Verbinding maken met Experience Platform

U kunt een verbinding maken met vervallende of niet-vervallende gegevens. Als u verbinding wilt maken, selecteert u het tabblad **[!DNL Connection]** op het tabblad objectweergave van [!DNL PostgreSQL] en voert u uw Experience Platform-referenties voor de volgende instellingen in. Aanvullende instructies aan [ opstelling een handverbinding ](https://confluence.dbvis.com/display/UG100/Setting+Up+a+Connection+Manually) zijn beschikbaar op de officiële website DBVisualizer.

>[!NOTE]
>
>Alle geloofsbrieven die door BDVisualizer in de lijst hieronder worden vereist zijn het zelfde voor het verlopen en niet-verlopen geloofsbrieven tenzij vermeld in de parameterbeschrijving.

| Verbindingsparameter | Beschrijving |
|---|---|
| **[!UICONTROL Name]** | Maak een naam voor de verbinding. U wordt geadviseerd om een mensvriendelijke naam te verstrekken om de verbinding te erkennen. |
| **[!UICONTROL Database Server]** | Dit is uw Experience Platform **[!UICONTROL Host]** referentie. |
| **[!UICONTROL Database Port]** | De poort voor [!DNL Query Service] . U moet haven **80** of **gebruiken 5432** om met [!DNL Query Service] te verbinden. |
| **[!UICONTROL Database]** | Gebruik uw Experience Platform **[!UICONTROL Database]** -referentie: `prod:all` . |
| **[!UICONTROL Database Userid]** | Dit is je Experience Platform-organisatie-id. Gebruik de Experience Platform **[!UICONTROL Username]** -referentie. De id heeft de notatie `ORG_ID@AdobeOrg` . |
| **[!UICONTROL Database Password]** | Deze alfanumerieke tekenreeks is uw Experience Platform **[!UICONTROL Password]** referentie. Als u niet-verlopen geloofsbrieven wilt gebruiken, is deze waarde de samengevoegde argumenten van `technicalAccountID` en `credential` gedownload in het configuratieJSON dossier. De wachtwoordwaarde heeft de vorm: {technicalAccountId}:{credential}. Het configuratie-JSON-bestand voor niet-vervallende gegevens is een eenmalige download tijdens de initialisatie waarbij Adobe geen kopie van het bestand bewaart. |

Nadat u alle relevante gegevens hebt ingevoerd, selecteert u **[!DNL Connect]** .

Het dialoogvenster [!DNL Connect] wordt voor het eerst van de sessie weergegeven. Voer uw gebruikersnaam en wachtwoord in en selecteer **[!DNL Connect]** . Er verschijnt een bericht in het logbestand ter bevestiging van een geslaagde verbinding.

## Volgende stappen

Nu u [!DNL DbVisualizer] met [!DNL Query Service] hebt verbonden, kunt u [!DNL DbVisualizer] gebruiken om query&#39;s te schrijven. Voor meer informatie over om vragen te schrijven en in werking te stellen, gelieve de [ gids op vraaguitvoering ](../best-practices/writing-queries.md) te lezen.
