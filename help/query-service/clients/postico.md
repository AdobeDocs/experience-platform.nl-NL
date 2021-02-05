---
keywords: Experience Platform;huis;populaire onderwerpen;de dienst van de vraag;de vraagdienst;postico;Postico;verbind met de vraagdienst;
solution: Experience Platform
title: Connect Postico aan de Dienst van de Vraag
topic: connect
description: Dit document bevat de koppeling voor de installatie van de back-upclient Postico for Adobe Experience Platform Query Service.
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# [!DNL Postico] verbinden met de Dienst van de Vraag (MAC)

In dit document worden de stappen beschreven voor het verbinden van [!DNL Postico] met Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Deze gids veronderstelt u reeds toegang tot [!DNL Postico] hebt en vertrouwd met hoe te om zijn interface te navigeren. Meer informatie over [!DNL Postico] vindt u in de [officiële [!DNL Postico] documentatie](https://eggerapps.at/postico/docs).
> 
> Daarnaast is [!DNL Postico] **alleen** beschikbaar op MacOS-apparaten.

Als u [!DNL Postico] wilt verbinden met Query Service, opent u [!DNL Postico] en selecteert u **[!DNL New Favorite]**.

![](../images/clients/postico/open-postico.png)

U kunt nu waarden invoeren om verbinding te maken met Adobe Experience Platform.

Voor meer informatie bij het vinden van uw gegevensbestandnaam, gastheer, haven, en login geloofsbrieven, bezoek de [geloofsbrieven pagina op Platform](https://platform.adobe.com/query/configuration). Als u uw referenties wilt zoeken, meldt u zich aan bij [!DNL Platform] en selecteert u **[!UICONTROL Vragen]**, gevolgd door **[!UICONTROL Referenties]**.

Na het opnemen van uw geloofsbrieven, selecteer **[!DNL Connect]** om met de Dienst van de Vraag te verbinden.

![](../images/clients/postico/authentication-details.png)

Na het verbinden met Platform, zult u een lijst van alle relaties kunnen zien die eerder met de Dienst van de Vraag worden gemaakt.

![](../images/clients/postico/show-queries.png)

## SQL-instructies maken

Als u een nieuwe SQL-query wilt maken, selecteert en opent u &quot;SQL-query&quot;.

![](../images/clients/postico/create-query.png)

Er wordt een vak weergegeven en van hieruit kunt u de query typen die u wilt uitvoeren. Wanneer gebeëindigd, selecteer **[!DNL Execute Statement]** om de vraag in werking te stellen.

![](../images/clients/postico/run-statement.png)

Er wordt een tabel weergegeven met de resultaten van de voltooide query.

![](../images/clients/postico/query-results.png)

## Volgende stappen

Nu u met [!DNL Query Service] hebt verbonden, kunt u [!DNL Postico] gebruiken om vragen te schrijven. Voor meer informatie over hoe te om vragen te schrijven en in werking te stellen, te lezen [lopende vraaggids](../best-practices/writing-queries.md).