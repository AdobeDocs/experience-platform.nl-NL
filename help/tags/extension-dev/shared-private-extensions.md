---
title: Gedeelde persoonlijke extensiepakketten
description: Leer hoe u persoonlijke extensiepakketten kunt delen in Adobe Experience Platform-tags.
source-git-commit: f45f58b4679b619708204cdb0c18174a4836ce8d
workflow-type: tm+mt
source-wordcount: '1167'
ht-degree: 0%

---

# Gedeelde extensiepakketten voor persoonlijke extensies

Adobe Experience Platform Tags bieden nu ondersteuning voor **[!UICONTROL Usage Authorizations]** , een krachtige functie waarmee u extensiepakketten van het type private veilig kunt delen met vertrouwde partners zonder deze openbaar te maken in de extensiecatalogus. Met deze functie wordt een veilige brug tussen organisaties gemaakt, zodat u elkaars aangepaste extensiecode kunt benutten en tegelijk uw privacy en controle over uw eigen oplossingen kunt behouden.

## Extensiepakketten delen met andere organisaties

>[!NOTE]
>
>Extensiepakketten moeten een privéversie of een openbare versie hebben om te kunnen worden gedeeld via [!UICONTROL Usage Authorizations] . Versies die zijn gemarkeerd als Beschikbaarheid voor Ontwikkeling komen niet in aanmerking voor delen en worden niet weergegeven in het vervolgkeuzemenu voor machtigingen. Dit geldt ook als een eerdere versie (bijvoorbeeld 1.0.0) al is gedeeld. Nieuwere versies (bijvoorbeeld 1.0.1) moeten ten minste privé zijn voordat ze door ontvangende organisaties kunnen worden geautoriseerd of geïnstalleerd.
>
>Alle richtlijnen voor het delen van extensiepakketten voor privéextensies zijn ook van toepassing als u deze pakketten later openbaar wilt maken. Dezelfde overwegingen met betrekking tot zichtbaarheid, versioning, beveiliging, compatibiliteit, ondersteuning en documentatie blijven relevant, ongeacht de beschikbaarheidsstatus van het pakket.

Zowel openbare als particuliere extensiepakketten kunnen via [!UICONTROL Usage Authorizations] worden gedeeld, hoewel er voor extensies in beschikbaarheid van ontwikkelaars geen machtigingen aan deze pakketten kunnen worden gekoppeld.

Organisaties ontwikkelen vaak gespecialiseerde extensies die zijn afgestemd op hun unieke zakelijke behoeften. Deze uitbreidingen kunnen merkgebonden logica, douaneintegratie, of gevoelige configuraties bevatten die niet openbaar zouden moeten worden gemaakt. De vergunningen van het gebruik lossen deze uitdaging door toe te laten:

- **Selectief delend**: Deel privé uitbreidingen slechts met vertrouwde op partnerorganisaties
- **Bewaarde privacy**: Houd gevoelige uitbreidingscode uit de openbare catalogus
- **Samenwerking ontwikkeling**: Laat vertrouwde op partners toe om van uw douaneoplossingen te profiteren
- **beheerde toegang**: handhaaf volledige controle over wie tot uw privé uitbreidingen toegang heeft en kan gebruiken

Bij het deelproces zijn twee belangrijke deelnemers betrokken:

1. **het Delen organisatie**: De organisatie die bezit en het privé uitbreidingspakket deelt
2. **Ontvangende organisatie**: De vertrouwde op organisatie die toegang tot de gedeelde uitbreiding krijgt

Wanneer een persoonlijke versie wordt gedeeld, krijgt de ontvangende organisatie toegang tot die specifieke versie, die tot een directe verbinding tussen de twee organisaties leidt. Als een nieuwere versie later privé wordt gemaakt, zal het ook aan de ontvangende organisatie beschikbaar zijn zonder extra stappen van hun te vereisen.

## Een gebruiksvergunning voor een extensiepakket maken

Als u een extensie wilt delen, navigeert u naar de gebruikersinterface voor gegevensverzameling en selecteert u **[!UICONTROL Tags]** in de linkernavigatie. Selecteer hier een bestaande eigenschap of maak een nieuwe eigenschap.

