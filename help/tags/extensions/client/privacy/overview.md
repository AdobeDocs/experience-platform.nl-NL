---
title: Overzicht van Adobe Privacy Extension
description: Meer informatie over de extensie Adobe Privacy in Adobe Experience Platform.
exl-id: 8401861e-93ad-48eb-8796-b26ed8963c32
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '868'
ht-degree: 0%

---

# Overzicht van Adobe Privacy-extensie

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Gelieve te verwijzen naar het volgende [ document ](../../../term-updates.md) voor een geconsolideerde verwijzing van de terminologieveranderingen.

Met de uitbreiding van de Adobe Privacy-tag kunt u gebruikers-id&#39;s die aan eindgebruikers zijn toegewezen, verzamelen en verwijderen door oplossingen te Adoben op client-side apparaten. Verzamelde IDs kan dan naar [ Adobe Experience Platform Privacy Service ](../../../../privacy-service/home.md) worden verzonden om tot de verwante persoonlijke gegevens van het individu in de gesteunde toepassingen van Adobe Experience Cloud toegang te hebben of te schrappen.

Deze gids behandelt hoe te om de uitbreiding van de Privacy van de Adobe in de UI van het Experience Platform of UI van de Inzameling van Gegevens te installeren en te vormen.

>[!NOTE]
>
>Als u verkiest deze functionaliteit te installeren zonder markeringen te gebruiken, zie het [ overzicht van de Bibliotheek van JavaScript van de Privacy ](../../../../privacy-service/js-library.md) voor stappen op hoe te om het gebruiken van ruwe code uit te voeren.

## De extensie installeren en configureren

Selecteer **[!UICONTROL Extensions]** in de linkernavigatie, gevolgd door de tab **[!UICONTROL Catalog]** . Gebruik de zoekbalk om de lijst met beschikbare extensies te versmallen tot u de Adobe Privacy hebt gevonden. Selecteer **[!UICONTROL Install]** om door te gaan.

![ installeer de uitbreiding ](../../../images/extensions/client/privacy/install.png)

Het volgende scherm staat u toe om te vormen welke bronnen en oplossingen u de uitbreiding wilt om IDs van te verzamelen. De volgende oplossingen worden ondersteund voor de extensie:

* Adobe Analytics (AA)
* Adobe Audience Manager (AAM)
* Adobe Target
* Adobe Experience Cloud Identity Service (Visitor, of ECID)
* Adobe Advertising Cloud (AdCloud)

Selecteer een of meer oplossingen en selecteer vervolgens **[!UICONTROL Update]** .

![ Uitgezochte oplossingen ](../../../images/extensions/client/privacy/select-solutions.png)

Het scherm werkt bij om input voor de vereiste configuratieparameters te tonen die op de oplossingen worden gebaseerd u selecteerde.

![ Vereiste eigenschappen ](../../../images/extensions/client/privacy/required-properties.png)

Gebruikend dropdown menu hieronder, kunt u extra oplossing-specifieke parameters aan de configuratie ook toevoegen.

![ Facultatieve eigenschappen ](../../../images/extensions/client/privacy/optional-properties.png)

