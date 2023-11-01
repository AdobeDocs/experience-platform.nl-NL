---
title: (Bèta) De handelsbank - CRM-verbinding
description: Activeer profielen aan uw rekening van het Bureau van de Handel voor publiek gericht en onderdrukking die op de gegevens van CRM wordt gebaseerd.
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1114'
ht-degree: 0%

---

# (bèta) De [!DNL Trade Desk] - CRM-verbinding

>[!IMPORTANT]
>
>[!DNL The Trade Desk - CRM] Doel in Platform is momenteel in bèta. De documentatie en functionaliteit kunnen worden gewijzigd.
>
>Met de release van EUID (European Unified ID) ziet u nu twee [!DNL The Trade Desk - CRM] bestemmingen in de [doelcatalogus](/help/destinations/catalog/overview.md).
>* Als u gegevens in de EU verzamelt, moet u de **[!DNL The Trade Desk - CRM (EU)]** bestemming.
>* Als u gegevens in de APAC- of NAMER-gebieden bront, gebruikt u de **[!DNL The Trade Desk - CRM (NAMER & APAC)]** bestemming.
>
>Beide bestemmingen in Experience Platform zijn momenteel in bèta. Deze bestemmingsschakelaar en documentatiepagina worden gecreeerd en gehandhaafd door *[!DNL Trade Desk]* team. Neem contact op met uw [!DNL Trade Desk] de documentatie en de functionaliteit kunnen worden gewijzigd.

## Overzicht {#overview}

Dit document is ontworpen om u te helpen profielen te activeren voor uw [!DNL Trade Desk] account voor doelgroepen en suppressie op basis van CRM-gegevens.

[!DNL The Trade Desk(TTD)] het uploadbestand van e-mailadressen op geen enkel moment rechtstreeks afhandelt, en [!DNL The Trade Desk] sla je onbewerkte e-mails (zonder hashing) op.

>[!TIP]
>
>Gebruiken [!DNL The Trade Desk] CRM-bestemmingen voor CRM-gegevenstoewijzing, zoals e-mailadres of hashed-e-mailadres. Gebruik de [andere bestemming van de handelsbank](/help/destinations/catalog/advertising/tradedesk.md) in de Adobe Experience Platform-catalogus voor cookies en toegewezen apparaat-id.

## Vereisten {#prerequisites}

Voordat u het publiek kunt activeren op [!DNL The Trade Desk], moet u contact opnemen met uw [!DNL The Trade Desk] accountmanager om het CRM-instapcontract te ondertekenen. [!DNL The Trade Desk] zal dan toestemming geven en uw adverteerder identiteitskaart delen om uw bestemming te vormen.

## Vereisten voor ID-afstemming {#id-matching-requirements}

Afhankelijk van het type id&#39;s dat u in Adobe Experience Platform invoert, moet u aan de desbetreffende vereisten voldoen. Lees de [Overzicht van naamruimte van id](/help/identity-service/namespaces.md) voor meer informatie .

## Ondersteunde identiteiten {#supported-identities}

