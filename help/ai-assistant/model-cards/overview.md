---
title: Modelkaarten voor AI-modeltransparantie in Adobe Experience Platform
description: Meer weten over modelkaarten in Adobe Experience Platform?
hide: true
hidefromtoc: true
source-git-commit: 21a95bd678cf83c72a08213b647ef778cfb49cfc
workflow-type: tm+mt
source-wordcount: '2386'
ht-degree: 0%

---

# Modelkaarten voor transparantie van AI-modellen in Adobe Experience Platform

Modelkaarten zijn de standaardindelingen waarmee transparantie van het AI-model wordt doorgegeven. Modelkaarten zijn openbaar en zijn bedoeld om zowel het bestaande als het toekomstige inzicht van klanten in de door Adobe gebruikte AI-modellen te verbeteren. Modelkaarten zijn doorgaans statisch. Er zijn echter verschillende aspecten van AI-modellen die in de loop der tijd kunnen veranderen, zoals lijntype, afwijking en andere transparantiekenmerken.

Lees dit document voor meer informatie over modelkaarten in Adobe Experience Platform.

## Modelkaartsecties {#model-card-sections}

Lees het volgende voor een gids over de verschillende secties van een modelkaart, met inbegrip van informatie de vragen die zij behandelen.

### Modeloverzicht {#model-overview}

+++Vragen en voorbeeldantwoorden weergeven

