---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen;API;verenigd profiel;verenigd profiel;verenigd profiel;profiel;rtcp;inschakelen profiel;profiel inschakelen
title: Real-time handleiding voor de API voor klantprofiel
topic: guide
description: Met de realtime-API voor klantprofiel kunnen ontwikkelaars profielgegevens verkennen en ermee werken, waaronder weergaveprofielen, beleid voor samenvoegen maken en bijwerken, profielgegevens exporteren of samplen en profielgegevens verwijderen die niet langer vereist zijn of die door een fout zijn toegevoegd. Volg deze handleiding voor het uitvoeren van toetsbewerkingen met de API.
translation-type: tm+mt
source-git-commit: 24a5af0440f58b4e1db639ec971c4e1611f107d8
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] API-handleiding

[!DNL Real-time Customer Profile] kunt u een holistische weergave van elk van uw individuele klanten in Adobe Experience Platform bekijken. [!DNL Profile] staat u toe om verschillende klantengegevens van veelvoudige kanalen, zoals online, off-line, CRM, en derdegegevens, in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt.

De [!DNL Real-time Customer Profile] API bevat meerdere eindpunten, die hieronder worden beschreven. Gelieve te bezoeken de individuele eindpuntgidsen voor details en te verwijzen naar [begonnen gids](getting-started.md) voor belangrijke informatie over vereiste kopballen, lezend steekproefAPI vraag, en meer.

Als u alle beschikbare eindpunten en CRUD-bewerkingen wilt weergeven, gaat u naar de [Real-time API-referentiewagen voor klantprofiel](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml).

Voor een gids voor het werken met [!DNL Real-time Customer Profile] gegevens in [!DNL Experience Platform] UI, gelieve te verwijzen naar [de gebruikershandleiding van het Profiel](../ui/user-guide.md).

## (Alpha) Berekende kenmerken {#computed-attributes}

>[!IMPORTANT]
>
>De functie voor berekende kenmerken staat in alfa en is niet beschikbaar voor alle gebruikers. Documentatie en functionaliteit kunnen worden gewijzigd.

Berekende kenmerken zijn functies die worden gebruikt om gegevens op gebeurtenisniveau samen te voegen tot kenmerken op profielniveau. Deze functies worden automatisch berekend zodat zij over segmentatie, activering, en verpersoonlijking kunnen worden gebruikt.

Elk berekend kenmerk bevat een expressie, ofwel &quot;rule&quot;, die binnenkomende gegevens evalueert en de resulterende waarde in een profielkenmerk opslaat. Met deze berekeningen kunt u eenvoudig vragen beantwoorden die betrekking hebben op de waarde van levenslange aankopen, de tijd tussen aankopen of het aantal geopende toepassingen, zonder dat u telkens wanneer de informatie nodig is, handmatig complexe berekeningen hoeft uit te voeren. Deze berekende kenmerkwaarden kunnen dan in een profiel worden bekeken, worden gebruikt om een segment tot stand te brengen, of door een aantal verschillende toegangspatronen worden betreden.

U kunt gegevens verwerkte attributen tot stand brengen, bekijken, uitgeven en schrappen gebruikend het `config/computedAttributes` eindpunt. Meer informatie over het gebruik van berekende kenmerken vindt u in het [overzicht van berekende kenmerken](../computed-attributes/overview.md). Voor API verrichtingen, bezoek [gegevens verwerkte attributen API eindgids](../computed-attributes/ca-api.md).

## Randprojecties {#edge-projections}

Adobe Experience Platform maakt het mogelijk om de ervaringen van klanten in real time aan te passen door gegevens gemakkelijk toegankelijk te maken op strategisch gelegen servers die &quot;randen&quot; worden genoemd. De [!DNL Real-time Customer Profile] API verstrekt eindpunten voor het werken met randen door componenten genoemd &quot;projecties.&quot; Dit omvat projectieconfiguraties om te bepalen welke gegevens aan elke rand moeten worden geprojecteerd, evenals projectiebestemmingen om te bepalen waar te om een projectie te leiden. Voor gedetailleerde informatie over het werken met randprojecties, gelieve [projectieconfiguraties en bestemmingseindpuntgids](edge-projections.md) te bezoeken.

## Entiteiten ([!DNL Profile] toegang) {#entities}

