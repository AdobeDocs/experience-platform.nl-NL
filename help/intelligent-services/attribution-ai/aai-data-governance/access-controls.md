---
keywords: Experience Platform;thuis;populaire onderwerpen;toegangsbeheer;adobe admin console
solution: Experience Platform
feature: Attribution AI
title: Toegangsbeheer voor Attribution AI
description: Dit document verstrekt informatie over op attributen-gebaseerd toegangsbeheer voor Attribution AI.
source-git-commit: 2cce166592c4d4b7f9d62bc3385fb8ccdd74c958
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 1%

---


# Toegangsbeheer

Het toegangsbeheer voor Attribution AI wordt via Adobe Experience Platform in de [Adobe Admin Console](https://adminconsole.adobe.com/). Deze functionaliteit gebruikt productprofielen in Admin Console, die gebruikers met toestemmingen en zandbakken verbinden.

Voor meer informatie over toegangsbeheer, zie [toegangsbeheeroverzicht](../../access-control/home).

## Op kenmerken gebaseerd toegangsbeheer

>[!IMPORTANT]
>
>Toegangsbeheer op basis van kenmerken is momenteel alleen beschikbaar in een beperkte versie.

[Op kenmerken gebaseerd toegangsbeheer](../../../help/access-control/abac/overview.md) is een mogelijkheid van Adobe Experience Platform die beheerders in staat stelt de toegang tot specifieke objecten en/of mogelijkheden te beheren op basis van kenmerken. Kenmerken kunnen metagegevens zijn die aan een object worden toegevoegd, zoals een label dat aan een schemaveld of -segment wordt toegevoegd. Een beheerder bepaalt toegangsbeleid dat attributen omvat om de toestemmingen van de gebruikerstoegang te beheren.

Met deze functionaliteit kunt u XDM-schemavelden (Experience Data Model) labelen met labels die bereik voor organisatie of gegevensgebruik definiëren. Parallel hieraan kunnen beheerders de gebruikers- en rolbeheerinterface gebruiken om toegangsbeleid te definiëren rondom XDM-schemavelden en de toegang die gebruikers of groepen gebruikers (interne, externe of externe gebruikers) krijgen beter te beheren. Bovendien, op attribuut-gebaseerde toegangsbeheer staat beheerders toe om toegang tot specifieke segmenten te beheren.

Via attribuut-based toegangsbeheer, kunnen de beheerders gebruikers&#39; toegang tot zowel gevoelige persoonlijke gegevens (SPD) als persoonlijk identificeerbare informatie (PII) over alle werkschema&#39;s en middelen van het Platform controleren. Beheerders kunnen gebruikersrollen definiëren die alleen toegang hebben tot specifieke velden en gegevens die overeenkomen met die velden.

Wegens op attribuut-gebaseerde toegangsbeheer, zouden sommige gebieden en functionaliteiten toegang beperkt kunnen hebben en voor bepaalde de dienstmodellen van de Attribution AI niet beschikbaar zijn. Voorbeelden zijn Identiteit, Score Definition en Klonen.

Bovenaan in de werkruimte Attribution AI **pagina met inzichten** hebben de gegevens die in de zijbalk worden weergegeven beperkte toegang.

![De werkruimte van de Attribution AI met de beperkte schemagebieden benadrukt.](./images/user-guide/access-restricted.png)

Als u datasets met beperkte schema&#39;s op selecteert **[!UICONTROL Create model workflow]** pagina, verschijnt een waarschuwingsteken naast de naam van de dataset met het bericht: [!UICONTROL Restricted information is excluded].

![De werkruimte van de Attribution AI met de beperkte benadrukt datasetgebieden.](./images/user-guide/restricted-info-excluded.png)

Wanneer u datasets met beperkt schema op voorproef **[!UICONTROL Create model workflow]** pagina, lijkt een waarschuwing u te laten weten dat [!UICONTROL Due to access restrictions, certain information isn't displayed in the dataset preview.]

![De werkruimte van de Attribution AI met de resultaten van beperkte vooraf bekeken schemagebieden benadrukt.](./images/user-guide/restricted-dataset-preview.png)

Nadat u een model met beperkte informatie creeert en te werk gaat **[!UICONTROL Define goal]** stap, wordt een waarschuwing getoond bij de bovenkant: [!UICONTROL Due to access restrictions, certain information isn't displayed in the configuration.]

![De werkruimte Attribution AI met de beperkte velden van de modelresultaten gemarkeerd.](./images/user-guide/information-not-displayed-save-and-exit.png)

## Volgende stappen

Door deze gids te lezen, bent u geïntroduceerd aan de belangrijkste principes van toegangscontrole in [!DNL Experience Platform]. U kunt nu doorgaan naar het dialoogvenster [gebruikershandleiding voor toegangsbeheer](./ui/overview.md) voor gedetailleerde stappen over het gebruik van de [!DNL Admin Console] om productprofielen te maken en machtigingen toe te wijzen voor [!DNL Platform].
