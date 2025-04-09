---
title: Klanten met AI-kwaliteitsscore
description: Leer meer over het AI-model dat wordt gebruikt voor de AI van de Klant.
hide: true
hidefromtoc: true
source-git-commit: 21a95bd678cf83c72a08213b647ef778cfb49cfc
workflow-type: tm+mt
source-wordcount: '1629'
ht-degree: 0%

---

# Klanten met AI-kwaliteitsscore

Als deel van [ Intelligente Diensten in Adobe Experience Platform ](../../../intelligent-services/home.md), kunt u [ AI van de Klant ](../../../intelligent-services/customer-ai/overview.md) gebruiken om klantenvoorspellingen en verklaringen op het individuele niveau te produceren.

Met behulp van invloedrijke factoren kunt u de AI van de Klant gebruiken om u te vertellen wat een klant waarschijnlijk zal doen en waarom. Bovendien kunt u profiteren van de voorspellingen en inzichten van de Klant AI om de ervaringen van de Klant te personaliseren door de meest aangewezen aanbiedingen en het overseinen te dienen.

Lees deze modelkaart voor informatie over het AI-model dat wordt gebruikt om de AI van de Klant van stroom te voorzien.

## Modeloverzicht {#model-overview}

* AI van de klant is een door AI aangedreven model dat wordt ontworpen om aandrijvingsscores voor gebruikers te produceren die op hun gedrag in het verleden en interactie met een bedrijf worden gebaseerd. Gebruik de AI van de Klant om de waarschijnlijkheid te voorspellen dat een klant specifieke acties onderneemt, zoals het doen van een aankoop, het in dienst nemen van inhoud, of het koelen. Dit model wordt geïmplementeerd in Experience Platform en kan worden geïntegreerd met verschillende workflows voor marketing en klantanalyse.
* Het model is ontworpen om marketers en de teams van de klantenovereenkomst van actionable inzicht te voorzien door de waarschijnlijkheid te voorspellen dat een klant een bepaalde actie zal uitvoeren, zoals het maken van een aankoop, het aanmelden voor een abonnement, of het in dienst nemen van een e-mailcampagne. De output staat ondernemingen toe om publiekssegmentatie te optimaliseren en klanteninteractie aan te passen die op voorspeld gedrag wordt gebaseerd.
* Dit is een **classificatiemodel** voor begeleid leren dat de waarschijnlijkheid voorspelt dat een gebeurtenis zich voordoet (aankoop, churn, betrokkenheid) op basis van historische klantgegevens. Het wordt getraind gebruikend gradient-versterkende beslissingsbomen (GBDT) met logistieke regressie aan modelaandrangscores.
* De primaire gebruikers van dit model zijn marketingprofessionals, data-analisten en klantbetrokkenheidsteams die Experience Platform gebruiken om datagestuurde marketingstrategieën aan te sturen.
* AI van de klant integreert rechtstreeks in de AI-services van Experience Platform, waardoor gebruikers toegang hebben tot modeluitvoer via vooraf gebouwde API&#39;s en dashboards. De propensity-scores die door het model worden gegenereerd, kunnen worden gebruikt in [Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/get-started) en [Real-Time CDP](../../../rtcdp/home.md) om doelgroepsegmentatie te verfijnen en marketingstrategieën op maat te maken.

## Beoogd gebruik {#intended-use}

* Dit model wordt hoofdzakelijk gebruikt voor **klantensegmentatie, gerichte marketing, en kinnevoorspelling**. De ondernemingen hefboomwerking dit model aan **voorspellen klantenkoopintentie, optimaliseren marketing campagnes, en verbeteren verpersoonlijkingsinspanningen**. Een e-commercebedrijf kan het model bijvoorbeeld gebruiken om klanten met een hoge intentie te identificeren en hen exclusieve promoties aan te bieden.
* De tellers worstelen vaak met **identificerend de juiste klanten om** te richten en **optimaliserend betrokkenheidsinspanningen**. Dit model **vermindert giswerk** door een gegeven-gedreven benadering van klant te verstrekken die richt, ervoor zorgt dat de marketing middelen efficiënt worden toegewezen.
* Het model is van toepassing op meerdere bedrijfstakken, waaronder e-handel, detailhandel, financiële diensten, telecommunicatie en media. Om het even welk bedrijf dat op klantenovereenkomst en gepersonaliseerde marketing baseert kan van dit model profiteren.
* Het model **zou niet voor hoog-risico besluitvorming**, zoals financieel krediet het scoren, medische diagnostiek, of wettelijke beoordelingen moeten worden gebruikt. Bovendien is het niet bedoeld om persoonlijk gevoelig gedrag (gezondheidsomstandigheden, politieke voorkeuren) te voorspellen vanwege potentiële ethische bezwaren.

