---
title: (Bèta) De handelsbank - CRM-verbinding
description: Activeer profielen aan uw rekening van het Bureau van de Handel voor publiek gericht en onderdrukking die op de gegevens van CRM wordt gebaseerd.
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: 38447348bc96b2f3f330ca363369eb423efea1c8
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 1%

---

# (bèta) De [!DNL Trade Desk] - CRM-verbinding

>[!IMPORTANT]
>
> [!DNL The Trade Desk - CRM] doel in Platform is momenteel in bèta. De documentatie en functionaliteit kunnen worden gewijzigd.

## Overzicht {#overview}

>[!IMPORTANT]
>
> Deze documentatiepagina is gemaakt door de *[!DNL Trade Desk]* team. Neem contact op met uw [!DNL Trade Desk] vertegenwoordiger.

Dit document is ontworpen om u te helpen profielen te activeren voor uw [!DNL Trade Desk] account voor doelgroepen en suppressie op basis van CRM-gegevens.

>[!TIP]
>
>Gebruiken [!DNL The Trade Desk] CRM-bestemming voor CRM-gegevenstoewijzing, zoals e-mailadres of hashed-e-mailadres. Gebruik de [andere bestemming van de handelsbank](/help/destinations/catalog/advertising/tradedesk.md) in de Adobe Experience Platform-catalogus voor cookies en toegewezen apparaat-id.

[!DNL The Trade Desk] (TTD) kan het geüploade bestand met e-mailadressen nooit rechtstreeks verwerken, en [!DNL The Trade Desk] sla je onbewerkte e-mails (zonder hashing) op.

## Vereisten {#prerequisites}

Voordat u segmenten kunt activeren [!DNL The Trade Desk], moet u contact opnemen met uw [!DNL The Trade Desk] accountmanager om het CRM-instapcontract te ondertekenen. [!DNL The Trade Desk] zal dan toestemming geven en uw adverteerder identiteitskaart delen om uw bestemming te vormen.

## Vereisten voor ID-afstemming {#id-matching-requirements}

Afhankelijk van het type id&#39;s dat u in Adobe Experience Platform invoert, moet u aan de desbetreffende vereisten voldoen. Lees de [Overzicht van naamruimte van id](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=nl) voor meer informatie .

## Ondersteunde identiteiten {#supported-identities}

