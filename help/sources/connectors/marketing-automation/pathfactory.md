---
title: Overzicht van PathFactory Source
description: Leer hoe u PathFactory via API's of de gebruikersinterface met Adobe Experience Platform kunt verbinden.
last-substantial-update: 2024-04-30T00:00:00Z
badge: Beta
exl-id: befb73c4-fd6a-4512-9124-d23a1c27e0e0
source-git-commit: ca17854830edabaf2bd74265258d6f0096f2888e
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 0%

---

# [!DNL PathFactory]

>[!NOTE]
>
>De bron [!DNL PathFactory] is in bèta. Gelieve te lezen het [ overzicht van bronnen ](../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde bronnen.

[[!DNL PathFactory] ](https://www.pathfactory.com/) biedt een cloudplatform dat bedrijven helpt bij het beheren van inhoudsreizen en het aansturen van betrokkenheid via intelligente inzichten in inhoud. Deze gids bepaalt hoe u gegevens van PathFactory in Experience Platform kunt integreren, gebruikend de schakelaars van PathFactory voor optimale gegevensopname.

U kunt gegevens van [[!DNL PathFactory] ](https://www.pathfactory.com/) opnemen gebruikend drie primaire bronnen:

* **[!DNL Visitors]**: Vermeld de gegevens van de klant en neem contact op als verslagen om uw publiek beter te begrijpen.
* **[!DNL Sessions]**: Gebeurtenissen uit de tijdreeks die afzonderlijke gebruikerssessieactiviteiten op uw platform bijhouden.
* **[!DNL Page Views]**: Gebeurtenissen uit de tijdreeks die inzicht verschaffen in welke pagina&#39;s worden weergegeven, zodat u de prestaties van de inhoud kunt analyseren.

Lees het onderstaande document voor informatie over hoe u uw [!DNL PathFactory] bronaccount kunt instellen.

## IP adres lijst van gewenste personen {#ip-allow-list}

Een lijst van IP adressen kan vereisen om aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de ](../../ip-address-allow-list.md) pagina van de lijst van gewenste personen van het 0} IP adres {voor meer informatie.[

## Vereisten {#prerequisites}

Voordat u begint met het integreren van [[!DNL PathFactory] ](https://www.pathfactory.com/) -connectors met Experience Platform, moet u controleren of aan de volgende voorwaarden is voldaan:

* **a [ rekening PathFactory]**.
   * Neem contact op met [[!DNL PathFactory] ](https://www.pathfactory.com/portal/company/contactus.shtml) als u nog geen geldig account hebt.
* **een actief abonnement** aan om het even welk [!DNL PathFactory] product.
* **Gebruikersnaam, wachtwoord, en domein**.
   * Deze referenties zijn vereist voor toegang tot uw [!DNL PathFactory] -account en de bijbehorende gegevens.
* **Symbolische Eindpunten van de Toegang** en **API**.
   * Deze zijn nodig om verbinding te maken met [!DNL PathFactory] API&#39;s.

### Hoe te om Verantwoordelijkheden en de Tokens van de Toegang te verkrijgen {#gather-credentials}

Als u verbinding wilt maken met [!DNL PathFactory] , moet u de volgende gegevens opgeven:

| Credentials | Beschrijving | Endpoint |
| --- | --- | --- |
| Gebruikersnaam | Uw [!DNL PathFactory] gebruikersnaam van de account. | Niet van toepassing |
| Wachtwoord | Wachtwoord voor uw [!DNL PathFactory] account. | Niet van toepassing |
| Domein | Het domein dat aan uw [!DNL PathFactory] account is gekoppeld. | Niet van toepassing |
| Toegangstoken | Een uniek token dat wordt gebruikt voor API-verificatie. | Niet van toepassing |
| Eindpunt van bezoekers | Het API-eindpunt voor bezoekersgegevens. | `/api/public/v3/data_lake_apis/visitors.json` |
| Sessieeindpunt | Het API-eindpunt voor sessiegegevens. | `/api/public/v3/data_lake_apis/sessions.json` |
| Eindpunt van paginaweergaven | Het API-eindpunt voor paginaweergavegegevens. | `/api/public/v3/data_lake_apis/page_views.json` |

Voor gedetailleerde instructies op hoe te om uw gebruikersbenaming, wachtwoord, domein, en toegangstoken te verkrijgen, bezoek het [[!DNL PathFactory]  Centrum van de Steun ](https://support.pathfactory.com/categories/adobe/). Deze bron bevat uitgebreide handleidingen voor het ophalen en beheren van uw referenties.

### Machtigingen configureren voor Experience Platform

U moet zowel **[!UICONTROL View Sources]** als **[!UICONTROL Manage Sources]** machtigingen hebben ingeschakeld voor uw account om uw [!DNL PathFactory] -account aan Experience Platform te kunnen koppelen. Neem contact op met de productbeheerder om de benodigde machtigingen te verkrijgen. Voor meer informatie, lees de [ gids UI van de toegangscontrole ](../../../access-control/ui/overview.md).

## Verbinden [!DNL PathFactory] met platform {#pathfactory-connect}

In de onderstaande documentatie vindt u informatie over het tot stand brengen van een verbinding tussen [!DNL PathFactory] en Platform via API&#39;s of de gebruikersinterface:

* [ creeer een bronverbinding en dataflow om  [!DNL PathFactory]  gegevens aan Platform te brengen gebruikend APIs ](../../tutorials/api/create/marketing-automation/pathfactory.md).
* [ verbind uw  [!DNL PathFactory]  rekening met Experience Platform gebruikend UI ](../../tutorials/ui/create/marketing-automation/pathfactory.md).
* [ creeer een dataflow voor een bronverbinding gebruikend UI ](../../tutorials/ui/dataflow/marketing-automation.md).
