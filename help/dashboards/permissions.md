---
solution: Experience Platform
title: Toegang voor dashboards van Experience Platforms verkrijgen en verlenen
type: Documentation
description: Gebruikers de mogelijkheid bieden om dashboards van Experience Platforms weer te geven, te bewerken en bij te werken met Adobe Admin Console.
exl-id: 2e50790f-b3ab-4851-a9a5-7cb98bf98ce3
source-git-commit: 052e365c6127961363b7b5333cb0f4f82ab5479a
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 6%

---

# Toegangsmachtigingen voor dashboards

Als u gebruikers de mogelijkheid wilt geven om dashboards weer te geven, te bewerken en bij te werken, moet u eerst machtigingen inschakelen. In Adobe Experience Platform wordt toegangsbeheer geboden via de [Adobe Admin Console](https://adminconsole.adobe.com/). Gebruikers kunnen via de productprofielen in de [!DNL Admin Console].

Dit document bevat een overzicht van de beschikbare machtigingen voor dashboards, inclusief de functies die ze kunnen gebruiken en de gebruikersfuncties die ze kunnen inschakelen. Voor gedetailleerde informatie over het verkrijgen en toewijzen van toegangsmachtigingen, begint u met het lezen van de [toegangsbeheeroverzicht](../access-control/home.md).

## Vereisten

Om toegangsbeheer voor te vormen [!DNL Experience Platform], moet u beheerdersrechten hebben voor een organisatie die een [!DNL Experience Platform] productintegratie. Zie het Adobe Help Center-artikel op [administratieve taken](https://helpx.adobe.com/enterprise/using/admin-roles.html) voor meer informatie .

## Beschikbare dashboardmachtigingen {#available-permissions}

De [!DNL Dashboards] de dienst verleent drie toestemmingen die, wanneer gecombineerd, volledige toegang tot [!UICONTROL Profiles], [!UICONTROL Segments], [!UICONTROL Destinations], en [!UICONTROL Licence Usage] dashboards in Adobe Experience Platform. Deze machtigingen zijn:

| Machtiging | Beschrijving |
|---|---|
| **Standaarddashboards beheren** | Deze machtiging is **algemene lees- en schrijfmachtigingen**. Hiermee kunt u [aangepaste widgets maken](./customize/custom-widgets.md) en [Het widgetschema bewerken](./customize/edit-schema.md) via de [!UICONTROL Widget library]. |
| **Standaarddashboards weergeven** | Dit biedt **alleen-lezen** functionaliteit voor de [!UICONTROL Profiles], [!UICONTROL Destinations], en [!UICONTROL Segments] dashboards en verleent toegang tot hen door de linkernavigatie van het Platform. Het voegt er ook aan toe [!UICONTROL Dashboards] aan de linkernavigatie en toegang tot [!UICONTROL Dashboards] tabblad Overzicht en integratie. |
| **Licentieverbruikdashboard weergeven** | Met deze machtiging kunnen gebruikers **alleen-lezen** toegang tot [het licentiegebruiksdashboard](./guides/license-usage.md) in de interface van het Experience Platform. |

Er zijn vijf machtigingen die niet zijn opgenomen in het dialoogvenster [!DNL Dashboard] rubriek die mogelijk vereist is, afhankelijk van uw behoeften. In de volgende tabel worden de categorielocaties in de Admin Console weergegeven:

>[!IMPORTANT]
>
>Beide **[!DNL Manage Standard Dashboards]** en de **[!DNL View Standard Dashboards]** machtigingen **vereisen** een machtiging &quot;view&quot; of &quot;manage&quot; van de [!DNL Profile Management] of [!DNL Destinations] in de Admin Console om de desbetreffende secties in de gebruikersinterface van het Platform te activeren.

| Machtiging | Locatie van de categorie Admin Console |
|---|---|
| [!DNL View Profiles] | [!DNL Profile Management] |
| [!DNL View Segments] | [!DNL Profile Management] |
| [!DNL View Destinations] | [!DNL Destinations] |
| [!DNL Manage Queries] | [!DNL Query Service] |
| [!DNL Manage Sandboxes] | [!DNL Sandbox Administration] |

## Toegangsbeheermatrix

De volgende toegang-controle matrijs verstrekt een verdeling waarvan toestemmingen worden vereist en welke functie zij betreffende toegang tot de verschillende dashboardeigenschappen verstrekken. De toestemmingen zijn vermeld over de hoogste horizontale rij en de werkruimte UI van het Platform is vermeld langs de linkerkolom.

|  | [!UICONTROL View Standard Dashboard] OF [!UICONTROL Manage Standard Dashboard] | [!UICONTROL View Profiles],<br/>[!UICONTROL View Segments],<br/> [!UICONTROL View Destinations] | [!UICONTROL Manage Queries] &amp; [!UICONTROL Manage Sandboxes] | [!UICONTROL View License Usage Dashboard] |
|---|---|---|---|---|
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] in de linkernavigatie. | N.v.t. | **De machtiging Weergeven of Beheren is vereist.** voor elk respectieve dashboard. | N.v.t. | N.v.t. |
| [!DNL Dashboards] in de linkernavigatie. | INGESCHAKELD | **Ten minste één VEREIST**. | N.v.t. | N.v.t. |
| [!DNL Dashboards] [!DNL Inventory] <br/>(het tabblad Bladeren) | INGESCHAKELD | N.v.t. | N.v.t. | N.v.t. |
| [!DNL Dashboards] [!DNL Integrations] tab <br/>(wordt gebruikt om Power BI te installeren) | INGESCHAKELD | **Ten minste één VEREIST** | N.v.t. | N.v.t. |
| Knop Power BI installeren en workflow | INGESCHAKELD | N.v.t. | **VEREIST** | N.v.t. |
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] dashbaords.<br/>De mogelijkheid om widgetschema&#39;s te bewerken en nieuwe kenmerken toe te voegen voor widgetaanpassing | **Standaard dashboard beheren vereist** | **VEREIST (voor elk respectieve dashboard)** | N.v.t. | N.v.t. |
| [!DNL License Usage Dashboard] | N.v.t. | N.v.t. | N.v.t. | INGESCHAKELD |

{style=&quot;table-layout:auto&quot;}

## Machtigingen toevoegen aan uw productprofiel

Met de bovenstaande informatie kunt u de juiste machtigingen aan het productprofiel toevoegen. Zie de documentatie voor volledige instructies op [hoe te om toestemmingen door de toegangscontrole UI toe te voegen](../access-control/ui/permissions.md).

Voor een beschrijving van de machtigingen raadpleegt u de [beschikbare machtigingen](#available-permissions) in dit document.

>[!NOTE]
>
>U hoeft niet alle machtigingen voor alle gebruikers in te schakelen. Afhankelijk van de structuur van uw organisatie kunt u verschillende productprofielen voor bepaalde gebruikers maken en beperkte toegang (zoals alleen-lezen) verlenen. Raadpleeg de documentatie over het beheren van gebruikers voor een productprofiel voor meer informatie [hoe te om toestemmingen voor specifieke gebruikers toe te wijzen](../access-control/ui/users.md).

Zodra u de noodzakelijke toegangstoestemmingen hebt toegevoegd, kunnen de gebruikers binnen uw organisatie beginnen om dashboards binnen het Experience Platform UI te bekijken en andere acties uit te voeren die op de toestemmingen worden gebaseerd die u hebt toegewezen.
