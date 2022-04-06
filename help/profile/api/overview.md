---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen;API;verenigd profiel;verenigd profiel;verenigd profiel;profiel;rtcp;inschakelen profiel;profiel inschakelen
title: Real-time handleiding voor de API voor klantprofiel
description: Met de realtime-API voor klantprofiel kunnen ontwikkelaars profielgegevens verkennen en ermee werken, waaronder weergaveprofielen, beleid voor samenvoegen maken en bijwerken, profielgegevens exporteren of samplen en profielgegevens verwijderen die niet langer vereist zijn of die door een fout zijn toegevoegd. Volg deze handleiding voor het uitvoeren van toetsbewerkingen met de API.
exl-id: ce39b95b-cff7-46cf-a14c-8203017c8826
source-git-commit: 9f00bff31f9e7d2da1294d3d1f24cba7870a4614
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 0%

---

# [!DNL Real-time Customer Profile] API-handleiding

[!DNL Real-time Customer Profile] kunt u een holistische weergave van elk van uw individuele klanten in Adobe Experience Platform bekijken. [!DNL Profile] staat u toe om verschillende klantengegevens van veelvoudige kanalen, zoals online, off-line, CRM, en derdegegevens, in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt.

De [!DNL Real-time Customer Profile] API bevat meerdere eindpunten, die hieronder worden beschreven. Ga naar de afzonderlijke eindpunthulplijnen voor meer informatie en raadpleeg de [gids Aan de slag](getting-started.md) voor belangrijke informatie over vereiste kopballen, lees steekproefAPI vraag, en meer.

