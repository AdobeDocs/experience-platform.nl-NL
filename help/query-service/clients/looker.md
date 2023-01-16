---
keywords: Experience Platform;huis;populaire onderwerpen;de dienst van de Vraag;de vraagdienst;Leider;Leider;verbindt met de vraagdienst;
solution: Experience Platform
title: Verbinding maken met Zoekservice
description: Dit document doorloopt de stappen voor het verbinden van de Teller met de Dienst van de Vraag van Adobe Experience Platform.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: b059a0191fbf2c3e5d2dfceb9802e2aaa429f7ed
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 0%

---

# Verbinden [!DNL Looker] aan de Dienst van de Vraag

In dit document worden de stappen beschreven voor het verbinden [!DNL Looker] met Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Deze handleiding gaat ervan uit dat u al toegang hebt tot [!DNL Looker] en zijn vertrouwd met hoe te om zijn interface te navigeren. Meer informatie over [!DNL Looker] kunt u vinden in het dialoogvenster [ambtenaar [!DNL Looker] documentatie](https://docs.looker.com/).

## Nieuwe databaseverbinding maken {#create-connection}

Nadat u zich hebt aangemeld [!DNL Looker], selecteert u **[!DNL Admin]**, gevolgd door **[!DNL Connections]**. De [!DNL Connections] pagina wordt geopend. Op de [!DNL Connections] pagina, selecteert u **[!DNL Add Connection]**.

Voer vanaf hier de gegevens in voor de verbindingsinstellingen die hieronder worden vermeld. Zie de officiële documentatie van de Teller voor [instructies voor het maken van een nieuwe databaseverbinding en beschrijvingen van de beschikbare eigenschappen](https://cloud.google.com/looker/docs/connecting-to-your-db#creating_a_new_database_connection).

- **[!DNL Name]:** De naam van de verbinding.
- **[!DNL Dialect]:** Het dialect dat voor het SQL gegevensbestand wordt gebruikt. [!DNL Query Service] gebruik **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** Het gastheereindpunt en zijn haven voor [!DNL Query Service].
- **[!DNL Database]:** De database die wordt gebruikt.
- **[!DNL Username and Password]:** De aanmeldingsgegevens die worden gebruikt. De gebruikersnaam heeft de vorm van `ORG_ID@AdobeOrg`.
- **SSL**: Schakel SSL in om een veilige verbinding via het netwerk te garanderen.

Om de geloofsbrieven te vinden noodzakelijk om de Teller met de Dienst van de Vraag te verbinden, login aan het Platform UI en selecteer **[!UICONTROL Queries]** van de linkernavigatie, gevolgd door **[!UICONTROL Credentials]**. Meer informatie over het zoeken naar uw **host**, **poort**, **database**, **gebruikersnaam**, en **password** referenties, lees de [aanmeldingsgids](../ui/credentials.md).

![De pagina Credentials van de werkruimte van de Vragen van het Experience Platform met Geloofsbrieven en de Vervalende Gemarkeerde Referenties.](../images/clients/looker/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] biedt ook niet-vervallende geloofsbrieven aan om voor eenmalig opstelling met derdecliënten toe te staan. Zie de documentatie voor [volledige instructies op hoe te om niet vervallende geloofsbrieven te produceren en te gebruiken](../ui/credentials.md#non-expiring-credentials). U moet dit proces voltooien als u de Minder afhankelijk van de software wilt maken. De `credential` en `technicalAccountId` de verkregen waarden omvatten de waarde voor de Teller `password` parameter.

Voor meer informatie over SSL-ondersteuning voor verbindingen van derden in Adobe Experience Platform raadpleegt u de [[!DNL Query Service] SSL-documentatie](./ssl-modes.md). Dit document bevat instructies voor het maken van een verbinding met `verify-full` SSL-modus.

Nadat u de verbindingsgegevens hebt ingevoerd, selecteert u **[!DNL Test These Settings]** om ervoor te zorgen dat uw gegevens correct werken. Meer informatie over [het testen van uw verbindingsmontages](https://cloud.google.com/looker/docs/connecting-to-your-db#testing_your_connection_settings) worden verstrekt in de officiële documentatie van de Leider. Na een geslaagde verbinding wordt op het scherm een bericht weergegeven dat u verbinding kunt maken. Als de verbinding is gelukt, selecteert u **[!DNL Add Connection]** om uw verbinding te maken.

## Volgende stappen

Nu hebt u verbinding met [!DNL Query Service]kunt u [!DNL Looker] om query&#39;s te schrijven. Lees voor meer informatie over het schrijven en uitvoeren van query&#39;s de [gids voor uitvoeren van query&#39;s](../best-practices/writing-queries.md).
