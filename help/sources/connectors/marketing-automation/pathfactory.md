---
title: Overzicht van PathFactory Source
description: Leer hoe u PathFactory via API's of de gebruikersinterface met Adobe Experience Platform kunt verbinden.
last-substantial-update: 2024-04-30T00:00:00Z
exl-id: befb73c4-fd6a-4512-9124-d23a1c27e0e0
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 0%

---

# [!DNL PathFactory]

[[!DNL PathFactory] ](https://www.pathfactory.com/) biedt een cloudplatform dat bedrijven helpt bij het beheren van inhoudsreizen en het aansturen van betrokkenheid via intelligente inzichten in inhoud. In deze handleiding wordt beschreven hoe u gegevens van PathFactory kunt integreren in Experience Platform en de connectors van PathFactory kunt gebruiken voor optimale gegevensinvoer.

U kunt gegevens van [[!DNL PathFactory] ](https://www.pathfactory.com/) opnemen gebruikend drie primaire bronnen:

* **[!DNL Visitors]**: Vermeld de gegevens van de klant en neem contact op als verslagen om uw publiek beter te begrijpen.
* **[!DNL Sessions]**: Gebeurtenissen uit de tijdreeks die afzonderlijke gebruikerssessieactiviteiten op uw platform bijhouden.
* **[!DNL Page Views]**: Gebeurtenissen uit de tijdreeks die inzicht verschaffen in welke pagina&#39;s worden weergegeven, zodat u de prestaties van de inhoud kunt analyseren.

Lees het onderstaande document voor informatie over hoe u uw [!DNL PathFactory] bronaccount kunt instellen.

## IP adres lijst van gewenste personen {#ip-allow-list}

U moet gebied-specifieke IP adressen aan uw lijst van gewenste personen toevoegen alvorens uw bronnen aan Experience Platform aan te sluiten. Voor meer informatie, lees de gids op [ voegend op lijst van gewenste personen IP adressen om met Experience Platform ](../../ip-address-allow-list.md) voor meer informatie te verbinden.

## Vereisten {#prerequisites}

Voordat u begint met het integreren van [[!DNL PathFactory] ](https://www.pathfactory.com/) -connectors met Experience Platform, moet u aan de volgende voorwaarden voldoen:

* **a [ rekening PathFactory]**.
   * Neem contact op met [[!DNL PathFactory] ](https://www.pathfactory.com/portal/company/contactus.shtml) als u nog geen geldig account hebt.
* **een actief abonnement** aan om het even welk [!DNL PathFactory] product.
* **Gebruikersnaam, wachtwoord, en domein**.
   * Deze referenties zijn vereist voor toegang tot uw [!DNL PathFactory] -account en de bijbehorende gegevens.
* **Symbolische Eindpunten van de Toegang** en **API**.
   * Deze zijn nodig om verbinding te maken met [!DNL PathFactory] API&#39;s.

### Hoe te om Verantwoordelijkheden en de Tokens van de Toegang te verkrijgen {#gather-credentials}

Als u [!DNL PathFactory] wilt verbinden met Experience Platform, moet u de volgende referenties opgeven:

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

U moet zowel **[!UICONTROL View Sources]** - als **[!UICONTROL Manage Sources]** -machtigingen hebben ingeschakeld voor uw account om uw [!DNL PathFactory] -account te kunnen verbinden met Experience Platform. Neem contact op met de productbeheerder om de benodigde machtigingen te verkrijgen. Voor meer informatie, lees de [ gids UI van de toegangscontrole ](../../../access-control/ui/overview.md).

## Verbinden [!DNL PathFactory] met Experience Platform {#pathfactory-connect}

In de onderstaande documentatie vindt u informatie over het tot stand brengen van een verbinding tussen [!DNL PathFactory] en Experience Platform via API&#39;s of de gebruikersinterface:

* [ creeer een bronverbinding en dataflow om  [!DNL PathFactory]  gegevens aan Experience Platform te brengen gebruikend APIs ](../../tutorials/api/create/marketing-automation/pathfactory.md).
* [ verbind uw  [!DNL PathFactory]  rekening met Experience Platform gebruikend UI ](../../tutorials/ui/create/marketing-automation/pathfactory.md).
* [ creeer een dataflow voor een bronverbinding gebruikend UI ](../../tutorials/ui/dataflow/marketing-automation.md).
