---
keywords: doelpersonalisatie; bestemming; doelbestemming ervaringsplatform;doelbestemming adobe;
title: Adobe Target-verbinding
description: Adobe Target is een toepassing die realtime, door AI aangedreven personalisatie- en experimentatiemogelijkheden biedt voor alle inkomende klantinteracties voor websites, mobiele apps en nog veel meer.
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: 46e732dfc630ad1875a57289a6e6cf9c964b9547
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 0%

---

# Adobe Target-verbinding {#adobe-target-connection}

## Overzicht {#overview}

Adobe Target is een toepassing die realtime, door AI aangedreven personalisatie- en experimentatiemogelijkheden biedt voor alle inkomende klantinteracties voor websites, mobiele apps en nog veel meer.

Adobe Target is een personalisatieverbinding in Adobe Experience Platform.

## Vereisten {#prerequisites}

Bij het configureren van de Adobe Target-verbinding naar [een gegevensstroom-id gebruiken](#parameters), moet u beschikken over de [Adobe Experience Platform Web SDK](../../../edge/home.md) geïmplementeerd.

Als u de Adobe Target-verbinding configureert zonder een gegevensstroom-id te gebruiken, hoeft u de Web SDK niet te implementeren.

>[!IMPORTANT]
>
>Voordat u een [!DNL Adobe Target] verbinding, lees de gids over hoe te [vorm verpersoonlijkingsbestemmingen voor zelfde-pagina en volgende-pagina verpersoonlijking](../../ui/configure-personalization-destinations.md). Deze gids neemt u door de vereiste configuratiestappen voor zelfde-pagina en volgende-paginagrootte het gebruiksgevallen van het verpersoonlijkingsgebruik, over veelvoudige Experience Platforms. Voor personalisatie op dezelfde pagina en op de volgende pagina moet u een gegevensstroom-id gebruiken wanneer u de Adobe Target-verbinding configureert.

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!DNL Profile request]** | U vraagt om alle segmenten die in de Adobe Target-bestemming zijn toegewezen voor één profiel. |
| Uitvoerfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op segmentevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Gebruiksscenario’s {#use-cases}

**Banner homepage aanpassen**

Een huisverhuurbedrijf en verkoopbedrijf willen hun homepage met een banner personaliseren, die op de kwalificaties van het klantensegment in Adobe Experience Platform wordt gebaseerd. Het bedrijf kan selecteren welk publiek een persoonlijke ervaring zou moeten krijgen en hen naar Adobe Target sturen als doelcriterium voor hun Target-aanbieding.

## Verbinden met de bestemming {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="Informatie over gegevensstroom-id&#39;s"
>abstract="Met deze optie bepaalt u in welke gegevensstroom de segmenten worden opgenomen. Het drop-down menu toont slechts gegevensstromen die de toegelaten configuratie van het Doel hebben. Als u randsegmentatie wilt gebruiken, moet u een gegevensstroom-id selecteren. Als u Geen selecteert, worden alle gevallen uitgeschakeld waarin randsegmentatie wordt gebruikt."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html#parameters" text="Meer informatie over het selecteren van gegevensstromen"

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md).

Adobe Experience Platform maakt automatisch verbinding met het Adobe Target-exemplaar van uw bedrijf. Er is geen verificatie vereist.

### Verbindingsparameters {#parameters}

while [opzetten](../../ui/connect-destination.md) voor deze bestemming moet u de volgende informatie opgeven:

* **Naam**: Vul de voorkeursnaam voor dit doel in.
* **Beschrijving**: Voer een beschrijving in voor uw bestemming. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken. Dit veld is optioneel.
* **DataStream-id**: Dit bepaalt in welke gegevensstroom van de Inzameling van Gegevens de segmenten zullen worden omvat. Het drop-down menu toont slechts gegevensstromen die de toegelaten bestemming van het Doel hebben. Zie [configureren van een gegevensstroom](../../../edge/datastreams/overview.md#target) voor gedetailleerde informatie over hoe te om een gegevensstroom voor Adobe Target te vormen.
   * **[!UICONTROL None]**: Selecteer deze optie als u de personalisatie van Adobe Target moet configureren, maar u de optie [Experience Platform Web SDK](../../../edge/home.md). Als u deze optie gebruikt, ondersteunen segmenten die van Experience Platform naar doel zijn geëxporteerd, alleen verpersoonlijking van volgende sessie en wordt randsegmentatie uitgeschakeld. Zie de onderstaande tabel voor meer informatie.

| Geen gegevensstroom geselecteerd | Gegevensstroom geselecteerd |
|---|---|
| <ul><li>[Randsegmentatie](../../../segmentation/ui/edge-segmentation.md) wordt niet ondersteund.</li><li>[Zelfde pagina en volgende pagina personalisatie](../../ui/configure-personalization-destinations.md) worden niet ondersteund.</li><li>U kunt segmenten alleen voor de productiesandbox delen met de Adobe Target-verbinding.</li><li>Om volgende-zittingsverpersoonlijking te vormen zonder een gegevensstroomidentiteitskaart te gebruiken, gebruik [at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html?lang=en).</li></ul> | <ul><li>De segmentatie van de rand werkt zoals verwacht.</li><li>[Zelfde pagina en volgende pagina personalisatie](../../ui/configure-personalization-destinations.md) worden ondersteund.</li><li>Delen van segmenten wordt ondersteund voor andere sandboxen.</li></ul> |

## Segmenten naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Lezen [Profielen en segmenten activeren om aanvraagdoelen te profileren](../../ui/activate-profile-request-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

## Geëxporteerde gegevens {#exported-data}

Adobe Target leest profielgegevens van het Adobe Experience Platform Edge Network, zodat er geen gegevens worden geëxporteerd.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] dwingt gegevensbeheer af, lees de [Overzicht van gegevensbeheer](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).