Als u alle beschikbare eindpunten en CRUD-bewerkingen wilt weergeven, gaat u naar de [API-naslagwerker voor realtime klantprofiel](https://www.adobe.com/go/profile-apis-en).

Voor een gids voor het werken met [!DNL Real-time Customer Profile] gegevens in de [!DNL Experience Platform] UI, gelieve te verwijzen naar [Gebruikershandleiding voor profielen](../ui/user-guide.md).

## (Alpha) Berekende kenmerken {#computed-attributes}

>[!IMPORTANT]
>
>De functie voor berekende kenmerken staat in alfa en is niet beschikbaar voor alle gebruikers. Documentatie en functionaliteit kunnen worden gewijzigd.

Berekende kenmerken zijn functies die worden gebruikt om gegevens op gebeurtenisniveau samen te voegen tot kenmerken op profielniveau. Deze functies worden automatisch berekend zodat zij over segmentatie, activering, en verpersoonlijking kunnen worden gebruikt.

Elk berekend kenmerk bevat een expressie, ofwel &quot;rule&quot;, die binnenkomende gegevens evalueert en de resulterende waarde in een profielkenmerk opslaat. Met deze berekeningen kunt u eenvoudig vragen beantwoorden die betrekking hebben op de waarde van levenslange aankopen, de tijd tussen aankopen of het aantal geopende toepassingen, zonder dat u telkens wanneer de informatie nodig is, handmatig complexe berekeningen hoeft uit te voeren. Deze berekende kenmerkwaarden kunnen dan in een profiel worden bekeken, worden gebruikt om een segment tot stand te brengen, of door een aantal verschillende toegangspatronen worden betreden.

U kunt berekende kenmerken maken, weergeven, bewerken en verwijderen met de opdracht `config/computedAttributes` eindpunt. Als u wilt weten hoe u berekende kenmerken gebruikt, raadpleegt u de [overzicht van berekende kenmerken](../computed-attributes/overview.md). Ga voor API-bewerkingen naar de [API-eindpuntgids voor berekende kenmerken](../computed-attributes/ca-api.md).

## Edge-prognoses {#edge-projections}

Adobe Experience Platform maakt het mogelijk om de ervaringen van klanten in real time aan te passen door gegevens gemakkelijk toegankelijk te maken op strategisch gelegen servers die &quot;randen&quot; worden genoemd. De [!DNL Real-time Customer Profile] API biedt eindpunten voor het werken met randen via componenten die &#39;projecties&#39; worden genoemd. Dit omvat projectieconfiguraties om te bepalen welke gegevens aan elke rand moeten worden geprojecteerd, evenals projectiebestemmingen om te bepalen waar te om een projectie te leiden. Voor meer informatie over het werken met randprojecties gaat u naar de [projectieconfiguraties en de gids voor eindpunten van bestemmingen](edge-projections.md).

## Entiteiten ([!DNL Profile] toegang) {#entities}

Via Adobe Experience Platform hebt u toegang tot [!DNL Real-time Customer Profile] gegevens die RESTful APIs of het gebruikersinterface gebruiken. Als u wilt leren hoe u met de API toegang krijgt tot entiteiten, beter bekend als &quot;profielen&quot;, voert u de stappen uit die in het dialoogvenster [eindgebruikershandleiding voor entiteiten](entities.md). Als u toegang wilt krijgen tot profielen met de [!DNL Platform] UI, verwijs naar [Gebruikershandleiding voor profielen](../ui/user-guide.md).

## Exporttaken ([!DNL Profile] export) {#profile-export}

[!DNL Real-time Customer Profile] de gegevens kunnen naar een dataset voor verdere verwerking, zoals het uitvoeren van publiekssegmenten voor activering of profielattributen voor rapportering worden uitgevoerd. Exporttaken voor publiekssegmenten maken deel uit van de [!DNL Adobe Experience Platform Segmentation Service] API, lees de [eindgids voor segmentatie van exporttaken](../../profile/api/export-jobs.md) voor meer informatie. Voor stapsgewijze instructies over het maken en beheren van exporttaken voor profielkenmerken gaat u naar de [eindgebruikershandleiding exporttaken](export-jobs.md).

## Beleid samenvoegen {#merge-policies}

Wanneer u gegevens uit meerdere bronnen samenbrengt in [!DNL Experience Platform], samenvoegbeleid zijn de regels die [!DNL Platform] gebruikt om te bepalen hoe de gegevens voorrang krijgen en welke gegevens worden gecombineerd om individuele klantenprofielen tot stand te brengen. Met de [!DNL Real-time Customer Profile] API, kunt u nieuw samenvoegbeleid tot stand brengen, bestaand beleid beheren, en een standaardsamenvoegbeleid voor uw organisatie plaatsen. Als u met een samenvoegbeleid wilt werken met de API, gaat u naar de [eindhulplijn voor samenvoegbeleid](merge-policies.md).

Als u meer wilt weten over samenvoegingsbeleid en hun rol in het Platform, leest u eerst de [overzicht van samenvoegbeleid](../merge-policies/overview.md).

## Voorbeeldstatus voorvertonen ([!DNL Profile] voorvertoning) {#profile-preview}

Aangezien de gegevens in Platform worden opgenomen, wordt een steekproefbaan in werking gesteld om de profieltelling en andere gegevens-verwante metriek van het Profiel van de Klant in real time bij te werken. De resultaten van deze voorbeeldtaak kunnen worden weergegeven met de opdracht `/previewsamplestatus` eindpunt, deel van Real-time het Profiel van de Klant API. Dit eindpunt kan ook worden gebruikt om van profieldistributies door zowel dataset als identiteit namespace een lijst te maken, evenals veelvoudige rapporten te produceren om zicht in de samenstelling van de Opslag van het Profiel van uw organisatie te bereiken.  Ga als volgt te werk om aan de slag te gaan `/profilepreviewstatus` eindpunt, verwijs naar [voorbeeldstatuseindhulplijn voorbeeld](preview-sample-status.md).

## Systeemtaken profiel {#profile-system-jobs}

Profiel-toegelaten gegevens die in worden opgenomen [!DNL Platform] wordt opgeslagen in het dialoogvenster [!DNL Data Lake] en de [!DNL Real-time Customer Profile] gegevensopslag. Soms kan het nodig zijn een gegevensset of batch uit de [!DNL Profile] opslaan om gegevens te verwijderen die u niet meer nodig hebt of die bij vergissing zijn toegevoegd. Hiervoor moet u de API gebruiken om een [!DNL Profile System Job], ook bekend als &quot;[!DNL delete request]&quot;, die indien nodig kunnen worden gewijzigd, bewaakt of verwijderd. Leer hoe u met verwijderingsverzoeken werkt met de opdracht `/system/jobs` in de [!DNL Real-time Customer Profile] API, voert u de stappen uit die in de [eindgids voor profielsysteemtaken](profile-system-jobs.md).

## Profielkenmerken bijwerken {#update-profile}

Soms kan het nodig zijn gegevens bij te werken in de profielopslag van uw organisatie. U moet bijvoorbeeld records corrigeren of een kenmerkwaarde wijzigen. Dit kan door partijopname worden gedaan en vereist een profiel-Toegelaten dataset die met een upsert markering wordt gevormd. Voor meer informatie over hoe te om een dataset voor attributenupdates te vormen, gelieve te verwijzen naar het leerprogramma voor [het toelaten van een dataset voor Profiel en upsert](../../catalog/datasets/enable-upsert.md).

## Volgende stappen {#next-steps}

Beginnen het maken vraag gebruikend [!DNL Real-time Customer Profile] API, lees de [gids Aan de slag](getting-started.md) dan selecteer één van de eindpuntgidsen om te leren hoe te om specifiek te gebruiken [!DNL Profile]-gerelateerde eindpunten. Werken met [!DNL Profile] gegevens die [!DNL Experience Platform] UI, gelieve te verwijzen naar [Gebruikershandleiding voor het profiel van de klant in realtime](../ui/user-guide.md).
