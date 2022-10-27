---
keywords: Experience Platform;huis;populaire onderwerpen;de dienst van de Vraag;de vraagdienst;Leider;Leider;verbindt met de vraagdienst;
solution: Experience Platform
title: Verbinding maken met Zoekservice
topic-legacy: connect
description: Dit document doorloopt de stappen voor het verbinden van de Teller met de Dienst van de Vraag van Adobe Experience Platform.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: 75e97efcb68439f1b837af93b62c96f43e5d7a31
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# Verbinden [!DNL Looker] aan de Dienst van de Vraag

In dit document worden de stappen beschreven voor het verbinden [!DNL Looker] met Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Deze handleiding gaat ervan uit dat u al toegang hebt tot [!DNL Looker] en zijn vertrouwd met hoe te om zijn interface te navigeren. Meer informatie over [!DNL Looker] kunt u vinden in het dialoogvenster [ambtenaar [!DNL Looker] documentatie](https://docs.looker.com/).

Nadat u zich hebt aangemeld [!DNL Looker], selecteert u **[!DNL Admin]**, gevolgd door **[!DNL Connections]**.

![De [!DNL Looker] dashboard met verbindingen die zijn gemarkeerd in het vervolgkeuzemenu Admin.](../images/clients/looker/click-admin-connections.png)

Selecteer op deze pagina **[!DNL New Connection]**.

![De werkruimte Verbindingen met Nieuwe gemarkeerde Verbinding.](../images/clients/looker/click-new-connection.png)

Vanaf hier kunt u de gegevens voor de verbindingsinstellingen invullen.

![De de montagespagina van Verbindingen voor een Nieuwe Verbinding.](../images/clients/looker/new-connection.png)

- **[!DNL Name]:** De naam van de verbinding.
- **[!DNL Dialect]:** Het dialect dat voor het SQL gegevensbestand wordt gebruikt. [!DNL Query Service] gebruik **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** Het gastheereindpunt en zijn haven voor [!DNL Query Service].
- **[!DNL Database]:** De database die wordt gebruikt.
- **[!DNL Username and Password]:** De aanmeldingsgegevens die worden gebruikt. De gebruikersnaam heeft de vorm van `ORG_ID@AdobeOrg`.
- **SSL**: Schakel SSL in om een veilige verbinding via het netwerk te garanderen.

>[!IMPORTANT]
>
>Zie de [[!DNL Query Service] SSL-documentatie](./ssl-modes.md) voor meer informatie over SSL-ondersteuning voor verbindingen van derden met Adobe Experience Platform Query Service en over het maken van verbindingen met deze service `verify-full` SSL-modus.

Voor meer informatie over het vinden van uw gastheer en haven, gegevensbestandnaam, en login geloofsbrieven, gelieve te lezen [aanmeldingsgids](../ui/credentials.md). Meld u aan om uw referenties te zoeken [!DNL Platform]selecteert u vervolgens **[!UICONTROL Queries]**, gevolgd door **[!UICONTROL Credentials]**.

Selecteer **[!DNL Test These Settings]** om ervoor te zorgen dat uw gegevens correct werken. Als dat het geval is, wordt hieronder een bericht weergegeven dat u verbinding kunt maken. Als uw verbinding inderdaad is gelukt, selecteert u **[!DNL Add Connection]** om uw verbinding te maken.

![De de montagespagina van Verbindingen voor Nieuwe Verbinding met Test deze benadrukte montages.](../images/clients/looker/click-test-connection.png)

## Volgende stappen

Nu hebt u verbinding met [!DNL Query Service]kunt u [!DNL Looker] om query&#39;s te schrijven. Lees voor meer informatie over het schrijven en uitvoeren van query&#39;s de [gids voor uitvoeren van query&#39;s](../best-practices/writing-queries.md).
