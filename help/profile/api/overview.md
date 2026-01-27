---
keywords: Experience Platform;profiel;real-time klantprofiel;problemen;API;verenigd profiel;verenigd profiel;verenigd;Profiel;rtcp;inschakelen profiel;Profiel inschakelen
title: Real-Time API-handleiding voor klantprofiel
description: Met de realtime-API voor klantprofiel kunnen ontwikkelaars profielgegevens verkennen en ermee werken, waaronder weergaveprofielen, beleid voor samenvoegen maken en bijwerken, profielgegevens exporteren of samplen en profielgegevens verwijderen die niet langer vereist zijn of die door een fout zijn toegevoegd. Volg deze gids voor het uitvoeren van de belangrijkste bewerkingen met de API.
role: Developer
exl-id: ce39b95b-cff7-46cf-a14c-8203017c8826
source-git-commit: 82a9b405a1d36155c84cd27a005c7ec469164ef3
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 1%

---

# [!DNL Real-Time Customer Profile] API-handleiding

Met [!DNL Real-Time Customer Profile] kunt u een holistische weergave van elk van uw individuele klanten in Adobe Experience Platform bekijken. [!DNL Profile] staat u toe om verschillende klantengegevens van veelvoudige kanalen, zoals online, off-line, CRM, en derdegegevens, in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt.

De API van [!DNL Real-Time Customer Profile] bevat meerdere eindpunten, die hieronder worden beschreven. Gelieve te bezoeken de individuele eindpuntgidsen voor details en te verwijzen naar [ begonnen gids ](getting-started.md) voor belangrijke informatie over vereiste kopballen, lezend steekproefAPI vraag, en meer.

