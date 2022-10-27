---
keywords: Experience Platform;thuis;populaire onderwerpen;tableau;Tableau;queryservice;Query-service;Verbinden met queryservice;
solution: Experience Platform
title: Connect Tableau naar Query Service
topic-legacy: connect
description: Dit document doorloopt de stappen voor het verbinden van Tableau met de Dienst van de Vraag van Adobe Experience Platform.
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: 9c450f340706040593dfea5292702c4b00dd9852
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---

# Verbinden [!DNL Tableau] aan de Dienst van de Vraag

In dit document worden de stappen beschreven voor het verbinden [!DNL Tableau] met Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Deze handleiding gaat ervan uit dat u al toegang hebt tot [!DNL Tableau] en zijn vertrouwd met hoe te om zijn interface te navigeren. Meer informatie over [!DNL Tableau] kunt u vinden in het dialoogvenster [ambtenaar [!DNL Tableau] documentatie](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

Verbinding maken [!DNL Tableau] tot [!DNL Query Service], open [!DNL Tableau]en in de **[!DNL To a Server]** sectie selecteren **[!DNL More]** gevolgd door **[!DNL PostgreSQL]**

![De [!DNL Tableau] dashboard met Meer en [!DNL PostgreSQL] gemarkeerd.](../images/clients/tableau/open-connection.png)

U kunt nu waarden invoeren om verbinding te maken met Adobe Experience Platform. Voor meer informatie over het vinden van uw gegevensbestandnaam, gastheer, haven, en login geloofsbrieven, gelieve te lezen [aanmeldingsgids](../ui/credentials.md). Meld u aan om uw referenties te zoeken [!DNL Platform]selecteert u vervolgens **[!UICONTROL Queries]**, gevolgd door **[!UICONTROL Credentials]**.

Controleer of u de **[!UICONTROL Require SSL]** voordat u probeert verbinding te maken.

>[!IMPORTANT]
>
>Zie de [[!DNL Query Service] SSL-documentatie](./ssl-modes.md) voor meer informatie over SSL-ondersteuning voor verbindingen van derden met Adobe Experience Platform Query Service en over het maken van verbindingen met deze service `verify-full` SSL-modus.

![De [!DNL PostgreSQL] verbindingsdialoogvenster met voltooide verbindingsgegevens.](../images/clients/tableau/sign-in.png)

>[!IMPORTANT]
>
>De genestelde gegevensstructuren in derdehulpmiddelen van BI kunnen worden afgevlakt om hun bruikbaarheid te verbeteren en de vereiste werkbelasting te verminderen om gegevens terug te winnen, te analyseren, om te zetten en te melden. Zie de documentatie op de[`FLATTEN` functie](../best-practices/flatten-nested-data.md) voor instructies over het activeren van deze instelling wanneer u verbinding maakt met een database.

Nadat u al uw referenties hebt ingevuld, selecteert u **[!DNL Sign In]** om door te gaan.

U hebt nu verbinding gemaakt met Adobe Experience Platform en er wordt een lijst met uw tabellen weergegeven aan de zijkant.

![Een nieuwe [!DNL Tableau] dashboard met de lijsten van de Dienst van de Vraag die in het linkerpaneel worden benadrukt.](../images/clients/tableau/connected.png)

## Volgende stappen

Nu hebt u verbinding met [!DNL Query Service]kunt u [!DNL Tableau] om query&#39;s te schrijven. Lees voor meer informatie over het schrijven en uitvoeren van query&#39;s de handleiding op [uitvoeren, query&#39;s](../best-practices/writing-queries.md).
