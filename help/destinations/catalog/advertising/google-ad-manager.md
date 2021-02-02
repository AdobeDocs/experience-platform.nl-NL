---
keywords: google ad manager;google ad;doubleclick;DoubleClick AdX;DoubleClick;Google Ad Manager;Google Admanager
title: Doel van Google Ad Manager
seo-title: Doel van Google Ad Manager
description: 'Google Ad Manager, voorheen bekend als DoubleClick voor uitgevers of DoubleClick AdX, is een advertentieplatform van Google dat uitgevers de middelen geeft om de weergave van advertenties op hun websites, via video en in mobiele apps te beheren. '
seo-description: 'Google Ad Manager, voorheen bekend als DoubleClick voor uitgevers of DoubleClick AdX, is een advertentieplatform van Google dat uitgevers de middelen geeft om de weergave van advertenties op hun websites, via video en in mobiele apps te beheren. '
translation-type: tm+mt
source-git-commit: bb2fc2658d32c59b476dd9d526eb8bc2f055a1af
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 0%

---


# [!DNL Google Ad Manager Destination]

## Overzicht

[!DNL Google Ad Manager], voorheen bekend  [!DNL DoubleClick] bij Publishers of  [!DNL DoubleClick AdX], is een advertentieplatform van  [!DNL Google] waaruit uitgevers de middelen krijgen om de weergave van advertenties op hun websites, via video en in mobiele apps te beheren.

## Doelspecificaties

Neem nota van de volgende details die voor [!DNL Google Ad Manager] bestemmingen specifiek zijn:

* U kunt de volgende [identiteiten](../../../identity-service/namespaces.md) naar [!DNL Google Ads] bestemmingen verzenden: [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en), Google cookie-id, IDFA, GAID, Roku-id&#39;s, Microsoft-id&#39;s en Amazon Fire TV-id&#39;s.
   * Google gebruikt [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) om gebruikers in Californië als doelgroep op te nemen, en de Google Cookie-id voor alle andere gebruikers.
* Geactiveerd publiek wordt gecreeerd programmatically in het [!DNL Google] platform.
* Platform bevat momenteel geen metrische waarde om succesvolle activering te valideren. Raadpleeg de tellingen van het publiek in Google om de integratie te valideren en inzicht te krijgen in doelgroepen.

>[!IMPORTANT]
>
>Als u uw eerste bestemming met [!DNL Google Ad Manager] wilt maken en de [ID-synchronisatiefunctionaliteit](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) in het verleden (met Audience Manager of andere toepassingen) niet hebt ingeschakeld, neemt u contact op met Adobe Consulting of de klantenservice om id-syncs in te schakelen. Als u eerder [!DNL Google] integraties in Audience Manager had opgezet, de syncs van identiteitskaart u opstelling dragen over aan Platform.

### Exporttype {#export-type}

**Segmentexport** : u exporteert alle leden van een segment (publiek) naar de Google-bestemming.

## Vereisten

### Lijst van gewenste personen

>[!NOTE]
>
>De lijst van gewenste personen is verplicht alvorens uw eerste [!DNL Google Ad Manager] bestemming in Platform te plaatsen. Controleer of het hieronder beschreven proces voor lijst van gewenste personen is voltooid door [!DNL Google] voordat u een doel maakt.

Voordat u de [!DNL Google Ad Manager]-bestemming in Platform maakt, moet u contact opnemen met [!DNL Google] om Adobe op de lijst met toegestane gegevensproviders te plaatsen en om uw account aan de lijst van gewenste personen toe te voegen. Neem contact op met [!DNL Google] en geef de volgende informatie op:

* **Account-id** : Dit is Adobe account-ID met  [!DNL Google]. Neem contact op met de klantenservice van Adobe of uw Adobe om deze id te verkrijgen.
* **Klant-id** : Dit is Adobe-klant-id met  [!DNL Google]. Neem contact op met de klantenservice van Adobe of uw Adobe om deze id te verkrijgen.
* **Netwerk-id** : dit is je account met  [!DNL Google Ad Manager]
* **Koppelings-id**  publiek: dit is je account met  [!DNL Google Ad Manager]
* Je accounttype. DFP door koper van Google of AdX.

## Doel configureren

Selecteer **[!UICONTROL Verbindingen]** > **[!UICONTROL Doelen]** en selecteer **[!DNL Google Ad Manager]** en **[!UICONTROL Configureren]**.

![Doel van Google Ad Manager verbinden](../../assets/catalog/advertising/google-ad-manager/catalog.png)

>[!NOTE]
>
>Als er al een verbinding met dit doel bestaat, kunt u een **[!UICONTROL knop Activeer]** op de doelkaart zien. Voor meer informatie over het verschil tussen **[!UICONTROL Activate]** en **[!UICONTROL Configure]**, verwijs naar [Catalog](../../ui/destinations-workspace.md#catalog) sectie van de documentatie van de bestemmingswerkruimte.

In **Opstelling** stap van creeer bestemmingswerkschema, vul [!UICONTROL BasisInformatie] voor de bestemming in.

![Basisinformatie Google Ad Manager](../../assets/catalog/advertising/google-ad-manager/setup.png)

* **[!UICONTROL Naam]**: Vul de voorkeursnaam voor dit doel in.
* **[!UICONTROL Omschrijving]**: Optioneel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken.
* **[!UICONTROL Accounttype]**: Selecteer een optie, afhankelijk van uw account bij Google:
   * `DFP by Google` gebruiken voor [!DNL DoubleClick] voor uitgevers
   * `AdX buyer` gebruiken voor [!DNL Google AdX]
* **[!UICONTROL Account-id]**: Vul je account-id in met  [!DNL Google]. Dit kan uw identiteitskaart van het Netwerk of uw identiteitskaart van de Verbinding van het publiek zijn. Dit is doorgaans een id van acht cijfers.
* **[!UICONTROL Geval]** voor gebruik bij het in de handel brengen: Gebruiksgevallen voor marketingdoeleinden geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door de Adobe gedefinieerde gebruiksgevallen voor marketingdoeleinden of u kunt uw eigen gebruiksscenario voor marketingdoeleinden maken. Zie [Overzicht van beleidsregels voor gegevensgebruik](../../../data-governance/policies/overview.md) voor meer informatie over gevallen van marketinggebruik.

>[!NOTE]
>
>Wanneer u een [!DNL Google Ad Manager]-bestemming instelt, werkt u samen met uw [!DNL Google Account Manager]- of Adobe-vertegenwoordiger om te begrijpen welk accounttype u hebt.

## Segmenten activeren naar [!DNL Google Ad Manager]

Zie [Gegevens naar doelen activeren](../../ui/activate-destinations.md) voor instructies over het activeren van segmenten naar [!DNL Google Ad Manager].

## Geëxporteerde gegevens

Controleer uw [!DNL Google Ad Manager]-account om te controleren of gegevens naar de [!DNL Google Ad Manager]-bestemming zijn geëxporteerd. Als de activering succesvol was, worden de soorten publiek in uw account ingevuld.