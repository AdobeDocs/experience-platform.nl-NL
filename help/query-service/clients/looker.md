---
keywords: Experience Platform;home;populaire onderwerpen;de dienst van de Vraag;de vraagdienst;Leider;Leider;verbindt met de vraagdienst;
solution: Experience Platform
title: Verbinding maken met Zoekservice
description: Dit document doorloopt de stappen voor het verbinden van de Teller met de Dienst van de Vraag van Adobe Experience Platform.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# Verbinden [!DNL Looker] met de Dienst van de Vraag

In dit document worden de stappen beschreven voor het maken van een verbinding tussen [!DNL Looker] en Adobe Experience Platform [!DNL Query Service] .

>[!NOTE]
>
> In deze handleiding wordt ervan uitgegaan dat u al toegang hebt tot [!DNL Looker] en dat u bekend bent met de manier waarop u door de interface kunt navigeren. Meer informatie over [!DNL Looker] kan in de [ officiële  [!DNL Looker]  documentatie ](https://docs.looker.com/) worden gevonden.

## Nieuwe databaseverbinding maken {#create-connection}

Nadat u zich hebt aangemeld bij [!DNL Looker] , selecteert u **[!DNL Admin]** , gevolgd door **[!DNL Connections]** . De pagina [!DNL Connections] wordt geopend. Selecteer op de pagina [!DNL Connections] de optie **[!DNL Add Connection]** .

Voer vanaf hier de gegevens in voor de verbindingsinstellingen die hieronder worden vermeld. Zie de officiële documentatie van de Teller voor [ instructies om een nieuwe gegevensbestandverbinding en beschrijvingen van de beschikbare eigenschappen ](https://cloud.google.com/looker/docs/connecting-to-your-db#creating_a_new_database_connection) tot stand te brengen.

- **[!DNL Name]:** De naam van uw verbinding.
- **[!DNL Dialect]:** Het dialect dat voor het SQL gegevensbestand wordt gebruikt. [!DNL Query Service] gebruikt **[!DNL PostgreSQL]** .
- **[!DNL Host and Port]:** Het eindpunt van de host en de bijbehorende poort voor [!DNL Query Service] .
- **[!DNL Database]:** De database die wordt gebruikt.
- **[!DNL Username and Password]:** De login geloofsbrieven die zullen worden gebruikt. De gebruikersnaam heeft de notatie `ORG_ID@AdobeOrg` .
- **SSL**: Laat SSL toe om een veilige verbinding over het netwerk te verzekeren.

Als u de gegevens wilt zoeken die nodig zijn om verbinding te maken met Zoekservice, meldt u zich aan bij de gebruikersinterface van Experience Platform en selecteert u **[!UICONTROL Queries]** in de linkernavigatie, gevolgd door **[!UICONTROL Credentials]** . Voor meer informatie bij het vinden van uw **gastheer**, **haven**, **gegevensbestand**, **gebruikersbenaming**, en **wachtwoord** geloofsbrieven, te lezen gelieve de [ geloofsbrieven gids ](../ui/credentials.md).

![ de pagina van Geloofsbrieven van de werkruimte van de Vragen van Experience Platform met Geloofsbrieven en de Verpletterende Gemaakte Referenties.](../images/clients/looker/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] biedt ook niet-vervallende referenties, zodat een eenmalige installatie met externe clients mogelijk is. Zie de documentatie voor [ volledige instructies op hoe te om niet-het verlopen geloofsbrieven ](../ui/credentials.md#non-expiring-credentials) te produceren en te gebruiken. U moet dit proces voltooien als u de Minder afhankelijk van de software wilt maken. De verkregen waarden `credential` en `technicalAccountId` omvatten de waarde voor de parameter Loker `password` .

Om over SSL steun voor derdeverbindingen in Adobe Experience Platform te leren, zie de [[!DNL Query Service]  SSL documentatie ](./ssl-modes.md). Dit document bevat instructies voor het maken van een verbinding met de SSL-modus `verify-full` .

Nadat u de verbindingsgegevens hebt ingevoerd, selecteert u **[!DNL Test These Settings]** om te controleren of uw referenties naar behoren werken. Meer informatie over [ het testen van uw verbindingsmontages ](https://cloud.google.com/looker/docs/connecting-to-your-db#testing_your_connection_settings) wordt verstrekt in de officiële documentatie van de Teller. Na een geslaagde verbinding wordt op het scherm een bericht weergegeven dat u verbinding kunt maken. Wanneer de verbinding is gelukt, selecteert u **[!DNL Add Connection]** om de verbinding te maken.

## Volgende stappen

Nu u verbinding hebt met [!DNL Query Service], kunt u [!DNL Looker] gebruiken om query&#39;s te schrijven. Voor meer informatie over hoe te om vragen te schrijven en in werking te stellen, te lezen gelieve de [ lopende vraaggids ](../best-practices/writing-queries.md).
