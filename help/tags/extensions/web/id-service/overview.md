---
title: Overzicht van Adobe Experience Cloud Identity Service
description: Meer informatie over de extensie van de Adobe Experience Cloud Identity Service in Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 0%

---

# Overzicht van Adobe Experience Cloud Identity Service

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Gebruik deze verwijzing voor informatie over het vormen van de uitbreiding van identiteitskaart van Adobe Experience Cloud, en de opties beschikbaar wanneer het gebruiken van deze uitbreiding om een regel te bouwen.

Gebruik deze uitbreiding om de Dienst van de Identiteit van de Experience Cloud met uw bezit te integreren. Met de Experience Cloud Identity Service kunt u unieke en permanente id&#39;s voor bezoekers van uw site maken en opslaan.

## De extensie Experience Cloud-id configureren

Deze sectie bevat een verwijzing naar de beschikbare opties bij het configureren van de extensie Experience Cloud-id.

Als de extensie Experience Cloud-id nog niet is geïnstalleerd, opent u de eigenschap en selecteert u **[!UICONTROL Extensions > Catalog]**, plaatst u de aanwijzer op de extensie Experience Cloud-id en selecteert u **[!UICONTROL Install]**.

Als u de extensie wilt configureren, opent u het tabblad Extensies, plaatst u de muisaanwijzer op de extensie en selecteert u **[!UICONTROL Configure]**.

![](../../../images/optin.jpg)

De volgende configuratieopties zijn beschikbaar:

### Experience Cloud Organisatie-id

De id voor uw Experience Cloud-organisatie.

Uw id bestaat uit een alfanumerieke tekenreeks van 24 tekens, gevolgd door `@AdobeOrg`. Als u deze id niet kent, neemt u contact op met de klantenservice.

### Specifieke paden uitsluiten

De Experience Cloud-id wordt niet geladen als de URL overeenkomt met een van de opgegeven paden.

(Optioneel) Schakel Regex in als dit een reguliere expressie is.

Selecteer **[!UICONTROL Add]** om een ander pad uit te sluiten.

### Aanmelden

Gebruik de opties bij Inschakelen om te bepalen of bezoekers moeten deelnemen aan Adobe-services op uw site, zoals of ze cookies moeten maken die bezoekersactiviteiten volgen.

Opt In is het gecentraliseerde referentiepunt voor alle clientbibliotheken met oplossingen voor Platforms om te bepalen of cookies op het apparaat of de browser van een gebruiker kunnen worden gemaakt wanneer deze uw site bezoekt. Opt In biedt geen ondersteuning voor het verzamelen of opslaan van voorkeuren voor gebruikersmachtigingen.

**Inschakelen inschakelen?**

De geselecteerde optie bepaalt of uw website wacht op toestemming om de activiteiten van een bezoeker op uw website te volgen.

Er zijn drie opties:

* **Nee:** wacht niet op toestemming om de bezoeker te volgen. Dit is het standaardgedrag als u geen optie selecteert.
* **Ja:** wacht op toestemming om de bezoeker te volgen.
* **Deze waarde wordt tijdens runtime bepaald met behulp van function:** Programmatiatically determine whether the value is true or false at runtime. Als u deze optie selecteert, wordt het veld Gegevenselement selecteren beschikbaar. Selecteer een gegevenselement dat kan bepalen of op toestemming moet wachten. Dit gegevenselement wordt omgezet in een booleaanse waarde. U kunt bijvoorbeeld een gegevenselement selecteren dat toestemming geeft, afhankelijk van de vraag of het land van de bezoeker zich in de EU bevindt.

**Is Opt In-opslag ingeschakeld?**

Als deze optie is ingeschakeld, wordt de toestemming opgeslagen in een cookie van de eerste fabrikant op uw domein. Als deze optie niet is ingeschakeld, worden de machtigingsinstellingen opgeslagen in uw CMP of een cookie die u beheert.

**Opt in Cookie-domein?**

Gebruik deze optionele instelling om het domein op te geven waar de Opt in-cookie wordt opgeslagen als opslag is ingeschakeld. U kunt een domein ingaan, of een gegevenselement selecteren dat het domein bevat.

**Opt in het verlopen van de opslag?**

Geef op wanneer het cookie Opt in vervalt wanneer opslag is ingeschakeld, in seconden.

Voer een getal in en selecteer vervolgens een tijdseenheid in de vervolgkeuzelijst. Typ bijvoorbeeld 2 en selecteer **[!UICONTROL Weeks]**. De standaardwaarde is 13 maanden.

**Toestemmingen?**

Geef vorige toestemming door aan de bibliotheek Opt in. Selecteer een gegevenselement dat de toestemming bevat. Het elementtype moet een object of een JSON-tekenreeks zijn. Hiermee overschrijft u goedkeuringen voor vooraf aanmelden.

Voorbeeld:

`"{"aa":true,"aam":true,"ecid":true}"`

**Goedkeuringen vooraf aanmelden?**

Bepaal welke categorieën worden goedgekeurd of geweigerd wanneer geen voorkeur door de bezoeker is geplaatst. De toestemming wordt verondersteld voor de geselecteerde oplossingen vanaf de tijd de pagina wordt geladen. Het elementtype moet een object of een JSON-tekenreeks zijn (voorbeeld: `{aam: true}`).

### Variabelen

Stel naam-waardeparen in als Experience Cloud ID-instantie-eigenschappen. Gebruik de vervolgkeuzelijst om een variabele te selecteren en typ of selecteer een waarde. Voor informatie over elke variabele, verwijs naar [Experience Cloud de documentatie van de Dienst van de Identiteit](https://experiencecloud.adobe.com/resources/help/en_US/mcvid/mcvid-overview.html).

## Handelingstypen voor Experience Cloud-id-extensie

In deze sectie worden de actietypen beschreven die beschikbaar zijn in de extensie Experience Cloud-id.

### Typen handelingen

#### Klant-id&#39;s instellen

Stel een of meer klant-id&#39;s in.

1. Voer de integratiecode in.

   De integratiecode moet de waarde bevatten die is ingesteld als gegevensbron in Audience Manager- of klantkenmerken.

1. Selecteer een waarde.

   De waarde moet een gebruikers-id zijn. Gegevenselementen zijn het meest geschikt voor dynamische waarden, zoals id&#39;s van een client-specifiek intern systeem.

1. Selecteer een verificatiestatus.

   Beschikbare opties zijn:

   * Onbekend
   * Geverifieerd
   * Afgemeld

1. (Optioneel) Selecteer **[!UICONTROL Add]** om meer klant-id&#39;s in te stellen.
1. Selecteer **[!UICONTROL Keep Changes]**.
