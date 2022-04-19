---
keywords: Experience Platform;thuis;populaire onderwerpen;tableau;Tableau;queryservice;Query-service;Verbinden met queryservice;
solution: Experience Platform
title: Connect Tableau naar Query Service
topic-legacy: connect
description: Dit document doorloopt de stappen voor het verbinden van Tableau met de Dienst van de Vraag van Adobe Experience Platform.
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: ad3e1b0de6dd3b82cc82f0dc3d0f36b12cd3899e
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# Verbinden [!DNL Tableau] aan de Dienst van de Vraag

In dit document worden de stappen beschreven voor het verbinden van Tableau met Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Deze handleiding gaat ervan uit dat u al toegang hebt tot [!DNL Tableau] en zijn vertrouwd met hoe te om zijn interface te navigeren. Meer informatie over [!DNL Tableau] kunt u vinden in het dialoogvenster [ambtenaar [!DNL Tableau] documentatie](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

Verbinding maken [!DNL Tableau] tot [!DNL Query Service], open [!DNL Tableau]en in de **[!DNL To a Server]** sectie selecteren **[!DNL More]** gevolgd door **[!DNL PostgreSQL]**

![](../images/clients/tableau/open-connection.png)

U kunt nu waarden invoeren om verbinding te maken met Adobe Experience Platform. Voor meer informatie over het vinden van uw gegevensbestandnaam, gastheer, haven, en login geloofsbrieven, gelieve te lezen [aanmeldingsgids](../ui/credentials.md). Meld u aan om uw referenties te zoeken [!DNL Platform]selecteert u vervolgens **[!UICONTROL Queries]**, gevolgd door **[!UICONTROL Credentials]**.

Controleer of u de **[!UICONTROL SSL Required]** voordat u probeert verbinding te maken.

>[!IMPORTANT]
>
>Zie de [[!DNL Query Service] SSL-documentatie](./ssl-modes.md) voor meer informatie over SSL-ondersteuning voor verbindingen van derden met Adobe Experience Platform Query Service en over het maken van verbindingen met deze service `verify-full` SSL-modus.

Nadat u al uw referenties hebt ingevuld, selecteert u **[!DNL Sign In]** om door te gaan.

![](../images/clients/tableau/sign-in.png)

U hebt nu verbinding gemaakt met Adobe Experience Platform en er wordt een lijst met uw tabellen weergegeven aan de zijkant.

![](../images/clients/tableau/connected.png)

## Volgende stappen

Nu hebt u verbinding met [!DNL Query Service]kunt u [!DNL Tableau] om query&#39;s te schrijven. Lees voor meer informatie over het schrijven en uitvoeren van query&#39;s de handleiding op [uitvoeren, query&#39;s](../best-practices/writing-queries.md).
