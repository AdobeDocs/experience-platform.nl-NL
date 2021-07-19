---
keywords: Experience Platform;huis;populaire onderwerpen;segmentatie;Segmentatie;Segmentovereenkomst;segmentovereenkomst
solution: Experience Platform
title: Overzicht van afstemming van segment
topic-legacy: overview
description: Segmentovereenkomst is een segmentdelende service in Adobe Experience Platform waarmee twee of meer gebruikers in het Platform segmentgegevens kunnen uitwisselen op een veilige, beheerde en privacyvriendelijke manier.
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '1825'
ht-degree: 0%

---


# (Alfa) Overzicht [!DNL Segment Match]

>[!IMPORTANT]
>
>[!DNL Segment Match] bevindt zich momenteel in alfa. De documentatie en de functionaliteit kunnen worden gewijzigd.

Adobe Experience Platform Segment Match is een segment-delende dienst die voor twee of meer gebruikers van het Platform toestaat om segmentgegevens op een veilige, beheerde, en privacy-vriendelijke manier uit te wisselen. [!DNL Segment Match] gebruikt de privacynormen van het Platform en persoonlijke herkenningstekens zoals gehakte e-mails, gehakte telefoonaantallen, en apparatenherkenningstekens zoals IDFAs en GAIDs.

Met [!DNL Segment Match] kunt u:

* Het overlappingsproces van de identiteit beheren.
* Schattingen vóór het delen weergeven.
* Pas de etiketten van het gegevensgebruik toe om te controleren of de gegevens met partners kunnen worden gedeeld.
* Behoud het beheer van de levenscyclus van het gedeelde publiek na het publiceren van een voer en zet een dynamische uitwisseling van gegevens door mogelijkheden voort om toe te voegen, te schrappen, en te delen.

[!DNL Segment Match] gebruikt een proces van identiteitsoverlapping om ervoor te zorgen dat het delen van segmenten op een veilige en privacy-gerichte manier wordt gedaan. Een **overlappende identiteit** is een identiteit die een gelijke in zowel uw segment als het segment van uw geselecteerde partner heeft. Voordat een segment wordt gedeeld tussen een afzender en een ontvanger, wordt tijdens het proces voor identiteitsoverlap gecontroleerd of er sprake is van overlapping in naamruimten en toestemmingscontroles tussen de verzender en de ontvanger(s). Beide overlappende controles moeten overgaan opdat een segment wordt gedeeld.

De volgende secties verstrekken meer informatie over [!DNL Segment Match], met inbegrip van details over opstelling en zijn end-to-end werkschema.

## Instellen

In de volgende secties wordt beschreven hoe u [!DNL Segment Match] kunt instellen en configureren:

### Identiteitsgegevens en naamruimten instellen {#namespaces}

De eerste stap om met [!DNL Segment Match] te beginnen is ervoor te zorgen u gegevens tegen gesteunde identiteitsnamespaces inkt.

Identiteitsnaamruimten zijn een onderdeel van [Adobe Experience Platform Identity Service](../../identity-service/home.md). Elke identiteit van de klant bevat een bijbehorende naamruimte die de context van de identiteit aangeeft. Een naamruimte kan bijvoorbeeld een waarde van &quot;name<span>@email.com&quot; onderscheiden als e-mailadres of &quot;443522&quot; als een numerieke CRM-id.

Een volledig gekwalificeerde identiteit omvat een waarde van identiteitskaart en een namespace. Wanneer recordgegevens worden vergeleken met profielfragmenten (bijvoorbeeld wanneer [!DNL Real-time Customer Profile] profielgegevens samenvoegt), moeten zowel de identiteitswaarde als de naamruimte overeenkomen.

In de context van [!DNL Segment Match], worden namespaces gebruikt in het overlappingsproces wanneer het delen van gegevens.

De lijst met ondersteunde naamruimten ziet er als volgt uit:

