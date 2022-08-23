---
title: Predictieve lead- en account scoring in Real-time CDP B2B
type: Documentation
description: Een overzicht en meer informatie over de voorspellende lood en rekeningseigenschap in Experience Platform CDP B2B.
exl-id: d3afbabb-005d-4537-831a-857c88043759
source-git-commit: 99b3b2d73b87a64fcaa9ba51563c0942fc21a0dc
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 0%

---

# Predictieve lead- en account scoring in Real-time CDP B2B

B2B-marketers staan voor meerdere uitdagingen boven aan de marketingtrechter. Om doeltreffend te zijn, hebben B2B-marketers een geautomatiseerde manier nodig om het grote aantal mensen te kwalificeren, zodat zij zich kunnen richten op de doelstellingen met hoge waarde. De kwalificatie moet worden afgestemd op het uiteindelijke verkoopresultaat, en niet alleen op de marketingconversie.

Rekeningen, zijn de uiteindelijke entiteiten die B2B producten en de diensten kopen. Om effectief te kunnen verhandelen en verkopen, moeten B2B-marketers niet alleen weten hoe groot de kans is dat de persoon, maar ook de rekening, kan kopen.

Op rekening gebaseerde marketing, in het bijzonder, strategische rekeningen als marketingdoelstellingen. De neiging-aan-koele scores van de rekening helpen de B2B marktpartijen zeer om voorrang onder de rekeningen te geven om hun rendement op investering te maximaliseren.

De voorspellende lood en de rekening die dienst de bovengenoemde uitdagingen door te leren van en voor de de omzettingsgebeurtenissen van het opportuniteitsstadium te voorspellen, en persoonactiviteiten op rekeningsniveau te groeperen om de rekeningsscores te produceren. De scores zijn gemakkelijk beschikbaar als aangepaste velden voor persoonlijke profielen en accountprofielen en kunnen eenvoudig worden opgenomen als segmentcriteria om uw publiek te verfijnen. De belangrijkste invloedrijke factoren zijn ook beschikbaar op zowel het geaggregeerde als het eenheidspeil om B2B-marketers te helpen beter te begrijpen welke elementen de scores hebben bepaald.

## Werken met voorspellende lead en accountscoring {#how-it-works}

>[!NOTE]
>
>[!DNL Marketo] de gegevensbron wordt momenteel vereist aangezien het de enige gegevensbron is die de omzettingsgebeurtenissen op het niveau van het persoonprofiel kan verstrekken.

De voorspellende Lood en het Scoren van de Rekening gebruikt een boom-gebaseerde (willekeurige bos/gradiënt het bevorderen) machine het leren methode om het voorspellende lood te bouwen die model scoren.

De beheerders hebben de capaciteit om veelvoudige profiel te vormen die doelstellingen scoring, ook als modellen worden bedoeld, voor elke gevormde omzettingsgebeurtenis, die voor afzonderlijke scores toestaat om voor elk gevormd doel worden geproduceerd.

De voorspellende lood en de rekening het scoren steunt de volgende types en de gebieden van omzettingsdoelstelling:

| Type doel | Velden |
| --- | --- |
| `leadOperation.convertLead` | <ul><li>`leadOperation.convertLead.convertedStatus`</li><li>`leadOperation.convertLead.assignTo`</li></ul> |
| `opportunityEvent.opportunityUpdated` | <ul><li>`opportunityEvent.dataValueChanges.attributeName`</li><li>`opportunityEvent.dataValueChanges.newValue`</li><li>`opportunityEvent.dataValueChanges.oldValue`</li>Voorbeeld: `opportunityEvent.dataValueChanges.attributeName` equals `Stage` en `opportunityEvent.dataValueChanges.newValue` equals `Contract`</ul> |

Het algoritme houdt rekening met de volgende attributen en inputgegevens:

* Persoonsprofiel

| XDM-veld | Vereist/optioneel |
| --- | --- |
| `personComponents.sourceAccountKey.sourceKey` | Vereist |
| `workAddress.country` | Optioneel |
| `extSourceSystemAudit.createdDate` | Vereist |
| `extendedWorkDetails.jobTitle` | Optioneel |

>[!NOTE]
> 
>Het algoritme inspecteert slechts `sourceAccountKey.sourceKey` in de Person:personComponents gebiedsgroep.

* Accountprofiel

