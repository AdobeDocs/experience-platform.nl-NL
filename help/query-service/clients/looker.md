---
keywords: Experience Platform;home;popular topics;Query service;query service;Looker;looker;connect to query service;
solution: Experience Platform
title: Verbinding maken met Looker
topic: connect
translation-type: tm+mt
source-git-commit: c5d3be4706ca6d6a30e203067db6ddc894b9bfb4
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# Verbinden met [!DNL Looker]

Volg onderstaande stappen om verbinding te maken [!DNL Looker] met [!DNL Query Service] Adobe Experience Platform:

Nadat u zich hebt aangemeld [!DNL Looker], klikt u op **[!UICONTROL Beheer]**, gevolgd door **[!UICONTROL Verbindingen]**.

![](../images/clients/looker/click-admin-connections.png)

Klik op deze pagina op **Nieuwe verbinding**.

![](../images/clients/looker/click-new-connection.png)

Van hier, kunt u de details voor de Montages van de Verbinding invullen.

![](../images/clients/looker/new-connection.png)

- **Naam:** De naam van de verbinding.
- **Dialect:** Het dialect dat voor het SQL gegevensbestand wordt gebruikt. [!DNL Query Service] gebruik **[!DNL PostgreSQL]**.
- **Host en poort:** Het gastheereindpunt en zijn haven voor [!DNL Query Service].
- **Database:** De database die wordt gebruikt.
- **Gebruikersnaam en wachtwoord:** De aanmeldingsgegevens die worden gebruikt. De gebruikersnaam heeft de vorm van `ORG_ID@AdobeOrg`.

>[!NOTE]
>
>Ga naar de pagina met [referenties op het Platform](https://platform.adobe.com/query/configuration)voor meer informatie over het zoeken naar uw host en poort, databasenaam en aanmeldingsgegevens. Als u uw referenties wilt zoeken, meldt u zich aan bij [!DNL Platform], klikt u op **[!UICONTROL Vragen]** en vervolgens op **[!UICONTROL Referenties]**.

Nadat u de verbindingsgegevens hebt ingevoerd, klikt u op Deze instellingen **** testen om te controleren of uw referenties naar behoren werken. Als dat het geval is, wordt hieronder een bericht weergegeven dat u verbinding kunt maken. Als de verbinding daadwerkelijk tot stand is gebracht, klikt u op Verbinding **** toevoegen om de verbinding te maken.

![](../images/clients/looker/click-test-connection.png)

## Volgende stappen

Nu u met hebt verbonden [!DNL Query Service], kunt u gebruiken [!DNL Looker] om vragen te schrijven. Voor meer informatie over hoe te om vragen te schrijven en in werking te stellen, te lezen gelieve de [lopende vraaggids](../creating-queries/creating-queries.md).