[!DNL The Trade Desk] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](/help/identity-service/namespaces.md).

Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-e-mailadressen met hashing. Volg de instructies in de sectie met vereisten voor id-afstemming en gebruik de juiste naamruimten voor normale tekst en gehashte e-mailadressen.

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| Email | E-mailadressen (tekst wissen) | Selecteer `Email` doelIdentiteit wanneer uw bronidentiteit een E-mailnamespace of attribuut is. |
| Email_LC_SHA256 | E-mailadressen moeten worden gehasht met behulp van SHA256 en verlaagd. Zorg ervoor dat u alle [e-mailnormalisatie](https://github.com/UnifiedID2/uid2docs/tree/main/api#email-address-normalization) vereiste regels. U kunt deze instelling later niet wijzigen. | Selecteer `Email_LC_SHA256` doelIdentiteit wanneer uw bronidentiteit een E-mail_LC_SHA256 namespace of attribuut is. |

{style=&quot;table-layout:auto&quot;}

## Vereisten voor e-mailhashing {#hashing-requirements}

U kunt e-mailadressen hashen alvorens hen in Adobe Experience Platform op te nemen of onbewerkte e-mailadressen gebruiken.

Als u meer wilt weten over het invoeren van e-mailadressen in Experience Platform, raadpleegt u de [overzicht van batch-opname](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/overview.html?lang=en).

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
| Exporttype | **[!UICONTROL Segment export]** | U exporteert alle leden van een segment (publiek) met de id&#39;s (e-mail of gehashte e-mail) die worden gebruikt in de bestemming Handelsbureau. |
| Uitvoerfrequentie | **[!UICONTROL Daily Batch]** | Aangezien een profiel in Experience Platform wordt bijgewerkt dat op segmentevaluatie wordt gebaseerd, wordt het profiel (identiteiten) één keer per dag bijgewerkt stroomafwaarts aan het bestemmingsplatform. Meer informatie over [batchuploads](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=en#file-based). |

{style=&quot;table-layout:auto&quot;}

## Verbinden met de bestemming {#connect}

### Verifiëren voor doel {#authenticate}

[!DNL The Trade Desk] De Bestemming van CRM is een dagelijkse lading van het partijdossier en vereist geen authentificatie door de gebruiker.

### Bestemmingsdetails invullen {#fill-in-details}

Voordat u publieksgegevens naar een doel kunt verzenden of activeren, moet u een verbinding met uw eigen doelplatform instellen. while [opzetten](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en) voor deze bestemming moet u de volgende informatie opgeven:

* **[!UICONTROL Account Type]**: Kies **[!UICONTROL Existing Account]** optie.
* **[!UICONTROL Name]**: Een naam waarmee u deze bestemming in de toekomst zult erkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Advertiser ID]**: uw [!DNL Trade Desk Advertiser ID], die door uw [!DNL Trade Desk] Accountmanager of gevonden onder [!DNL Advertiser Preferences] in de [!DNL Trade Desk] UI.

Wanneer u verbinding maakt met de bestemming, is het instellen van een beleid voor gegevensbeheer volledig optioneel. Controleer het Experience Platform [gegevensbeheer - overzicht](https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/overview.html?lang=en) voor meer informatie .

## Segmenten naar dit doel activeren {#activate}

Zie [publieksgegevens activeren om exportdoelen voor batchprofielen te activeren](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en) voor instructies over het activeren van publiekssegmenten aan een bestemming.

In de **[!UICONTROL Scheduling]** pagina, kunt u het programma en de dossiernamen voor elk segment vormen u uitvoert. Het is verplicht het schema te configureren, maar het configureren van de bestandsnaam is optioneel.

>[!NOTE]
>
>Alle segmenten geactiveerd op [!DNL The Trade Desk] De Bestemming van CRM wordt automatisch geplaatst aan een dagelijkse frequentie en volledige dossieruitvoer.

In de **[!UICONTROL Mapping]** pagina, moet u attributen of identiteitsnamespaces van de bronkolom en kaart aan de doelkolom selecteren.

Hieronder ziet u een voorbeeld van correcte identiteitstoewijzing wanneer u segmenten activeert naar [!DNL The Trade Desk] CRM-bestemming.

>[!IMPORTANT]
>
> [!DNL The Trade Desk] CRM-bestemming accepteert geen onbewerkte en gehashte e-mailadressen als identiteiten in dezelfde activeringsstroom. Maak afzonderlijke activeringsstromen voor onbewerkte en gehashte e-mailadressen.

Bronvelden selecteren:

* Selecteer `Email` naamruimte of attribuut als bronidentiteit als het onbewerkte e-mailadres wordt gebruikt bij het invoeren van gegevens.
* Selecteer `Email_LC_SHA256` naamruimte of attribuut als bronidentiteit als u de e-mailadressen van de klant bij het invoeren van gegevens in het Platform hebt onderbroken.

Doelvelden selecteren:

* Selecteer `Email` naamruimte als doelidentiteit wanneer uw bronnaamruimte of -kenmerk `Email`.
* Selecteer `Email_LC_SHA256` naamruimte als doelidentiteit wanneer uw bronnaamruimte of -kenmerk `Email_LC_SHA256`.

## Gegevens exporteren valideren {#validate}

Om te controleren dat de gegevens correct uit Experience Platform en naar worden uitgevoerd [!DNL The Trade Desk], zoek de segmenten onder de Adobe 1PD-datatielijn in [!DNL The Trade Desk] Platform voor gegevensbeheer (DMP). Hier volgen de stappen om de bijbehorende id te vinden in het dialoogvenster [!DNL Trade Desk] UI:

1. Klik eerst op de knop **[!UICONTROL Data]** Tab en revisie **[!UICONTROL First-Party]**.
2. Omlaag schuiven op de pagina, onder **[!UICONTROL Imported Data]**, vindt u de **[!UICONTROL Adobe 1PD Tile]**.
3. Klik op de **[!UICONTROL Adobe 1PD]** tegel, waarin alle segmenten worden weergegeven die aan de [!DNL Trade Desk] bestemming voor uw adverteerder. U kunt ook de zoekfunctie gebruiken.
4. Segment-id # van Experience Platform wordt weergegeven als Segmentnaam in het dialoogvenster [!DNL Trade Desk] UI.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] handhaaft gegevensbeheer, zie [Overzicht van gegevensbeheer](/help/data-governance/home.md).
