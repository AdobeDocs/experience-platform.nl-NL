---
solution: Experience Platform
title: Toegang verkrijgen en verlenen voor Experience Platform-dashboards
type: Documentation
description: Gebruikers de mogelijkheid bieden om Experience Platform-dashboards te bekijken, te bewerken en bij te werken met Adobe Admin Console.
exl-id: 2e50790f-b3ab-4851-a9a5-7cb98bf98ce3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 5%

---

# Toegangsmachtigingen voor dashboards

Als u gebruikers de mogelijkheid wilt geven om dashboards weer te geven, te bewerken en bij te werken, moet u eerst machtigingen inschakelen. In Adobe Experience Platform, wordt de toegangscontrole verstrekt door [&#x200B; Adobe Admin Console &#x200B;](https://adminconsole.adobe.com/). Gebruikers worden via productprofielen in de [!DNL Admin Console] gekoppeld aan machtigingen en sandboxen.

Dit document bevat een overzicht van de beschikbare machtigingen voor dashboards, inclusief de functies die ze kunnen gebruiken en de gebruikersfuncties die ze kunnen inschakelen. Voor gedetailleerde informatie bij het verkrijgen van en het toewijzen van toegangstoestemmingen, gelieve te beginnen door het [&#x200B; overzicht van de toegangscontrole &#x200B;](../access-control/home.md) te lezen.

## Vereisten

Als u toegangsbeheer voor [!DNL Experience Platform] wilt configureren, moet u beheerdersrechten hebben voor een organisatie die een [!DNL Experience Platform] -productintegratie heeft. Zie het artikel van het Centrum van de Hulp van Adobe op [&#x200B; administratieve rollen &#x200B;](https://helpx.adobe.com/nl/enterprise/using/admin-roles.html) voor meer informatie.

## Beschikbare dashboardmachtigingen {#available-permissions}

De service [!DNL Dashboards] biedt drie machtigingen die, wanneer ze worden gecombineerd, volledige toegang bieden tot de dashboards [!UICONTROL Profiles] , [!UICONTROL Segments] , [!UICONTROL Destinations] en [!UICONTROL License Usage] in Adobe Experience Platform. Deze machtigingen zijn:

| Machtiging | Beschrijving |
|---|---|
| **beheert Standaard dashboards** | Deze toestemming is a **globale lees en schrijf toestemmingen**. Het staat u toe om douane widgets [&#128279;](./customize/custom-widgets.md) tot stand te brengen en [&#x200B; het widgetschema &#x200B;](./customize/edit-schema.md) door [!UICONTROL Widget library] uit te geven. |
| **Standaarddashboards van de Mening** | Dit verstrekt **read-only** functionaliteit voor [!UICONTROL Profiles], [!UICONTROL Destinations], en [!UICONTROL Segments] dashboards en verleent toegang tot hen door de linkernavigatie van Experience Platform. De code voegt ook [!UICONTROL Dashboards] toe aan de linkernavigatie en toegang tot het tabblad [!UICONTROL Dashboards] voorraad en integratie. |
| **Dashboard van het Gebruik van de Vergunning van de Mening** | Deze toestemming staat gebruikers **read-only** toegang toe tot [&#x200B; het dashboard van het vergunningsgebruik &#x200B;](./guides/license-usage.md) binnen Experience Platform UI. |

De categorie [!DNL Dashboard] bevat vijf machtigingen die mogelijk vereist zijn, afhankelijk van uw behoeften. In de volgende tabel worden de categorielocaties in de Admin Console weergegeven:

>[!IMPORTANT]
>
>Zowel **[!DNL Manage Standard Dashboards]** als **[!DNL View Standard Dashboards]** toestemmingen **vereisen** een &quot;mening&quot;of &quot;beheer&quot;toestemming van de [!DNL Profile Management] of [!DNL Destinations] categorie in Admin Console om de relevante secties binnen Experience Platform UI te activeren.

| Machtiging | Locatie van Admin Console-categorie |
|---|---|
| [!DNL View Profiles] | [!DNL Profile Management] |
| [!DNL View Segments] | [!DNL Profile Management] |
| [!DNL View Destinations] | [!DNL Destinations] |
| [!DNL Manage Queries] | [!DNL Query Service] |
| [!DNL Manage Sandboxes] | [!DNL Sandbox Administration] |

## Toegangscontrolematrix

De volgende toegang-controle matrijs verstrekt een verdeling waarvan toestemmingen worden vereist en welke functie zij betreffende toegang tot de verschillende dashboardeigenschappen verstrekken. Machtigingen worden weergegeven in de bovenste horizontale rij en de gebruikersinterface van Experience Platform wordt weergegeven in de linkerkolom.

|   | [!UICONTROL View Standard Dashboard] OR [!UICONTROL Manage Standard Dashboard] | [!UICONTROL View Profiles], <br/>[!UICONTROL View Segments], <br/> [!UICONTROL View Destinations] | [!UICONTROL Manage Queries] &amp; [!UICONTROL Manage Sandboxes] | [!UICONTROL View License Usage Dashboard] |
|---|---|---|---|---|
| [!DNL Profiles], <br/>[!DNL Segments], <br/>[!DNL Destinations] in de linkernavigatie. | N.v.t. | **A &quot;Mening&quot;of &quot;leidt&quot;toestemming wordt VEREIST** voor elk respectieve dashboard. | N.v.t. | N.v.t. |
| [!DNL Dashboards] in de linkernavigatie. | INGESCHAKELD | **minstens één VEREIST**. | N.v.t. | N.v.t. |
| [!DNL Dashboards] [!DNL Inventory] <br/> (het tabblad Bladeren) | INGESCHAKELD | N.v.t. | N.v.t. | N.v.t. |
| [!DNL Dashboards] [!DNL Integrations] tab <br/> (wordt gebruikt om Power BI te installeren) | INGESCHAKELD | **minstens één VEREIST** | N.v.t. | N.v.t. |
| Power BI-knop Installeren en workflow | INGESCHAKELD | N.v.t. | **VEREIST** | N.v.t. |
| [!DNL Profiles], <br/>[!DNL Segments], <br/>[!DNL Destinations] dashboards.<br/> de capaciteit om widgetschema&#39;s uit te geven en nieuwe attributen voor widgetaanpassing toe te voegen | **beheer-norm-dashboard VEREIST** | **VEREIST (voor elk respectieve dashboard)** | N.v.t. | N.v.t. |
| [!DNL License Usage Dashboard] | N.v.t. | N.v.t. | N.v.t. | INGESCHAKELD |

{style="table-layout:auto"}

## Machtigingen toevoegen aan uw productprofiel

Met de bovenstaande informatie kunt u de juiste machtigingen aan het productprofiel toevoegen. Zie de documentatie voor volledige instructies op [&#x200B; hoe te om toestemmingen door de toegangscontrole UI &#x200B;](../access-control/ui/permissions.md) toe te voegen.

Voor beschrijvingen van de toestemmingen, gelieve te verwijzen naar de [&#x200B; beschikbare toestemmingensectie &#x200B;](#available-permissions) vroeger in dit document.

>[!NOTE]
>
>U hoeft niet alle machtigingen voor alle gebruikers in te schakelen. Afhankelijk van de structuur van uw organisatie kunt u verschillende productprofielen voor bepaalde gebruikers maken en beperkte toegang (zoals alleen-lezen) verlenen. Zie de documentatie bij het beheren van gebruikers voor een productprofiel om [&#x200B; te leren hoe te om toestemmingen voor specifieke gebruikers &#x200B;](../access-control/ui/users.md) toe te wijzen.

Zodra u de noodzakelijke toegangstoestemmingen hebt toegevoegd, kunnen de gebruikers binnen uw organisatie beginnen dashboards te bekijken binnen Experience Platform UI en andere acties uit te voeren die op de toestemmingen worden gebaseerd die u hebt toegewezen.
