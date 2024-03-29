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
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Met de uitbreiding van de Adobe Privacy-tag kunt u gebruikers-id&#39;s die aan eindgebruikers zijn toegewezen, verzamelen en verwijderen door oplossingen te Adoben op client-side apparaten. Verzamelde id&#39;s kunnen vervolgens worden verzonden naar [Adobe Experience Platform Privacy Service](../../../../privacy-service/home.md) om de persoonlijke gegevens van de verwante persoon te openen of te verwijderen in ondersteunde Adobe Experience Cloud-toepassingen.

Deze gids behandelt hoe te om de uitbreiding van de Privacy van de Adobe in de UI van het Experience Platform of UI van de Inzameling van Gegevens te installeren en te vormen.

>[!NOTE]
>
>Als u deze functies liever installeert zonder tags te gebruiken, raadpleegt u de [Overzicht van de Privacy JavaScript-bibliotheek](../../../../privacy-service/js-library.md) voor stappen voor het implementeren met onbewerkte code.

## De extensie installeren en configureren

Selecteren **[!UICONTROL Extensions]** in de linkernavigatie, gevolgd door **[!UICONTROL Catalog]** tab. Gebruik de zoekbalk om de lijst met beschikbare extensies te versmallen tot u de Adobe Privacy hebt gevonden. Selecteren **[!UICONTROL Install]** om door te gaan.

![De extensie installeren](../../../images/extensions/client/privacy/install.png)

Het volgende scherm staat u toe om te vormen welke bronnen en oplossingen u de uitbreiding wilt om IDs van te verzamelen. De volgende oplossingen worden ondersteund voor de extensie:

* Adobe Analytics (AA)
* Adobe Audience Manager (AAM)
* Adobe Target
* Adobe Experience Cloud Identity Service (Visitor, of ECID)
* Adobe Advertising Cloud (AdCloud)

Selecteer een of meer oplossingen en selecteer vervolgens **[!UICONTROL Update]**.

![Oplossingen selecteren](../../../images/extensions/client/privacy/select-solutions.png)

Het scherm werkt bij om input voor de vereiste configuratieparameters te tonen die op de oplossingen worden gebaseerd u selecteerde.

![Vereiste eigenschappen](../../../images/extensions/client/privacy/required-properties.png)

Gebruikend dropdown menu hieronder, kunt u extra oplossing-specifieke parameters aan de configuratie ook toevoegen.

![Optionele eigenschappen](../../../images/extensions/client/privacy/optional-properties.png)