Wanneer u de gewenste eigenschap hebt geselecteerd of gemaakt, selecteert u **[!UICONTROL Extensions]** in de linkernavigatie en selecteert u vervolgens de tab **[!UICONTROL Usage Authorizations]** .

Hier ziet u een lijst met bestaande gedeelde machtigingen die in twee categorieën zijn ingedeeld:

- **Gedeeld met deze org**: Uitbreidingen die andere organisaties met u hebben gedeeld.
- **Gedeeld met andere organisaties**: Uitbreidingen die u met andere organisaties hebt gedeeld.

Selecteer **[!UICONTROL Add Authorization]**.

![&#x200B; Het tabblad [!UICONTROL Usage Authorizations] dat een lijst weergeeft met extensies die worden gedeeld met deze org, markeren [!UICONTROL Add Authorization]](../images/shared-extensions/add-authorization.png)

>[!IMPORTANT]
>
>U moet de eigenaar van de organisatie van het doel **`Organization ID`** verkrijgen. Organisaties kunnen niet op naam worden doorzocht.

Selecteer de extensies die u wilt delen in het vervolgkeuzemenu in **[!UICONTROL Extension]** . In de lijst worden extensies die eigendom zijn van uw organisatie, samen met de beschikbaarheidsstatus weergegeven. De uitbreidingen waarvan recentste versie in **de beschikbaarheid van de Ontwikkeling** is zullen niet in deze lijst verschijnen.

Voer vervolgens de id van de ontvangende organisatie in en selecteer **[!UICONTROL Save]** .

![&#x200B; De [!UICONTROL Create extension package usage authorization] -pagina waarop een geselecteerde extensie en een Adobe-organisatie-id worden weergegeven die is ingevoerd, wordt gemarkeerd [!UICONTROL Save]](../images/shared-extensions/save-authorization.png)

U keert terug naar het tabblad [!UICONTROL Usage Authorizations] waar u de extensie kunt zien in uw **[!UICONTROL Shared with other orgs]** -lijst. De status zal **wachten op Goedkeuring** tonen tot de ontvangende organisatie de vergunning goedkeurt, op welk punt het aan **Goedgekeurd** zal worden bijgewerkt.

![&#x200B; het [!UICONTROL Usage Authorizations] lusje dat een lijst van uitbreidingen toont die met andere organen worden gedeeld, die de nieuwe vergunning &#x200B;](../images/shared-extensions/new-authorization.png) benadrukken

>[!TIP]
>
>U kunt extensies ook rechtstreeks delen via **[!UICONTROL Extension Catalog]** door het menu (⋯) op de uitbreidingskaart te selecteren en vervolgens de optie voor delen te selecteren in het menu.

Wanneer een vergunning actief is, toont de gedeelde uitbreiding a ***delend*** badge in de catalogus erop wijst die het met andere organisaties wordt gedeeld.

![&#x200B; het [!UICONTROL Catalog] lusje dat de gedeelde uitbreiding met de badge &#x200B;](../images/shared-extensions/sharing-badge.png) toont

## Gedeelde extensies autoriseren en beheren

>[!NOTE]
>
>Als ontvangende organisatie kunt u gedeelde extensies alleen goedkeuren of afwijzen. U kunt de machtigingsdetails niet beheren of wijzigen, omdat deze worden beheerd door de organisatie die de machtiging deelt.

Als u een gedeelde extensie wilt autoriseren voor uw organisatie, navigeert u naar de gebruikersinterface voor gegevensverzameling en selecteert u **[!UICONTROL Tags]** in de linkernavigatie en selecteert u de eigenschap. Selecteer vervolgens **[!UICONTROL Extensions]** in de linkernavigatie en selecteer vervolgens de tab **[!UICONTROL Usage Authorizations]** .

U kunt een lijst van gedeelde uitbreidingen met inbegrip van die **zien die op Goedkeuring** in de **[!UICONTROL Shared with this org]** sectie wachten. Selecteer de extensie die u wilt goedkeuren en selecteer vervolgens **[!UICONTROL Approve]** .

![&#x200B; Het [!UICONTROL Usage Authorizations] lusje dat een lijst toont van uitbreidingen die met dit org met de uitbreiding worden gedeeld die op Goedkeuring wacht geselecteerd, benadrukkend [!UICONTROL Approve]](../images/shared-extensions/approve-authorization.png)

>[!NOTE]
>
>U kunt een aanvraag ook afwijzen op het tabblad **[!UICONTROL Usage Authorizations]** als de gedeelde extensie niet langer wordt vereist door uw organisatie.

Selecteer **[!UICONTROL OK]** in het dialoogvenster **[!UICONTROL Authorization Usages]** .

![&#x200B; Het dialoogvenster [!UICONTROL Authorization Usages] markeren [!UICONTROL OK]](../images/shared-extensions/confirmation.png)

U bent teruggekeerd aan het [!UICONTROL Usage Authorizations] lusje waar u de uitbreiding kunt zien nu een **Goedgekeurde** status toont.

![&#x200B; het [!UICONTROL Usage Authorizations] lusje dat een lijst van uitbreidingen toont die met deze org worden gedeeld, die de uitbreiding met Goedgekeurde status benadrukken &#x200B;](../images/shared-extensions/approved-authorization.png)

Zodra de vergunning wordt goedgekeurd, is de uitbreiding beschikbaar in uw catalogus en kan worden geïnstalleerd en worden gebruikt zoals om het even welke andere uitbreiding. De gedeelde uitbreiding toont a ***Ontvangend*** badge die op het wijst is een uitbreiding die aan u door een andere organisatie wordt gedeeld.

![&#x200B; het [!UICONTROL Catalog] lusje dat de gedeelde uitbreiding met &quot;Ontvangend&quot;badge &#x200B;](../images/shared-extensions/receiving-badge.png) toont

## Intrekking van vergunningen

Als de organisatie die eigenaar is, kunt u op elk gewenst moment een autorisatie verwijderen, ongeacht de huidige status (In afwachting van goedkeuring, Afgewezen of Goedgekeurd).

**als uw uitbreiding nooit openbaar werd gemaakt:**
- Alle privéversies die de ontvangende organisatie al heeft geïnstalleerd, blijven in de lijst met geïnstalleerde extensies staan.
- Als de ontvangende organisatie nooit uw uitbreiding heeft geïnstalleerd, zal het nergens meer in hun interface verschijnen.

**als uw uitbreiding openbaar werd gemaakt:**
- Elke privéversie die de ontvangende organisatie heeft geïnstalleerd, blijft zichtbaar in de lijst met geïnstalleerde extensies.
- Als zij uw privé versie nooit hebben geïnstalleerd, zullen zij nog de recentste openbare versie in hun catalogus zien en kunnen het installeren.
- Ze kunnen desgewenst ook van uw persoonlijke versie naar de meest recente openbare versie worden gedowngraded.

Wanneer u een vergunning intrekt, behoudt de ontvangende organisatie bepaalde rechten om hun bestaande implementaties te beschermen:

- **Vervolg gebruik**: De ontvangende organisatie kan het gebruiken van om het even welke privé versie houden zij reeds geïnstalleerd, zelfs nadat u toegang herroept.
- **bouwt bescherming**: Als de ontvangende organisatie uw privé v1.0.0 installeerde en u later privé v1.0.1 vrijgeeft, zullen zij niet de nieuwere versie zien maar kunnen blijven bouwen met v1.0.0 zonder verstoring.
- **Toekomstige verbeteringen**: Als u later uw uitbreiding openbaar maakt (bijvoorbeeld, die v2.0.0 openlijk vrijgeven), kan de ontvangende organisatie van hun privé v1.0.0 direct aan nieuw openbaar v2.0.0 bevorderen.

>[!IMPORTANT]
>
>Als u de autorisatie intrekt, worden bestaande builds of implementaties niet verbroken. Ontvangende organisaties handhaven toegang tot om het even welke privé versies die zij reeds hebben geïnstalleerd om bedrijfscontinuïteit te verzekeren.

## Volgende stappen

In dit document wordt getoond hoe u de functie voor gedeelde extensies in Experience Platform kunt gebruiken. Voor informatie over uitbreidingsontwikkeling, zie de [&#x200B; gids van de gebruiker van de uitbreidingsontwikkeling &#x200B;](./getting-started.md).

Voor een overzicht op hoog niveau van uitbreidingsontwikkeling in Experience Platform, verwijs naar de [&#x200B; overzichtsdocumentatie &#x200B;](./overview.md).
