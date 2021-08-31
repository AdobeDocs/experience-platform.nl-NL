---
keywords: Experience Platform;huis;populaire onderwerpen;de dienst van de Vraag;de vraagdienst;Leider;Leider;verbindt met de vraagdienst;
solution: Experience Platform
title: Verbinding maken met Zoekservice
topic-legacy: connect
description: Dit document doorloopt de stappen voor het verbinden van de Teller met de Dienst van de Vraag van Adobe Experience Platform.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: 910a38ccb556ec427584d9b522e29f6877d1c987
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# [!DNL Looker] verbinden met de Dienst van de Vraag

In dit document worden de stappen beschreven voor het verbinden van [!DNL Looker] met Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Deze gids veronderstelt u reeds toegang tot [!DNL Looker] hebt en vertrouwd met hoe te om zijn interface te navigeren. Meer informatie over [!DNL Looker] vindt u in de [officiële [!DNL Looker] documentatie](https://docs.looker.com/).

Nadat u zich hebt aangemeld bij [!DNL Looker], selecteert u **[!DNL Admin]**, gevolgd door **[!DNL Connections]**.

![](../images/clients/looker/click-admin-connections.png)

Selecteer **[!DNL New Connection]** op deze pagina.

![](../images/clients/looker/click-new-connection.png)

Vanaf hier kunt u de gegevens voor de verbindingsinstellingen invullen.

![](../images/clients/looker/new-connection.png)

- **[!DNL Name]:** De naam van de verbinding.
- **[!DNL Dialect]:** Het dialect dat voor het SQL gegevensbestand wordt gebruikt. [!DNL Query Service] gebruik  **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** Het gastheereindpunt en zijn haven voor  [!DNL Query Service].
- **[!DNL Database]:** De database die wordt gebruikt.
- **[!DNL Username and Password]:** De aanmeldingsgegevens die worden gebruikt. De gebruikersnaam heeft de notatie `ORG_ID@AdobeOrg`.

>[!NOTE]
>
>Lees voor meer informatie over het zoeken naar uw host en poort, databasenaam en aanmeldingsgegevens de [aanmeldingsgids](../ui/credentials.md). Als u uw referenties wilt zoeken, meldt u zich aan bij [!DNL Platform] en selecteert u **[!UICONTROL Queries]**, gevolgd door **[!UICONTROL Credentials]**.

Nadat u de verbindingsgegevens hebt ingevoerd, selecteert u **[!DNL Test These Settings]** om ervoor te zorgen dat uw referenties correct werken. Als dat het geval is, wordt hieronder een bericht weergegeven dat u verbinding kunt maken. Als uw verbinding inderdaad succesvol is, uitgezocht **[!DNL Add Connection]** om uw verbinding tot stand te brengen.

![](../images/clients/looker/click-test-connection.png)

## Volgende stappen

Nu u met [!DNL Query Service] hebt verbonden, kunt u [!DNL Looker] gebruiken om vragen te schrijven. Voor meer informatie over hoe te om vragen te schrijven en in werking te stellen, te lezen [lopende vraaggids](../best-practices/writing-queries.md).
