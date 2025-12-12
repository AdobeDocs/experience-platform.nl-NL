---
title: Overzicht van Adobe Experience Cloud Identity Service
description: Meer informatie over de extensie van de Adobe Experience Cloud Identity Service in Adobe Experience Platform.
exl-id: 9bfcb666-a3f1-46ad-8678-2c63738da2b2
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 0%

---

# Overzicht van de extensie Adobe Experience Cloud Identity Service

Gebruik deze verwijzing voor informatie over het vormen van de uitbreiding van identiteitskaart van Adobe Experience Cloud, en de opties beschikbaar wanneer het gebruiken van deze uitbreiding om een regel te bouwen.

Gebruik deze extensie om de Experience Cloud Identity Service te integreren met uw eigenschap. Met de Experience Cloud Identity Service kunt u unieke en permanente id&#39;s voor bezoekers van uw site maken en opslaan.

## De extensie Experience Cloud-id configureren

Deze sectie bevat een verwijzing naar de opties die beschikbaar zijn wanneer u de extensie voor de Experience Cloud-id configureert.

Als de extensie Experience Cloud-id nog niet is geïnstalleerd, opent u de eigenschap en selecteert u **[!UICONTROL Extensions > Catalog]** . Plaats de aanwijzer op de extensie Experience Cloud-id en selecteer **[!UICONTROL Install]** .

Als u de extensie wilt configureren, opent u het tabblad Extensies, plaatst u de muisaanwijzer op de extensie en selecteert u **[!UICONTROL Configure]** .

![](../../../images/optin.jpg)

De volgende configuratieopties zijn beschikbaar:

### Experience Cloud-organisatie-id

De id voor je Experience Cloud-organisatie.

De id bestaat uit een alfanumerieke tekenreeks van 24 tekens, gevolgd door `@AdobeOrg` . Als u deze id niet kent, neemt u contact op met de klantenservice.

### Specifieke paden uitsluiten

De Experience Cloud-id wordt niet geladen als de URL overeenkomt met een van de opgegeven paden.

(Optioneel) Schakel Regex in als dit een reguliere expressie is.

Selecteer **[!UICONTROL Add]** om een ander pad uit te sluiten.

### Aanmelden

Gebruik de opties bij Inschakelen om te bepalen of bezoekers moeten deelnemen aan Adobe-services op uw site, zoals of ze cookies moeten maken die bezoekersactiviteiten volgen.

Opt In is het centrale referentiepunt voor alle clientbibliotheken van de Experience Platform-oplossing om te bepalen of cookies op het apparaat of de browser van een gebruiker kunnen worden gemaakt wanneer deze uw site bezoeken. Opt In biedt geen ondersteuning voor het verzamelen of opslaan van voorkeuren voor gebruikersmachtigingen.

**laat Opt binnen toe?**

De geselecteerde optie bepaalt of uw website wacht op toestemming om de activiteiten van een bezoeker op uw website te volgen.

Er zijn drie opties:

* **Nr:** wacht niet op toestemming om de bezoeker te volgen. Dit is het standaardgedrag als u geen optie selecteert.
* **ja:** wacht op toestemming om de bezoeker te volgen.
* **die bij runtime wordt bepaald gebruikend functie:** bepaalt programmatically of de waarde waar of vals bij runtime is. Als u deze optie selecteert, wordt het veld Gegevenselement selecteren beschikbaar. Selecteer een gegevenselement dat kan bepalen of op toestemming moet wachten. Dit gegevenselement wordt omgezet in een booleaanse waarde. U kunt bijvoorbeeld een gegevenselement selecteren dat toestemming geeft, afhankelijk van de vraag of het land van de bezoeker zich in de EU bevindt.

**is Opt in Toegelaten opslag?**

Als deze optie is ingeschakeld, wordt de toestemming opgeslagen in een cookie van de eerste fabrikant op uw domein. Als deze optie niet is ingeschakeld, worden de machtigingsinstellingen opgeslagen in uw CMP of een cookie die u beheert.

**Opt in het Domein van het Koekje?**

Gebruik deze optionele instelling om het domein op te geven waar de Opt in-cookie wordt opgeslagen als opslag is ingeschakeld. U kunt een domein ingaan, of een gegevenselement selecteren dat het domein bevat.

**Opt in de Verval van de Opslag?**

Geef op wanneer het cookie Opt in vervalt wanneer opslag is ingeschakeld, in seconden.

Voer een getal in en selecteer vervolgens een tijdseenheid in de vervolgkeuzelijst. Voer bijvoorbeeld 2 in en selecteer **[!UICONTROL Weeks]** . De standaardwaarde is 13 maanden.

**Toestemmingen?**

Geef vorige toestemming door aan de bibliotheek Opt in. Selecteer een gegevenselement dat de toestemming bevat. Het elementtype moet een object of een JSON-tekenreeks zijn. Hiermee overschrijft u goedkeuringen voor vooraf aanmelden.

Voorbeeld:

`"{"aa":true,"aam":true,"ecid":true}"`

**Vooraf kiezen in Goedkeuringen?**

Bepaal welke categorieën worden goedgekeurd of geweigerd wanneer geen voorkeur door de bezoeker is geplaatst. De toestemming wordt verondersteld voor de geselecteerde oplossingen vanaf de tijd de pagina wordt geladen. Het elementtype moet een object of een JSON-tekenreeks zijn (bijvoorbeeld: `{aam: true}`).

### Variabelen

Stel naam-waardeparen in als Experience Cloud ID-instantie-eigenschappen. Gebruik de vervolgkeuzelijst om een variabele te selecteren en typ of selecteer een waarde. Voor informatie over elke variabele, verwijs naar de [ documentatie van de Dienst van de Identiteit van Experience Cloud ](https://experiencecloud.adobe.com/resources/help/en_US/mcvid/mcvid-overview.html).

## Handelingstypen voor Experience Cloud ID-extensie

In deze sectie worden de actietypen beschreven die beschikbaar zijn in de extensie Experience Cloud-id.

### Typen handelingen

#### Klant-id&#39;s instellen

Stel een of meer klant-id&#39;s in.

1. Voer de integratiecode in.

   De integratiecode moet de waarde bevatten die is ingesteld als gegevensbron in Audience Manager of Customer Attributes.

1. Selecteer een waarde.

   De waarde moet een gebruikersnaam zijn. Gegevenselementen zijn het meest geschikt voor dynamische waarden, zoals id&#39;s van een client-specifiek intern systeem.

1. Selecteer een verificatiestatus.

   Beschikbare opties zijn:

   * Onbekend
   * Geverifieerd
   * Afgemeld

1. (Optioneel) Selecteer **[!UICONTROL Add]** om meer klant-id&#39;s in te stellen.
1. Selecteer **[!UICONTROL Keep Changes]**.
