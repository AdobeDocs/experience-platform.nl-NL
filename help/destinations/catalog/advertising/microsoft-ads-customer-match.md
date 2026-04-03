---
keywords: reclame; microsoft advertenties; klantovereenkomst;
title: Microsoft Ads Customer Match Connection
description: Gebruik de Microsoft Ads Customer Match-bestemming om klanten op e-mailadres te benaderen en opnieuw contact met hen op te nemen via het Microsoft Advertising Network, inclusief advertenties voor zoeken en publiek.
badge: label="Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 4d405ffb-f600-463b-a215-44e806b6d139
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '1511'
ht-degree: 0%

---

# [!DNL Microsoft Ads Customer Match]-verbinding {#microsoft-ads-customer-match-destination}

>[!AVAILABILITY]
>
>Deze bestemmingsschakelaar is momenteel in beperkte beschikbaarheid. Neem contact op met uw Adobe-vertegenwoordiger voor toegang.

## Overzicht {#overview}

Gebruik de bestemming [!DNL Microsoft Ads Customer Match] om klanten op e-mailadres aan te passen en met hen over [!DNL Microsoft Advertising Network], met inbegrip van onderzoek en de advertenties van de Publiek opnieuw in dienst te nemen. Koppel uw [!DNL Microsoft Advertising] -account aan [!DNL Real-Time CDP] om het maken en beheren van lijsten door klanten rechtstreeks vanuit Experience Platform te automatiseren.

## Gebruiksscenario&#39;s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer om de [!DNL Microsoft Ads Customer Match] bestemming te gebruiken, zijn hier voorbeelden van gebruiksgevallen die de klanten van Adobe Experience Platform door deze eigenschap kunnen oplossen.

### Bestaande klanten met gepersonaliseerde aanbiedingen opnieuw aanbieden {#use-case-1}

Een e-commercemerk wil bestaande klanten bereiken via [!DNL Microsoft Search] en [!DNL Microsoft Audience Network] om aanbiedingen aan te passen op basis van hun eerdere aankopen en browsergeschiedenis. Het merk kan e-mailadressen van hun eigen CRM in Experience Platform opnemen, publiek maken van hun eigen offline gegevens en deze soorten publiek naar [!DNL Microsoft Ads Customer Match] sturen om te worden gebruikt voor zoekopdrachten en publieksadvertenties, zodat hun advertentie-uitgaven worden geoptimaliseerd.

### Nieuwe producten promoten bij bestaande klanten {#use-case-2}

Een technologiebedrijf lanceerde een nieuw product en wil het bewustzijn van klanten stimuleren die eerder verwante producten kochten. Ze uploaden e-mailadressen vanuit hun CRM-database naar Experience Platform en gebruiken de e-mailadressen als id&#39;s. Het publiek wordt gecreëerd op basis van klanten die verwante producten bezitten. Deze soorten publiek worden naar [!DNL Microsoft Ads Customer Match] verzonden, zodat het bedrijf zich kan richten op huidige klanten en vergelijkbare klanten in de [!DNL Microsoft Advertising Network] .

## Ondersteunde identiteiten {#supported-identities}