>[!NOTE]
>
>Zie de sectie over [ configuratieparameters ](../../../../privacy-service/js-library.md#config-params) in het overzicht van de Bibliotheek van JavaScript van de Privacy voor details op de toegelaten configuratiewaarden voor elke gesteunde oplossing.

Nadat u de parameters voor de geselecteerde oplossingen hebt toegevoegd, selecteert u **[!UICONTROL Save]** om de configuratie op te slaan.

![ Facultatieve eigenschappen ](../../../images/extensions/client/privacy/save-config.png)

## De extensie gebruiken {#using}

De uitbreiding van de Privacy van de Adobe verstrekt drie actietypen die in a [ regel ](../../../ui/managing-resources/rules.md) kunnen worden gebruikt wanneer een bepaalde gebeurtenis voorkomt en de voorwaarden worden voldaan:

* **[!UICONTROL Retrieve Identities]**: De opgeslagen identiteitsgegevens van de gebruiker worden opgehaald.
* **[!UICONTROL Remove Identities]**: De opgeslagen identiteitsgegevens van de gebruiker worden verwijderd.
* **[!UICONTROL Retrieve Then Remove Identities]**: De opgeslagen identiteitsgegevens van de gebruiker worden opgehaald en vervolgens verwijderd.

Voor elk van de bovenstaande handelingen moet u een callback JavaScript-functie opgeven die de opgehaalde identiteitsgegevens accepteert en verwerkt als een objectparameter. Van hier, kunt u deze identiteiten opslaan, hen tonen, of hen verzenden naar [ Privacy Service API ](../../../../privacy-service/api/overview.md) aangezien u vereist.

Wanneer u de extensie Adobe Privacy gebruikt, moet u de vereiste callback-functie opgeven in de vorm van een gegevenselement. Raadpleeg de volgende sectie voor stappen over het configureren van dit gegevenselement.

### Een gegevenselement definiëren om identiteiten af te handelen

Start het maken van een nieuw gegevenselement door **[!UICONTROL Data Elements]** te selecteren in de linkernavigatie, gevolgd door **[!UICONTROL Add Data Element]** . Wanneer u zich op het configuratiescherm bevindt, selecteert u **[!UICONTROL Core]** voor de extensie en **[!UICONTROL Custom Code]** voor het type gegevenselement. Selecteer van hieruit **[!UICONTROL Open Editor]** in het rechterdeelvenster.

![ Uitgezochte type van gegevenselement ](../../../images/extensions/client/privacy/data-element-type.png)

Definieer in het dialoogvenster dat wordt weergegeven een JavaScript-functie die de opgehaalde identiteiten zal verwerken. Callback moet één enkel voorwerp-type argument (`ids` in het hieronder voorbeeld goedkeuren). De functie kan vervolgens de id&#39;s verwerken die u maar wilt, en kan ook alle variabelen en functies aanroepen die wereldwijd op uw site beschikbaar zijn voor verdere verwerking.

>[!NOTE]
>
>Voor meer informatie over de structuur van het `ids` voorwerp dat de callback functie wordt verwacht te behandelen, verwijs naar de [ codesteekproeven ](../../../../privacy-service/js-library.md#samples) die in het overzicht voor de Bibliotheek van JavaScript van de Privacy worden verstrekt.

Selecteer **[!UICONTROL Save]** als u klaar bent.

![ bepaalt callback functie ](../../../images/extensions/client/privacy/define-custom-code.png)

U kunt andere douane-code gegevenselementen blijven creëren als u verschillende callbacks voor verschillende gebeurtenissen vereist.

### Een regel maken met een privacyactie

Na het vormen van een callback gegevenselement om opgehaalde IDs te behandelen, kunt u een regel tot stand brengen die de uitbreiding van de Privacy van de Adobe aanhaalt wanneer een bepaalde gebeurtenis op uw plaats samen met om het even welke andere voorwaarden voorkomt u vereist.

Wanneer het vormen van de actie voor de regel, uitgezochte **[!UICONTROL Adobe Privacy]** voor de uitbreiding. Voor het actietype, selecteer één van [ drie functies ](#using) die door de uitbreiding worden verstrekt.

![ Uitgezochte actietype ](../../../images/extensions/client/privacy/action-type.png)

In het rechterdeelvenster wordt u gevraagd een gegevenselement te selecteren dat zal dienen als callback van de handeling. Selecteer het gegevensbestandpictogram (![ Pictogram van het Gegevensbestand ](../../../images/extensions/client/privacy/database.png)) en kies het gegevenselement u vroeger van de lijst creeerde. Selecteer **[!UICONTROL Keep Changes]** om door te gaan.

![ Uitgezochte gegevenselement ](../../../images/extensions/client/privacy/add-data-element.png)

Van hier, kunt u de regel blijven vormen zodat de actie van de Privacy van de Adobe onder de gebeurtenissen en de voorwaarden brandt u vereist. Selecteer **[!UICONTROL Save]** als u tevreden bent.

![ sparen de regel ](../../../images/extensions/client/privacy/save-rule.png)

U kunt nu de regel toevoegen aan een bibliotheek om te implementeren als build op uw website voor testdoeleinden. Zie het overzicht op de [ markeringen die stroom publiceren ](../../../ui/publishing/overview.md) voor meer informatie.

## De extensie uit- of verwijderen

Nadat u de extensie hebt geïnstalleerd, kunt u deze uitschakelen of verwijderen. Selecteer **[!UICONTROL Configure]** op de Adobe Privacy-kaart in de geïnstalleerde extensies en selecteer vervolgens **[!UICONTROL Disable]** of **[!UICONTROL Uninstall]** .

## Volgende stappen

Deze handleiding behandelde het gebruik van de extensie Adobe Privacy in de gebruikersinterface. Voor meer informatie over de functionaliteit die door de uitbreiding wordt verstrekt, met inbegrip van voorbeelden van hoe te om het te gebruiken gebruikend ruwe code, zie het [ overzicht van de Bibliotheek van JavaScript van de Privacy ](../../../../privacy-service/js-library.md) in de documentatie van de Privacy Service.