| XDM-veld | Vereist/optioneel |
| --- | --- |
| `accountKey.sourceKey` | Vereist |
| `extSourceSystemAudit.createdDate` | Vereist |
| `accountOrganization.industry` | Optioneel |
| `accountOrganization.numberOfEmployees` | Optioneel |
| `accountOrganization.annualRevenue.amount` | Optioneel |

* Experience Event

| XDM-veld | Vereist/optioneel |
| --- | --- |
| `_id` | Vereist |
| `personKey.sourceKey` | Vereist |
| `timestamp` | Vereist |
| `eventType` | Vereist |

Meerdere modellen worden ondersteund, waarbij de volgende vaste limieten zijn ingesteld:

* Elke productiesandbox heeft recht op vijf modellen.
* Elke ontwikkelingssandbox heeft recht op één model.

De gegevenskwaliteitseisen zijn als volgt:

* Idealiter zijn er twee jaar van de meest recente gegevens voor opleidingsdoeleinden.
* De minimale gegevenslengte is zes maanden plus een voorspellingsvenster.
* Voor elk voorspeldoel, zijn minstens 10 gekwalificeerde omzettingsgebeurtenissen vereist.

De het scoren banen worden in werking gesteld dagelijks en de resultaten worden bewaard als profiel en rekeningsattributen, die dan in segmentdefinities en verpersoonlijking kunnen worden gebruikt. Inzichten van de out-of-the-box analyse zijn ook beschikbaar op het accountoverzichtdashboard.

Zie de documentatie voor meer informatie over hoe te [voorspelbare leads en accountscoring beheren](/help/rtcdp/b2b-ai-ml-services/manage-predictive-lead-and-account-scoring.md) service.

## Voorspelende resultaten voor leads en accounts weergeven {#how-to-view}

Nadat de baan in werking wordt gesteld, worden de resultaten bewaard in een nieuwe systeemdataset voor elk model onder de naam `LeadsAI.Scores` - ***de score***. Elke groep van het scoreveld kan bij worden gevestigd `{CUSTOM_FIELD_GROUP}.LeadsAI.the_score_name`.

| Kenmerk | Beschrijving |
| --- | --- |
| Score | De relatieve waarschijnlijkheid dat een profiel het voorspelde doel binnen het bepaalde tijdkader bereikt. Deze waarde moet niet worden beschouwd als een waarschijnlijkheidspercentage, maar veeleer als de waarschijnlijkheid van een profiel in vergelijking met de totale populatie. Deze score varieert van 0 tot 100. |
| Percentage | Deze waarde biedt informatie over de prestaties van een profiel ten opzichte van andere profielen met een vergelijkbare score. De percentages variëren van 1 tot 100. |
| Modeltype | Het geselecteerde modeltype geeft aan of dit een persoon of een accountscore is. |
| Score-datum | De datum waarop de scoring heeft plaatsgevonden. |
| Influentiële factoren | Voorspelde redenen waarom een profiel waarschijnlijk wordt omgezet. Factoren bestaan uit de volgende kenmerken:<ul><li>Code: Het profiel of gedragskenmerk dat de voorspelde score van een profiel positief beïnvloedt.</li><li>Waarde: De waarde van het profiel of gedragskenmerk.</li><li>Belangrijk: Geeft het gewicht aan dat het profiel of het gedragskenmerk heeft op de voorspelde score (laag, gemiddeld, hoog).</li></ul> |

### Klantprofielscores weergeven

Selecteer **[!UICONTROL Profiles]** onder de klantensectie in het linkerpaneel, en ga dan identiteitsnamespace en identiteitswaarde in. Als u klaar bent, selecteert u **[!UICONTROL View]**.

Selecteer vervolgens het profiel in de lijst.

![Klantprofiel](/help/rtcdp/accounts/images/b2b-view-customer-profile.png)

De **[!UICONTROL Detail]** De pagina bevat nu voorspellende scores. Klik op het diagrampictogram naast de voorspellende score.

![Voorspelscore voor klantprofiel](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score.png)

Een popup dialoog toont de score, de algemene scoreverdeling, de hoogste invloedrijke factoren voor deze score, en de definitie van het scoredoel.

![Voorspelende score voor klantprofiel](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score-details.png)

## Het controleren van voorspellende lood en rekenschap het scoren banen {#monitoring-jobs}

U kunt de standaardmetriek en de dagelijkse baan-in werking gestelde status door het dashboard controleren. De meetwaarden zijn:

* Totaal aantal personen/accountprofielen met score
* Volgende scoretaak (datum)
* Volgende trainingsbaan (datum)

Zie de documentatie over [monitoring van banen voor voorspellend leiderschap en accountscoring](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).
