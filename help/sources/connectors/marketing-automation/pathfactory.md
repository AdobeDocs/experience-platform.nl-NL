---
title: Overzicht van bron van PathFactory
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
>De [!DNL PathFactory] De bron is in bèta. Lees de [overzicht van bronnen](../../home.md#terms-and-conditions) voor meer informatie over het gebruik van bronnen met een bètalabel.

[[!DNL PathFactory]](https://www.pathfactory.com/) biedt een op de cloud gebaseerd platform dat bedrijven helpt bij het beheren van inhoudsreizen en het aansturen van betrokkenheid via intelligente inzichten in inhoud. Deze gids bepaalt hoe u gegevens van PathFactory in Experience Platform kunt integreren, gebruikend de schakelaars van PathFactory voor optimale gegevensopname.

U kunt gegevens invoeren van [[!DNL PathFactory]](https://www.pathfactory.com/) gebruik van drie primaire bronnen:

* **[!DNL Visitors]**: Voeg klanten en contactgegevens toe als verslagen om uw publiek beter te begrijpen.
* **[!DNL Sessions]**: De gebeurtenissen van de tijdreeks die de individuele activiteiten van de gebruikerszitting op uw platform volgen.
* **[!DNL Page Views]**: Gebeurtenissen uit tijdreeksen die inzicht verschaffen in welke pagina&#39;s worden weergegeven, zodat u de prestaties van de inhoud kunt analyseren.

Lees het onderstaande document voor meer informatie over het instellen van uw [!DNL PathFactory] bronaccount.

## IP adres lijst van gewenste personen {#ip-allow-list}

Een lijst van IP adressen kan vereisen om aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de [IP adres lijst van gewenste personen](../../ip-address-allow-list.md) voor meer informatie.

## Vereisten {#prerequisites}

Voordat u begint met integreren [[!DNL PathFactory]](https://www.pathfactory.com/) De schakelaars met Experience Platform, verzekeren u aan de volgende eerste vereisten voldoet:

* **A [PathFactory-account]**.
   * Contact [[!DNL PathFactory]](https://www.pathfactory.com/portal/company/contactus.shtml) als u nog geen geldige account hebt.
* **Een actief abonnement** aan [!DNL PathFactory] product.
* **Gebruikersnaam, wachtwoord en domein**.
   * Deze referenties zijn vereist voor toegang tot uw [!DNL PathFactory] en de gegevens ervan.
* **Toegangstoken** en **API-eindpunten**.
   * Deze zijn nodig om verbinding te maken met [!DNL PathFactory] API&#39;s.

### Hoe te om Verantwoordelijkheden en de Tokens van de Toegang te verkrijgen {#gather-credentials}

Verbinding maken [!DNL PathFactory] aan Experience Platform, moet u de volgende geloofsbrieven verstrekken:

| Credentials | Beschrijving | Endpoint |
| --- | --- | --- |
| Gebruikersnaam | Uw [!DNL PathFactory] gebruikersnaam account. | Niet van toepassing |
| Wachtwoord | Uw [!DNL PathFactory] wachtwoord account. | Niet van toepassing |
| Domein | Het domein dat aan uw [!DNL PathFactory] account. | Niet van toepassing |
| Toegangstoken | Een uniek token dat wordt gebruikt voor API-verificatie. | Niet van toepassing |
| Eindpunt van bezoekers | Het API-eindpunt voor bezoekersgegevens. | `/api/public/v3/data_lake_apis/visitors.json` |
| Sessieeindpunt | Het API-eindpunt voor sessiegegevens. | `/api/public/v3/data_lake_apis/sessions.json` |
| Eindpunt van paginaweergaven | Het API-eindpunt voor paginaweergavegegevens. | `/api/public/v3/data_lake_apis/page_views.json` |

Ga voor gedetailleerde instructies over het verkrijgen van uw gebruikersnaam, wachtwoord, domein en toegangstoken naar de [[!DNL PathFactory] Ondersteuningscentrum](https://support.pathfactory.com/categories/adobe/). Deze bron bevat uitgebreide handleidingen voor het ophalen en beheren van uw referenties.

### Machtigingen configureren voor Experience Platform

U moet beide hebben **[!UICONTROL View Sources]** en **[!UICONTROL Manage Sources]** machtigingen die zijn ingeschakeld voor uw account om verbinding te maken met uw [!DNL PathFactory] aan Experience Platform. Neem contact op met de productbeheerder om de benodigde machtigingen te verkrijgen. Lees voor meer informatie de [gebruikershandleiding voor toegangsbeheer](../../../access-control/ui/overview.md).

## Verbinden [!DNL PathFactory] naar platform {#pathfactory-connect}

In de onderstaande documentatie vindt u informatie over de verbinding [!DNL PathFactory] naar Platform met API&#39;s of de gebruikersinterface:

* [Een bronverbinding en gegevensstroom maken voor [!DNL PathFactory] gegevens naar platform met API&#39;s](../../tutorials/api/create/marketing-automation/pathfactory.md).
* [Verbind uw [!DNL PathFactory] account aan Experience Platform met behulp van de gebruikersinterface](../../tutorials/ui/create/marketing-automation/pathfactory.md).
* [Een gegevensstroom maken voor een bronverbinding met behulp van de gebruikersinterface](../../tutorials/ui/dataflow/marketing-automation.md).