| Vraag | Benodigde informatie | Voorbeeldantwoord |
| --- | --- | --- |
| Wat is de naam van het model? | Officiële naam en versie van het AI-model | **<br> CustomerAI van de Propensiteit van 0} KlantAI Score Model v2.0 {is een op AI-Gerichte model dat wordt ontworpen om aandrijvingsscores voor gebruikers te produceren die op hun verleden gedrag en interactie met een zaken worden gebaseerd.** Het helpt de waarschijnlijkheid voorspellen dat een klant specifieke acties onderneemt, zoals het doen van een aankoop, het in dienst nemen van inhoud, of het koelen. Dit model wordt opgesteld binnen Adobe Experience Platform en integreert met diverse marketing en klantenanalytische werkschema&#39;s.</br> |
| Wat is het doel van het model? | Een korte beschrijving van wat het model moet doen. | Het model is ontworpen om marketers en de teams van de klantenovereenkomst van actionable inzicht te voorzien door de waarschijnlijkheid te voorspellen dat een klant een bepaalde actie zal uitvoeren, zoals het maken van een aankoop, het aanmelden voor een abonnement, of het in dienst nemen van een e-mailcampagne. De output staat ondernemingen toe om publiekssegmentatie te optimaliseren en klanteninteractie aan te passen die op voorspeld gedrag wordt gebaseerd. |
| Welk type model is het? | Het type model, zoals classificatie, regressie, generatief enz. | Dit is a s **onder toezicht het leren classificatiemodel** dat de waarschijnlijkheid van een gebeurtenis voorspelt die (b.v., aankoop, churn, overeenkomst) gegeven historische klantengegevens voorkomt. Het wordt getraind gebruikend gradient-versterkende beslissingsbomen (GBDT) met logistieke regressie aan modelaandrangscores. |
| Wie zijn de beoogde gebruikers? | De interne en externe gebruikersgroepen waarvoor het model is bedoeld. | De belangrijkste gebruikers van dit model zijn marketingprofessionals, gegevensanalisten en teams voor klantbetrokkenheid die Adobe Experience Platform gebruiken om gegevensgestuurde marketingstrategieën te ontwikkelen. |
| Hoe integreert dit model met Adobe Experience Platform? | De gebruikte integratiegegevens en API&#39;s en hoe deze in de workflows passen. | CustomerAI integreert direct in **Adobe Experience Platform AI diensten**, die gebruikers toestaan om modeloutput door prebuilt APIs en dashboards toegang te hebben. De aandrijvingsscores die door het model worden geproduceerd kunnen binnen **Adobe Journey Optimizer** worden gebruikt, **en Adobe Real-Time CDP**, om publiekssegmentatie en op maat gemaakte strategieën te verfijnen. |

{style="table-layout:auto"}

+++

### Beoogd gebruik {#intended-use}

+++Vragen en voorbeeldantwoorden weergeven

| Vraag | Benodigde informatie | Voorbeeldantwoord |
| --- | --- | --- |
| Wat zijn de belangrijkste gevallen van gebruik? | De scenario&#39;s waarin het model naar verwachting zal worden gebruikt. | Dit model wordt hoofdzakelijk gebruikt voor **klantensegmentatie, gerichte marketing, en kinnevoorspelling**. De ondernemingen hefboomwerking dit model aan **voorspellen klantenkoopintentie, optimaliseren marketing campagnes, en verbeteren verpersoonlijkingsinspanningen**. Een e-commercebedrijf kan het model bijvoorbeeld gebruiken om klanten met een hoge intentie te identificeren en hen exclusieve promoties aan te bieden. |
| Welke problemen lost dit model op? | De belangrijkste pijnpunten die door het model worden behandeld. | De tellers worstelen vaak met **identificerend de juiste klanten om** te richten en **optimaliserend betrokkenheidsinspanningen**. Dit model **vermindert giswerk** door a **gegeven-gedreven benadering** aan klant te verstrekken die richt, ervoor zorgt dat de marketing middelen efficiënt worden toegewezen. |
| Voor welke bedrijfstakken of domeinen is dit model relevant? | Een lijst van de van toepassing zijnde bedrijfstakken. | Het model is toepasselijk over veelvoudige industrieën, met inbegrip van **e-commerce, kleinhandel, financiële diensten, telecommunicatie, en media**. Om het even welk bedrijf dat op klantenovereenkomst en gepersonaliseerde marketing baseert kan van dit model profiteren. |
| Hoe moet dit model niet worden gebruikt? | Alle gevallen van misbruik die moeten worden vermeden. | Het model **zou niet voor hoog-risico besluitvorming**, zoals **financieel krediet het scoren, medische diagnostiek, of wettelijke beoordelingen** moeten worden gebruikt. Bovendien, is het niet bedoeld voor gebruik in **voorspelend persoonlijk gevoelig gedrag** (zoals, gezondheidsvoorwaarden, politieke voorkeur) toe te schrijven aan potentiële ethische zorgen. |

{style="table-layout:auto"}

+++

### Invoer en uitvoer van modellen {#model-inputs-and-outputs}

+++Vragen en voorbeeldantwoorden weergeven

| Vraag | Benodigde informatie | Voorbeeldantwoord |
| --- | --- | --- |
| Welke soorten gegevens neemt het model als input? | De gegevenstypen die het model als invoer gebruikt, zijn onder andere: gegevensfuncties, indelingen en bronnen. | Het model verwerkt **gegevens van het klantengedrag, demografische attributen, en historische interactie**. Dit omvat gegevens zoals de frequentie van het websitebezoek, de aankoopgeschiedenis in het verleden, de betrokkenheid bij marketing e-mails, en demografische informatie. |
| In welk formaat moeten de invoer zich bevinden? | De geaccepteerde invoerindelingen. | De gegevens van de input moeten als **JSON voorwerpen** worden gestructureerd die klantenattributen en gedragssignalen bevatten. Voor batch-verwerking accepteert het model **CSV-bestanden** die zijn opgemaakt volgens Adobe Experience Platform-normen voor gegevensinvoer. |
| Wat levert het model op? | Het type uitvoer dat door het model wordt gegenereerd. | Het model geeft een dichtheid tussen 0 en 1, waarbij hogere waarden een grotere kans op een voorspelde gebeurtenis aangeven. Bovendien, verstrekt het eigenschapbelangrijkscores, die gebruikers toestaan om te begrijpen welke factoren de voorspelling beïnvloedden. |
| Wat zijn enkele voorbeelden van invoer en uitvoer? | A sample input and corresponding output. | <ul><li>**Invoer van het Voorbeeld:** json { &quot;customer_id&quot;: 12345, &quot;over het verleden_aankopen&quot;: 3, &quot;last_visit_days&quot;: 7, &quot;email_click_rate&quot;: 0.4}</li><li>**Uitvoer van het Voorbeeld:** json { &quot;customer_id&quot;: 12345, &quot;propensity_score&quot;: 0.82}</li></ul> |

{style="table-layout:auto"}

+++

### Trainingsgegevens {#training-data}

+++Vragen en voorbeeldantwoorden weergeven

| Vraag | Benodigde informatie | Voorbeeldantwoord |
| --- | --- | --- |
| Welke gegevensbestanden zijn gebruikt om het model op te leiden? | Een beschrijving van de gegevensbronnen. | Het model is opgeleid op basis van geanonimiseerde gegevens over klantinteractie van eerste bedrijven die via Adobe Experience Platform zijn verzameld. Het omvat historische gegevens over klantgedrag, transactieverslagen, e-mailinteracties, en betrokkenheidsmetriek over veelvoudige industrieën. |
| Wat is de grootte en de bron van de gegevens? | Het volume en de oorsprong van de opleidingsdataset. | De dataset van de opleiding bestaat uit 10 miljoen klantenverslagen die uit een diverse reeks klanten van Adobe Experience Platform worden aangekocht. Deze verslagen omvatten historische klanteninteractie, transactionele gegevens, gedragsafspraken logboeken, en demografische informatie van diverse industrieën zoals kleinhandel, e-handel, telecommunicatie, en financiën. De gegevens werden verzameld over een periode van 24 maanden en zorgden ervoor dat de seizoensgebonden trends en de langetermijnpatronen van de betrokkenheid voldoende werden weergegeven. |
| Zijn er bekende vooroordelen in de dataset? | Bias-overwegingen en mitigatieinspanningen. | De dataset is voornamelijk afkomstig van gebruikers met een hoge betrokkenheid, wat selectievertekening kan veroorzaken. Om dit te verlichten, past het model gestratificeerde bemonstering, voorkeur controletechnieken, en de strategieën van de gegevensaugmentatie toe. |
| Hoe worden de gegevens vooraf verwerkt? | Stappen genomen om de gegevens te reinigen en voor te bereiden. | De dataset ondergaat uitgebreide preprocessing om gegevensconsistentie, kwaliteit, en bruikbaarheid te verzekeren. <ol><li>**Behandelend Ontbrekende Waarden**: De ontbrekende waarden worden gericht gebruikend een combinatie gemiddelde toerekening (voor numerieke gebieden), wijzetoewijzing (voor categoriale gebieden), en vooruitlopende modellering (voor complexe ontbrekende gevallen).</li><li>**Categorische Codering:** Categorische variabelen zoals klantensegmenten en aankoopcategorieën worden omgezet in numerieke vertegenwoordiging door het één-hete coderen en doel het coderen technieken.</li><li>**Scaling &amp; Normalisatie van de Eigenschap:** Min-maximum het schrapen wordt toegepast voor begrensde variabelen (b.v., leeftijd, inkomen), terwijl z-score normalisering voor normaal verdeelde eigenschappen wordt gebruikt.</li><li>**Extra Voorbehandeling:** de pijpleiding omvat uitbijieropsporing en verwijdering, dubbel filtreren, tijdstempelnormalisatie, en eigenschapstechniek om voorspelbaar te verbeteren.</li></ol> |

{style="table-layout:auto"}

+++

### Modelarchitectuur en -opleiding {#model-architecture-and-training}

+++Vragen en voorbeeldantwoorden weergeven

| Vraag | Benodigde informatie | Voorbeeldantwoord |
| --- | --- | --- |
| Welke architectuur gebruikt het model? | Het type neurale netwerk, de methode van het samenvoegen, enz. | Het model maakt gebruik van GGBDT (Gradient Boosting Decision Trees) met XGBoost, geoptimaliseerd voor gestructureerde gegevens. Het wordt getraind op historische reeksen van klantgebeurtenissen om voorspellende gedragspatronen te identificeren. |
| Welke algoritmen zijn toegepast? | De machine leertechnieken die werden gebruikt. | Het model wordt gebouwd gebruikend een onder toezicht staande het leren benadering, leveraging Gradient Boosting Besluit Trees (GBDT) met XGBoost als primair het leren algoritme. Bovendien wordt logistieke regressie opgenomen als basismodel voor het benchmarken van voorspellende nauwkeurigheid. |
| Welke opleidingskaders werden gebruikt? | De bibliotheken of platforms die voor training worden gebruikt. | Het model is ontwikkeld met TensorFlow, XGBoost en scikit-learn. De training wordt uitgevoerd op Adobe AI-cloudinfrastructuur met NVIDIA V100 GPU&#39;s, die grootschalige gegevenssets ondersteunen. |
| Welke computermiddelen werden gebruikt voor training? | De hardware- en cloudbronnen die voor training zijn gebruikt. | NVIDIA V100 GPU&#39;s, getraind op Google Cloud-infrastructuur. |
| Welke evaluatiemethoden zijn gebruikt? | De metriek en testprocedures die voor evaluatie werden gebruikt. | AUC-ROC, precisie-herinnering, en dwars-bevestiging. |

{style="table-layout:auto"}

+++

### Prestaties en evaluatie {#performance-and-evaluation}

+++Vragen en voorbeeldantwoorden weergeven

| Vraag | Benodigde informatie | Voorbeeldantwoord |
| --- | --- | --- |
| Hoe werd het model getest? | De methoden die worden gebruikt om prestaties te valideren. | Het model werd getest met behulp van een holdout-validatiebenadering, waarbij 80% van de gegevens werd gebruikt voor training, en 20% was gereserveerd voor evaluatie. |
| Welke evaluatiemetriek werd gebruikt? | De belangrijkste prestatie-indicatoren. | De doeltreffendheid van het model wordt gemeten gebruikend **AUC-ROC (0.85)**, **precisie-herinner (0.78)**, en **F1-score (0.80)**. Deze metriek helpen de voorspellende macht van het model over verschillende segmenten beoordelen. |
| Hoe variëren de prestaties in verschillende scenario&#39;s? | De contextspecifieke prestatievariaties. | Lagere nauwkeurigheid voor nieuwe klantsegmenten met beperkte historische gegevens. |
| Zijn er bekende tekortkomingen of tekortkomingen? | Eventuele beperkingen of storingspunten. | Het model kan onderpresteren voor klanten met beperkte historische gegevens (koudstartprobleem). Bovendien kunnen seizoensinvloeden, zoals de trends voor vakantiewinkelen, vaak opnieuw worden opgeleid om de nauwkeurigheid te behouden. |

{style="table-layout:auto"}

+++

### Fairness en afwijking {#fairness-and-bias}

+++Vragen en voorbeeldantwoorden weergeven

| Vraag | Benodigde informatie | Voorbeeldantwoord |
| --- | --- | --- |
| Welke billijkheidscontroles zijn uitgevoerd? | De analyse- en mitigatieprocessen die zijn uitgevoerd. | Het model onderging demografische pariteitstests en tegengestelde billijkheidsbeoordelingen om prestatiesverschillen tussen verschillende gebruikerssegmenten te ontdekken. |
| Heeft het model een onevenredig grote invloed op bepaalde groepen? | Eventuele verschillen in prestaties die zijn vastgesteld. | De analyse onthulde een 5% prestatiesdaling voor gebruikers met lage historische interactiegegevens. Om dit te verhelpen, worden in het model technieken voor herweging tijdens de opleiding opgenomen. |
| Hoe verzacht het model bis? | De technieken die worden gebruikt om afwijking aan te pakken. | De gegevensset is gestratificeerd om te zorgen voor een evenredige vertegenwoordiging van de verschillende demografische gegevens van de klant, en tijdens de opleiding worden billijkheidsbeperkingen ingevoerd om te voorkomen dat het model een bepaalde groep begunstigt. Regelmatige vertekende audits worden uitgevoerd op basis van een demografische pariteitsanalyse, waarbij aanpassingen mogelijk zijn als er prestatieverschillen worden vastgesteld. |

{style="table-layout:auto"}

+++

### Uitleg en interpreteerbaarheid {#explainability-and-interpretability}

+++Vragen en voorbeeldantwoorden weergeven

| Vraag | Benodigde informatie | Voorbeeldantwoord |
| --- | --- | --- |
| Can users understand why the model makes certain decisions? | The interpretability methods used by the model. | The model leverages **SHapley Additive Explanations (SHAP)** to quantify the impact of each input feature on its predictions, providing transparency into how customer attributes influence propensity scores. De waarden van de SHAP laten zowel globale interpretabiliteit toe, die de meest invloedrijke factoren over alle voorspellingen identificeert, als lokale interpretabiliteit, die individuele voorspellingen voor specifieke klanten verklaren. |
| What tools or techniques are available for interpretability? | The available explainability tools. | The model supports **Local Interpretable Model-Agnostic Explanations (LIME)** and SHAP to provide insights into how input features influence predictions. LIME genereert lokale uitleg door gepertureerde versies van de invoergegevens te maken en wijzigingen in voorspellingen te observeren, terwijl SHAP aan elke functie bijdragewaarden toekent, waardoor zowel de algemene als de lokale interpretabiliteit van modelbeslissingen wordt geboden. |

{style="table-layout:auto"}

+++

### Robuustheid en generalisatie {#robustness-and-generalization}

+++Vragen en voorbeeldantwoorden weergeven

| Vraag | Benodigde informatie | Voorbeeldantwoord |
| --- | --- | --- |
| Hoe goed presteert het model op onzichtbare gegevens? | De bevindingen over het testen van de generalisatieprestaties. | Het model handhaaft **80% AUC-ROC** wanneer getest op onzichtbare datasets, die sterke generalisatie aan nieuwe klantenverslagen aantonen. De prestaties blijven stabiel voor verschillende klantsegmenten, maar vertonen een lichte verslechtering wanneer het gedrag van de gebruiker aanzienlijk afwijkt van historische patronen. |
| Is het model onderworpen aan stresstests voor tegengestelde input? | De details van de robuustheidsbeoordeling. | Het model is beoordeeld op basis van gepertureerde en tegenstrijdige input, waaronder ontbrekende gegevens, uitbijtinjecties en opzettelijke verkeerde etikettering. Hoewel de prestaties onder normale omstandigheden robuust blijven, werd een kleine nauwkeurigheidsvermindering (ongeveer 3-5%) waargenomen onder extreme omschakelingsaanpassingen. |

{style="table-layout:auto"}

+++

### Beveiligings- en privacyoverwegingen {#security-and-privacy-considerations}

+++Vragen en voorbeeldantwoorden weergeven

| Vraag | Benodigde informatie | Voorbeeldantwoord |
| --- | --- | --- |
| Verwerkt het model gevoelige gegevens? | Alle informatie voldoet aan de privacywetgeving. | Het model verwerkt of behoudt geen persoonlijk identificeerbare informatie (PII) en alle gegevens die voor de opleiding worden gebruikt, worden geanonimiseerd en samengevoegd. Het houdt zich aan strikte naleving van het privacybeleid van GDPR, CCPA en interne Adobe om verantwoordelijk gegevensgebruik te verzekeren. |
| Welke technieken voor privacybescherming zijn gebruikt? | De technieken die worden gebruikt om privacymaatregelen te waarborgen. | Het model bevat verschillende privacytechnieken om gecontroleerde ruis aan gegevens toe te voegen, zodat personen niet opnieuw kunnen worden geïdentificeerd. Bovendien worden hashing, anonymization, en kenization methodes gebruikt om PII vóór modelopleiding en gevolgtrekking te verwijderen. |

{style="table-layout:auto"}

+++

### Toezicht en onderhoud {#monitoring-and-maintenance}

+++Vragen en voorbeeldantwoorden weergeven

| Vraag | Benodigde informatie | Voorbeeldantwoord |
| --- | --- | --- |
| Hoe worden de modelprestaties in de loop der tijd gecontroleerd? | Gegevens over de traceringsmechanismen die voor het model worden gebruikt. | Het model wordt voortdurend bewaakt via WatsonX, waarbij belangrijke prestatie-indicatoren worden bijgehouden, zoals het verloop van de nauwkeurigheid, verschuivingen van het belang van de functie en voorspelbaarheid. Anomaly detection and alarting mechanism notify the team when significant disations from expected behavior occur. |
| Hoe vaak wordt het model opnieuw opgeleid? | De frequentie van updates op het model. | Het model wordt maandelijks bijgeschoold met behulp van bijgewerkte gegevens van de klanteninteractie om blijvende relevantie te verzekeren. Periodieke omscholing helpt het verschuiven van gegevens en seizoensschommelingen te beperken, wat een invloed kan hebben op de voorspellende nauwkeurigheid. |

{style="table-layout:auto"}

+++

### Ethische overwegingen en verantwoordelijke AI {#ethical-considerations-and-responsible-ai}

+++Vragen en voorbeeldantwoorden weergeven

| Vraag | Benodigde informatie | Voorbeeldantwoord |
| --- | --- | --- |
| Welke ethische bezwaren heeft dit model? | De potentiële risico&#39;s die zijn vastgesteld. | Het model zou een vertekend beeld kunnen geven in de besluitvorming als het niet correct wordt gecontroleerd. Als bepaalde demografie bijvoorbeeld oververtegenwoordigd is in de trainingsgegevens, kan het model ten onrechte bepaalde klantgroepen bevoordelen. |
| Hoe sluit het model zich aan bij de verantwoordelijke AI-principes? | Informatie over hoe het model voldoet aan de ethische richtlijnen van AI. | Adobe Experience Platform volgt de verantwoordelijke AI-richtlijnen, waarbij ervoor wordt gezorgd dat modellen vóór de implementatie onderworpen worden aan vertekende controles, aan een billijkheidstest en aan menselijk toezicht. |

{style="table-layout:auto"}

+++

### Bekende beperkingen {#known-limitations}

+++Vragen en voorbeeldantwoorden weergeven

| Vraag | Benodigde informatie | Voorbeeldantwoord |
| --- | --- | --- |
| What are known limitations of the model? | Any identified performance or use case constraints. | Het model kan moeite hebben om de resultaten voor nieuw gelanceerde producten of klantsegmenten waar onvoldoende historische gegevens beschikbaar zijn, nauwkeurig te voorspellen. Bovendien kunnen seizoensschommelingen in het gedrag van klanten schommelingen in voorspellende nauwkeurigheid veroorzaken als deze tijdens de herscholing niet in aanmerking worden genomen. |
| Under what conditions does the model perform poorly? | Any identified weaknesses regarding the model. | De prestaties nemen af wanneer de geschiedenis van de klant gering is, bijvoorbeeld voor eerste kopers of gebruikers met minimale betrokkenheidsgegevens. Additionally, if customer behaviors shift due to external factors like economic downturns or industry trends, the model may require rapid adaptation to maintain accuracy. |

{style="table-layout:auto"}

+++

### Toekomstige verbeteringen {#future-improvements}

+++Vragen en voorbeeldantwoorden weergeven

| Vraag | Benodigde informatie | Voorbeeldantwoord |
| --- | --- | --- |
| Welke verbeteringen zijn gepland voor toekomstige herhalingen? | Het stappenplan voor verbeteringen. | Toekomstige herhalingen omvatten overdrachtstechnieken om prestaties voor koudstartgebruikers te verbeteren en aanpassingsvermogen aan veranderend klantengedrag te verbeteren. Daarnaast wordt realtime gegevensintegratie geïntroduceerd om de responsiviteit en nauwkeurigheid van modellen in dynamische marketingomgevingen te verbeteren. |

{style="table-layout:auto"}

+++