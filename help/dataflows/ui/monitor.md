---
title: Overzicht van het dashboard controleren
description: Leer hoe u het dashboard voor bewaking gebruikt in de gebruikersinterface van Adobe Experience Platform
exl-id: 06ea5380-d66e-45ae-aa02-c8060667da4e
source-git-commit: cca405c58551a52a044ac513921298637974e88e
workflow-type: tm+mt
source-wordcount: '951'
ht-degree: 0%

---

# Overzicht van het dashboard controleren

Met het dashboard voor bewaking in de gebruikersinterface van Adobe Experience Platform kunt u de reis van uw gegevens van inname naar activering bekijken. Met het controledashboard kunt u:

* Controleer de reis van uw gegevens van Bronnen, de Dienst van de Identiteit, het Profiel van de Klant in real time, Soorten publiek, en tenslotte in Doelen.
* U kunt verschillende metriek en statussen weergeven, afhankelijk van het werkgebied waarin de gegevens zich bevinden.
* Filter de weergave voor gegevenscontrole op het gegevenstype.

Het controledashboard ondersteunt de weergave van verschillende gegevenstypen:

* **Klant &amp; Rekening**: De gegevens van de Klant verwijzen naar de gegevens die in [&#x200B; Real-Time Customer Data Platform &#x200B;](../../rtcdp/home.md) worden gebruikt, terwijl de rekeningsgegevens naar [&#x200B; gegevens van rekeningsprofielen &#x200B;](../../rtcdp/accounts/account-profile-overview.md) verwijzen die wanneer geabonneerd aan [&#x200B; Real-Time CDP, B2B edition &#x200B;](../../rtcdp/b2b-overview.md) toegankelijk zijn. Als uw Real-Time CDP-licentie Real-Time CDP, B2B edition niet bevat, kunt u alleen het dashboard voor bewaking gebruiken om de klantgegevens te controleren.
* **Vooruitzicht**: [&#x200B; de profielen van het Vooruitzicht &#x200B;](../../profile/ui/prospect-profile.md) worden gebruikt om mensen te vertegenwoordigen die nog niet met uw bedrijf in dienst hebben genomen maar u wilt bereiken. Met perspectiefprofielen, kunt u uw klantenprofielen met attributen van vertrouwde op derdepartners aanvullen. U moet een licentie hebben met Real-Time CDP (App Service), Adobe Experience Platform Activation, Real-Time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate om het gegevenstype voor perspectiefgegevens te kunnen bekijken.
* **de profielverrijking van de Rekening**: De profielen van de rekening laten u toe om rekeningsinformatie uit veelvoudige bronnen te verenigen. U moet een licentie hebben voor Real-Time CDP, B2B edition om de gegevens over de verrijking van het accountprofiel te controleren.

Lees dit document om te leren hoe u het dashboard voor bewaking kunt gebruiken om de reis van uw gegevens over verschillende Experience Platform-services te volgen.

## Aan de slag

Voor dit document is een goed begrip van de volgende Experience Platform-componenten vereist:

* [&#x200B; Dataflows &#x200B;](../home.md): Dataflows zijn vertegenwoordiging van gegevensbanen die gegevens over Experience Platform bewegen. U kunt de werkruimte voor bronnen gebruiken om gegevensstromen te maken die gegevens van een bepaalde bron naar Experience Platform invoeren.
* [&#x200B; Bronnen &#x200B;](../../sources/home.md): De bronnen van het gebruik in Experience Platform om gegevens van een toepassing van Adobe of een derdegegevensbron in te voeren.
* [&#x200B; Dienst van de Identiteit &#x200B;](../../identity-service/home.md): Verkrijg een betere mening van individuele klanten en hun gedrag door identiteiten over apparaten en systemen te overbruggen.
* [&#x200B; Real-Time Profiel van de Klant &#x200B;](../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [&#x200B; Segmentatie &#x200B;](../../segmentation/home.md): Gebruik de Dienst van de Segmentatie om segmenten en publiek van uw gegevens van het Profiel van de Klant in real time tot stand te brengen.
* [&#x200B; Doelen &#x200B;](../../destinations/home.md): De bestemmingen zijn pre-gebouwde integratie met algemeen gebruikte toepassingen die voor de naadloze activering van gegevens van Experience Platform voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen toestaan.

## Handleiding voor het controledashboard

Selecteer in de gebruikersinterface van Experience Platform **[!UICONTROL Monitoring]** onder [!UICONTROL Data Management] in de linkernavigatie.

![&#x200B; het controledashboard in Experience Platform UI.](../assets/ui/monitor-overview/monitoring.png)

Selecteer **[!UICONTROL Data Type]** en gebruik vervolgens het vervolgkeuzemenu om het type gegevens te selecteren dat u wilt weergeven. De gegevenstypes worden bepaald door het schemaklassen van het Model van de Gegevens van de Ervaring (XDM) om ervoor te zorgen dat hun gegevens een standaardformaat wanneer ingebed in Experience Platform volgen. Raadpleeg de volgende documentatie voor meer informatie:

* [B2B-rekeninggegevenstype](../../rtcdp/b2b-tutorial.md)
* [Gegevenstype prospectie](../../rtcdp/partner-data/prospecting.md)

U kunt de weergave filteren op basis van de volgende gegevenstypen:

>[!BEGINTABS]

>[!TAB  allen ]

Selecteer **[!UICONTROL All]** om uw dashboard bij te werken en metriek weer te geven voor alle gegevens die gedurende een bepaalde periode aan Experience Platform zijn toegevoegd.

![&#x200B; het type van controlegegevens dat aan &quot;allen&quot;wordt geplaatst.](../assets/ui/monitor-overview/all.png)

>[!TAB  Klant &amp; Rekening ]

Selecteer **[!UICONTROL Customer & Account]** om uw dashboard bij te werken en metriek weer te geven op Customer &amp; Account-gegevens die gedurende een bepaalde periode aan Experience Platform zijn doorgegeven.

![&#x200B; het type van controlegegevens dat aan &quot;Klant &amp; Rekening&quot;wordt geplaatst.](../assets/ui/monitor-overview/customer-account.png)

>[!TAB  de profielverrijking van de Rekening ]

Selecteer **[!UICONTROL Account profile enrichment]** om het dashboard bij te werken en metriek weer te geven op de gegevens voor profielverrijking. **Nota**: U kunt de metriek van de de profielverrijking van de rekening slechts bekijken als u [&#x200B; B2B- gegevens &#x200B;](../../rtcdp/b2b-tutorial.md) gerechtigd bent.

![&#x200B; het type van controlegegevens dat aan &quot;de profielverrijking van de Rekening&quot;wordt geplaatst.](../assets/ui/monitor-overview/account-profile-enrichment.png)

>[!ENDTABS]

Gebruik de bovenste koptekst van het dashboard voor een ervaring van cross-service controle. U kunt uw metriek en grafiekmening filtreren door de eigenschapkaart van uw keus van de kopbal van de gegevenscategorie te selecteren.

>[!BEGINTABS]

>[!TAB  het meer van Gegevens ]

Selecteer **[!UICONTROL Data lake]** om metriek op uw gegevens te bekijken het meer inname tarief. Lees de gids over [&#x200B; controle gegevens meer ingeslikt &#x200B;](monitor-sources.md) voor meer informatie.

![&#x200B; het controledashboard in UI met de geselecteerde kaart van het gegevensmeer.](../assets/ui/monitor-overview/data-lake.png)

>[!TAB  Identiteiten ]

Selecteer **[!UICONTROL Identities]** om de snelheid te bekijken waarmee uw identiteitsgegevens zijn verwerkt. Lees de gids over [&#x200B; controleidentiteitsgegevens &#x200B;](monitor-identities.md) voor meer informatie.

![&#x200B; het controledashboard in UI met geselecteerde identiteitskaart.](../assets/ui/monitor-overview/identities.png)

>[!TAB  Profielen ]

Selecteer **[!UICONTROL Profiles]** om de successnelheid van de verwerking van uw profielgegevens weer te geven. Lees de gids over [&#x200B; controleprofielgegevens &#x200B;](monitor-profiles.md) voor meer informatie.

![&#x200B; het controledashboard in UI met de geselecteerde profielkaart.](../assets/ui/monitor-overview/profiles.png)

>[!TAB Doelgroepen]

Selecteer **[!UICONTROL Audiences]** om metriek op uw publiek en segmentatietaken weer te geven. Lees de gids over [&#x200B; controlerende publieksgegevens &#x200B;](monitor-audiences.md) voor meer informatie.

![&#x200B; het controledashboard in de UI met de geselecteerde publiekskaart.](../assets/ui/monitor-overview/audiences.png)

>[!TAB Doelen]

Selecteer **[!UICONTROL Destinations]** om metriek op uw [!UICONTROL Streaming activate rate] en [!UICONTROL Batch failed dataflow runs] weer te geven. Lees de gids over [&#x200B; controledoelgegevens &#x200B;](monitor-destinations.md) voor meer informatie.

![&#x200B; het controledashboard in UI met de geselecteerde bestemmingskaart.](../assets/ui/monitor-overview/destinations.png)

>[!ENDTABS]

### Bewakingstijdframe configureren {#configure-monitoring-time-frame}

Standaard worden op het dashboard voor bewaking meetgegevens weergegeven over gegevens die in de afgelopen 24 uur zijn ingevoerd. Selecteer **[!UICONTROL Last 24 hours]** als u het tijdframe wilt bijwerken.

![&#x200B; het controledashboard in UI met de geselecteerde tijdconfiguratie.](../assets/ui/monitor-overview/select-time.png)

U kunt een nieuw tijdkader voor uw gegevens controlemening in het dialoogvenster vormen dat verschijnt. U kunt een aangepast tijdframe maken of een keuze maken in de lijst met vooraf geconfigureerde opties:

* [!UICONTROL Last 24 hours]
* [!UICONTROL Last 7 days]
* [!UICONTROL Last 30 days]

Selecteer **[!UICONTROL Apply]** als u klaar bent.

![&#x200B; de configuratie van het tijdkader pop - op venster in het controledashboard.](../assets/ui/monitor-overview/update-time.png)

## Volgende stappen

Door dit document te lezen, kunt u nu door het controledashboard in UI navigeren. Lees de onderstaande documentatie voor informatie over hoe u gegevens voor een specifieke Experience Platform-service kunt controleren:

* [&#x200B; de opname van het gegevenspeer van de Monitor &#x200B;](monitor-sources.md).
* [&#x200B; de identiteitsgegevens van de Monitor &#x200B;](monitor-identities.md).
* [&#x200B; de profielgegevens van de Monitor &#x200B;](monitor-profiles.md).
* [&#x200B; de publieksgegevens van de Monitor &#x200B;](monitor-audiences.md).
* [&#x200B; de bestemmingsgegevens van de Monitor &#x200B;](monitor-destinations.md).

<!-- >[!TAB Prospect]

Select **[!UICONTROL Prospect]** to update your dashboard and display metrics on prospecting data that has been ingested to Experience Platform over the course of a given period. **Note**: You can only view prospect data type activities if you are [entitled to prospect data](../../rtcdp/partner-data/prospecting.md). -->