## Invoer en uitvoer van modellen {#model-inputs-and-outputs}

* Het model verwerkt gedragsgegevens van klanten, demografische kenmerken, en historische interactie. Dit omvat gegevens zoals de frequentie van het websitebezoek, de aankoopgeschiedenis in het verleden, de betrokkenheid bij marketing e-mails, en demografische informatie.
* Invoergegevens moeten zijn gestructureerd als JSON-objecten die klantkenmerken en gedragssignalen bevatten. Voor batchverwerking accepteert het model CSV-bestanden die zijn opgemaakt volgens de Experience Platform-standaarden voor gegevensinvoer.
* Het model geeft een dichtheid tussen 0 en 1, waarbij hogere waarden een grotere kans op een voorspelde gebeurtenis aangeven. Bovendien, verstrekt het eigenschapbelangrijkscores, die gebruikers toestaan om te begrijpen welke factoren de voorspelling beïnvloedden.

**input van het Voorbeeld**

```json
{
  "customer_id": 12345,
  "past_purchases": 3,
  "last_visit_days": 7,
  "email_click_rate": 0.4
}
```

**output van het Voorbeeld**

```json
{
  "customer_id": 12345,
  "propensity_score": 0.82
}
```

## Trainingsgegevens

* Het model werd getraind op **eerste partij, geanonimiseerde gegevens van de klanteninteractie** die via Experience Platform worden verzameld. Het omvat historische klant **gedragsgegevens, transactieverslagen, e-mailinteracties, en betrokkenheidsmetriek** over veelvoudige industrieën.
* De trainingsdataset bestaat uit **10 miljoen klantenverslagen** die uit een diverse reeks klanten van Experience Platform worden geput. Deze verslagen omvatten **historische klanteninteractie, transactionele gegevens, gedragsbetrokkenheidslogboeken, en demografische informatie** van diverse industrieën zoals kleinhandel, e-commerce, telecommunicatie, en financiën. De gegevens werden verzameld over een periode van 24 maanden en zorgden ervoor dat de seizoensgebonden trends en de langetermijnpatronen van de betrokkenheid voldoende werden weergegeven.
* De dataset is voornamelijk afkomstig van gebruikers met een hoge betrokkenheid, wat selectievertekening kan veroorzaken. Om dit te verlichten, past het model gestratificeerde bemonstering, voorkeur controletechnieken, en de strategieën van de gegevensaugmentatie toe.
* De dataset ondergaat uitgebreide preprocessing om gegevensconsistentie, kwaliteit, en bruikbaarheid te verzekeren.
   * **Behandelend Ontbrekende Waarden**: De ontbrekende waarden worden gericht gebruikend een combinatie gemiddelde toerekening (voor numerieke gebieden), wijzetoewijzing (voor categoriale gebieden), en vooruitlopende modellering (voor complexe ontbrekende gevallen).
   * **Categorische het Coderen**: De Categorische variabelen zoals klantensegmenten en aankoopcategorieën worden omgezet in numerieke vertegenwoordiging door het enig-hete coderen en doel het coderen technieken.
   * **Scaling &amp; Normalisatie van de Eigenschap**: Min-maximum het schrapen wordt toegepast voor begrensde variabelen (leeftijd, inkomen), terwijl z-score normalisering voor normaal verdeelde eigenschappen wordt gebruikt.
   * **Extra Preprocessing**: De pijpleiding omvat uitbijieropsporing en verwijdering, dubbel filtreren, tijdstempelnormalisatie, en eigenschapstechniek om vooruitlopende modellering te verbeteren.

## Modelarchitectuur en -opleiding