>[!NOTE]
>
>Zie de sectie over [configuratieparameters](../../../../privacy-service/js-library.md#config-params) in het overzicht Privacy JavaScript Library voor meer informatie over de geaccepteerde configuratiewaarden voor elke ondersteunde oplossing.

Als u klaar bent met het toevoegen van parameters voor de geselecteerde oplossingen, selecteert u **[!UICONTROL Save]** om de configuratie op te slaan.

![Optionele eigenschappen](../../../images/extensions/client/privacy/save-config.png)

## De extensie gebruiken {#using}

De uitbreiding van de Privacy van de Adobe verstrekt drie actietypes die in een [regel](../../../ui/managing-resources/rules.md) wanneer zich een bepaalde gebeurtenis voordoet en aan de voorwaarden is voldaan:

* **[!UICONTROL Retrieve Identities]**: De opgeslagen identiteitsgegevens van de gebruiker worden opgehaald.
* **[!UICONTROL Remove Identities]**: De opgeslagen identiteitsgegevens van de gebruiker worden verwijderd.
* **[!UICONTROL Retrieve Then Remove Identities]**: De opgeslagen identiteitsgegevens van de gebruiker worden opgehaald en vervolgens verwijderd.

Voor elk van de bovenstaande handelingen moet u een callback JavaScript-functie opgeven die de opgehaalde identiteitsgegevens als objectparameter accepteert en verwerkt. Vanaf hier kunt u deze identiteiten opslaan, weergeven of verzenden naar de [Privacy Service-API](../../../../privacy-service/api/overview.md) zoals u nodig hebt.

Wanneer u de extensie Adobe Privacy gebruikt, moet u de vereiste callback-functie opgeven in de vorm van een gegevenselement. Raadpleeg de volgende sectie voor stappen over het configureren van dit gegevenselement.

### Een gegevenselement definiëren om identiteiten af te handelen

Start het maken van een nieuw gegevenselement door **[!UICONTROL Data Elements]** in de linkernavigatie, gevolgd door **[!UICONTROL Add Data Element]**. Als u zich op het configuratiescherm bevindt, selecteert u **[!UICONTROL Core]** voor de verlenging en **[!UICONTROL Custom Code]** voor het elementtype data. Van hier, selecteer **[!UICONTROL Open Editor]** in het rechterdeelvenster.

![Type gegevenselement selecteren](../../../images/extensions/client/privacy/data-element-type.png)

Definieer in het dialoogvenster dat wordt weergegeven een JavaScript-functie die de opgehaalde identiteiten afhandelt. De callback moet één enkel voorwerp-type argument goedkeuren (`ids` in het onderstaande voorbeeld). De functie kan vervolgens de id&#39;s verwerken die u maar wilt, en kan ook alle variabelen en functies aanroepen die wereldwijd op uw site beschikbaar zijn voor verdere verwerking.

>[!NOTE]
>
>Voor meer informatie over de structuur van de `ids` object dat de callback-functie naar verwachting zal verwerken, raadpleegt u het [codevoorbeelden](../../../../privacy-service/js-library.md#samples) in het overzicht voor de Privacy JavaScript-bibliotheek.

Selecteer **[!UICONTROL Save]**.

![Callback-functie definiëren](../../../images/extensions/client/privacy/define-custom-code.png)

U kunt andere douane-code gegevenselementen blijven creëren als u verschillende callbacks voor verschillende gebeurtenissen vereist.

### Een regel maken met een privacyactie

Na het vormen van een callback gegevenselement om opgehaalde IDs te behandelen, kunt u een regel tot stand brengen die de uitbreiding van de Privacy van de Adobe aanhaalt wanneer een bepaalde gebeurtenis op uw plaats samen met om het even welke andere voorwaarden voorkomt u vereist.

Wanneer het vormen van de actie voor de regel, selecteer **[!UICONTROL Adobe Privacy]** voor de extensie. Selecteer bij het handelingstype een van de opties [drie functies](#using) verstrekt door de uitbreiding.

![Handelingstype selecteren](../../../images/extensions/client/privacy/action-type.png)

In het rechterdeelvenster wordt u gevraagd een gegevenselement te selecteren dat zal dienen als callback van de handeling. Selecteer het databasepictogram (![Databasepictogram](../../../images/extensions/client/privacy/database.png)) en kiest u het gegevenselement dat u eerder in de lijst hebt gemaakt. Selecteren **[!UICONTROL Keep Changes]** om door te gaan.

![Gegevenselement selecteren](../../../images/extensions/client/privacy/add-data-element.png)

Van hier, kunt u de regel blijven vormen zodat de actie van de Privacy van de Adobe onder de gebeurtenissen en de voorwaarden brandt u vereist. Als u tevreden bent, selecteert u **[!UICONTROL Save]**.

![De regel opslaan](../../../images/extensions/client/privacy/save-rule.png)

U kunt nu de regel toevoegen aan een bibliotheek om te implementeren als build op uw website voor testdoeleinden. Zie het overzicht op de [labels publiceren, stroom](../../../ui/publishing/overview.md) voor meer informatie .

## De extensie uit- of verwijderen

Nadat u de extensie hebt geïnstalleerd, kunt u deze uitschakelen of verwijderen. Selecteren **[!UICONTROL Configure]** op de Adobe Privacy-kaart in uw geïnstalleerde extensies en selecteer vervolgens **[!UICONTROL Disable]** of **[!UICONTROL Uninstall]**.

## Volgende stappen

Deze handleiding behandelde het gebruik van de extensie Adobe Privacy in de gebruikersinterface. Voor meer informatie over de functies die door de extensie worden geboden, waaronder voorbeelden van het gebruik ervan met onbewerkte code, raadpleegt u de [Overzicht van de Privacy JavaScript-bibliotheek](../../../../privacy-service/js-library.md) in de documentatie bij de Privacy Service.
