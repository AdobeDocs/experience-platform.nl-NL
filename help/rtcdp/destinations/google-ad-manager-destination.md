---
keywords: google ad manager;google ad;doubleclick;DoubleClick AdX;DoubleClick;Google Ad Manager;Google ad manager
title: Doel van Google Ad Manager
seo-title: Doel van Google Ad Manager
description: 'Google Ad Manager, voorheen bekend als DoubleClick voor uitgevers of DoubleClick AdX, is een advertentieplatform van Google dat uitgevers de middelen geeft om de weergave van advertenties op hun websites, via video en in mobiele apps te beheren. '
seo-description: 'Google Ad Manager, voorheen bekend als DoubleClick voor uitgevers of DoubleClick AdX, is een advertentieplatform van Google dat uitgevers de middelen geeft om de weergave van advertenties op hun websites, via video en in mobiele apps te beheren. '
translation-type: tm+mt
source-git-commit: 485c4b1c3c68755396da087d4b5864c8a36e64df
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---


# [!DNL Google Ad Manager Destination]

## Overzicht

[!DNL Google Ad Manager], voorheen bekend [!DNL DoubleClick] bij Publishers of [!DNL DoubleClick AdX], is een advertentieplatform van [!DNL Google] waaruit uitgevers de middelen krijgen om de weergave van advertenties op hun websites te beheren, via video en in mobiele apps.

## Doelspecificaties

Let op de volgende details die specifiek zijn voor [!DNL Google Ad Manager] bestemmingen:

* U kunt de volgende [identiteiten](../../identity-service/namespaces.md) naar [!DNL Google Ad Manager] bestemmingen verzenden: **Google-cookie-id, IDFA, GAID, Roku-id&#39;s, Microsoft-id&#39;s, Amazon Fire TV-id&#39;s**.
* Geactiveerd publiek wordt programmatically gecreeerd op het [!DNL Google] platform.
* Adobe In real time CDP omvat momenteel geen metrisch om succesvolle activering te bevestigen. Raadpleeg de tellingen van het publiek in Google om de integratie te valideren en inzicht te krijgen in doelgroepen.

>[!IMPORTANT]
>
>Als u uw eerste bestemming wilt maken met [!DNL Google Ad Manager] en in het verleden (met Audience Manager of andere toepassingen) de functionaliteit [voor het synchroniseren van](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) id&#39;s niet hebt ingeschakeld in de Experience Cloud-id-service, neemt u contact op met Adobe Consulting of de klantenservice om id-syncs in te schakelen. Als u eerder opstellings [!DNL Google] integraties in Audience Manager had, de syncs van identiteitskaart u opstelling dragen over aan Adobe in real time CDP.

### Exporttype {#export-type}

**[!DNL Segment Export]** - u exporteert alle leden van een segment (publiek) naar de Google-bestemming.

## Vereisten

### Lijst van gewenste personen

>[!NOTE]
>
>De lijst van gewenste personen is verplicht alvorens uw eerste [!DNL Google Ad Manager] bestemming in Adobe in real time CDP te vestigen. Controleer of het hieronder beschreven lijst van gewenste personen-proces is voltooid door [!DNL Google] voordat u een doel maakt.

Voordat u de [!DNL Google Ad Manager] bestemming maakt in CDP in real-time Adobe, moet u contact opnemen [!DNL Google] voor Adobe die wordt geplaatst in de lijst met toegestane gegevensproviders en voor uw account die wordt toegevoegd aan de lijst van gewenste personen. Neem contact op met [!DNL Google] en geef de volgende informatie op:

* **Account-id** : Dit is Adobe account-ID met [!DNL Google]. Neem contact op met de klantenservice van Adobe of uw Adobe om deze id te verkrijgen.
* **Klant-id** : Dit is Adobe-klant-id met [!DNL Google]. Neem contact op met de klantenservice van Adobe of uw Adobe om deze id te verkrijgen.
* **Netwerk-id** : dit is je account met [!DNL Google Ad Manager]
* **Koppelings-id** publiek: dit is je account met [!DNL Google Ad Manager]
* Je accounttype. DFP door koper van Google of AdX.

## Doel configureren

1. Selecteer in **[!UICONTROL Verbindingen]** > **[!UICONTROL Doelen]** de optie **[!DNL Google Ad Manager]** en selecteer **[!UICONTROL Configureren]**.
   ![Doel van Google Ad Manager verbinden](/help/rtcdp/destinations/assets/google-1-destination.png)

   >[!NOTE]
   >
   >Als er al een verbinding met dit doel bestaat, ziet u een knop **[!UICONTROL Activeren]** op de doelkaart. Voor meer informatie over het verschil tussen **[!UICONTROL Activate]** en **[!UICONTROL Configure]**, verwijs naar de sectie van de [Catalogus](/help/rtcdp/destinations/destinations-workspace.md#catalog) van de documentatie van de bestemmingswerkruimte.

2. In de stap van de **Opstelling** van creeer bestemmingswerkschema, vul de [!UICONTROL BasisInformatie] voor de bestemming in. <br>

   ![Basisinformatie Google Ad Manager](/help/rtcdp/destinations/assets/google-1-destination-setup-step.png)
* **[!UICONTROL Naam]**: Vul de voorkeursnaam voor dit doel in.
* **[!UICONTROL Omschrijving]**: Optioneel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken.
* **[!UICONTROL Accounttype]**: Selecteer een optie, afhankelijk van uw account bij Google:
   * Gebruiken `DFP by Google` voor [!DNL DoubleClick] uitgevers
   * Gebruiken `AdX buyer` voor [!DNL Google AdX]
* **[!UICONTROL Account-id]**: Vul je account-id in met [!DNL Google]. Dit kan uw identiteitskaart van het Netwerk of uw identiteitskaart van de Verbinding van het publiek zijn. Dit is doorgaans een id van acht cijfers.
* **[!UICONTROL Geval]** voor gebruik bij het in de handel brengen: Gebruiksgevallen voor marketingdoeleinden geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door de Adobe gedefinieerde gebruiksgevallen voor marketingdoeleinden of u kunt uw eigen gebruiksscenario voor marketingdoeleinden maken. Voor meer informatie over het op de markt brengen van gebruiksgevallen, zie de [Governance van Gegevens in Echte tijd CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) pagina. Voor informatie over de individuele Adobe-bepaalde het in de handel brengen gebruiksgevallen, zie het overzicht [van het het gebruiksbeleid van](/help/data-governance/policies/overview.md#core-actions)Gegevens.

>[!NOTE]
>
> Wanneer u een [!DNL Google Ad Manager] bestemming instelt, werkt u samen met uw vertegenwoordiger [!DNL Google Account Manager] of Adobe om te begrijpen welk accounttype u hebt.

## Segmenten activeren om [!DNL Google Ad Manager]

Voor instructies op hoe te om segmenten te activeren, zie [!DNL Google Ad Manager]Gegevens aan Doelen [](/help/rtcdp/destinations/activate-destinations.md)activeren.

## Geëxporteerde gegevens

Controleer uw [!DNL Google Ad Manager] account om te controleren of gegevens naar de [!DNL Google Ad Manager] bestemming zijn geëxporteerd. Als de activering succesvol was, worden de soorten publiek in uw account ingevuld.