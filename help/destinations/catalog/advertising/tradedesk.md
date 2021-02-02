---
keywords: reclame; de handelsdienst;
title: De bestemming van het handelsbureau
seo-title: De bestemming van het handelsbureau
description: 'De Trade Desk is een zelfbedieningsplatform waarmee adverteerders doelgerichte digitale campagnes kunnen voeren op het hele scherm, de video en de mobiele voorraad. '
seo-description: De Trade Desk is een zelfbedieningsplatform waarmee adverteerders doelgerichte digitale campagnes kunnen voeren op het hele scherm, de video en de mobiele voorraad.
translation-type: tm+mt
source-git-commit: 95f57f9d1b3eeb0b16ba209b9774bd94f5758009
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---


# [!DNL The Trade Desk] doel

## Overzicht {#overview}

[!DNL The Trade Desk] doel helpt u profielgegevens te verzenden naar  [!DNL The Trade Desk].

[!DNL The Trade Desk] is een zelfbedieningsplatform dat kopers van advertenties in staat stelt doelgerichte digitale campagnes uit te voeren op het hele scherm, de video en mobiele inventarisatiebronnen.

Als u profielgegevens naar [!DNL The Trade Desk] wilt verzenden, moet u eerst verbinding maken met het doel.

## Doelspecificaties {#destination-specs}

Let op de volgende details die specifiek zijn voor het doel [!DNL The Trade Desk]:

* U kunt de volgende [identiteiten](../../../identity-service/namespaces.md) naar [!DNL The Trade Desk] bestemmingen verzenden: [!DNL The Trade Desk ID], [!DNL IDFA], [!DNL GAID].

## Gebruiksscenario’s {#use-cases}

Als markeerteken, wil ik segmenten kunnen gebruiken die van [!DNL Trade Desk IDs] of apparaat IDs worden gebouwd om het opnieuw richten of publiek gerichte digitale campagnes tot stand te brengen.

## Type exporteren {#export-type}

**[!DNL Segment export]** - u exporteert alle leden van een segment (publiek) naar de bestemming.

## Verbinden met doel {#connect-destination}

Selecteer **[!UICONTROL Verbindingen]** > **[!UICONTROL Doelen]** en selecteer [!DNL The Trade Desk] en **[!UICONTROL Configureren]**.

![Vorm de bestemming van de handelsbureau](../../assets/catalog/advertising/tradedesk/configure.png)

>[!NOTE]
>
>Als er al een verbinding met dit doel bestaat, kunt u een **[!UICONTROL knop Activeer]** op de doelkaart zien. Voor meer informatie over het verschil tussen **[!UICONTROL Activate]** en **[!UICONTROL Configure]**, verwijs naar [Catalog](../../ui/destinations-workspace.md#catalog) sectie van de documentatie van de bestemmingswerkruimte.
>
>![Activeer de bestemming van het handelsbureau](../../assets/catalog/advertising/tradedesk/activate.png)

In de stap [!UICONTROL Authentication] moet u [!DNL The Trade Desk] verbindingsdetails invoeren:

* **[!UICONTROL Naam]**: Een naam waarmee u deze bestemming in de toekomst zult erkennen.
* **[!UICONTROL Omschrijving]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Account-id]**: Je  [!DNL Trade Desk] [!UICONTROL account-id].
* **[!UICONTROL Clientgeheim]**: De  `clientSecret` parameter die in de  [!DNL OAuth2] clientreferenties wordt gebruikt.
* **[!UICONTROL Serverlocatie]**: Vraag uw  [!DNL The Trade Desk] vertegenwoordiger welke regionale server u zou moeten gebruiken. Dit zijn de beschikbare regionale servers waaruit u kunt kiezen:

   * **[!UICONTROL Europa]**
   * **[!UICONTROL Singapore]**
   * **[!UICONTROL Tokyo]**
   * **[!UICONTROL Noord-Amerika Oost]**
   * **[!UICONTROL North America West]**
   * **[!UICONTROL Latijns-Amerika]**

* **[!UICONTROL Geval]** voor gebruik bij het in de handel brengen: Gebruiksgevallen voor marketingdoeleinden geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door de Adobe gedefinieerde gebruiksgevallen voor marketingdoeleinden of u kunt uw eigen gebruiksscenario voor marketingdoeleinden maken. Zie de pagina [Gegevensbeheer in Adobe Experience Platform](../../../data-governance/policies/overview.md) voor meer informatie over gevallen van marketinggebruik. Zie [Overzicht van beleidsregels voor gegevensgebruik](../../../data-governance/policies/overview.md) voor informatie over de afzonderlijke door Adobe gedefinieerde gevallen van marketinggebruik.

![De Stap van de Authentificatie van de Handelsdesk](../../assets/catalog/advertising/tradedesk/authenticate.png)

Klik **[!UICONTROL Doel maken]**. Uw doel is nu gemaakt. U kunt [!UICONTROL Opslaan &amp; afsluiten] klikken als u segmenten later wilt activeren, of u kunt [!UICONTROL Volgende] selecteren om de workflow voort te zetten en segmenten te selecteren om te activeren. In beide gevallen raadpleegt u de volgende sectie [Segmenten activeren](#activate-segments) voor de rest van de workflow.

## Segmenten {#activate-segments} activeren

Zie [Profielen en segmenten activeren naar een doel](../../ui/activate-destinations.md#select-attributes) voor informatie over de workflow voor segmentactivering.

In [Segmentprogramma](../../ui/activate-destinations.md#segment-schedule) stap, moet u uw segmenten aan hun overeenkomstige identiteitskaart of vriendschappelijke naam in de bestemming manueel in kaart brengen.

Wanneer het in kaart brengen van segmenten, adviseren wij u de [!DNL Platform] segmentnaam of een kortere vorm van het, voor gemak van gebruik te gebruiken. Nochtans, te hoeven segmentidentiteitskaart of de naam in uw bestemming niet om in uw [!DNL Platform] rekening aan te passen. Elke waarde die u in het toewijzingsveld invoegt, wordt weerspiegeld door het doel.

Als u veelvoudige apparatenafbeeldingen (koekje IDs, [!DNL IDFA], [!DNL GAID]) gebruikt, zorg ervoor om de zelfde toewijzingswaarde voor alle drie afbeeldingen te gebruiken. [!DNL The Trade Desk] zij zullen allen in één enkel segment, met een apparaat-vlakke onderbreking bijeenvoegen.

![Id voor segmenttoewijzing](../../assets/common/segment-mapping-id.png)

## Geëxporteerde gegevens {#exported-data}

Controleer uw [!DNL The Trade Desk]-account om te controleren of gegevens zijn geëxporteerd naar de [!DNL The Trade Desk]-bestemming. Als de activering succesvol was, worden de soorten publiek in uw account ingevuld.
