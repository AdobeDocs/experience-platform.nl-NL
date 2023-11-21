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

[Toegangsbeheer op basis van kenmerken](../../../access-control/abac/overview.md) is een mogelijkheid van Adobe Experience Platform die beheerders in staat stelt de toegang tot specifieke objecten en/of mogelijkheden te beheren op basis van kenmerken. Kenmerken kunnen metagegevens zijn die aan een object worden toegevoegd, zoals een label dat aan een schemaveld of -segment wordt toegevoegd. Een beheerder bepaalt toegangsbeleid dat attributen omvat om de toestemmingen van de gebruikerstoegang te beheren.

Met deze functionaliteit kunt u XDM-schemavelden (Experience Data Model) labelen met labels die bereik voor organisatie of gegevensgebruik definiëren. Parallel hieraan kunnen beheerders de gebruikers- en rolbeheerinterface gebruiken om toegangsbeleid te definiëren rondom XDM-schemavelden en de toegang die gebruikers of groepen gebruikers (interne, externe of externe gebruikers) krijgen beter te beheren. Bovendien, op attribuut-gebaseerde toegangsbeheer staat beheerders toe om toegang tot specifieke segmenten te beheren.

Via attribuut-gebaseerde toegangscontrole, kunnen de beheerders van uw organisatie gebruikers&#39; toegang tot zowel gevoelige persoonlijke gegevens (SPD) als persoonlijk identificeerbare informatie (PII) over alle werkschema&#39;s en middelen van het Platform controleren. Beheerders kunnen gebruikersrollen definiëren die alleen toegang hebben tot specifieke velden en gegevens die overeenkomen met die velden.

Als gevolg van attribuut-gebaseerde toegangscontrole, zouden sommige gebieden en functionaliteiten toegang beperkt hebben en voor bepaalde de dienstmodellen van de AI van de Klant onbeschikbaar zijn. Voorbeelden zijn Identiteit, Score Definition en Klonen.

![De AI-werkruimte van de Klant met de beperkte velden van de resultaten van het servicemodel gemarkeerd.](../images/user-guide/unavailable-functionalities.png)

Bovenaan in de AI-werkruimte van de klant **pagina met inzichten**, merk op dat de details in de zijbalk, de score, de identiteit, en de profielattributen allen &quot;Toegang Beperkt tonen.&quot;

![De AI-werkruimte van de Klant met de beperkte velden van het schema gemarkeerd.](../images/user-guide/access-restricted.png)

Wanneer u datasets met beperkt schema op voorproef **[!UICONTROL Create model workflow]** pagina, lijkt een waarschuwing u te laten weten dat [!UICONTROL Due to access restrictions, certain information isn't displayed in the dataset preview.]

![De AI-werkruimte van de Klant met de beperkte velden van de voorvertoningsdatasets met de beperkte schemaresultaten gemarkeerd.](../images/user-guide/restricted-dataset-preview-save-and-exit-cai.png)

Nadat u een model met beperkte informatie creeert en te werk gaat **[!UICONTROL Define goal]** stap, wordt een waarschuwing getoond bij de bovenkant: [!UICONTROL Due to access restrictions, certain information isn't displayed in the configuration.]

![De AI-werkruimte van de Klant met de beperkte velden van de resultaten van het servicemodel gemarkeerd.](../images/user-guide/information-not-displayed-save-and-exit.png)

Wanneer u toegangsbeheer gebruikt, **AI van klant weergeven** en **AI van klant beheren** toegangsrechten verlenen toegang tot verschillende functies van de AI van de Klant. De **AI van klant beheren** met bevoegdheid **maken**,**update**, **delete**, **enable**, of **disable** een model terwijl **AI van klant weergeven** Hiermee kunt u het document lezen of weergeven. De **maken**, **update** en **delete** acties worden vastgelegd in auditlogboeken.

Raadpleeg de documentatie voor meer informatie [toewijzen van machtigingen voor toegangsbeheer](../../../access-control/home.md) of hoe [gebruik controlelogboeken om toegang en activiteit te controleren](../../../landing/governance-privacy-security/audit-logs/overview.md).

## Volgende stappen

Door deze gids te lezen, bent u geïntroduceerd aan de belangrijkste principes van toegangscontrole in [!DNL Experience Platform]. U kunt nu doorgaan naar het dialoogvenster [gebruikershandleiding voor toegangsbeheer](../overview.md) voor gedetailleerde stappen over het gebruik van de [!DNL Admin Console] om productprofielen te maken en machtigingen toe te wijzen voor [!DNL Platform].
