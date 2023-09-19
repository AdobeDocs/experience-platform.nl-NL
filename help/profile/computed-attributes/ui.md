---
title: Gebruikershandleiding berekende kenmerken
description: Leer hoe u berekende kenmerken maakt, weergeeft en bijwerkt met de gebruikersinterface van Adobe Experience Platform.
source-git-commit: 631b67eb6609381235113009acefaf0d0cd8063c
workflow-type: tm+mt
source-wordcount: '1406'
ht-degree: 0%

---


# Gebruikershandleiding voor berekende kenmerken

>[!NOTE]
>
>Om toegang tot gegevens verwerkte attributen te krijgen, zult u de aangewezen toestemmingen moeten hebben (**Berekende kenmerken weergeven** en **Berekende kenmerken beheren**). Lees voor meer informatie over de vereiste machtigingen de [toegangsbeheerdocumentatie](../../access-control/home.md). Lees voor meer informatie over het toepassen van deze machtigingen de [machtigingengids beheren](../../access-control/ui/permissions.md).

In Adobe Experience Platform zijn berekende kenmerken functies die worden gebruikt om gegevens op gebeurtenisniveau samen te voegen tot kenmerken op profielniveau. Deze functies worden automatisch berekend zodat zij over segmentatie, activering, en verpersoonlijking kunnen worden gebruikt.

In dit document wordt uitgelegd hoe u berekende kenmerken kunt maken en bijwerken met de gebruikersinterface van Adobe Experience Platform.

## Aan de slag

Deze UI-gids vereist inzicht in de verschillende [!DNL Experience Platform] diensten die betrokken zijn bij het beheer [!DNL Real-Time Customer Profiles]. Voordat u deze handleiding leest of in de gebruikersinterface werkt, raadpleegt u de documentatie voor de volgende services:

- [[!DNL Real-Time Customer Profile]](../home.md): Biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Het gestandaardiseerde kader waarbinnen [!DNL Experience Platform] organiseert de gegevens van de klantenervaring.

## Berekende kenmerken weergeven {#view}

Selecteer in de gebruikersinterface van het Experience Platform de optie **[!UICONTROL Profiles]** in de linkernavigatie, gevolgd door **[!UICONTROL Computed attributes]** voor een lijst met de berekende kenmerken die beschikbaar zijn voor uw organisatie. Dit omvat informatie over de gegevens verwerkte naam van de attributen, beschrijving, laatste evaluatiedatum, en laatste evaluatiestatus.

![De [!UICONTROL Profile] en de [!UICONTROL Computed attributes] tabbladen worden gemarkeerd en geven gebruikers weer hoe ze de pagina met berekende kenmerken kunnen openen.](./images/ui/browse.png)

U kunt selecteren welke velden zichtbaar zijn ![Het pictogram voor het configureren van kolommen](./images/ui/configure-icon.png) om toe te voegen of te verwijderen welke gebieden u wilt worden getoond.