Om alle beschikbare eindpunten en verrichtingen van CRUD te bekijken, bezoek de [ Real-Time API van het Profiel van de Klant Verwijzing kwader ](https://www.adobe.com/go/profile-apis-en).

Voor een gids aan het werken met [!DNL Real-Time Customer Profile] gegevens in [!DNL Experience Platform] UI, gelieve te verwijzen naar de [ de gebruikersgids van het Profiel ](../ui/user-guide.md).

## Berekende kenmerken {#computed-attributes}

Berekende kenmerken zijn functies die worden gebruikt om gegevens op gebeurtenisniveau samen te voegen tot kenmerken op profielniveau. Deze functies worden automatisch berekend zodat zij over segmentatie, activering, en verpersoonlijking kunnen worden gebruikt.

Elk berekend kenmerk bevat een expressie, ofwel &quot;rule&quot;, die binnenkomende gegevens evalueert en de resulterende waarde in een profielkenmerk opslaat. Met deze berekeningen kunt u eenvoudig vragen beantwoorden die betrekking hebben op de waarde van levenslange aankopen, de tijd tussen aankopen of het aantal geopende toepassingen, zonder dat u telkens wanneer de informatie nodig is, handmatig complexe berekeningen hoeft uit te voeren. Deze berekende kenmerkwaarden kunnen dan in een profiel worden bekeken, worden gebruikt om een publiek tot stand te brengen, of door een aantal verschillende toegangspatronen worden betreden.

U kunt berekende kenmerken maken, weergeven, bewerken en verwijderen met behulp van het `ca/attributes/` -eindpunt. Leren hoe te om gegevens verwerkte attributen te gebruiken, verwijs naar het [ gegevens verwerkte attributenoverzicht ](../computed-attributes/overview.md). Voor API verrichtingen, bezoek de [ gegevens verwerkte API eindpuntgids van attributen ](../computed-attributes/api.md).

## Entiteiten ([!DNL Profile] access) {#entities}

>[!NOTE]
>
>U kunt deze eindpunten alleen gebruiken als u Real-Time CDP Ultimate hebt.

Via Adobe Experience Platform hebt u toegang tot [!DNL Real-Time Customer Profile] -gegevens via RESTful API&#39;s of de gebruikersinterface. Leren hoe te om tot entiteiten toegang te hebben, algemeen gekend als &quot;profielen&quot;, die API gebruiken, de stappen volgen die in de [ gids van het entiteiteneindpunt ](entities.md) worden geschetst. Om tot profielen toegang te hebben gebruikend [!DNL Experience Platform] UI, verwijs naar de [ de gebruikersgids van het Profiel ](../ui/user-guide.md).

## Exporttaken ([!DNL Profile] exporteren) {#profile-export}

[!DNL Real-Time Customer Profile] -gegevens kunnen naar een gegevensset worden geëxporteerd voor verdere verwerking, zoals het exporteren van soorten publiek voor activering of profielkenmerken voor rapportage. De banen van de uitvoer voor publiek maken deel uit van [!DNL Adobe Experience Platform Segmentation Service] API, te lezen gelieve de [ gids van het de baneneindpunt van de segmentatie van de uitvoer ](../../profile/api/export-jobs.md) om meer te leren. Voor geleidelijke instructies op hoe te om uitvoerbanen voor profielattributen tot stand te brengen en te beheren, gelieve de [ gids van het de baneneindpunt van de uitvoer ](export-jobs.md) te bezoeken.

## Beleid samenvoegen {#merge-policies}

Wanneer u gegevens uit meerdere bronnen samenbrengt in [!DNL Experience Platform] , worden samenvoegbeleidsregels gebruikt die [!DNL Experience Platform] gebruikt om te bepalen hoe de prioriteit van gegevens wordt bepaald en welke gegevens worden gecombineerd om individuele klantprofielen te maken. Met de API van [!DNL Real-Time Customer Profile] kunt u nieuwe regels voor samenvoeging maken, bestaand beleid beheren en een standaardbeleid voor samenvoeging voor uw organisatie instellen. Om met samenvoegbeleid te werken gebruikend API, bezoek de [ gids van het het eindpunt van samenvoegingsbeleid ](merge-policies.md).

Om meer over fusiebeleid, en hun rol binnen Experience Platform te leren, gelieve te beginnen door het [ overzicht van het fusiebeleid ](../merge-policies/overview.md) te lezen.

## Voorbeeldstatus voorvertonen ([!DNL Profile] voorvertoning) {#profile-preview}

Als gegevens in Experience Platform worden ingevoerd, wordt een voorbeeldtaak uitgevoerd om het aantal profielen en andere gegevensgerelateerde gegevens in het realtime-profiel van de klant bij te werken. De resultaten van deze voorbeeldbaan kunnen worden bekeken gebruikend het `/previewsamplestatus` eindpunt, deel van Real-Time het Profiel van de Klant API. Dit eindpunt kan ook worden gebruikt om van profieldistributies door zowel dataset als identiteit namespace een lijst te maken, evenals veelvoudige rapporten te produceren om zicht in de samenstelling van de opslag van het Profiel van uw organisatie te bereiken.  Om begonnen te worden gebruikend het `/profilepreviewstatus` eindpunt, verwijs naar de [ gids van het de eindpuntvan de voorproefstatus ](preview-sample-status.md).

## Systeemtaken profiel {#profile-system-jobs}

Profielgegevens die in [!DNL Experience Platform] worden ingevoerd, worden zowel in de [!DNL Data Lake] -gegevensopslag als in de [!DNL Real-Time Customer Profile] -gegevensopslag opgeslagen. Soms kan het nodig zijn om profielgegevens die zijn gekoppeld aan een gegevensset te verwijderen uit de profielenopslag om gegevens te verwijderen die niet meer nodig zijn of die ten onrechte zijn toegevoegd. Hiervoor moet u de API gebruiken om een [!DNL Profile System Job] -bestand te maken, ook wel &quot;[!DNL delete request]&quot; genoemd, dat u indien nodig kunt wijzigen, controleren of verwijderen. Leren hoe te met schrappingsverzoeken te werken gebruikend het `/system/jobs` eindpunt in [!DNL Real-Time Customer Profile] API, de stappen volgen die in de [ gids van het de baaneindpunt van het profielsysteem ](profile-system-jobs.md) worden geschetst.

## Profielkenmerken bijwerken {#update-profile}

Soms kan het nodig zijn gegevens bij te werken in het profielarchief van uw organisatie. U moet bijvoorbeeld records corrigeren of een kenmerkwaarde wijzigen. Dit kan door partijopname worden gedaan en vereist een profiel-Toegelaten dataset die met een upsert markering wordt gevormd. Voor meer informatie over hoe te om een dataset voor attributenupdates te vormen, gelieve te verwijzen naar het leerprogramma voor [ toelatend een dataset voor Profiel en op te nemen ](../../catalog/datasets/enable-upsert.md).

## Volgende stappen {#next-steps}

Begin makend vraag gebruikend [!DNL Real-Time Customer Profile] API, lees [ begonnen gids ](getting-started.md) toen selecteren één van de eindpuntgidsen om te leren hoe te om specifieke [!DNL Profile] verwante eindpunten te gebruiken. Om met [!DNL Profile] gegevens te werken die [!DNL Experience Platform] UI gebruiken, gelieve te verwijzen naar de [ Realtime gebruikersgids van het Profiel van de Klant ](../ui/user-guide.md).