[!DNL Microsoft Ads Customer Match] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [ identiteiten ](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| `email` | E-mailadressen met normale tekst | Slechts worden de gewone (unhashed) e-mailadressen gesteund als **bron** gebieden in de afbeeldingsstap. Vooraf gehashte bronvelden worden niet ondersteund. Experience Platform hakt e-mailadressen altijd door voordat ze naar [!DNL Microsoft Ads] worden geëxporteerd. |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | Ja | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [ ](../../../segmentation/home.md). |
| Alle andere doelgroepen | Ja | Deze categorie omvat alle oorsprong van het publiek buiten het publiek dat via [!DNL Segmentation Service] wordt gegenereerd. Lees over de [ diverse publieksoorsprong ](/help/segmentation/ui/audience-portal.md#customize). Voorbeelden zijn: <ul><li> de douane uploadt publiek [ ingevoerde ](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers,</li><li> gelijksoortige doelgroepen, </li><li> federaal publiek, </li><li> publiek dat wordt gegenereerd in andere Experience Platform-toepassingen, zoals [!DNL Adobe Journey Optimizer] , </li><li> en meer. </li></ul> |

{style="table-layout:auto"}

Ondersteund publiek per type publieksgegevens:

| Gegevenstype Publiek | Ondersteund | Beschrijving | Gebruiksscenario&#39;s |
|--------------------|-----------|-------------|-----------|
| [ het publiek van Mensen ](/help/segmentation/types/people-audiences.md) | Ja | Gebaseerd op klantenprofielen, die u toestaan om specifieke groepen mensen voor marketing campagnes te richten. | Frequente kopers, winkeliers |
| [ publiek van de Rekening ](/help/segmentation/types/account-audiences.md) | Nee | Doelpersonen binnen specifieke organisaties voor marketingstrategieën op basis van account. | B2B-marketing |
| [ Het publiek van het Vooruitzicht ](/help/segmentation/types/prospect-audiences.md) | Nee | De individuen van het doel die nog geen klanten zijn maar eigenschappen met uw doelpubliek delen. | Waarschuwing met gegevens van derden |
| [ de uitvoer van de Dataset ](/help/catalog/datasets/overview.md) | Nee | Verzamelingen gestructureerde gegevens die zijn opgeslagen in het [!DNL Adobe Experience Platform] Data Lake. | Rapportage, workflows voor gegevenswetenschap |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (e-mailadressen) die worden gebruikt in het doel van [!DNL Microsoft Ads Customer Match] . |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [ het stromen bestemmingen ](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Vereisten {#prerequisites}

Als u publieksgegevens naar [!DNL Microsoft Ads] wilt verzenden, hebt u een actieve [!DNL Microsoft Advertising] -account nodig. Voor details bij het creëren van een rekening, bezoek de [ documentatie van Microsoft Advertising ](https://help.ads.microsoft.com/#apex/ads/en/53090/0).

### Bepalingen en voorwaarden voor klantovereenkomst accepteren {#accept-customer-match-terms}

Voordat u het publiek activeert via deze bestemming, moet u eerst handmatig een lijst met overeenkomsten voor klanten maken in uw [!DNL Microsoft Advertising] -account. Deze eerste handleiding moet worden aangemaakt om de voorwaarden en bepalingen van de klantovereenkomst te accepteren, zodat gebruikers die vanuit Experience Platform worden verzonden automatisch kunnen worden aangemaakt. Als u deze stap niet voltooit, kunnen er fouten optreden bij het activeren van het publiek.

### Goedkeuring werkaccount (MS Entra) IT-beheerder {#work-account-admin-approval}

Als u zich verifieert met een Microsoft Work-account (ook wel Microsoft Entra-account genoemd), moet de IT-beheerder van uw organisatie mogelijk goedkeuring verlenen voordat u verbinding kunt maken met [!DNL Microsoft Advertising] .

Wanneer u probeert voor authentiek te verklaren gebruikend een Rekening van het Werk, kunt u aan een **vereiste Goedkeuring** pagina opnieuw worden gericht. Deze pagina vraagt om uitvulling voor het koppelen van de app en geeft een overzicht van de vereiste machtigingen, inclusief `ads.manage` . Verzend het verzoek en uw IT-beheerder ontvangt een melding om het te beoordelen. Je ontvangt ook een bevestigingsbericht dat je aanvraag is verzonden.

Zodra de IT-beheerder het verzoek heeft goedgekeurd in de Azure Portal, kunt u terugkeren naar Experience Platform en verifiëren met uw werkaccount. Raadpleeg de documentatie bij Microsoft voor hulp:

* [ Overzicht en neem actie op admin toestemmingsverzoeken ](https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/review-admin-consent-requests)
* [ vorm het werkschema van de admin toestemming ](https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/configure-admin-consent-workflow)
* [ vormt hoe de gebruikers aan toepassingen ](https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/configure-user-consent) goedkeuren

Als de IT-beheerder de aanvraag nog niet heeft goedgekeurd, mislukt de verificatie met de volgende fout: `AADSTS650052: The app needs access to a service ('https://ads.microsoft.com') that your organization has not subscribed to or enabled. Contact your IT Admin to review the configuration of your service subscriptions.`

### Accountconfiguratie {#account-configuration}

Wanneer het vormen van de bestemming, moet u de volgende informatie verstrekken:

* [!UICONTROL Customer ID]: uw [!DNL Microsoft Ads] Klant-id (CID), in gehele notatie. Zie de [ documentatie van Advertising van Microsoft ](https://learn.microsoft.com/en-us/advertising/guides/get-started?view=bingads-13#get-ids) voor instructies op hoe te om uw identiteitskaart van de Klant te vinden.
* [!UICONTROL Customer Account ID]: uw [!DNL Microsoft Ads] ID van uw klantenaccount. Zie de [ documentatie van Microsoft Advertising ](https://learn.microsoft.com/en-us/advertising/guides/get-started?view=bingads-13#get-ids) voor instructies op hoe te om uw identiteitskaart van de Rekening van de Klant te vinden.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven.

### Doelgegevens invullen {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_microsoft_ads_cm_customer_id"
>title="Klant-id"
>abstract="Je Microsoft Advertising Customer ID, ook wel Manager-account-id genoemd. Dit is de identificatiecode van het hoogste niveau in Microsoft Advertising die meerdere adverteerderaccounts (Customer Account ID&#39;s) kan bevatten."
>additional-url="https://learn.microsoft.com/en-us/advertising/guides/get-started?view=bingads-13#get-ids" text="Zoek je gebruikersnaam"

>[!CONTEXTUALHELP]
>id="platform_destinations_microsoft_ads_cm_customer_account_id"
>title="Customer Account-ID"
>abstract="Je Microsoft Advertising Customer Account ID, ook wel Advertiser-account-id genoemd. Dit identificeert een specifieke adverteerderaccount onder uw klant-id."
>additional-url="https://learn.microsoft.com/en-us/advertising/guides/get-started?view=bingads-13#get-ids" text="Zoek je Customer Account-ID"

>[!CONTEXTUALHELP]
>id="platform_destinations_microsoft_ads_cm_membership_duration"
>title="Looptijd lidmaatschap"
>abstract="Het aantal dagen dat een gebruiker in de lijst van de klantengelijke blijft. De toegestane waarden liggen tussen 1 en 390 dagen."

>[!CONTEXTUALHELP]
>id="platform_destinations_microsoft_ads_cm_list_availability"
>title="Beschikbaarheid van lijst met klanten afstemmen"
>abstract="Selecteer of de lijst met overeenkomsten voor klanten beschikbaar is voor één advertentieaccount of voor alle accounts in het beheerdersaccount. Selecteer Klant-id om de lijst beschikbaar te maken voor alle adverteerderaccounts onder uw Klant-id. Selecteer Customer Account ID om de lijst te beperken tot de specifieke Customer Account ID."
>additional-url="https://help.ads.microsoft.com/apex/index/3/en/56727" text="Meer informatie over het delen van publiekslijsten in Microsoft Advertising"

Terwijl [ vestiging ](../../ui/connect-destination.md) deze bestemming, u de volgende informatie moet verstrekken:

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Customer ID]**: Uw [!DNL Microsoft Ads] klant-id (CID). Zie de [ documentatie van Advertising van Microsoft ](https://learn.microsoft.com/en-us/advertising/guides/get-started?view=bingads-13#get-ids) voor instructies op hoe te om uw identiteitskaart van de Klant te vinden.
* **[!UICONTROL Customer Account ID]**: Uw [!DNL Microsoft Ads] id van uw klantenaccount. Zie de [ documentatie van Microsoft Advertising ](https://learn.microsoft.com/en-us/advertising/guides/get-started?view=bingads-13#get-ids) voor instructies op hoe te om uw identiteitskaart van de Rekening van de Klant te vinden.
* **[!UICONTROL Membership Duration]**: Het aantal dagen dat een gebruiker in de lijst van de klantengelijke blijft. De toegestane waarden liggen tussen 1 en 390 dagen.
* **[!UICONTROL Customer Match List Availability]**: selecteer de beschikbaarheid van de lijst van de klantengelijke. In [!DNL Microsoft Advertising] kan een klant-id meerdere Customer Account-id&#39;s (adverteerderaccounts) bevatten. Selecteer **[!UICONTROL Customer ID (all advertising accounts)]** om de lijst beschikbaar te maken voor alle adverteerderaccounts onder uw klant-id of **[!UICONTROL Customer Account ID (single advertising account)]** om de lijst te beperken tot de specifieke Customer Account ID die u hierboven hebt opgegeven. Zie de [ documentatie van Advertising van Microsoft ](https://help.ads.microsoft.com/apex/index/3/en/56727) voor meer details.

  ![ beeld UI van het Platform dat de gebieden van bestemmingsdetails voor de bestemming van de Gelijke van de Klant van Microsoft Ads toont.](../../assets/catalog/advertising/microsoft-ads-customer-match/destination-details.png)

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [ het intekenen aan bestemmingsalarm gebruikend UI ](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
>
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* naar bestemmingen uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Zie [ publieksgegevens aan het stromen publiek de uitvoerbestemmingen ](../../ui/activate-segment-streaming-destinations.md) voor instructies op het activeren van publiek aan deze bestemming activeren.

### Toewijzing {#mapping}

In de stap **[!UICONTROL Mapping]** moet u de e-mailidentiteit vanuit uw bronprofielen toewijzen aan de doelidentiteit in [!DNL Microsoft Ads Customer Match] .

* **het gebied van Source**: Selecteer `IdentityMap: Email` als brongebied om e-mailidentiteiten van uw profielen in kaart te brengen. U kunt ook een XDM-kenmerk, zoals `personalEmail.address` , als bronveld selecteren.
* **gebied van het Doel**: Selecteer `Identity: email` als doelgebied.

>[!IMPORTANT]
>
>U moet duidelijke tekst (unhashed) e-mailadressen als **bron** gebieden in kaart brengen. Vooraf gehashte bronidentiteiten zoals `Emails (SHA256, lowercased)` worden niet ondersteund. Experience Platform hakt e-mailadressen altijd door voordat ze naar [!DNL Microsoft Ads] worden geëxporteerd.

![ beeld UI die de afbeeldingsstap met E-mail Identiteitskaart toont die aan E-mail van de Identiteit wordt toegewezen.](../../assets/catalog/advertising/microsoft-ads-customer-match/mapping.png)

## Geëxporteerde gegevens {#exported-data}

Controleer uw [!DNL Microsoft Ads Customer Match] -account om te controleren of gegevens naar de [!DNL Microsoft Advertising] -bestemming zijn geëxporteerd. Als de activering is gelukt, worden de soorten publiek in uw account ingevuld als overeenkomende lijsten met klanten.

## Aanvullende bronnen {#additional-resources}

Zie het [ Microsoft Advertising Help Center ](https://help.ads.microsoft.com/) voor extra informatie.
