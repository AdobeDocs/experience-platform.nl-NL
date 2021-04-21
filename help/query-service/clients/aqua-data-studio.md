---
keywords: Experience Platform;huis;populaire onderwerpen;vraagdienst;de dienst van de Vraag;de Studio van Gegevens Aqua;de gegevensstudio van Aqua;verbind met de vraagdienst;
solution: Experience Platform
title: Connect Aqua Data Studio aan de Dienst van de Vraag
topic-legacy: connect
description: Dit document doorloopt de stappen voor het verbinden van de Studio van Gegevens Aqua met de Dienst van de Vraag van Adobe Experience Platform.
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 1%

---

# [!DNL Aqua Data Studio] verbinden met de Dienst van de Vraag

In dit document worden de stappen beschreven voor het verbinden van [!DNL Aqua Data Studio] met Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Deze gids veronderstelt u reeds toegang tot [!DNL Aqua Data Studio] hebt en vertrouwd met hoe te om zijn interface te navigeren. Meer informatie over [!DNL Aqua Data Studio] vindt u in de [officiële [!DNL Aqua Data Studio] documentatie](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1).

Nadat u [!DNL Aqua Data Studio] hebt geïnstalleerd, moet u de server eerst registreren. Selecteer **[!DNL Server]** in het hoofdmenu, gevolgd door **[!DNL Register Server]**.

![](../images/clients/aqua-data-studio/register-server.png)

Het dialoogvenster **[!DNL Register Server]** wordt weergegeven. Selecteer **[!DNL PostgreSQL]** in de lijst aan de linkerkant onder het tabblad **[!DNL General]**. Geef in het dialoogvenster dat wordt weergegeven de volgende gegevens op voor de serverinstellingen.

- **[!DNL Name]**: De naam van de verbinding.
- **[!DNL Login Name and Password]**: De aanmeldingsgegevens die worden gebruikt. De gebruikersnaam heeft de vorm van `ORG_ID@AdobeOrg`.
- **[!DNL Host and Port]**: Het gastheereindpunt en zijn haven voor  [!DNL Query Service]. U moet poort 80 gebruiken om verbinding te maken met [!DNL Query Service].
- **[!DNL Database]:** De database die wordt gebruikt.

>[!NOTE]
>
>Voor meer informatie bij het vinden van uw login geloofsbrieven, gastheer, haven, en gegevensbestandnaam, bezoek de [geloofsbrieven pagina op Platform](https://platform.adobe.com/query/configuration). Als u uw referenties wilt zoeken, meldt u zich aan bij [!DNL Platform] en selecteert u **[!UICONTROL Queries]**, gevolgd door **[!UICONTROL Credentials]**.

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

Selecteer het tabblad **[!DNL Driver]**. Stel de waarde onder **[!DNL Parameters]** in als `?sslmode=require`

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

Nadat u de verbindingsgegevens hebt ingevoerd, selecteert u **[!DNL Test Connection]** om ervoor te zorgen dat uw referenties correct werken. Als uw verbinding succesvol is, uitgezocht **[!DNL Save]** om uw server te registreren. De verbinding wordt na een geslaagde registratie op het dashboard weergegeven. Hierbij wordt bevestigd dat u nu verbinding kunt maken met de server en de schemaobjecten kunt bekijken.

## Volgende stappen

Nu u met [!DNL Query Service] hebt verbonden, kunt u **[!DNL Query Analyzer]** binnen [!DNL Aqua Data Studio] gebruiken om SQL verklaringen uit te voeren en uit te geven. Voor meer informatie over hoe te om vragen te schrijven en in werking te stellen, te lezen [lopende vraaggids](../best-practices/writing-queries.md).