* Het model maakt gebruik van **[!DNL Gradient Boosting Decision Trees](GBDT) met[!DNL XGBoost]** , geoptimaliseerd voor gestructureerde gegevens. Het wordt getraind op historische reeksen van klantgebeurtenissen om voorspellende gedragspatronen te identificeren.
* Het model wordt gebouwd gebruikend een onder toezicht staande het leren benadering, leveraging GBDT met [!DNL XGBoost] als primair het leren algoritme. Bovendien wordt logistieke regressie opgenomen als basismodel voor het benchmarken van voorspellende nauwkeurigheid.
* Het model is ontwikkeld met **[!DNL TensorFlow]** , **[!DNL XGBoost]** en **[!DNL scikit-learn]** . De opleiding loopt op de wolkeninfrastructuur van Adobe AI gebruikend **[!DNL NVIDIA V100]GPUs**, ondersteunend grote datasets.
* [!DNL NVIDIA V100 GPUs] , getraind op Google Cloud-infrastructuur.
* [!DNL AUC-ROC] , precisie-terugroepen en kruisvalidatie.

## Prestaties en evaluatie

* Het model werd getest met behulp van een holdout-validatiebenadering, waarbij 80% van de gegevens werd gebruikt voor training, en 20% was gereserveerd voor evaluatie.
* De effectiviteit van het model wordt gemeten met [!DNL AUC-ROC] (0,85), precision-repeat (0,78) en F1-score (0,80). Deze metriek helpen de voorspellende macht van het model over verschillende segmenten beoordelen.
* Lagere nauwkeurigheid voor nieuwe klantsegmenten met beperkte historische gegevens.
* Het model kan onderpresteren voor klanten met beperkte historische gegevens (koudstartprobleem). Bovendien kunnen seizoensgebonden effecten (vakantieboodschappentrends) veelvuldig herscholing vereisen om de nauwkeurigheid te behouden.

## Fairness en afwijking

* Het model onderging **demografische pariteit het testen** en **tegenzijdige billijkheidsevaluaties** om prestatiesverschillen over verschillende gebruikerssegmenten te ontdekken.
* De analyse openbaarde a **5% prestatiesdaling voor gebruikers met lage historische interactiegegevens**. Om dit te verhelpen, worden in het model tijdens de opleiding technieken voor herweging toegepast.
* De gegevensset is gestratificeerd om te zorgen voor een evenredige vertegenwoordiging van de verschillende demografische gegevens van de klant, en tijdens de opleiding worden billijkheidsbeperkingen ingevoerd om te voorkomen dat het model een bepaalde groep begunstigt. Regelmatige vertekende audits worden uitgevoerd op basis van een demografische pariteitsanalyse, waarbij aanpassingen mogelijk zijn als er prestatieverschillen worden vastgesteld.

## Uitleg en interpreteerbaarheid

* Het model hefboomwerkingen **[!DNL SHapley Additive Explanations](SHAP)** om het effect van elke inputeigenschap op zijn voorspellingen te kwantificeren, die transparantie verstrekken in hoe de klantenattributen de aandrijvingsscores beïnvloeden. De waarden van de SHAP laten zowel globale interpretabiliteit toe, die de meest invloedrijke factoren over alle voorspellingen identificeert, als lokale interpretabiliteit, die individuele voorspellingen voor specifieke klanten verklaren.
* Het model steunt **[!DNL Local Interpretable Model-Agnostic Explanations](LIME)** en SCHAP om inzicht in te verstrekken hoe de inputeigenschappen voorspellingen beïnvloeden. LIME genereert lokale uitleg door gepertureerde versies van de invoergegevens te maken en wijzigingen in voorspellingen te observeren, terwijl SHAP aan elke functie bijdragewaarden toekent, waardoor zowel de algemene als de lokale interpretabiliteit van modelbeslissingen wordt geboden.

## Robuustheid en generalisatie

* Het model handhaaft 80% [!DNL AUC-ROC] wanneer getest op onzichtbare datasets, die sterke generalisatie aan nieuwe klantenverslagen aantonen. De prestaties blijven stabiel voor verschillende klantsegmenten, maar vertonen een lichte verslechtering wanneer het gedrag van de gebruiker aanzienlijk afwijkt van historische patronen.
* Het model is beoordeeld op basis van gepertureerde en tegenstrijdige input, waaronder ontbrekende gegevens, uitbijtinjecties en opzettelijke verkeerde etikettering. Hoewel de prestaties onder normale omstandigheden robuust blijven, werd een kleine nauwkeurigheidsvermindering (ongeveer 3-5%) waargenomen onder extreme omschakelingsaanpassingen.