| Naamruimte | Beschrijving |
| --------- | ----------- |
| E-mails (SHA256, verlaagd) | A namespace for pre-hashed email address. Waarden die in deze naamruimte worden opgegeven, worden omgezet in kleine letters voordat er een hash plaatsvindt met SHA256. De spaties aan het begin en aan het einde moeten worden bijgesneden alvorens een e-mailadres wordt genormaliseerd. Deze instelling kan niet met terugwerkende kracht worden gewijzigd. Raadpleeg het volgende document over [SHA256-hash-ondersteuning](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html?lang=en#hashing-support) voor meer informatie. |
| Telefoon (SHA256_E.164) | A namespace that represents raw phone numbers that need to be hashed using both SHA256 and E.164 format. |
| ECID | Een naamruimte die een ECID-waarde (Experience Cloud ID) vertegenwoordigt. Naar deze naamruimte kan ook worden verwezen door de volgende aliassen: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Zie het [ECID-overzicht](../../identity-service/ecid.md) voor meer informatie. |
| Apple IDFA (ID for Advertisers) | Een naamruimte die Apple-id voor adverteerders vertegenwoordigt. Zie het volgende document op [op rente-gebaseerde advertenties](https://support.apple.com/en-us/HT202074) voor meer informatie. |
| Google-advertentie-id | Een naamruimte die staat voor een Google-advertentie-id. Raadpleeg het volgende document op [Google Advertising ID](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en) voor meer informatie. |

### Configuratie van toestemming instellen

U moet een toestemmingsconfiguratie verstrekken en zijn standaardwaarde aan of `opt-in` of `opt-out` voor een toestemmingscontrole plaatsen.

De controle van de opt-in en opt-out toestemming bepaalt of u met de toestemming kunt werken om gebruikersgegevens door gebrek te delen. Als het gebrek van de toestemmingsconfiguratie aan `opt-in` wordt geplaatst, dan kunnen de gebruikersgegevens worden gedeeld, tenzij een gebruiker uitdrukkelijk kiest uit. Als het gebrek aan `opt-out` wordt geplaatst, dan kunnen de gebruikersgegevens niet worden gedeeld, tenzij een gebruiker uitdrukkelijk binnen kiest.

De standaardtoestemmingsconfiguratie voor [!DNL Segment Match] wordt geplaatst aan `opt-out`. Als u een aanmeldingsmodel voor uw gegevens wilt afdwingen, stuurt u een e-mailverzoek naar uw accountmanager van Adobe.

Voor meer informatie over het `share` attribuut dat wordt gebruikt om gegeven-delend toestemmingswaarde te plaatsen, zie de volgende documentatie op [privacy en toestemmingsgebiedgroep](../../xdm/field-groups/profile/consents.md). Voor informatie over de specifieke gebiedsgroep die wordt gebruikt om de toestemming van de consument voor inzameling en gebruik van gegevens te vangen met betrekking tot privacy, verpersoonlijking en marketing voorkeur, zie het volgende [Toestemming voor Privacy, Personalisatie en het In de handel brengen Voorkeur GitHub voorbeeld](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/consent/consent-preferences.schema.md).

### Gegevensgebruikslabels configureren

De laatste voorwaarde u moet vestigen is een nieuw etiket van het gegevensgebruik te vormen om gegevens te verhinderen delend. Via labels voor gegevensgebruik kunt u bepalen welke gegevens mogen worden gedeeld via [!DNL Segment Match].

Met labels voor gegevensgebruik kunt u gegevenssets en velden categoriseren op basis van het gebruiksbeleid dat op die gegevens van toepassing is. Labels kunnen op elk gewenst moment worden toegepast, zodat u op flexibele wijze gegevens kunt beheren. De beste praktijken bevorderen etiketteringsgegevens zodra het in Experience Platform wordt opgenomen, of zodra de gegevens voor gebruik in Platform beschikbaar worden.

[!DNL Segment Match] gebruikt het etiket C11, een contractetiket specifiek voor  [!DNL Segment Match] dat u aan om het even welke datasets of attributen manueel kunt toevoegen om ervoor te zorgen dat zij van het  [!DNL Segment Match] partner-delend proces worden uitgesloten. Het label C11 geeft gegevens aan die niet mogen worden gebruikt in processen [!DNL Segment Match]. Nadat u hebt bepaald welke datasets en/of gebieden u van [!DNL Segment Match] wilt uitsluiten en dienovereenkomstig het etiket C11 toevoegt, wordt het etiket automatisch afgedwongen door de [!DNL Segment Match] werkschema. [!DNL Segment Match] het  [!UICONTROL Restrict data sharing] kernbeleid wordt automatisch ingeschakeld. Voor specifieke instructies op hoe te om de etiketten van het gegevensgebruik op datasets toe te passen, zie de zelfstudie over [het beheren van de etiketten van het gegevensgebruik in UI](../../data-governance/labels/user-guide.md).

Voor een lijst van de etiketten van het gegevensgebruik en hun definities, zie [de verklarende woordenlijst van de etiketten van het gegevensgebruik](../../data-governance/labels/reference.md). Voor informatie over het beleid van het gegevensgebruik, zie [beleidsoverzicht van het gegevensgebruik](../../data-governance/policies/overview.md).

## [!DNL Segment Match] end-to-end workflow

Zodra u opstelling uw identiteitsgegevens en namespaces, toestemmingsconfiguratie, en het etiket van het gegevensgebruik hebt, kunt u beginnen met het werken met [!DNL Segment Match] en zijn eigenschappen.

### Partner beheren

In Platform UI, selecteer **[!UICONTROL Segments]** van de linkernavigatie en selecteer dan **[!UICONTROL Feeds]** van de hoogste kopbal.

![segments-feed.png](../images/ui/segment-match/segments-feed.png)

De pagina [!UICONTROL Feeds] bevat een lijst met feeds die zijn ontvangen van partners en feeds die u hebt gedeeld. Om een lijst van bestaande partners te bekijken of een verbinding met een nieuwe partner te vestigen, uitgezocht **[!UICONTROL Manage partners]**.

![manage-partners.png](../images/ui/segment-match/manage-partners.png)

Een verbinding tussen twee partners is een &quot;bidirectionele handdruk&quot;die als zelfbediening methode voor gebruikers dienst doet om hun organisaties van het Platform op een zandbakniveau samen te verbinden. De verbinding is vereist om het Platform te informeren dat een overeenkomst is gesloten en dat Platform de deelservices tussen u en uw partner(s) kan vergemakkelijken.

>[!NOTE]
>
>De &quot;bidirectionele handdruk&quot;tussen u en uw partner is strikt een verbinding. Tijdens dit proces worden geen gegevens uitgewisseld.

U kunt een lijst van verbindingen met bestaande partners in de belangrijkste interface van het [!UICONTROL Manage partners] scherm bekijken. Op de rechterspoorlijn is het [!UICONTROL Share setting] paneel, dat u van de optie voorziet om nieuwe [!UICONTROL connect ID] evenals een inputdoos te produceren waar u [!UICONTROL connect ID] van een partner kunt ingaan.

![determine-connection.png](../images/ui/segment-match/establish-connection.png)

Als u een nieuwe [!UICONTROL connect ID] wilt maken, selecteert u **[!UICONTROL Regenerate]** onder [!UICONTROL Share setting] en selecteert u vervolgens het kopieerpictogram naast de zojuist gegenereerde id.

![delen-instelling.png](../images/ui/segment-match/share-setting.png)

Als u een partner wilt verbinden met behulp van de [!UICONTROL connect ID], voert u de unieke id-waarde in het invoervak onder [!UICONTROL Connect partner] in en selecteert u **[!UICONTROL Request]**.

![connect-partner.png](../images/ui/segment-match/connect-partner.png)

### Feed maken

Een **feed** is een groepering van gegevens (segmenten), de regels voor hoe die gegevens kunnen worden blootgesteld of gebruikt, en de configuraties die bepalen hoe uw gegevens tegen de gegevens van uw partners worden aangepast. Een feed kan onafhankelijk worden beheerd en via [!DNL Segment Match] worden uitgewisseld met andere gebruikers in de Platform.

Als u een nieuwe feed wilt maken, selecteert u **[!UICONTROL Create feed]** in het dashboard [!UICONTROL Feeds].

![create-feed.png](../images/ui/segment-match/create-feed.png)

De basisopstelling van een voer omvat een naam, een beschrijving, en configuraties betreffende marketing gebruiksgevallen en identiteitsmontages. Geef een naam en een beschrijving voor uw feed op en pas vervolgens de gevallen van marketinggebruik toe waarvan u wilt dat uw gegevens worden uitgesloten. U kunt meerdere keren hoofdlettergebruik selecteren in een lijst met:

* [!UICONTROL Analytics]
* [!UICONTROL Combine with PII]
* [!UICONTROL Cross-site targeting]
* [!UICONTROL Data Science]
* [!UICONTROL Email targeting]
* [!UICONTROL Export to third party]
* [!UICONTROL Onsite advertising]
* [!UICONTROL Onsite personalization]
* [!UICONTROL Segment Match]
* [!UICONTROL Single identity personalization]

Selecteer ten slotte de juiste naamruimten voor uw feed. Zie de [tabel met identiteitsgegevens en naamruimten](#namespaces) voor informatie over de specifieke naamruimten die worden ondersteund door [!DNL Segment Match]. Selecteer **[!UICONTROL Next]** als u klaar bent.

![publiek delen.png](../images/ui/segment-match/audience-sharing.png)

Zodra u de montages van uw voer hebt gevestigd, selecteer de segmenten u van uw lijst van eerste-partijsegmenten wilt delen. U kunt meer van één segment uit de lijst selecteren en u kunt de juiste spoorlijn gebruiken om uw lijst van geselecteerde segmenten te beheren. Als u klaar bent, selecteert u **[!UICONTROL Next]**.

![select-segments.png](../images/ui/segment-match/select-segments.png)

De [!UICONTROL Share] pagina verschijnt, die u van een interface voorzien om de partners te selecteren u uw voer met wilt delen. Tijdens deze stap, kunt u het pre-aandeel overlap schattingsrapport ook bekijken en het aantal overlappende identiteiten door namespace tussen u en uw partner zien, het aantal overlappende identiteiten die toestemming hebben om gegevens te delen.

Selecteer **[!UICONTROL Analyze by segment]** om het schattingsrapport te bekijken.

![analyze.png](../images/ui/segment-match/analyze.png)

Het overlappende ramingenrapport staat u toe om overlappende en toestemmingscontroles per partner en per segment te beheren alvorens uw voer te delen.

| Metrics | Beschrijving |
| ------- | ----------- |
| Geschatte identiteiten met toestemming | Het totale aantal overlappende identiteiten die aan de toestemmingsvereisten voldoen die voor uw organisatie worden gevormd. |
| Geschatte overlappende identiteiten | Het aantal identiteiten die voor het geselecteerde segment kwalificeren en ook een gelijke met de geselecteerde partner hebben. Deze identiteiten worden weergegeven door naamruimte en vertegenwoordigen geen individuele profielidentiteiten. De overlap schattingen zijn gebaseerd op profielschetsen. |

Selecteer **[!UICONTROL Close]** als u klaar bent.

![overlap-rapport.png](../images/ui/segment-match/overlap-report.png)

Nadat u uw partners hebt geselecteerd en het rapport voor overlappende ramingen hebt bekeken, selecteert u **[!UICONTROL Next]** om door te gaan.

![share.png](../images/ui/segment-match/share.png)

De stap [!UICONTROL Review] wordt weergegeven, zodat u uw nieuwe feed kunt bekijken voordat deze wordt gedeeld en gepubliceerd. Deze stap omvat details over de identiteitsinstelling die u toepaste, evenals informatie over de gevallen, segmenten en partners van het marketinggebruik die u hebt geselecteerd.

Selecteer **[!UICONTROL Finish]** om door te gaan.

![review.png](../images/ui/segment-match/review.png)

### Feed bijwerken

Als u segmenten wilt toevoegen of verwijderen, selecteert u **[!UICONTROL Create feed]** op de pagina [!UICONTROL Feeds] en selecteert u **[!UICONTROL Existing feed]**. Selecteer in de lijst met bestaande feed die wordt weergegeven de feed die u wilt bijwerken en selecteer **[!UICONTROL Next]**.

![voederlijst](../images/ui/segment-match/feed-list.png)

De lijst met segmenten wordt weergegeven. Van hieruit kunt u nieuwe segmenten aan uw feed toevoegen en kunt u de rechterrail gebruiken om segmenten te verwijderen die u niet meer nodig hebt. Nadat u de segmenten in uw feed hebt beheerd, selecteert u **[!UICONTROL Next]** en voert u de hierboven beschreven stappen uit om de bijgewerkte feed te voltooien.

![update](../images/ui/segment-match/update.png)

>[!NOTE]
>
>Wanneer u toevoegt of een segment uit een gedeelde voer verwijdert, moet de ontvangende partner de verandering bevestigen door [!DNL Profile] knevel in hun lijst van ontvangen voer opnieuw toe te laten.

### Een inkomende feed accepteren

Als u een binnenkomende feed wilt weergeven, selecteert u **[!UICONTROL Received]** in de koptekst van de pagina [!UICONTROL Feeds] en selecteert u vervolgens de feed die u in de lijst wilt weergeven. Als u de feed wilt accepteren, selecteert u **[!UICONTROL Enable for profile]** en laat u de status enkele ogenblikken bijwerken van [!UICONTROL Pending] naar [!UICONTROL Enabled].

![receive.png](../images/ui/segment-match/received.png)

Nadat u een gedeelde feed hebt geaccepteerd, kunt u beginnen met het gebruik van de gedeelde gegevens om nieuwe segmenten te maken.

## Volgende stappen

Door dit document te lezen hebt u inzicht gekregen in [!DNL Segment Match], de mogelijkheden ervan en de end-to-end workflow. Raadpleeg de volgende documenten voor meer informatie over andere services van Platforms:

* [[!DNL Segmentation Service]](../home.md)
* [[!DNL Identity Service]](../../identity-service/home.md)
* [[!DNL Real-time Customer Profile] - overzicht](../../profile/home.md)
