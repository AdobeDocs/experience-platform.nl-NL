---
keywords: google ad manager;google ad;doubleclick;DoubleClick AdX;DoubleClick;Google Ad Manager;Google Admanager
title: Google Ad Manager-verbinding
description: 'Google Ad Manager, voorheen bekend als DoubleClick voor uitgevers of DoubleClick AdX, is een advertentieplatform van Google dat uitgevers de middelen geeft om de weergave van advertenties op hun websites, via video en in mobiele apps te beheren.  '
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 0%

---


# [!DNL Google Ad Manager] verbinding

## Overzicht {#overview}

[!DNL Google Ad Manager], voorheen bekend  [!DNL DoubleClick] bij Publishers of  [!DNL DoubleClick AdX], is een advertentieplatform van  [!DNL Google] waaruit uitgevers de middelen krijgen om de weergave van advertenties op hun websites, via video en in mobiele apps te beheren.

## Doelspecificaties

Neem nota van de volgende details die voor [!DNL Google Ad Manager] bestemmingen specifiek zijn:

* Geactiveerd publiek wordt gecreeerd programmatically in het [!DNL Google] platform.
* Platform bevat momenteel geen metrische waarde om succesvolle activering te valideren. Raadpleeg de tellingen van het publiek in Google om de integratie te valideren en inzicht te krijgen in doelgroepen.

>[!IMPORTANT]
>
>Als u uw eerste bestemming met [!DNL Google Ad Manager] wilt maken en de [ID-synchronisatiefunctionaliteit](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) in het verleden (met Audience Manager of andere toepassingen) niet hebt ingeschakeld, neemt u contact op met Adobe Consulting of de klantenservice om id-syncs in te schakelen. Als u eerder [!DNL Google] integraties in Audience Manager had opgezet, de syncs van identiteitskaart u opstelling dragen over aan Platform.

## Ondersteunde identiteiten {#supported-identities}

[!DNL Google Ad Manager] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven.

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Selecteer deze doelidentiteit wanneer uw bronidentiteit een GAID-naamruimte is. |
| IDFA | [!DNL Apple ID for Advertisers] | Selecteer deze doelidentiteit wanneer uw bronidentiteit een IDFA-naamruimte is. |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), ook bekend als  [!DNL Device ID]. Een numerieke apparaat-id van 38 cijfers waarmee de Audience Manager werkt. | Google gebruikt [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) om gebruikers in Californië aan te wijzen, en Google Cookie ID voor alle andere gebruikers. |
| [!DNL Google] cookie-id | [!DNL Google] cookie-id | [!DNL Google] gebruikt deze id om gebruikers buiten Californië als doel in te stellen. |
| RIDA | Roku ID for Advertising. Deze id identificeert unieke Roku-apparaten. |  |
| GEMAAKT | Microsoft Advertising ID. Deze id identificeert apparaten waarop Windows 10 wordt uitgevoerd op unieke wijze. |  |
| Amazon Fire TV ID | Deze id is uniek voor Amazon Fire TV&#39;s. |  |

## Exporttype {#export-type}

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

Selecteer **[!DNL Google Ad Manager]** in **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** en selecteer **[!UICONTROL Configure]**.

![Doel van Google Ad Manager verbinden](../../assets/catalog/advertising/google-ad-manager/catalog.png)

>[!NOTE]
>
>Als er al een verbinding met dit doel bestaat, kunt u een **[!UICONTROL Activate]** knop op de doelkaart zien. Raadpleeg voor meer informatie over het verschil tussen **[!UICONTROL Activate]** en **[!UICONTROL Configure]** de sectie [Catalog](../../ui/destinations-workspace.md#catalog) van de documentatie van de doelwerkruimte.

In **Opstelling** stap van creeer bestemmingswerkschema, vul [!UICONTROL Basic Information] voor de bestemming in.

![Basisinformatie Google Ad Manager](../../assets/catalog/advertising/google-ad-manager/setup.png)

* **[!UICONTROL Name]**: Vul de voorkeursnaam voor dit doel in.
* **[!UICONTROL Description]**: Optioneel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken.
* **[!UICONTROL Account Type]**: Selecteer een optie, afhankelijk van uw account bij Google:
   * `DFP by Google` gebruiken voor [!DNL DoubleClick] voor uitgevers
   * `AdX buyer` gebruiken voor [!DNL Google AdX]
* **[!UICONTROL Account ID]**: Vul je account-id in met  [!DNL Google]. Dit kan uw identiteitskaart van het Netwerk of uw identiteitskaart van de Verbinding van het publiek zijn. Dit is doorgaans een id van acht cijfers.
* **[!UICONTROL Marketing action]**: Marketingsacties geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door Adobe gedefinieerde marketingacties of u kunt uw eigen marketingactie maken. Voor meer informatie over marketing acties, zie [Overzicht van het beleid van het gebruik van Gegevens](../../../data-governance/policies/overview.md).

>[!NOTE]
>
>Wanneer u een [!DNL Google Ad Manager]-bestemming instelt, werkt u samen met uw [!DNL Google Account Manager]- of Adobe-vertegenwoordiger om te begrijpen welk accounttype u hebt.

## Segmenten activeren naar [!DNL Google Ad Manager]

Zie [Gegevens naar doelen activeren](../../ui/activate-destinations.md) voor instructies over het activeren van segmenten naar [!DNL Google Ad Manager].

## Geëxporteerde gegevens

Controleer uw [!DNL Google Ad Manager]-account om te controleren of gegevens naar de [!DNL Google Ad Manager]-bestemming zijn geëxporteerd. Als de activering succesvol was, worden de soorten publiek in uw account ingevuld.