| Veld | Beschrijving |
| ----- | ----------- |
| [!UICONTROL Name] | De weergavenaam van het berekende kenmerk. |
| [!UICONTROL Description] | De beschrijving voor het berekende kenmerk. |
| [!UICONTROL Evaluation method] | De evaluatiemethode voor de gegevens verwerkte attributen. Alleen op dit moment **partij** wordt ondersteund. |
| [!UICONTROL Last evaluated] | Dit tijdstempel vertegenwoordigt de laatste geslaagde evaluatieronde. Alleen gebeurtenissen die zijn uitgevoerd **voor** deze tijdstempel wordt meegenomen in de laatste geslaagde evaluatie. |
| [!UICONTROL Last evaluation status] | De status die verklaart al dan niet de gegevens verwerkte attributen met succes in de laatste evaluatielooppas werd berekend. Mogelijke waarden zijn **[!UICONTROL Success]** of **[!UICONTROL Failed]**. |
| [!UICONTROL Refresh frequency] | Een indicatie hoe vaak het berekende attribuut naar verwachting zal worden vernieuwd. Mogelijke waarden zijn uurwaarden, dagwaarden, weekwaarden of maandwaarden. |
| [!UICONTROL Fast refresh] | Een waarde die toont al dan niet snel verfrist voor dit compute attribuut wordt toegelaten. Als de snelle verfrissing wordt toegelaten, laat dit de gegevens verwerkte attributen op een dagelijkse basis, eerder dan op een wekelijkse, bi-wekelijkse, of maandbasis worden verfrist. Deze waarde is alleen van toepassing op berekende kenmerken met een terugzoekperiode die langer is dan een week. |
| [!UICONTROL Lifecycle status] | De huidige status van het berekende kenmerk. Er zijn drie mogelijke statussen: <ul><li>**[!UICONTROL Draft]:** Het berekende kenmerk doet dit **niet** hebben nog een gebied dat op het schema wordt gecreeerd. In deze status kan het berekende kenmerk worden bewerkt. </li><li>**[!UICONTROL Published]:** Het berekende attribuut heeft een gebied dat op het schema wordt gecreeerd en is klaar om te worden gebruikt. In deze status wordt het berekende kenmerk **kan** worden bewerkt.</li><li>**[!UICONTROL Inactive]:** Het berekende kenmerk is uitgeschakeld. Lees voor meer informatie over de inactieve status de [Pagina met veelgestelde vragen](./faq.md#inactive-status). </li> |
| [!UICONTROL Created] | Een tijdstempel met de datum en tijd waarop het berekende kenmerk is gemaakt. |
| [!UICONTROL Last modified] | Een tijdstempel met de datum en tijd waarop het berekende kenmerk voor het laatst is gewijzigd. |

U kunt de weergegeven berekende kenmerken ook filteren op basis van de levenscyclusstatus. Selecteer de ![trechter](./images/ui/filter-icon.png) pictogram.

![Het filterpictogram wordt gemarkeerd.](./images/ui/select-filter.png)

U kunt nu de berekende kenmerken filteren op status ([!UICONTROL Draft], [!UICONTROL Published], en [!UICONTROL Inactive]).

![De opties waarmee u de berekende kenmerken kunt filteren, worden gemarkeerd. Deze opties omvatten [!UICONTROL Draft], [!UICONTROL Published], en [!UICONTROL Inactive].](./images/ui/view-filters.png)

Bovendien kunt u een berekend attribuut selecteren om meer gedetailleerde informatie over het te zien. Lees voor meer informatie over de pagina met gegevens over berekende kenmerken de [de sectie met details van een berekend kenmerk weergeven](#view-details).

## Een berekend kenmerk maken {#create}

Als u een nieuw berekende kenmerk wilt maken, selecteert u **[!UICONTROL Create computed attribute]** om de nieuwe berekende kenmerkworkflow in te voeren.

![De [!UICONTROL Create computed attributes] wordt gemarkeerd en geeft gebruikers weer hoe ze een berekende kenmerkpagina kunnen maken.](./images/ui/create.png)

De **[!UICONTROL Create computed attribute]** wordt weergegeven. Op deze pagina kunt u de basisgegevens toevoegen voor het berekende kenmerk dat u wilt maken.

| Veld | Beschrijving |
| ----- | ----------- |
| [!UICONTROL Display name] | The name which the computed attribute will be known by. Deze weergavenaam moet uniek blijven voor elk berekend kenmerk. Als beste praktijken, zou deze vertoningsnaam herkenningstekens met betrekking tot het gegevens verwerkte attribuut moeten bevatten. Bijvoorbeeld &quot;Som van aankopen voor schoenen in de afgelopen 7 dagen&quot;. |
| [!UICONTROL Field name] | Een naam die wordt gebruikt om naar het berekende attribuut in andere stroomafwaartse diensten te verwijzen. Deze naam wordt automatisch afgeleid van de vertoningsnaam en in camelCase geschreven. |
| [!UICONTROL Description] | Een beschrijving van het berekende kenmerk dat u wilt maken. |

![De [!UICONTROL Basic information] van de [!UICONTROL Create computed attribute] pagina is gemarkeerd.](./images/ui/basic-information.png)

Nadat u de berekende kenmerkdetails hebt toegevoegd, kunt u uw regels gaan definiëren.

### Gebeurtenisfiltervoorwaarden opgeven

Als u een regel wilt maken, selecteert u eerst kenmerken in het menu **[!UICONTROL Events]** om gebeurtenissen naar beneden te filteren waarop u wilt samenvoegen. Momenteel worden alleen niet-arraytype-gebeurteniskenmerken ondersteund.

![De [!UICONTROL Events] wordt gemarkeerd.](./images/ui/events.png)

Nadat u het kenmerk hebt geselecteerd dat u wilt gebruiken in de berekende kenmerkdefinitie, kunt u kiezen met welke waarde deze waarde wordt vergeleken.

![De beschikbare vergelijkingstypen worden weergegeven.](./images/ui/select-comparison.png)

### Samenvoegingsfunctie toepassen

Nu kunt u een functie op het veld toepassen vanuit de voorwaardelijke uitvoer. Selecteer eerst het type aggregatiefunctie. Beschikbare opties zijn [!UICONTROL Sum], [!UICONTROL Min], [!UICONTROL Max], [!UICONTROL Count], en [!UICONTROL Most Recent]. Meer informatie over deze functies vindt u in het gedeelte [Functiesectie](./overview.md#functions) van het berekende kenmerkenoverzicht.

![De berekende kenmerkfuncties worden weergegeven.](./images/ui/select-function.png)

Nadat u een functie hebt gekozen, kunt u het veld kiezen waarop u wilt aggregeren. Welke velden in aanmerking komen, is afhankelijk van de geselecteerde functie.

![In het gemarkeerde veld ziet u het kenmerk waarop u de functie wilt samenvoegen.](./images/ui/select-eligible-field.png)

### Duur van opzoeken

Na het toepassen van de samenvoegingsfunctie, zult u de raadplegingsperiode van de gegevens verwerkte attributen moeten bepalen. Deze terugzoekperiode geeft de tijdsduur aan waarop u gebeurtenissen wilt samenvoegen. Deze terugzoekduur kan worden opgegeven in uren, dagen, weken of maanden.

![De terugzoekduur wordt gemarkeerd.](./images/ui/select-lookback-duration.png)

### Snel vernieuwen {#fast-refresh}

>[!CONTEXTUALHELP]
>id="platform_profile_computedAttributes_fastRefresh"
>title="Snel vernieuwen"
>abstract="Met Snel vernieuwen kunt u uw kenmerken up-to-date houden. Als u deze optie inschakelt, kunt u uw berekende kenmerken dagelijks vernieuwen, zelfs voor langere terugzoekperiodes, zodat u snel kunt reageren op gebruikersactiviteiten. Deze waarde is alleen van toepassing op berekende kenmerken met een terugzoekperiode die langer is dan een week."

Tijdens het toepassen van de samenvoegingsfunctie, kunt u snel toelaten verfrist zich als de raadplegingsperiode groter is dan één week.

![De [!UICONTROL Fast Refresh] selectievakje is gemarkeerd.](./images/ui/enable-fast-refresh.png)

Met Snel vernieuwen kunt u uw kenmerken up-to-date houden. Als u deze optie inschakelt, kunt u uw berekende kenmerken dagelijks vernieuwen, zelfs voor langere terugzoekperiodes, zodat u snel kunt reageren op gebruikersactiviteiten.

Lees voor meer informatie over snel vernieuwen de [sectie voor snel vernieuwen](./overview.md#fast-refresh) van het berekende kenmerkenoverzicht.

Als deze stappen zijn voltooid, kunt u dit berekende kenmerk nu opslaan als concept of het meteen publiceren.

![De [!UICONTROL Save as draft] en [!UICONTROL Publish] worden gemarkeerd.](./images/ui/draft-or-publish.png)

## De details van een berekend kenmerk weergeven {#view-details}

Als u de details van een berekend kenmerk wilt weergeven, selecteert u het berekende kenmerk waarover u details wilt zien in het dialoogvenster [!UICONTROL **Bladeren**] pagina.

![Een berekend kenmerk wordt gemarkeerd.](./images/ui/select.png)

De inhoud van de pagina verschilt, afhankelijk van het feit of het berekende kenmerk **[!UICONTROL Published]** of in **[!UICONTROL Draft]**.

### Gepubliceerd berekend kenmerk {#published}

Als u een gepubliceerd, berekend kenmerk selecteert, wordt de detailpagina met berekende kenmerken weergegeven.

![De detailpagina van het berekende kenmerk wordt weergegeven.](./images/ui/details.png)

Deze pagina bevat een overzicht van de gegevens van het berekende kenmerk en een grafiek met de waardeverdeling en voorbeeldprofielen die in aanmerking komen voor het berekende kenmerk.

>[!NOTE]
>
>De waardeverdeling weerspiegelt de verdeling van kenmerkwaarden voor profielen op het moment van de monstertaak. De berekende kenmerkwaarde in het voorbeeldprofiel weerspiegelt de meest recente samengevoegde profielwaarde voor een paar voorbeeldprofielen.

### Concept, berekend kenmerk {#draft}

Wanneer u een concept van een berekend kenmerk selecteert, wordt **[!UICONTROL Edit computed attributes]** wordt weergegeven. Deze pagina, net als de pagina [!UICONTROL Create computed attributes] , kunt u de basisgegevens en de definitie van het berekende kenmerk bewerken voordat u het concept kunt bijwerken of publiceren.

![De pagina [!UICONTROL Edit computed attributes] wordt weergegeven.](./images/ui/edit.png)

## Berekende kenmerken gebruiken {#usage}

Nadat u een berekend kenmerk hebt gemaakt, kunt u **gepubliceerd** berekende kenmerken in andere downstreamdiensten. Aangezien de gegevens verwerkte attributen profielkenmerkgebieden zijn die op uw profiel worden gecreeerd verenigen schema, kunt u gegevens verwerkte attributenwaarden voor een Real-Time Profiel van de Klant opzoeken, hen in een publiek gebruiken, hen activeren aan een bestemming, of hen gebruiken voor verpersoonlijking in reizen in Adobe Journey Optimizer.

![De Bouwer van het Segment wordt getoond, tonend een gegevens verwerkt attribuut als deel van de compositie van de segmentdefinitie.](./images/ui/use-ca.png)

## Volgende stappen

Voor meer informatie over berekende kenmerken leest u de [overzicht van berekende kenmerken](./overview.md). Voor informatie over het maken en configureren van berekende kenmerken met behulp van de API leest u de [handleiding voor ontwikkelaars van berekende kenmerken](./api.md).
