---
keywords: Experience Platform;home;populaire onderwerpen;toegangsbeheer;adobe-beheerconsole
solution: Experience Platform
feature: Attribution AI
title: Toegangsbeheer voor kenmerken-AI
description: Dit document bevat informatie over op kenmerken gebaseerd toegangsbeheer voor Attribution AI.
exl-id: 3ed672bf-1fa6-4893-99e0-afc2b2179543
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# Toegangsbeheer in kenmerken-AI

De controle van de toegang voor Attributie AI wordt verstrekt door Adobe Experience Platform in [&#x200B; Adobe Admin Console &#x200B;](https://adminconsole.adobe.com/). Deze functionaliteit maakt gebruik van productprofielen in Admin Console, die gebruikers koppelen aan machtigingen en sandboxen.

Voor meer informatie over toegangsbeheer, zie het [&#x200B; overzicht van de toegangscontrole &#x200B;](../../../access-control/home.md).

## Toegangsbeheer op basis van kenmerken

>[!IMPORTANT]
>
>Toegangsbeheer op basis van kenmerken is momenteel alleen beschikbaar in een beperkte versie.

[&#x200B; op attributen-gebaseerde toegangscontrole &#x200B;](../../../access-control/abac/overview.md) is een vermogen van Adobe Experience Platform dat beheerders toelaat om toegang tot specifieke voorwerpen en/of mogelijkheden te controleren die op attributen worden gebaseerd. Kenmerken kunnen metagegevens zijn die aan een object worden toegevoegd, zoals een label dat aan een schemaveld of -segment wordt toegevoegd. Een beheerder bepaalt toegangsbeleid dat attributen omvat om de toestemmingen van de gebruikerstoegang te beheren.

Met deze functionaliteit kunt u XDM-schemavelden (Experience Data Model) labelen met labels die bereik voor organisatie of gegevensgebruik definiëren. Parallel hieraan kunnen beheerders de gebruikers- en rolbeheerinterface gebruiken om toegangsbeleid te definiëren rondom XDM-schemavelden en de toegang die gebruikers of groepen gebruikers (interne, externe of externe gebruikers) krijgen beter te beheren. Bovendien, op attribuut-gebaseerde toegangsbeheer staat beheerders toe om toegang tot specifieke segmenten te beheren.

Via op kenmerken gebaseerde toegangscontrole kunnen beheerders de toegang van gebruikers tot zowel gevoelige persoonlijke gegevens (SPD) als persoonlijk identificeerbare informatie (PII) in alle Experience Platform-workflows en -bronnen beheren. Beheerders kunnen gebruikersrollen definiëren die alleen toegang hebben tot specifieke velden en gegevens die overeenkomen met die velden.

Als gevolg van attribuut-gebaseerde toegangscontrole, zouden sommige gebieden en functionaliteiten toegang beperkt kunnen hebben en voor bepaalde de dienstmodellen van AttributionAI niet beschikbaar zijn. Voorbeelden zijn Identiteit, Score Definition en Klonen.

Bij de bovenkant van de de werkruimte van Attributie AI **inzichten pagina**, hebben de details die in sidebar tonen beperkte toegang.

![&#x200B; de werkruimte van AI van de Attributie met de beperkte benadrukte schemagebieden.](../images/user-guide/access-restricted.png)

Als u datasets met beperkte schema&#39;s op de **[!UICONTROL Create model workflow]** pagina selecteert, verschijnt een waarschuwingsteken naast de naam van de dataset met het bericht: [!UICONTROL Restricted information is excluded].

![&#x200B; de werkruimte van Attributie AI met de beperkte benadrukt datasetgebieden.](../images/user-guide/restricted-info-excluded.png)

Wanneer u een voorvertoning weergeeft van gegevenssets met een beperkt schema op de pagina **[!UICONTROL Create model workflow]** , verschijnt er een waarschuwing om u te laten weten dat [!UICONTROL Due to access restrictions, certain information isn't displayed in the dataset preview.]

![&#x200B; de werkruimte van AI van de Attributie met de resultaten van beperkte vooraf bekeken benadrukte schemagebieden.](../images/user-guide/restricted-dataset-preview.png)

Nadat u een model met beperkte informatie hebt gemaakt en de stap **[!UICONTROL Define goal]** hebt uitgevoerd, wordt bovenaan een waarschuwing weergegeven: [!UICONTROL Due to access restrictions, certain information isn't displayed in the configuration.]

![&#x200B; de werkruimte van AI van de Attributie met de beperkte gebieden van de benadrukte modelresultaten.](../images/user-guide/information-not-displayed-save-and-exit.png)

## Volgende stappen

Door deze gids te lezen, bent u geïntroduceerd aan de belangrijkste principes van toegangsbeheer in [!DNL Experience Platform]. U kunt nu aan de [&#x200B; gebruikershandleiding van de toegangscontrole &#x200B;](../overview.md) voor gedetailleerde stappen op blijven hoe gebruiken [!DNL Admin Console] om productprofielen tot stand te brengen en toestemmingen voor [!DNL Experience Platform] toe te wijzen.
