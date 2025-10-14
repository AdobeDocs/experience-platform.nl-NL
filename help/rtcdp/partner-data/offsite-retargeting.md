---
title: Offsite opnieuw oprichten van niet-geverifieerde bezoekers
description: Leer hoe te om niet voor authentiek verklaarde gebruikers opnieuw te richten door perspectief te gebruiken IDs om een gegevens verwerkt attribuut tot stand te brengen dat kan worden gebruikt om een publiek van niet voor authentiek verklaarde gebruikers tot stand te brengen.
feature: Use Cases, Customer Acquisition
exl-id: cffa3873-d713-445a-a3e1-1edf1aa8eebb
source-git-commit: 5b37b51308dc2097c05b0e763293467eb12a2f21
workflow-type: tm+mt
source-wordcount: '1358'
ht-degree: 0%

---

# Offsite herbestemming van niet-geregistreerde bezoekers

>[!AVAILABILITY]
>
>Deze functionaliteit is beschikbaar voor klanten die een licentie hebben verkregen voor Real-Time CDP (App Service), Adobe Experience Platform Activation, Real-Time CDP, Real-Time CDP Premiere, Real-Time CDP Ultimate. Lees meer over deze pakketten in de [&#x200B; productbeschrijvingen &#x200B;](https://helpx.adobe.com/nl/legal/product-descriptions.html) en contacteer uw vertegenwoordiger van de Adobe voor meer informatie.

Leer hoe u een publiek van niet-geverifieerde bezoekers kunt maken en deze opnieuw kunt richten met behulp van door de partner geleverde duurzame id&#39;s.

![&#x200B; Infographic die de stroom van partnergegevens van opname in Adobe Experience Platform aan output via publiek aan een stroomafwaartse bestemming toont.](../assets/offsite-retargeting/header.png)

## Waarom dit gebruiksgeval overwegen? {#why-use-case}

Met de geleidelijke afschaffing van cookies van derden moeten de digitale marketers zich opnieuw voorstellen hoe ze hun strategieën voor het opnieuw betrekken van anonieme bezoekers kunnen bedenken. De merken die verkiezen om met identiteitsverkopers voor de erkenning van de bezoeker in real time te integreren kunnen partner ook gebruiken verstrekte duurzame herkenningstekens voor off-site betaalde-media heroriënteren.

Ondanks het grote verkeersvolume zien veel merken een aanzienlijke daling in de conversiefase. Bezoekers doen mee met inhoud en productdemo&#39;s, maar vertrekken zonder zich aan te melden of een aankoop te doen.

U kunt niet alleen een publiek maken op basis van on-site betrokkenheid om marketingberichten aan uw wensen aan te passen, u kunt ook de ondersteuning van de Adobe voor partner-id&#39;s gebruiken om opnieuw contact op te nemen met bezoekers die betaalmedia-bestemmingen gebruiken.

## Vereisten en planning {#prerequisites-and-planning}

Houd rekening met de volgende voorwaarden tijdens uw planningsproces wanneer u van plan bent niet-geverifieerde bezoekers opnieuw te sturen:

- Heb ik opstelling partner IDs met juiste identiteit namespaces?

Bovendien, om het gebruiksgeval uit te voeren, zult u van de volgende functionaliteit van Real-Time CDP en UI elementen gebruik maken. Zorg ervoor dat u de noodzakelijke op attribuut-gebaseerde toegangsbeheertoestemmingen voor al deze gebieden hebt of vraag uw systeembeheerder om u de noodzakelijke toestemmingen te verlenen.

- [Doelgroepen](../../segmentation/home.md)
- [Berekende kenmerken](../../profile/computed-attributes/overview.md)
- [Doelen](../../destinations/home.md)
- [Web SDK](../../web-sdk/home.md)

## Partnergegevens in Real-Time CDP ophalen {#get-data-in}

Als u een publiek van niet-geverifieerde bezoekers wilt maken, moet u eerst de partnergegevens in Real-Time CDP ophalen.

Leren hoe te om gegevens in Real-Time CDP het best in te voeren gebruikend Web SDK, gelieve te lezen de [&#x200B; secties van het gegevensbeheer en van de de inzameling van gebeurtenisgegevens &#x200B;](./onsite-personalization.md#data-management) van het gebruiksgeval van het onsite verpersoonlijkingsgebruik.

## Door partner opgegeven id&#39;s voorwaarts plaatsen {#bring-partner-ids-forward}

Na het invoeren van de partner verstrekte IDs in een gebeurtenisdataset, zult u deze gegevens in de profielverslagen moeten krijgen. U kunt dit doen door berekende attributen te gebruiken.

Met de berekende kenmerken kunt u de gedragsgegevens van het profiel snel omzetten in geaggregeerde waarden op profielniveau. Hierdoor kunt u deze expressies gebruiken, zoals &quot;totaal van levenslange aanschaf&quot; voor het profiel, zodat u het berekende kenmerk eenvoudig kunt gebruiken bij uw publiek. Meer informatie over gegevens verwerkte attributen kan in het [&#x200B; gegevens verwerkte attributenoverzicht &#x200B;](../../profile/computed-attributes/overview.md) worden gevonden.

Selecteer **[!UICONTROL Profiles]** gevolgd door **[!UICONTROL Computed attributes]** en **[!UICONTROL Create computed attribute]** om berekende kenmerken te openen.

![&#x200B; de [!UICONTROL Create computed attributes] knoop wordt benadrukt naast het [!UICONTROL Computed attributes] lusje binnen de [!UICONTROL Profiles] werkruimte.](../assets/offsite-retargeting/create-ca.png)

De pagina **[!UICONTROL Create computed attribute]** wordt weergegeven. Op deze pagina kunt u de componenten gebruiken om uw berekend attribuut tot stand te brengen.

![&#x200B; creeer een gegevens verwerkte attributenwerkruimte wordt getoond.](../assets/offsite-retargeting/ca-page.png)

>[!NOTE]
>
>Voor meer gedetailleerde informatie bij het creëren van gegevens verwerkte attributen, te lezen gelieve de [&#x200B; gegevens verwerkte gids UI van attributen &#x200B;](../../profile/computed-attributes/ui.md).

Voor dit gebruiksgeval, kunt u een gegevens verwerkt attribuut tot stand brengen dat, als partneridentiteitskaart bestaat, de meest recente waarde van partneridentiteitskaart binnen de laatste 24 uren krijgt.

Gebruikend de onderzoeksbar, kunt u van de &quot;identiteitskaart van de Partner&quot;gebeurtenis de plaats bepalen en toevoegen die [&#x200B; u tijdens de onsite het geval van het verpersoonlijkingsgebruik &#x200B;](#get-data-in) aan het gegevens verwerkte attributencanvas creeerde.

![&#x200B; het [!UICONTROL Events] lusje en de onderzoeksbar worden benadrukt.](../assets/offsite-retargeting/ca-add-partner-id.png)

Na het toevoegen van de &quot;identiteitskaart van de Partner&quot;gebeurtenis aan de definitie, plaats de gebeurtenis het filtreren voorwaarde aan **[!UICONTROL Exists]**, plaats de gebeurtenis het filtreren voorwaarde om de **[!UICONTROL Most Recent]** waarde van toegevoegde partneridentiteitskaart, en met een raadplegingsperiode van 24 uren te zijn.

![&#x200B; de definitie van de gegevens verwerkte attributen u wilt tot stand brengen wordt benadrukt.](../assets/offsite-retargeting/ca-add-definition.png)

Geef het berekende attribuut een aangewezen naam (zoals &quot;identiteitskaart van de Partner&quot;) en een beschrijving, dan uitgezocht **[!UICONTROL Publish]** om het gegevens verwerkte proces van de attributenverwezenlijking te voltooien.

![&#x200B; de basisinformatie van de gegevens verwerkte attributen u wilt creëren wordt benadrukt.](../assets/offsite-retargeting/ca-publish.png)

## Een publiek maken met het berekende kenmerk {#create-audience}

Nu u het gegevens verwerkte attribuut hebt gecreeerd, kunt u dit gegevens verwerkte attribuut gebruiken om een publiek tot stand te brengen. In dit voorbeeld maakt u een publiek dat bestaat uit bezoekers die uw website meer dan vijf keer deze maand hebben bezocht maar zich nog niet hebben aangemeld.

Als u een publiek wilt maken, selecteert u **[!UICONTROL Audiences]**, gevolgd door **[!UICONTROL Create audience]** .

![&#x200B; wordt de [!UICONTROL Create audience] knoop benadrukt.](../assets/offsite-retargeting/create-audience.png)

Er wordt een dialoogvenster weergegeven waarin u wordt gevraagd tussen [!UICONTROL Compose audience] en [!UICONTROL Build rule] te kiezen. Selecteer **[!UICONTROL Build rule]** gevolgd door **[!UICONTROL Create]** .

![&#x200B; wordt de [!UICONTROL Build rule] knoop benadrukt.](../assets/offsite-retargeting/select-build-rule.png)

De pagina Segment Builder wordt weergegeven. Op deze pagina kunt u de componenten gebruiken om uw publiek op te bouwen.

![&#x200B; wordt de Bouwer van het Segment getoond.](../assets/offsite-retargeting/segment-builder.png)

>[!NOTE]
>
>Voor meer gedetailleerde informatie over het gebruiken van de Bouwer van het Segment, gelieve de [&#x200B; gids UI van de Bouwer van het Segment &#x200B;](../../segmentation/ui/segment-builder.md) te lezen.

Als u deze bezoekers wilt vinden, moet u eerst een **[!UICONTROL Page View]** -gebeurtenis toevoegen aan uw publiek. Selecteer de tab **[!UICONTROL Events]** onder **[!UICONTROL Fields]** , sleep de gebeurtenis **[!UICONTROL Page View]** en voeg deze toe aan het canvas van de gebeurtenissensectie.

![&#x200B; het [!UICONTROL Events] lusje in de [!UICONTROL Fields] sectie wordt benadrukt, terwijl het tonen van de [!UICONTROL Page View] gebeurtenis.](../assets/offsite-retargeting/add-page-view.png)

Selecteer de zojuist toegevoegde **[!UICONTROL Page View]** -gebeurtenis. Verander de raadplegingsperiode van **[!UICONTROL Any time]** in **[!UICONTROL This month]**, en verander de gebeurtenisregel om **minstens 5** te omvatten.

![&#x200B; Details van de toegevoegde [!UICONTROL Page View] gebeurtenis worden getoond.](../assets/offsite-retargeting/edit-event.png)

Nadat u de gebeurtenis hebt toegevoegd, moet u een kenmerk toevoegen. Aangezien u met ongeautoriseerde bezoekers werkt, kunt u het berekende attribuut toevoegen u enkel creeerde. Met dit nieuwe berekende kenmerk kunt u partner-id&#39;s koppelen aan een publiek.

Om de gegevens verwerkte attributen toe te voegen, onder **[!UICONTROL Attributes]**, selecteer **[!UICONTROL XDM Individual Profile]**, die door **[wordt gevolgd huurder identiteitskaart van uw organisatie &#x200B;](../../xdm/api/getting-started.md#know-your-tenant-id).** , **[!UICONTROL SystemComputedAttributes]** en **[!UICONTROL PartnerID]** . Voeg nu de **[!UICONTROL Value]** van het berekende kenmerk toe aan de sectie met kenmerken van het canvas.

![&#x200B; het omslag kleven om tot de gegevens verwerkte attributen toegang te hebben wordt getoond.](../assets/offsite-retargeting/access-computed-attribute.png)

Zoek bovendien naar **[!UICONTROL Personal Email]** en voeg het **[!UICONTROL Address]** kenmerk hieronder **[!UICONTROL PartnerID]** toe aan de sectie met kenmerken van het canvas.

![&#x200B; de [!UICONTROL PartnerID] gegevens verwerkte attributen en het [!UICONTROL Personal Email Address] attribuut worden benadrukt op het canvas van de Bouwer van het Segment.](../assets/offsite-retargeting/added-attributes.png)

Nu u uw attributen hebt toegevoegd, zult u hun evaluatiecriteria moeten plaatsen. Stel voor **[!UICONTROL PartnerID]** het criterium in op **[!UICONTROL exists]** en voor **[!UICONTROL Address]** op **[!UICONTROL does not exist]** .

![&#x200B; de juiste waarden van de attributen worden benadrukt.](../assets/offsite-retargeting/set-attribute-values.png)

U hebt nu een publiek gemaakt dat op zoek is naar intensieve bezoekers met een door partners opgegeven id, maar die zich nog niet hebben aangemeld voor uw site. Geef de doelgroep de naam &quot;Niet-geverifieerde gebruikers opnieuw toewijzen&quot; en selecteer **[!UICONTROL Save]** om het maken van een publiek te voltooien.

![&#x200B; de publiekseigenschappen worden benadrukt.](../assets/offsite-retargeting/save-audience-properties.png)

## Uw publiek activeren {#activate-audience}

Nadat u het publiek hebt gemaakt, kunt u dit publiek nu activeren naar downstreambestemmingen. Selecteer **[!UICONTROL Audiences]** op de linkernavigatieregel, zoek uw pas gecreëerde publiek, selecteer het ellipspictogram, en selecteer **[!UICONTROL Activate to destination]**.

![&#x200B; wordt de [!UICONTROL Activate to destination] knoop benadrukt.](../assets/offsite-retargeting/activate-to-destination.png)

>[!NOTE]
>
>Alle bestemmingstypes, met inbegrip van op dossier-gebaseerde bestemmingen, steunen publiekactivering met partner IDs.
>
>Voor meer informatie bij het activeren van publiek aan een bestemming, te lezen gelieve het [&#x200B; activeringsoverzicht &#x200B;](../../destinations/ui/activation-overview.md).

De pagina **[!UICONTROL Activate destination]** wordt weergegeven. Op deze pagina kunt u selecteren naar welk doel u de bestemming wilt activeren. Selecteer **[!UICONTROL Next]** nadat u het doel van de keuze hebt geselecteerd.

![&#x200B; de bestemming u het publiek aan wilt activeren wordt benadrukt.](../assets/offsite-retargeting/select-destination.png)

De pagina **[!UICONTROL Scheduling]** wordt weergegeven. Op deze pagina kunt u een programma maken dat bepaalt hoe vaak het publiek moet worden geactiveerd. Selecteer **[!UICONTROL Create schedule]** om een programma voor de activering van het publiek te maken.

![&#x200B; wordt de [!UICONTROL Create schedule] knoop benadrukt.](../assets/offsite-retargeting/select-create-schedule.png)

De pop-up [!UICONTROL Scheduling] wordt weergegeven. Op deze pagina kunt u het programma voor activering van uw publiek maken. Selecteer **[!UICONTROL Create]** nadat u het schema hebt geconfigureerd om door te gaan.

![&#x200B; vormt programmapopover wordt getoond.](../assets/offsite-retargeting/configure-schedule.png)

Selecteer **[!UICONTROL Next]** nadat u de planningsdetails hebt bevestigd.

![&#x200B; de details van het programma worden getoond.](../assets/offsite-retargeting/created-schedule.png)

De pagina **[!UICONTROL Select attributes]** wordt weergegeven. Op deze pagina kunt u selecteren welke kenmerken u samen met het geactiveerde publiek wilt exporteren. Minstens, zult u partneridentiteitskaart willen omvatten, aangezien dit u de bezoekers zal laten identificeren u van plan bent om zich te richten. Selecteer **[!UICONTROL Add new mapping]** en zoek naar het berekende kenmerk. Selecteer **[!UICONTROL Next]** nadat u de benodigde kenmerken hebt toegevoegd.

![&#x200B; zowel worden de [!UICONTROL Add new mapping] knoop als de gegevens verwerkte attributen benadrukt.](../assets/offsite-retargeting/add-new-mapping.png)

De pagina **[!UICONTROL Review]** wordt weergegeven. Op deze pagina kunt u de details van de activering van uw publiek bekijken. Selecteer **[!UICONTROL Finish]** als u tevreden bent met de opgegeven details.

![&#x200B; de [!UICONTROL Review] pagina wordt getoond, tonend details van de publieksactivering.](../assets/offsite-retargeting/review-destination-activation.png)

U hebt nu een publiek van niet-geverifieerde gebruikers geactiveerd voor een verdere herbestemming.

## Andere gebruiksgevallen {#other-use-cases}

U kunt verdere gebruiksgevallen onderzoeken die door de steun van partnergegevens in Real-Time CDP worden toegelaten:

- [&#x200B; verbind en verkrijg nieuwe klanten &#x200B;](./prospecting.md) door partnergegevens te gebruiken.
- [&#x200B; personaliseer onsite ervaringen &#x200B;](./offsite-retargeting.md) met partner-gesteunde bezoekerserkenning.
- [&#x200B; de profielen van de Supplement van de Eerste partij &#x200B;](./supplement-first-party-profiles.md) met partner-Geleverde attributen.