## Beveiligings- en privacyoverwegingen

* Het model **verwerkt of behoudt geen persoonlijk identificeerbare informatie (PII)**, en alle gegevens die voor opleiding worden gebruikt worden anonymized en bijeengevoegd. Het houdt zich aan strikte naleving van het privacybeleid van GDPR, CCPA en interne Adobe om verantwoordelijk gegevensgebruik te verzekeren.
* Het model bevat verschillende privacytechnieken om gecontroleerde ruis aan gegevens toe te voegen, zodat personen niet opnieuw kunnen worden geïdentificeerd. Bovendien, **het hakken, anonymization, en tokenization methodes worden gebruikt om PII** vóór modelopleiding en gevolgtrekking te verwijderen.

## Implementatie en integratie

* Het model wordt gehost op Adobe Experience Platform AI-services en geïntegreerd met verschillende Adobe-toepassingen. Het is beschikbaar via API-eindpunten, waardoor naadloze toegang mogelijk is voor realtime voorspellingen en batchverwerking in workflows voor marketing en klantbetrokkenheid.
* Het model wordt uitgevoerd op een implementatie op basis **van automatisch**[!DNL Kubernetes] schalen om verschillende workloads efficiënt af te handelen. Rekenresources omvatten [!DNL NVIDIA V100] GPU&#39;s voor training en geoptimaliseerde CPU-gebaseerde deductie voor real-time schaalbaarheid.

## Toezicht en onderhoud

* Het model wordt voortdurend **gecontroleerd via[!DNL WatsonX]**, het volgen van zeer belangrijke prestatiesindicatoren zoals nauwkeurigheidsverloop, eigenschapbelangrijkheidsverschuivingen, en voorspellingsstabiliteit. Anomaly detection and alarting mechanism notify the team when significant disations from expected behavior occur.
* Het model wordt maandelijks bijgeschoold met behulp van bijgewerkte gegevens van de klanteninteractie om blijvende relevantie te verzekeren. Periodieke omscholing helpt gegevensverschuiving en seizoensschommelingen te beperken die voorspellende nauwkeurigheid kunnen beïnvloeden

## Ethische problemen en verantwoordelijke AI

* Het model zou een vertekend beeld kunnen geven in de besluitvorming als het niet correct wordt gecontroleerd. Als bepaalde demografie bijvoorbeeld oververtegenwoordigd is in de trainingsgegevens, kan het model ten onrechte bepaalde klantgroepen bevoordelen.
* Experience Platform volgt verantwoordelijke AI richtlijnen, die ervoor zorgen dat de modellen **bias controles, eerlijkheidstests, en menselijk toezicht** vóór plaatsing ondergaan.

## Bekende beperkingen

* Het model kan moeite hebben om de resultaten voor nieuw gelanceerde producten of klantsegmenten waar onvoldoende historische gegevens beschikbaar zijn, nauwkeurig te voorspellen. Bovendien kunnen seizoensschommelingen in het gedrag van klanten schommelingen in voorspellende nauwkeurigheid veroorzaken als deze tijdens de herscholing niet in aanmerking worden genomen.
* De prestaties nemen af wanneer de geschiedenis van de klant gering is, bijvoorbeeld voor eerste kopers of gebruikers met minimale betrokkenheidsgegevens. Bovendien, als klantengedrag **verschuift toe te schrijven aan externe factoren zoals economische neergang of industrietrends**, kan het model snelle aanpassing vereisen om nauwkeurigheid te handhaven.

## Toekomstige verbeteringen

* Toekomstige herhalingen omvatten overdrachtstechnieken om prestaties voor koudstartgebruikers te verbeteren en aanpassingsvermogen aan veranderend klantengedrag te verbeteren. Daarnaast wordt realtime gegevensintegratie geïntroduceerd om de responsiviteit en nauwkeurigheid van modellen in dynamische marketingomgevingen te verbeteren.
