---
title: Media-gebeurtenis verzenden
description: Verzend mediagegevens naar de Adobe Experience Platform Edge Network.
source-git-commit: 639d3d3d8bfb51e6c97066aee61271d0b00ec455
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 0%

---

# Media-gebeurtenis verzenden

Met de handeling **[!UICONTROL Send media event]** wordt de media-gebeurtenis naar een gegevensstroom verzonden, die vervolgens kan worden gebruikt door apps en services zoals Adobe Experience Platform of Adobe Analytics. Deze handeling is handig wanneer u streaming media-inhoud bijhoudt op uw eigenschap.

{het beeld van 0} Experience Platform UI die het send scherm van de media gebeurtenis toont.![](../assets/send-media-event.png)

Welke opties beschikbaar zijn, is afhankelijk van de **[!UICONTROL Media event type]** die u selecteert. Voor alle mediagebeurtstypen is een **[!UICONTROL Player ID]** vereist. Dit is de naam van de Content Player.

Sommige gebeurtenistypen bieden de mogelijkheid om andere velden te configureren. Als een media gebeurtenistype niet hier vermeld is, dan is het enige beschikbare gebied [!UICONTROL Player ID]. De volgende mediagebeurtstypen zijn andere velden:

## [!UICONTROL Ad break start]

Hiermee kunt u de details van de advertentiepod configureren.

* **[!UICONTROL Ad break name]**: De vriendelijke naam van het advertentieeinde.
* **[!UICONTROL Ad break offset (seconds)]**: De verschuiving van de advertentie binnen de inhoud, in seconden.
* **[!UICONTROL Ad break index]**: De index van het advertentieeinde binnen de inhoud, die begint bij 1.

## [!UICONTROL Ad start]

Hiermee kunt u advertentiedetails configureren.

* **[!UICONTROL Ad name]**: De vriendelijke naam van de advertentie.
* **[!UICONTROL Ad ID]**: De id van de advertentie. Elke alpha-numerieke waarde wordt ondersteund.
* **[!UICONTROL Ad length (seconds)]**: De lengte van de video en, in seconden.
* **[!UICONTROL Advertiser]**: het bedrijf of merk waarvan het product in de advertentie wordt weergegeven.
* **[!UICONTROL Campaign ID]**: De id van de advertentiecampagne.
* **[!UICONTROL Creative ID]**: De id van de advertentie.
* **[!UICONTROL Creative URL]**: De URL van de advertentie.
* **[!UICONTROL Placement ID]**: De plaatsing-id van de advertentie.
* **[!UICONTROL Site ID]**: De id van de advertentiesite.
* **[!UICONTROL Pod position]**: De index van de advertentie binnen het bovenliggende element en het einde, te beginnen bij 0.

Dit gebeurtenistype ondersteunt ook de mogelijkheid om aangepaste metagegevens te leveren als onderdeel van de payload van een mediagebeurtenis.

## [!UICONTROL Bitrate change]