Via Adobe Experience Platform hebt u toegang tot [!DNL Real-time Customer Profile]-gegevens met RESTful-API&#39;s of de gebruikersinterface. Als u wilt leren hoe u toegang krijgt tot entiteiten, beter bekend als &quot;profielen&quot;, gebruikt u de API, volgt u de stappen die worden beschreven in de [eindpunthulplijn voor entiteiten](entities.md). Als u toegang wilt tot profielen met de interface [!DNL Platform], raadpleegt u de [Gebruikershandleiding voor profielen](../ui/user-guide.md).

## Exporttaken ([!DNL Profile] exporteren) {#profile-export}

[!DNL Real-time Customer Profile] de gegevens kunnen naar een dataset voor verdere verwerking, zoals het uitvoeren van publiekssegmenten voor activering of profielattributen voor rapportering worden uitgevoerd. Exporttaken voor publiekssegmenten maken deel uit van de [!DNL Adobe Experience Platform Segmentation Service] API. Lees de [segmentatie-eindgebruikershandleiding voor exporttaken](../../profile/api/export-jobs.md) voor meer informatie. Voor stapsgewijze instructies over het maken en beheren van exporttaken voor profielkenmerken gaat u naar de [gids voor het eindpunt van exporttaken](export-jobs.md).

## Beleid {#merge-policies} samenvoegen

Wanneer het brengen van gegevens uit veelvoudige bronnen in [!DNL Experience Platform], is het fusieprincipe de regels die [!DNL Platform] gebruikt om te bepalen hoe de gegevens zullen worden geprioriteerd en welke gegevens zullen worden gecombineerd om individuele klantenprofielen tot stand te brengen. Met de [!DNL Real-time Customer Profile]-API kunt u een nieuw samenvoegbeleid maken, bestaand beleid beheren en een standaardsamenvoegbeleid voor uw organisatie instellen. Meer over het werken met fusiebeleid gebruikend API, gelieve te bezoeken [de gids ](merge-policies.md) van het eindpunt van samenvoegingsbeleid.

Voor een gids aan het werken met samenvoegbeleid gebruikend [!DNL Platform] UI, te zien gelieve [de gebruikersgids van het beleid van de samenvoegen](../ui/merge-policies.md).

## Voorbeeldstatus voorvertoning ([!DNL Profile] voorvertoning) {#profile-preview}

Aangezien de gegevens die voor Profiel worden toegelaten in Experience Platform worden opgenomen, wordt het opgeslagen binnen het de gegevensopslag van het Profiel. Aangezien het aantal verslagen in de opslag van het Profiel stijgt of vermindert, wordt een steekproefbaan in werking gesteld die informatie betreffende hoeveel profielfragmenten en samengevoegde profielen in de gegevensopslag omvat. Met behulp van de profiel-API kunt u een voorvertoning weergeven van het meest recente voorbeeld en van de distributie van het lijstprofiel via gegevensset en naamruimte. Als u wilt beginnen met het gebruik van het `/profilepreviewstatus`-eindpunt, raadpleegt u de [voorbeeldstatuseindhulplijn](preview-sample-status.md).

## Systeemtaken profiel {#profile-system-jobs}

Profiel-toegelaten gegevens die in [!DNL Platform] worden opgenomen worden opgeslagen in [!DNL Data Lake] evenals [!DNL Real-time Customer Profile] gegevensopslag. Soms kan het nodig zijn om een dataset of batch uit de [!DNL Profile] opslag te verwijderen om gegevens te verwijderen die u niet meer nodig hebt of die bij fout zijn toegevoegd. Hiervoor moet u de API gebruiken om een [!DNL Profile System Job], ook wel &quot;[!DNL delete request]&quot; genoemd, te maken die u, indien nodig, kunt wijzigen, controleren of verwijderen. Als u wilt leren hoe u met verwijderingsverzoeken werkt met het `/system/jobs`-eindpunt in de [!DNL Real-time Customer Profile]-API, volgt u de stappen die worden beschreven in de [-gids voor het eindpunt van systeemtaken voor profielen](profile-system-jobs.md).

## Volgende stappen {#next-steps}

Wanneer u begint met het maken van aanroepen met de [!DNL Real-time Customer Profile]-API, leest u de [gids Aan de slag](getting-started.md) en selecteert u vervolgens een van de eindpunthulplijnen om te leren hoe u specifieke [!DNL Profile]-gerelateerde eindpunten kunt gebruiken. Als u met [!DNL Profile]-gegevens wilt werken met de [!DNL Experience Platform]-interface, raadpleegt u de [Gebruikershandleiding voor het realtime-klantprofiel](../ui/user-guide.md).