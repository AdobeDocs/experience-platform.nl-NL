---
title: AI-assistent openen in Experience Platform
description: Leer hoe u tot AI Medewerker in de UI van Experience Cloud kunt toegang hebben.
exl-id: c4cdff25-512c-4b4c-be91-ad9360067a0a
source-git-commit: 659e873f9bccdbc0e52a1943a924dc70d3170e96
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 0%

---

# AI-assistent openen in Experience Platform

In Adobe Experience Cloud hebt u toegang tot AI Assistant voor verschillende toepassingen.

>[!IMPORTANT]
>
>Als u een pop-upbericht ontvangt in de gebruikersinterface voor machtigingen die u laat weten dat uw organisatie eerst akkoord moet gaan met aanvullende juridische voorwaarden om toegang te krijgen tot AI Assistant, neemt u contact op met uw Adobe-accountteam voor instructies over deze voorwaarden.

## Aan de slag {#get-started}

U moet twee stappen uitvoeren die aan de voorwaarde voldoen voordat u toegang krijgt tot de AI-assistent.

1. Uw organisatie moet eerst instemmen met juridische voorwaarden. Neem voor meer informatie contact op met uw Adobe-accountteam.
2. Uw beheerders moeten u voldoende toestemmingen verlenen om tot AI Medewerker toegang te hebben.

Als u geen van deze twee stappen hebt voltooid die aan de voorwaarde voldoen, worden de volgende berichten weergegeven wanneer u het chatpictogram AI Assistant in de gebruikersinterface van Experience Platform selecteert.

>[!BEGINTABS]

>[!TAB Uw organisatie kan geen Medewerker van AI  gebruiken]

Het volgende bericht wordt weergegeven als u een organisatie gebruikt die wettelijk niet gemachtigd is om AI Assistant te gebruiken. In dit scenario moet u contact opnemen met uw Adobe-accountteam om de toegang te regelen.

![&#x200B; het pop-up bericht dat op Experience Platform UI verschijnt als de organisatie geen Medewerker AI kan gebruiken.](./images/access/modal-one.png)

>[!TAB  u hebt niet de juiste toestemmingen ]

Als uw organisatie wettelijk gemachtigd is om AI Assistant te gebruiken en u nog steeds geen toegang hebt tot de functie, wordt het volgende bericht weergegeven op de gebruikersinterface van Experience Platform. Dit scenario betekent dat u niet de voldoende toestemmingen hebt om tot de eigenschap toegang te hebben en u moet uw beheerders contacteren om toestemmingen op te lossen.

![&#x200B; het pop-up bericht dat op Experience Platform UI verschijnt als u niet de noodzakelijke toestemmingen voor AI Medewerker hebt.](./images/access/modal-two.png)

>[!ENDTABS]

## Toegang tot AI Assistant verkrijgen {#get-access-to-ai-assistant}

Voor de toegang tot AI Assistant gelden de volgende parameters:

* **toegang tot de toepassing:** u kunt tot AI Medewerker in Adobe Experience Platform, Adobe Real-Time CDP, Adobe Journey Optimizer, en [&#x200B; Customer Journey Analytics &#x200B;](https://experienceleague.adobe.com/en/docs/analytics-platform/using/ai-assistant) toegang hebben.
<!-- * **Contractual access:** Your company must agree to certain [!DNL GenAI]-related legal terms before your organization can use AI Assistant. Contact your organization's administrator or your Adobe Account Team if you are not able to access AI Assistant.  -->
* **Toestemmingen:** gebruik [&#x200B; Toestemmingen UI &#x200B;](../access-control/abac/ui/permissions.md) om toegang tot AI Medewerker in uw organisatie te verlenen of te herroepen. Om AI Medewerker te gebruiken, moet een bepaalde gebruiker tot een rol behoren die met **wordt voorzien toelaat AI Medewerker** en **de Operationele toestemmingen van de Mening**.
   * Als beheerder, kunt u **toevoegen toelaat AI Medewerker** aan een bepaalde rol en voegt een gebruiker aan die rol toe, om hen toe te staan om tot AI Medewerker in uw organisatie toegang te hebben. **Nota**: Deze toestemming staat de genoemde gebruiker toe om tot AI Medewerker toegang te hebben, verleent het hen geen administratieve capaciteit om anderen dan toegang tot AI Medewerker te geven.
   * Als beheerder, kunt u de **Operationele Inzichten van de Mening** aan een bepaalde rol toevoegen en een gebruiker toevoegen aan die rol, om hen toe te staan om de operationele mogelijkheden van de Inzichten van AI Medewerker te gebruiken.

Gebruik de [&#x200B; toestemmingen UI &#x200B;](../access-control/abac/ui/roles.md) om toestemmingen te verlenen om AI Medewerker in Experience Platform en Journey Optimizer te gebruiken. Voor informatie over hoe u toegang kunt krijgen tot AI Assistant in Customer Journey Analytics. Lees de documentatie in [&#x200B; Customer Journey Analytics &#x200B;](https://experienceleague.adobe.com/en/docs/analytics-platform/using/ai-assistant).

![&#x200B; de pagina van toestemmingen UI met Enable AI Medewerker en de Toestemmingen van de Inzicht van de Mening Operationele inbegrepen in een bepaalde rol.](./images/access/access-permissions.png)

Zodra u de vereiste toestemmingen hebt, kunt u tot AI Medewerker toegang hebben door het AI Hulppictogram op de hoogste kopbal van de toepassing te selecteren die u gebruikt.

![&#x200B; AI Medewerker met eerste gebruikerservaring.](./images/access/access-home.png)

Bekijk de volgende video om te leren hoe u toegang tot AI Assistant voor uw organisaties en gebruikers kunt configureren.

>[!VIDEO](https://video.tv.adobe.com/v/3436470/?learn=on)

## Volgende stappen

Zodra u volledige toegang tot AI Medewerker hebt, kunt u aan het gebruiken van de eigenschap tijdens uw werkschema&#39;s te werk gaan, de [&#x200B; AI Hulp UI gids &#x200B;](./ui-guide.md) voor meer informatie lezen.
