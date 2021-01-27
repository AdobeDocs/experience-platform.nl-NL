---
keywords: Experience Platform;home;popular topics;Query service;query service;Looker;looker;connect to query service;
solution: Experience Platform
title: Verbinding maken met Looker
topic: connect
description: Dit document doorloopt de stappen voor het verbinden van de Teller met de Dienst van de Vraag van Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 9fbb6b829cd9ddec30f22b0de66874be7710e465
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# Verbinden met [!DNL Looker]

Als u [!DNL Looker] wilt verbinden met [!DNL Query Service] op Adobe Experience Platform, volgt u de onderstaande stappen:

Nadat u zich hebt aangemeld bij [!DNL Looker], klikt u op **[!UICONTROL Admin]**, gevolgd door **[!UICONTROL Verbindingen]**.

![](../images/clients/looker/click-admin-connections.png)

Voor deze pagina, klik op **Nieuwe Verbinding**.

![](../images/clients/looker/click-new-connection.png)

Van hier, kunt u de details voor de Montages van de Verbinding invullen.

![](../images/clients/looker/new-connection.png)

- **Naam:** de naam van de verbinding.
- **Dialect:** Het dialect dat voor het SQL gegevensbestand wordt gebruikt. [!DNL Query Service] gebruik  **[!DNL PostgreSQL]**.
- **Gastheer en Haven:** het gastheereindpunt en zijn haven voor  [!DNL Query Service].
- **Database:** de database die wordt gebruikt.
- **Gebruikersnaam en wachtwoord:** de aanmeldingsgegevens die worden gebruikt. De gebruikersnaam heeft de notatie `ORG_ID@AdobeOrg`.

>[!NOTE]
>
>Voor meer informatie bij het vinden van uw gastheer en haven, gegevensbestandnaam, en login geloofsbrieven, bezoek de [geloofsbrieven pagina op Platform](https://platform.adobe.com/query/configuration). Om uw geloofsbrieven te vinden, login aan [!DNL Platform], klik **[!UICONTROL Vragen]**, dan klik **[!UICONTROL Referenties]**.

Nadat u de verbindingsgegevens hebt ingevoerd, klikt u op **[!UICONTROL Deze instellingen testen]** om te controleren of uw gegevens correct werken. Als dat het geval is, wordt hieronder een bericht weergegeven dat u verbinding kunt maken. Als uw verbinding inderdaad succesvol is, klik op **[!UICONTROL Add Verbinding]** om uw verbinding tot stand te brengen.

![](../images/clients/looker/click-test-connection.png)

## Volgende stappen

Nu u met [!DNL Query Service] hebt verbonden, kunt u [!DNL Looker] gebruiken om vragen te schrijven. Voor meer informatie over hoe te om vragen te schrijven en in werking te stellen, te lezen [lopende vraaggids](../best-practices/writing-queries.md).