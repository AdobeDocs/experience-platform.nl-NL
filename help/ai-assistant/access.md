---
title: Toegang tot AI Assistant (verouderd) in Experience Platform
description: Leer hoe u tot AI Medewerker in de UI van Experience Cloud kunt toegang hebben.
exl-id: c4cdff25-512c-4b4c-be91-ad9360067a0a
source-git-commit: daaf3ff0218b73a9fd827ab2ef090d8046cef3bb
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 0%

---

# Toegang tot AI Assistant (verouderd) in Experience Platform

>[!IMPORTANT]
>
>Dit document is van toepassing op AI Assistant (verouderd). Voor informatie over AI Medewerker (volgende-Gen), lees de [ AI HulpUI gids ](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/ai-assistant/ai-assistant-ui) in [ AI in Experience Cloud ](https://experienceleague.adobe.com/nl/docs/experience-cloud-ai/experience-cloud-ai/home) documentatie.

Raadpleeg de volgende tabel voor een vergelijking van AI Assistant (Legacy) en AI Assistant (Next-Gen):

| Functiegebied | AI Assistant (verouderd) | AI-assistent (Next-Gen) |
| --- | --- | --- |
| Gebruikerservaring | AI Assistant (verouderd) is alleen beschikbaar in een panel voor rechtse spoorwegsystemen. | AI Assistant (Next-Gen) is zowel beschikbaar in het rechterdeelvenster als in een indrukwekkende ervaring op volledig scherm. |
| Toepassingsgebied van de mogelijkheden | U kunt AI Assistant (Verouderd) gebruiken voor zowel productkennis als operationele inzichten. | U kunt de Medewerker van AI (Next-Gen) voor productkennis, operationele inzichten, evenals geavanceerde agentische vaardigheden en multi-step taakuitvoering gebruiken. |
| Platformarchitectuur | AI Assistant (Verouderd) is niet op de Agent Orchestrator-stapel gebaseerd. | De Medewerker van AI (Volgende-Gen) wordt aangedreven door [ Adobe Experience Platform Agent Orchestrator ](https://experienceleague.adobe.com/nl/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator), toelatend rekbaarheid en geavanceerde coördinatie over mogelijkheden. |
| Toepassingsdekking | AI Assistant (Legacy) is een toepassingsspecifieke implementatie. | U kunt AI Assistant (Next-Gen) gebruiken voor een uniforme AI Assistant-ervaring in alle Adobe Experience Cloud-toepassingen. |
| Toegangsmodel en machtigingsmodel | Toepassingsbereik toegangsmodel uitgelijnd op individuele productgrenzen. | Alle gebruikers krijgen toegang tot AI Assistant (Next-Gen) en bijbehorende Experience Platform-agents. **Nota**: <ul><li>**Adobe Experience Manager**: Uw beheerder moet u de toestemming verlenen om tot Medewerker (Volgende-Gen) door [ Adobe Admin Console ](https://helpx.adobe.com/nl/enterprise/using/admin-console.html) toegang te hebben.</li><li>**Customer Journey Analytics**: Uw beheerder moet u de toestemming verlenen om tot AI Medewerker door [ het Toegangsbeheer van Customer Journey Analytics ](https://experienceleague.adobe.com/en/docs/analytics-platform/using/technotes/access-control?lang=en) toegang te hebben. Hierdoor kunt u vragen stellen over productkennis en gegevensinzichten. |

In Adobe Experience Cloud hebt u toegang tot AI Assistant (verouderd) voor verschillende toepassingen.

>[!NOTE]
>
>Als u een pop-upbericht ontvangt in de gebruikersinterface voor machtigingen waarin wordt gemeld dat uw organisatie eerst met aanvullende wettelijke voorwaarden moet instemmen om toegang te krijgen tot AI Assistant (Legacy), neemt u contact op met uw Adobe-accountteam voor instructies over deze voorwaarden.

## Aan de slag {#get-started}

U moet twee stappen uitvoeren die aan de voorwaarde voldoen voordat u toegang krijgt tot AI Assistant (verouderd).

1. Uw organisatie moet eerst instemmen met juridische voorwaarden. Neem voor meer informatie contact op met uw Adobe-accountteam.
2. Uw beheerders moeten u voldoende machtigingen verlenen om toegang te krijgen tot AI Assistant (verouderd).

Als u geen van deze twee vereiste stappen hebt voltooid, worden de volgende berichten weergegeven wanneer u het chatpictogram AI Assistant (Legacy) in de gebruikersinterface van Experience Platform selecteert.

>[!BEGINTABS]

>[!TAB  Uw organisatie kan geen Medewerker AI (Verouderd) gebruiken ]

Het volgende bericht wordt weergegeven als u een organisatie gebruikt die wettelijk niet gemachtigd is om AI Assistant (Legacy) te gebruiken. In dit scenario moet u contact opnemen met uw Adobe-accountteam om de toegang te regelen.

![ het pop-up bericht dat op Experience Platform UI verschijnt als de organisatie geen Medewerker AI (Verouderd) kan gebruiken.](./images/access/modal-one.png)

>[!TAB  u hebt niet de juiste toestemmingen ]

Als uw organisatie wettelijk gemachtigd is om AI Assistant (Legacy) te gebruiken en u nog steeds geen toegang hebt tot de functie, wordt het volgende bericht weergegeven op de gebruikersinterface van Experience Platform. Dit scenario betekent dat u niet de voldoende toestemmingen hebt om tot de eigenschap toegang te hebben en u moet uw beheerders contacteren om toestemmingen op te lossen.

![ het pop-up bericht dat op Experience Platform UI verschijnt als u niet de noodzakelijke toestemmingen voor Medewerker AI (Verouderd) hebt.](./images/access/modal-two.png)

>[!ENDTABS]

## Toegang tot AI Assistant (verouderd) {#get-access-to-ai-assistant}

Voor de toegang tot AI Assistant (Legacy) gelden de volgende parameters:

* **toegang tot de toepassing:** u kunt tot Medewerker AI (Verouderd) in Adobe Experience Platform, Adobe Real-Time CDP, Adobe Journey Optimizer, en [ Customer Journey Analytics ](https://experienceleague.adobe.com/en/docs/analytics-platform/using/ai-assistant) toegang hebben.
<!-- * **Contractual access:** Your company must agree to certain [!DNL GenAI]-related legal terms before your organization can use AI Assistant (Legacy). Contact your organization's administrator or your Adobe Account Team if you are not able to access AI Assistant (Legacy).  -->
* **Toestemmingen:** gebruik [ Toestemmingen UI ](../access-control/abac/ui/permissions.md) om toegang tot AI Medewerker (Verouderd) in uw organisatie te verlenen of te herroepen. Om AI Medewerker (Verouderd) te gebruiken, moet een bepaalde gebruiker tot een rol behoren die met **wordt voorzien toelaat AI Medewerker** en **de Operationele toestemmingen van Inzichten van de Mening**.
   * Als beheerder, kunt u **toevoegen toelaat AI Medewerker** aan een bepaalde rol en voegt een gebruiker aan die rol toe, om hen toe te staan om tot AI Medewerker (Verouderd) in uw organisatie toegang te hebben. **Nota**: Deze toestemming staat de genoemde gebruiker toe om tot AI Medewerker (Verouderd) toegang te hebben, verleent het hen geen administratieve capaciteit om anderen dan toegang tot AI Medewerker (Verouderd) te geven.
   * Als beheerder, kunt u de **Operationele Inzichten van de Mening** aan een bepaalde rol toevoegen en een gebruiker toevoegen aan die rol, om hen toe te staan om de operationele mogelijkheden van de Inzichten van AI van de Medewerker (Verouderd) te gebruiken.

Gebruik de [ toestemmingen UI ](../access-control/abac/ui/roles.md) om toestemmingen te verlenen om AI Medewerker (Verouderd) in Experience Platform en Journey Optimizer te gebruiken. Voor informatie over hoe u toegang krijgt tot AI Assistant (Legacy) in Customer Journey Analytics. Lees de documentatie in [ Customer Journey Analytics ](https://experienceleague.adobe.com/en/docs/analytics-platform/using/ai-assistant).

![ de toestemmingenpagina UI met Enable AI Medewerker (Verouderd) en de Toestemmingen van de Inzichten van de Mening die in een bepaalde rol worden omvat.](./images/access/access-permissions.png)

Zodra u de noodzakelijke toestemmingen hebt, kunt u tot Medewerker (Verouderd) toegang hebben AI door de ![ Medewerker AI (Verouderd) te selecteren ](/help/images/icons/ai-assistant.png) pictogram op de hoogste kopbal van de toepassing die u gebruikt.

![ AI Medewerker (Verouderd) met eerste gebruikerservaring.](./images/access/access-home.png)

Bekijk de volgende video om te leren hoe u toegang tot AI Assistant (verouderd) voor uw organisaties en gebruikers kunt configureren.

>[!VIDEO](https://video.tv.adobe.com/v/3436470/?learn=on)

## Volgende stappen

Zodra u volledige toegang tot AI Medewerker (Verouderd) hebt, kunt u aan het gebruiken van de eigenschap tijdens uw werkschema&#39;s te werk gaan, de [ AI Medewerker (Verouderd) UI gids ](./ui-guide.md) voor meer informatie lezen.
