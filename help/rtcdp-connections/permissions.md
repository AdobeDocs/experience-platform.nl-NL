---
title: Machtigingsbeheer voor gegevensverzameling in Experience Platform
description: Een overzicht op hoog niveau van hoe u machtigingen kunt beheren en de toegang tot functies in Real-time Customer Data Platform (RTCDP)-verbindingen kunt beheren.
source-git-commit: e0be090bfce602c7a6e22a1e4be187d4abdfd600
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 2%

---

# Machtigingsbeheer voor gegevensverzameling in Experience Platform

[Gegevensverzameling in Adobe Experience Platform](./home.md) bestaat uit verschillende technologieën die samenwerken om uw gegevens te verzamelen en over te dragen. De toegang tot deze technologieën wordt gecontroleerd door granulaire op rol-gebaseerde toestemmingen in Adobe Admin Console.

Deze gids toont u hoe te om toestemmingen voor de eigenschappen van de gegevensinzameling te beheren.

## Aan de slag

Om toegangsbeheer voor gegevensinzameling te vormen, moet u beheerdervoorrechten voor een organisatie hebben die een productintegratie met de Inzameling van Gegevens van Adobe Experience Platform heeft. De minimale rol die machtigingen kan verlenen of intrekken, is een beheerder van het productprofiel. Andere beheerdersrollen die machtigingen kunnen beheren, zijn productbeheerders (die alle profielen binnen een product kunnen beheren) en systeembeheerders (geen beperkingen). Zie het artikel over [administratieve taken](https://helpx.adobe.com/enterprise/using/admin-roles.html) in de Adobe Enterprise Administration guide voor meer informatie.

Deze gids veronderstelt u vertrouwd met basisconcepten van de Admin Console zoals productprofielen en hoe zij producttoestemmingen aan individuele gebruikers en groepen verlenen. Zie voor meer informatie de [Gebruikershandleiding voor Admin Consoles](https://helpx.adobe.com/enterprise/using/admin-console.html).

## Beschikbare machtigingen

De relevante toestemmingen voor de Inzameling van Gegevens worden verstrekt door twee productbenamingen in Admin Console: **Adobe Experience Platform** en **Adobe Experience Platform-gegevensverzameling**. In de volgende secties worden de machtigingen beschreven die onder elk product worden verleend, en worden beschrijvingen gegeven van de specifieke mogelijkheden waartoe deze toegang verlenen.

### Adobe Experience Platform-machtigingen

De toestemmingen onder Adobe Experience Platform omvatten toegang tot gegevensstromen, identiteiten, schema&#39;s, en zandbakken. Voor stappen voor het configureren van Adobe Experience Platform-machtigingen raadpleegt u de [gebruikershandleiding voor toegangsbeheer](../access-control/ui/overview.md).

| Categorie | Machtiging | Beschrijving |
| --- | --- | --- |
| Sandboxen | (N.v.t.) | Afhankelijk van de [sandboxen](../sandboxes/home.md) die onder uw organisatie zijn gecreeerd, kunt u toegang tot elk van hen door deze toestemmingencategorie in Admin Console controleren. |
| Gegevensmodellering | Schema&#39;s beheren | Biedt de mogelijkheid om te bekijken, maken en bewerken [XDM-schema&#39;s (Experience Data Model)](../xdm/home.md). |
| Gegevensmodellering | Schema&#39;s weergeven | Hiermee verleent u alleen-lezen toegang tot schema&#39;s. |
| Identity Management | Identiteitsnaamruimten beheren | Biedt de mogelijkheid om te bekijken, maken en bewerken [naamruimten](../identity-service/namespaces.md). |
| Identity Management | Identiteitsnaamruimten weergeven | Hiermee wordt alleen-lezen toegang verleend tot naamruimten. |
| Gegevensverzameling | Gegevensstromen beheren | Biedt de mogelijkheid om te bekijken, maken en bewerken [gegevensstromen](../edge/datastreams/overview.md). |
| Gegevensverzameling | Gegevensstromen weergeven | Biedt alleen-lezen toegang tot gegevensstreams. |

{style=&quot;table-layout:auto&quot;}

<!-- (Feature not yet available?)
| Dashboards | Manage Custom Dashboards | |
| Dashboards | View Custom Dashboards | |
-->

### Machtigingen voor Adobe Experience Platform-gegevensverzameling

Machtigingen onder Adobe Experience Platform Data Collection beheren toegang tot tags en mogelijkheden voor het doorsturen van gebeurtenissen, waaronder eigenschappen, extensies en omgevingen. Voor stappen op hoe te om de toestemmingen van de Inzameling van Gegevens van Adobe Experience Platform te vormen, zie [sectie hieronder](#manage).

| Categorie | Machtiging | Beschrijving |
| --- | --- | --- |
| Platforms | Web | Toegang tot [webeigenschappen](../tags/ui/administration/companies-and-properties.md) in combinatie met andere eigendomsrechten. |
| Platforms | Mobile | Toegang tot [mobiele eigenschappen](../tags/ui/administration/companies-and-properties.md) in combinatie met andere eigendomsrechten. |
| Properties | (N.v.t.) | Afhankelijk van de eigenschappen die onder uw organisatie zijn gecreeerd, kunt u toegang tot elk van hen door deze toestemmingscategorie in Admin Console controleren.<br><br>De toegewezen bezitsrechten van een gebruiker zijn slechts op de eigenschappen van toepassing zij toegang tot door deze toestemmingscategorie zijn verleend. |
| Eigendomsrechten | Goedkeuren | Biedt de mogelijkheid om een bibliotheekbuild goed te keuren als onderdeel van de [publicatiestroom](../tags/ui/publishing/publishing-flow.md). |
| Eigendomsrechten | Ontwikkelen | Biedt de mogelijkheid om een bibliotheekbuild te ontwikkelen als onderdeel van de [publicatiestroom](../tags/ui/publishing/publishing-flow.md). |
| Eigendomsrechten | Eigenschap bewerken | Biedt de mogelijkheid om de basisconfiguratie te bewerken voor de eigenschappen waartoe een gebruiker toegang heeft. |
| Eigendomsrechten | Omgevingen beheren | Biedt de mogelijkheid om de [omgevingen](../tags/ui/publishing/environments.md) voor de eigenschappen waartoe een gebruiker toegang heeft. |
| Eigendomsrechten | Extensies beheren | Biedt de mogelijkheid om de [extensions](../tags/ui/managing-resources/extensions/overview.md) voor de eigenschappen waartoe een gebruiker toegang heeft. |
| Eigendomsrechten | Publicatie | Biedt de mogelijkheid om een bibliotheekbuild te publiceren als onderdeel van de [publicatiestroom](../tags/ui/publishing/publishing-flow.md). |
| Bedrijfsrechten | Extensies ontwikkelen | Biedt de mogelijkheid extensiepakketten te maken en te wijzigen die eigendom zijn van uw organisatie, inclusief persoonlijke releases en verzoeken om openbare release. |
| Bedrijfsrechten | Extensies beheren | Deze machtiging is alleen van toepassing als u een licentie voor Adobe Journey Optimizer hebt of een andere oplossing die toegang biedt tot mobiele berichten in de app en via pushberichten. Op deze manier kunt u de apps beheren die Adobe Experience Cloud kent, samen met de vereiste pushgegevens die nodig zijn om te communiceren met de Firebase Cloud Messaging-service en de Apple Push Notification-service. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Voor meer informatie over hoe deze toestemmingen mogelijkheden in markeringen beïnvloeden, met inbegrip van beleidsstrategieën voor gemeenschappelijke scenario&#39;s, zie de tagdocumentatie op [gebruikersmachtigingen](../tags/ui/administration/user-permissions.md).

## Rechten voor Adobe Experience Platform-gegevensverzameling beheren {#manage}

>[!IMPORTANT]
>
>Deze sectie behandelt slechts hoe te om toestemmingen voor het product van de Gegevensverzameling van Adobe Experience Platform in Admin Console te beheren. De stappen voor het beheer van machtigingen onder het Adobe Experience Platform-product zijn echter vergelijkbaar.
>
>Zie de [gebruikershandleiding voor toegangsbeheer](../access-control/ui/overview.md) voor gedetailleerde instructies over het beheren van Platform toestemmingen. Afhankelijk van product SKUs uw organisatie toegang tot heeft, kunt u niet elke toestemming hebben beschikbaar aan u.

Om toestemmingen voor de Inzameling van Gegevens te beheren, login aan [Admin Console](https://adminconsole.adobe.com/) en selecteert u **[!UICONTROL Products]** in de bovenste navigatie. Selecteer hier de kaart voor **[!UICONTROL Adobe Experience Platform Data Collection]**.

![Afbeelding die de productkaart voor gegevensverzameling in Admin Console weergeeft](./images/permissions/data-collection-card.png)

### Een productprofiel selecteren of maken

In het volgende scherm wordt een lijst weergegeven met beschikbare productprofielen voor gegevensverzameling onder uw organisatie, waarbij het standaardprofiel **[!DNL Default Data Collection All Access]**. U kunt desgewenst het standaardproductprofiel bewerken of u kunt **[!UICONTROL New Profile]** om er een te maken. Als u veelvoudige rollen of gebruikersgroepen in uw organisatie hebt die verschillende niveaus van toegang vereisen, zou u een afzonderlijk productprofiel voor elk van hen moeten creëren.

![Afbeelding met de productprofielen voor gegevensverzameling in Admin Console](./images/permissions/new-profile.png)

Nadat u een productprofiel hebt geselecteerd of gemaakt, kunt u de opdracht **[!UICONTROL Edit]** Te starten pictogrammen [bewerken, machtigingen](#edit-permissions) voor het profiel, of selecteer **[!UICONTROL Users]** te beginnen tab [gebruikers toewijzen](#assign-users) naar het profiel.

![Afbeelding met het tabblad Machtigingen voor een Admin Console met productprofielen](./images/permissions/edit-permission-categories.png)

### Machtigingen voor het productprofiel bewerken {#edit-permissions}

Wanneer u machtigingen voor een profiel bewerkt, worden in de linkerkolom de beschikbare machtigingen vermeld, terwijl de machtigingen die in het profiel zijn opgenomen in de rechterkolom worden weergegeven. Selecteer de vermelde toestemmingen om hen tussen één van beide kolom te bewegen.

![Afbeelding met machtigingen die zijn toegevoegd onder de meegeleverde kolom](./images/permissions/added-permissions.png)

Machtigingen zijn ingedeeld in categorieën. Als u wilt schakelen tussen categorieën, selecteert u de gewenste categorie in de linkernavigatie.

![Afbeelding met de sectie bedrijfsrechten onder machtigingen](./images/permissions/switch-category.png)

Selecteren **[!UICONTROL Save]** zodra u klaar bent met het configureren van machtigingen.

![Afbeelding met de machtigingsconfiguratie die wordt opgeslagen voor het productprofiel](./images/permissions/save-permissions.png)

De weergave van het productprofiel wordt opnieuw weergegeven met de toegevoegde machtigingen weergegeven.

![Afbeelding met de toegevoegde machtigingen voor het productprofiel](./images/permissions/permissions-added.png)

### Gebruikers toewijzen aan het productprofiel {#assign-users}

Als u gebruikers wilt toewijzen aan het productprofiel (en hun de geconfigureerde machtigingen van het profiel wilt verlenen), selecteert u de optie **[!UICONTROL Users]** tab, gevolgd door **[!UICONTROL Add user]**.

![Afbeelding die het tabblad Gebruikers voor een productprofiel in Admin Console weergeeft](./images/permissions/manage-users.png)

Voor meer informatie over het beheren van gebruikers voor een productprofiel raadpleegt u de [Documentatie Admin Console](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html).

## Volgende stappen

Deze gids behandelde de beschikbare toestemmingen voor de Inzameling van Gegevens UI en hoe te om hen door Admin Console te beheren. Raadpleeg voor meer informatie over het beheren van machtigingen voor andere Adobe Experience Platform-mogelijkheden de [toegangsbeheerdocumentatie](../access-control/home.md).