* **[!UICONTROL Quality of experience data]**: A [&#x200B; Kwaliteit van Ervaring &#x200B;](/help/xdm/data-types/qoe-data-details-collection.md) voorwerp dat bitrate, gelaten vallen kaders, kaders per seconde, en tijd specificeert te beginnen.

## [!UICONTROL Chapter start]

Staat u toe om hoofdstukdetails te vormen.

* **[!UICONTROL Chapter name]**: De naam van het hoofdstuk of segment.
* **[!UICONTROL Chapter length]**: De lengte van het hoofdstuk, in seconden.
* **[!UICONTROL Chapter index]**: De positie van het hoofdstuk binnen de inhoud.
* **[!UICONTROL Chapter offset]**: De verschuiving van het hoofdstuk vanaf het begin van de inhoud, in seconden.

Dit gebeurtenistype ondersteunt ook de mogelijkheid om aangepaste metagegevens te leveren als onderdeel van de payload van een mediagebeurtenis.

## [!UICONTROL Error]

Staat u toe om foutendetails te vormen.

* **[!UICONTROL Error name]**: De foutnaam.
* **[!UICONTROL Source]**: De bron van de fout.

## [!UICONTROL Session start]

Hiermee kunt u de details van mediasessies configureren.

* **[!UICONTROL Handle media session automatically]**: Een selectievakje waarmee de Web SDK automatisch de benodigde pings kan verzenden. U kunt dit vakje deselecteren als u wilt manueel verzenden pings zelf.
* **[!UICONTROL Playhead]**: De afspeelkop, in seconden.
* **[!UICONTROL Content type]**: Het inhoudstype. Elke tekenreekswaarde wordt ondersteund. Adobe biedt ook de volgende voorinstellingen:
   * [!UICONTROL Audiobook]
   * [!UICONTROL Downloaded video-on-demand]
   * [!UICONTROL Linear playback of the media asset]
   * [!UICONTROL Live streaming]
   * [!UICONTROL Podcast]
   * [!UICONTROL Radio show]
   * [!UICONTROL Song]
   * [!UICONTROL User-generated content]
   * [!UICONTROL Video-on-demand]
* **[!UICONTROL Clip length/runtime (seconds)]**: De maximale duur in seconden van de inhoud die wordt verbruikt. Voor live media met een onbekende duur is de waarde van `86400` de standaardwaarde.
* **[!UICONTROL Content ID]**: De inhoud-id van de inhoud.
* **[!UICONTROL Ad load type]**: Het type van de geladen advertentie. De volgende twee waarden worden ondersteund:
   * [!UICONTROL Ads same as TV]
   * [!UICONTROL Other (custom/dynamic ads)]
* **[!UICONTROL Album]**: Het album waartoe het nummer behoort.
* **[!UICONTROL Artist]**: De artiest van het nummer.
* **[!UICONTROL Asset ID]**: De unieke id voor de inhoud van het media-element. Deze id&#39;s worden meestal afgeleid van metagegevensautoriteiten zoals EIDR, TMS/Gracenote of Rovi. Deze id&#39;s kunnen ook afkomstig zijn van andere bedrijfseigen of interne systemen.
* **[!UICONTROL Author]**: De naam van de auteur van de audiobook.
* **[!UICONTROL Authorized]**: Een markering die bepaalt of de gebruiker is aangemeld via Adobe-verificatie.
* **[!UICONTROL Day part]**: De tijd van de dag waarop de inhoud werd uitgezonden of afgespeeld. Elke tekenreekswaarde wordt ondersteund.
* **[!UICONTROL Episode]**: Het nummer van de aflevering.
* **[!UICONTROL Feed type]**: Het type feed.
* **[!UICONTROL First air date]**: De datum waarop de inhoud voor het eerst op televisie is verzonden. Elke tekenreekswaarde wordt ondersteund, maar Adobe raadt u aan de notatie `YYYY-MM-DD` te gebruiken.
* **[!UICONTROL First digital date]**: De datum waarop de inhoud voor het eerst werd verzonden op een digitaal kanaal of platform. Elke tekenreekswaarde wordt ondersteund, maar Adobe raadt u aan de notatie `YYYY-MM-DD` te gebruiken.
* **[!UICONTROL Content name]**: De vriendelijke naam van de inhoud.
* **[!UICONTROL Genre]**: het type of de groep inhoud die door de inhoudsproducent wordt gedefinieerd. Dit veld ondersteunt meerdere waarden, gescheiden door een komma.
* **[!UICONTROL Label]**: De naam van het recordlabel.
* **[!UICONTROL Rating]**: De classificatie zoals gedefinieerd door de Ouderlijke Richtlijnen voor tv.
* **[!UICONTROL MVPD]**: De MVPD zoals opgegeven door Adobe-verificatie.
* **[!UICONTROL Network]**: De netwerk- of kanaalnaam.
* **[!UICONTROL Originator]**: De maker van de inhoud.
* **[!UICONTROL Publisher]**: De uitgever van audio-inhoud.
* **[!UICONTROL Season]**: Als de show deel van een reeks uitmaakt, het seizoenaantal van de show.
* **[!UICONTROL Show]**: Als de show deel van een reeks uitmaakt, de reeksnaam.
* **[!UICONTROL Show type]**: Het weergavetype. Elke tekenreekswaarde wordt ondersteund. Adobe biedt ook de volgende voorinstellingen:
   * [!UICONTROL Clip]
   * [!UICONTROL Full episode]
   * [!UICONTROL Other]
   * [!UICONTROL Preview/trailer]
* **[!UICONTROL Stream type]**: Het streamtype.
* **[!UICONTROL Stream format]**: De indeling van de stream, zoals HD of SD.
* **[!UICONTROL Station]**: De naam of id van het radiostation.

Dit gebeurtenistype ondersteunt ook de mogelijkheid om aangepaste metagegevens te leveren als onderdeel van de payload van een mediagebeurtenis. Het staat ook de configuratieoverschrijvingen van de gegevensstroom toe, die u controle geven over welke apps en de diensten deze gegevens ontvangen. Wanneer u een gegevensstroomconfiguratieopheffing in zowel een individueel bevel als binnen de de configuratiemontages van de markeringsuitbreiding plaatst, neemt het individuele bevel belangrijkheid. Zie [&#x200B; de configuratiemet voeten treedt van de Gegevensstroom &#x200B;](../configure/configuration-overrides.md) voor meer informatie.

## [!UICONTROL States update]

Staat u toe om de details van de staatsupdate te vormen. U kunt de volgende statussen starten of beëindigen:

* [!UICONTROL Closed captioning]
* [!UICONTROL Full screen]
* [!UICONTROL In focus]
* [!UICONTROL Mute]
* [!UICONTROL Picture in picture]

De volgende velden zijn beschikbaar:

* **[!UICONTROL States started]**: Een vervolgkeuzemenu waarmee u kunt aangeven dat een status is gestart. Als u de knop **[!UICONTROL Add another state that started]** selecteert, kunt u meerdere staten in dezelfde handeling starten.
* **[!UICONTROL States ended]**: Een vervolgkeuzemenu waarmee u kunt aangeven dat een staat is beëindigd. Als u de knop **[!UICONTROL Add another state that ended]** selecteert, kunt u meerdere frames in dezelfde handeling beëindigen.