[!DNL The Trade Desk] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](/help/identity-service/namespaces.md).

Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-e-mailadressen met hashing. Volg de instructies in de sectie met vereisten voor id-afstemming en gebruik de juiste naamruimten voor normale tekst en gehashte e-mailadressen.

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| Email | E-mailadressen (tekst wissen) | Invoer `email` als de doelidentiteit wanneer uw bronidentiteit een e-mailnaamruimte of attribuut is. |
| Email_LC_SHA256 | E-mailadressen moeten worden gehasht met behulp van SHA256 en verlaagd. Zorg ervoor dat u alle [e-mailnormalisatie](https://github.com/UnifiedID2/uid2docs/tree/main/api#email-address-normalization) vereiste regels. U kunt deze instelling later niet wijzigen. | Invoer `hashed_email` als de doelidentiteit wanneer uw bronidentiteit een naamruimte of attribuut Email_LC_SHA256 is. |

{style="table-layout:auto"}

## E-mailhashingvereisten {#hashing-requirements}

U kunt e-mailadressen hashen alvorens hen in Adobe Experience Platform op te nemen of onbewerkte e-mailadressen gebruiken.

Als u meer wilt weten over het invoeren van e-mailadressen in Experience Platform, leest u de [overzicht van batch-opname](/help/ingestion/batch-ingestion/overview.md).

Als u ervoor kiest om de e-mailadressen zelf te hashen, moet u aan de volgende vereisten voldoen:

* Voorloopspaties en volgspaties verwijderen.
* Zet alle ASCII-tekens om in kleine letters.
* In `gmail.com` e-mailadressen, verwijder de volgende karakters uit het gebruikersnaaddeel van het e-mailadres:
   * De periode (. (ASCII-code 46). U kunt bijvoorbeeld normaliseren `jane.doe@gmail.com` tot `janedoe@gmail.com`.
   * Het plusteken (+ (ASCII-code 43)) en alle daaropvolgende tekens. U kunt bijvoorbeeld normaliseren `janedoe+home@gmail.com` tot `janedoe@gmail.com`.

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (e-mail of gehashte e-mail) die worden gebruikt in de bestemming Handelsbureau. |
| Exportfrequentie | **[!UICONTROL Daily Batch]** | Aangezien een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, wordt het profiel (identiteiten) één keer per dag bijgewerkt stroomafwaarts aan het bestemmingsplatform. Meer informatie over [batchexport](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

### Verifiëren voor doel {#authenticate}

[!DNL The Trade Desk] CRM-bestemming is een dagelijkse bestandsupload waarvoor geen verificatie door de gebruiker is vereist.

### Bestemmingsdetails invullen {#fill-in-details}

Voordat u publieksgegevens naar een doel kunt verzenden of activeren, moet u een verbinding met uw eigen doelplatform instellen. while [opzetten](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html) voor deze bestemming moet u de volgende informatie opgeven:

* **[!UICONTROL Account Type]**: Kies de optie **[!UICONTROL Existing Account]** -optie.
* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst wilt herkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Advertiser ID]**: uw [!DNL Trade Desk Advertiser ID], die door uw [!DNL Trade Desk] Accountmanager of gevonden onder [!DNL Advertiser Preferences] in de [!DNL Trade Desk] UI.

![Platform UI het schermschot die tonen hoe te om bestemmingsdetails in te vullen.](/help/destinations/assets/catalog/advertising/tradedesk/configuredestination2.png)

Wanneer u verbinding maakt met de bestemming, is het instellen van een beleid voor gegevensbeheer volledig optioneel. Controleer het Experience Platform [gegevensbeheer - overzicht](/help/data-governance/policies/overview.md) voor meer informatie .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.
>* Om te exporteren *identiteiten*, hebt u de **[!UICONTROL View Identity Graph]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). <br> ![Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren."){width="100" zoomable="yes"}

Lezen [publieksgegevens activeren om exportdoelen voor batchprofielen te activeren](/help/destinations/ui/activate-batch-profile-destinations.md) voor instructies voor het activeren van het publiek naar een bestemming.

In de **[!UICONTROL Scheduling]** pagina, kunt u het programma en de dossiernamen voor elk publiek vormen u uitvoert. Het is verplicht het schema te configureren, maar het configureren van de bestandsnaam is optioneel.

![Platform UI screenshot om publieksactivering te plannen.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment1.png)

>[!NOTE]
>
>Alle soorten publiek geactiveerd voor [!DNL The Trade Desk] De Bestemming van CRM wordt automatisch geplaatst aan een dagelijkse frequentie en volledige dossieruitvoer.

![Platform UI screenshot om publieksactivering te plannen.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment2.png)

In de **[!UICONTROL Mapping]** pagina, moet u attributen of identiteitsnamespaces van de bronkolom en kaart aan de doelkolom selecteren.

![Platform UI-screenshot om publieksactivering in kaart te brengen.](/help/destinations/assets/catalog/advertising/tradedesk/mappingsegment1.png)

Hieronder ziet u een voorbeeld van correcte identiteitstoewijzing bij het activeren van het publiek naar [!DNL The Trade Desk] CRM-bestemming.

>[!IMPORTANT]
>
> [!DNL The Trade Desk] CRM-bestemming accepteert geen onbewerkte en gehashte e-mailadressen als identiteiten in dezelfde activeringsstroom. Maak afzonderlijke activeringsstromen voor onbewerkte en gehashte e-mailadressen.

Bronvelden selecteren:

* Selecteer de `Email` naamruimte of attribuut als bronidentiteit als het onbewerkte e-mailadres wordt gebruikt bij het invoeren van gegevens.
* Selecteer de `Email_LC_SHA256` naamruimte of attribuut als bronidentiteit als u de e-mailadressen van de klant bij het invoeren van gegevens in Platform hebt gewijzigd.

Doelvelden selecteren:

* Invoer  `email` als doelidentiteit wanneer uw bronnaamruimte of -kenmerk `Email`.
* Invoer  `hashed_email` als doelidentiteit wanneer uw bronnaamruimte of -kenmerk `Email_LC_SHA256`.

## Gegevens exporteren valideren {#validate}

Om te controleren dat de gegevens correct uit Experience Platform en naar worden uitgevoerd [!DNL The Trade Desk], gelieve het publiek onder Adobe 1PD gegevensblok te vinden binnen [!DNL The Trade Desk] Data Management Platform (DMP). Hier volgen de stappen om de bijbehorende id te vinden in het dialoogvenster [!DNL Trade Desk] UI:

1. Klik eerst op de knop **[!UICONTROL Data]** Tab en revisie **[!UICONTROL First-Party]**.
2. Omlaag schuiven, onder **[!UICONTROL Imported Data]**, vindt u de **[!UICONTROL Adobe 1PD Tile]**.
3. Klik op de **[!UICONTROL Adobe 1PD]** tegel, waarin alle soorten publiek worden vermeld die zijn geactiveerd voor de [!DNL Trade Desk] bestemming voor uw adverteerder. U kunt ook de zoekfunctie gebruiken.
4. Segment-id # van Experience Platform wordt weergegeven als Segmentnaam in het dialoogvenster [!DNL Trade Desk] UI.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] handhaaft gegevensbeheer, zie [Overzicht van gegevensbeheer](/help/data-governance/home.md).
