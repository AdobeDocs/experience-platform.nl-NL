---
keywords: Experience Platform;gebruikershandleiding;klantenservice;populaire onderwerpen;toegangsbeheer;model maken;
solution: Experience Platform
feature: Customer AI
title: Toegangsbeheer voor AI van de Klant
description: Dit document bevat informatie over op kenmerken gebaseerde toegangscontrole voor AI van de Klant.
exl-id: 02e3b6a4-304a-4ac4-b07c-010531101feb
source-git-commit: f28558d5939607cabf449cbc03b7e0f5406f6326
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# Toegangsbeheer op basis van kenmerken in AI van de Klant

>[!IMPORTANT]
>
>Toegangsbeheer op basis van kenmerken is momenteel alleen beschikbaar in een beperkte versie.

[ op attributen-gebaseerde toegangscontrole ](../../../access-control/abac/overview.md) is een vermogen van Adobe Experience Platform dat beheerders toelaat om toegang tot specifieke voorwerpen en/of mogelijkheden te controleren die op attributen worden gebaseerd. Kenmerken kunnen metagegevens zijn die aan een object worden toegevoegd, zoals een label dat aan een schemaveld of -segment wordt toegevoegd. Een beheerder bepaalt toegangsbeleid dat attributen omvat om de toestemmingen van de gebruikerstoegang te beheren.

Met deze functionaliteit kunt u XDM-schemavelden (Experience Data Model) labelen met labels die bereik voor organisatie of gegevensgebruik definiëren. Parallel hieraan kunnen beheerders de gebruikers- en rolbeheerinterface gebruiken om toegangsbeleid te definiëren rondom XDM-schemavelden en de toegang die gebruikers of groepen gebruikers (interne, externe of externe gebruikers) krijgen beter te beheren. Bovendien, op attribuut-gebaseerde toegangsbeheer staat beheerders toe om toegang tot specifieke segmenten te beheren.

Via attribuut-gebaseerde toegangscontrole, kunnen de beheerders van uw organisatie gebruikers&#39; toegang tot zowel gevoelige persoonlijke gegevens (SPD) als persoonlijk identificeerbare informatie (PII) over alle werkschema&#39;s en middelen van het Platform controleren. Beheerders kunnen gebruikersrollen definiëren die alleen toegang hebben tot specifieke velden en gegevens die overeenkomen met die velden.

Als gevolg van attribuut-gebaseerde toegangscontrole, zouden sommige gebieden en functionaliteiten toegang beperkt hebben en voor bepaalde de dienstmodellen van de AI van de Klant onbeschikbaar zijn. Voorbeelden zijn Identiteit, Score Definition en Klonen.

![ de werkruimte van de Klant AI met de beperkte gebieden van de benadrukte resultaten van het de dienstmodel.](../images/user-guide/unavailable-functionalities.png)

Bij de bovenkant van de de werkruimte van de Klant AI **inzichten pagina**, merk op dat de details in sidebar, de scoredefinitie, de identiteit, en profielattributen allen &quot;Toegang beperkt tonen.&quot;

![ de werkruimte van de Klant AI met de beperkte gebieden van het benadrukte schema.](../images/user-guide/access-restricted.png)

Wanneer u een voorvertoning weergeeft van gegevenssets met een beperkt schema op de pagina **[!UICONTROL Create model workflow]** , verschijnt er een waarschuwing om u te laten weten dat [!UICONTROL Due to access restrictions, certain information isn't displayed in the dataset preview.]

![ de werkruimte van de Klant AI met de beperkte gebieden van de voorproefdatasets met beperkte die schemaresultaten worden benadrukt.](../images/user-guide/restricted-dataset-preview-save-and-exit-cai.png)

Nadat u een model met beperkte informatie hebt gemaakt en de stap **[!UICONTROL Define goal]** hebt uitgevoerd, wordt boven aan het model een waarschuwing weergegeven: [!UICONTROL Due to access restrictions, certain information isn't displayed in the configuration.]

![ de werkruimte van de Klant AI met de beperkte gebieden van de benadrukte resultaten van het de dienstmodel.](../images/user-guide/information-not-displayed-save-and-exit.png)

Wanneer het gebruiken van toegangsbeheer, verlenen de **Klant AI van de Mening** en **AI van de Klant** voorrechten toegang tot verschillende functionaliteiten van Klant AI. De **beheert AI van de Klant** toestemming laat u **** creëren, **update**, **schrapt**, **toelaten**, of **onbruikbaar maken** een model terwijl **Klant AI van de Mening** u het laat lezen of bekijken. **creeer**, **update** en **schrapt** acties worden geregistreerd door controlelogboeken.

Zie de documentatie om [ te leren toewijzend toestemmingen voor toegangscontrole ](../../../access-control/home.md) of hoe te [ controlelogboeken gebruiken om toegang en activiteit ](../../../landing/governance-privacy-security/audit-logs/overview.md) te controleren.

## Volgende stappen

Door deze gids te lezen, bent u geïntroduceerd aan de belangrijkste principes van toegangsbeheer in [!DNL Experience Platform]. U kunt nu aan de [ gebruikershandleiding van de toegangscontrole ](../overview.md) voor gedetailleerde stappen op blijven hoe gebruiken [!DNL Admin Console] om productprofielen tot stand te brengen en toestemmingen voor [!DNL Platform] toe te wijzen.
