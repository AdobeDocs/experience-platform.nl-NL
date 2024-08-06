---
keywords: Experience Platform;home;Data Science Workspace;populaire onderwerpen;datawetenschapswerkruimte;datawetenschap
solution: Experience Platform
title: Overzicht van Data Science Workspace
description: Deze handleiding biedt een overzicht van de belangrijkste concepten met betrekking tot Data Science Workspace in Adobe Experience Platform.
exl-id: bef25073-0dfb-453d-8c32-7f44d917d62d
source-git-commit: 923c6f2deb4d1199cfc5dc9dc4ca7b4da154aaaa
workflow-type: tm+mt
source-wordcount: '2411'
ht-degree: 0%

---

# Overzicht van Data Science Workspace

>[!NOTE]
>
>Data Science Workspace is niet meer verkrijgbaar.
>
>Deze documentatie is bedoeld voor bestaande klanten met eerdere rechten op Data Science Workspace.

Adobe Experience Platform [!DNL Data Science Workspace] maakt gebruik van machinaal leren en kunstmatige intelligentie om inzichten van uw gegevens te onthullen. [!DNL Data Science Workspace] is geïntegreerd in Adobe Experience Platform en helpt u bij het maken van voorspellingen met behulp van uw inhoud en gegevenselementen voor verschillende Adobe-oplossingen.

Gegevenswetenschappers van alle vaardigheidsniveaus zullen geavanceerde, makkelijk te gebruiken hulpmiddelen vinden die snelle ontwikkeling, opleiding, en het stemmen van machine het leren recepten steunen - alle voordelen van AI technologie, zonder de ingewikkeldheid.

Met [!DNL Data Science Workspace] kunnen gegevenswetenschappers eenvoudig intelligente services-API&#39;s maken, aangedreven door machinaal leren. Deze services werken samen met andere Adobe-services, waaronder Adobe Target en Adobe Analytics Cloud, om je te helpen gepersonaliseerde, gerichte digitale ervaringen te automatiseren in web-, desktop- en mobiele apps.

Deze handleiding bevat een overzicht van de belangrijkste concepten die betrekking hebben op [!DNL Data Science Workspace] .

## Inleiding

De onderneming van vandaag plaatst een hoge prioriteit op het ontginnen van grote gegevens voor voorspellingen en inzichten die hen zullen helpen klantenervaringen personaliseren en meer waarde aan klanten - en aan de zaken leveren.
Hoe belangrijk het ook is, het overstappen van gegevens naar inzichten kan hoge kosten met zich meebrengen. Meestal vereist het deskundige gegevenswetenschappers die intensief en tijdrovend gegevensonderzoek uitvoeren om machinaal leermodellen te ontwikkelen, of recepten, die intelligente diensten aandrijven. Het proces is lang, de technologie is complex, en deskundige gegevenswetenschappers kunnen moeilijk te vinden zijn.

Met [!DNL Data Science Workspace] kunt u in Adobe Experience Platform op ervaring gerichte AI in de hele onderneming introduceren, zodat u gegevens naar inzichten kunt stroomlijnen en versnellen met:
- Een framework voor machinetlering en runtime
- Geïntegreerde toegang tot uw gegevens die in Adobe Experience Platform zijn opgeslagen
- Geïntegreerd gegevensschema gebaseerd op [!DNL Experience Data Model] (XDM)
- De verwerkingskracht die essentieel is voor het leren van machines/AI en het beheren van grote datasets
- Prebuilt machine het leren recepten om de sprong in AI gedreven ervaringen te versnellen
- Vereenvoudigd ontwerp, hergebruik en wijziging van recepten voor gegevenswetenschappers met verschillende vaardigheidsniveaus
- Intelligente publicatie en delen van services met slechts een paar muisklikken - zonder ontwikkelaar - en monitoring en omscholing voor continue optimalisatie van gepersonaliseerde klantervaringen

Data wetenschappers van alle vaardigheidsniveaus bereiken sneller en effectievere digitale ervaringen.

## Aan de slag

Voordat u dieper op de details van [!DNL Data Science Workspace] gaat ingaan, volgt een korte samenvatting van de belangrijkste termen:

| Term | Definitie |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [!DNL Data Science Workspace] | Met [!DNL Data Science Workspace] in [!DNL Experience Platform] kunnen klanten modellen voor machine learning maken met behulp van data binnen [!DNL Experience Platform] en oplossingen voor Adobe om intelligente inzichten en voorspellingen te genereren om prachtige digitale ervaringen voor eindgebruikers te creëren. |
| Kunstmatige intelligentie | Kunstmatige intelligentie is een theorie en ontwikkeling van computersystemen die in staat zijn taken uit te voeren die normaal menselijke intelligentie vereisen, zoals visuele waarneming, spraakherkenning, besluitvorming en vertaling tussen talen. |
| Machine Learning | Machine learning is het studiegebied dat computers de mogelijkheid biedt om te leren zonder dat het expliciet wordt geprogrammeerd. |
| [!DNL Sensei] ML Framework | [!DNL Sensei] ML Framework is een geïntegreerd raamwerk voor machine learning op alle Adoben dat data over [!DNL Experience Platform] gebruikt om datawetenschappers in staat te stellen op een snellere, schaalbare en herbruikbare manier computergestuurde intelligence-services te ontwikkelen. |
| [!DNL Experience Data Model] | [!DNL Experience Data Model] (XDM) is de standaardiseringsinspanning die door Adobe wordt geleid om standaardschema&#39;s zoals [!DNL Profile] en [!DNL ExperienceEvent], voor het Beheer van de Ervaring van de Klant te bepalen. |
| [!DNL JupyterLab] | [!DNL JupyterLab] is een open-source webinterface voor Project Jupyter en is nauw geïntegreerd in [!DNL Experience Platform] . |
| Ontvangers | Een recept is de term van de Adobe voor een modelspecificatie en is een container op hoofdniveau die een specifiek machine learning, AI-algoritme of samenstel van algoritmen, verwerkingslogica en configuratie vertegenwoordigt die nodig is om een getraind model te bouwen en uit te voeren en zo specifieke bedrijfsproblemen te helpen oplossen. |
| Model | Een model is een exemplaar van een machine-learningrecept dat is opgeleid met behulp van historische data en configuraties om een oplossing te vinden voor een bedrijfscase. |
| Training | Training is het proces van leerpatronen en inzichten uit gelabelde data. |
| Getraind model | Een getraind model vertegenwoordigt de uitvoerbare output van een model trainingsproces, waarin een reeks opleidingsgegevens werd toegepast op de modelinstantie. Een getraind model zal een verwijzing naar om het even welke intelligente Webdienst handhaven die van het wordt gecreeerd. Het getrainde model is geschikt voor scores en het creëren van een intelligente webservice. Wijzigingen in een getraind model kunnen als een nieuwe versie worden bijgehouden. |
| Scores | Scores is het proces waarbij inzichten worden gegenereerd op basis van data met behulp van een getraind model. |
| Service | Een geïmplementeerde service maakt gebruik van de functionaliteit van een kunstmatige intelligentie, een machine-learningmodel of een geavanceerd algoritme via een API, zodat andere services of toepassingen deze kunnen gebruiken om intelligente apps te maken. |

De volgende grafiek schetst de hiërarchische verhouding tussen Ontvangers, Modellen, de Runs van de Opleiding, en het Scoren Runs.

![](./images/home/recipe_hiearchy_ui.png)

## [!DNL Data Science Workspace] begrijpen

Met [!DNL Data Science Workspace] kunnen je datawetenschappers het omslachtige proces stroomlijnen om inzichten in grote datasets bloot te leggen. [!DNL Data Science Workspace] is gebaseerd op een gemeenschappelijk framework voor machine learning en een gemeenschappelijke runtime, en biedt geavanceerd workflowbeheer, modelbeheer en schaalbaarheid. Intelligente services bieden ondersteuning voor hergebruik van formules voor machine learning om een groot aantal toepassingen aan te sturen die zijn gemaakt met producten en oplossingen van Adoben.

### Toegang tot één-loketgegevens

Data is de hoeksteen van AI en machine learning.

[!DNL Data Science Workspace] is volledig geïntegreerd met Adobe Experience Platform, inclusief het Data Lake, [!DNL Real-Time Customer Profile] en [!DNL Unified Edge] . Ontdek al je organisatiegegevens die in Adobe Experience Platform tegelijk zijn opgeslagen, samen met veelgebruikte big data en deep learning libraries, zoals [!DNL Spark] ML en [!DNL TensorFlow] . Als u niet vindt wat u nodig hebt, neemt u uw eigen datasets op met het XDM gestandaardiseerde schema.

### Prebuilt machine learning recipes

[!DNL Data Science Workspace] bevat vooraf gebouwde machine-learningformules voor veelvoorkomende bedrijfsbehoeften, zoals de voorspelling van detailhandel en afwijkingsdetectie, zodat datawetenschappers en -ontwikkelaars niet helemaal opnieuw hoeven te beginnen. Momenteel worden drie recepten aangeboden, {de voorspelling van de 0} productaankoop ](./pre-built-recipes/product-purchase-prediction.md), [ productaanbevelingen ](./pre-built-recipes/product-recommendations.md), en [ kleinhandelsverkoop ](./pre-built-recipes/retail-sales.md).[

[//]: # (The built-in recipe gallery offers recommendations for prebuilt recipes based on your business needs.)

U kunt desgewenst een vooraf samengesteld recept aan uw behoeften aanpassen, een recept importeren of helemaal opnieuw beginnen om een aangepast recept te maken. Maar als je eenmaal een recept hebt getraind en hyper-tune, is het creëren van een intelligente aangepaste service niet meer nodig voor een ontwikkelaar - slechts een paar muisklikken en je bent klaar om een gerichte, gepersonaliseerde digitale ervaring op te bouwen.

### Workflow gericht op de datawetenschapper

Wat je niveau van datawetenschap ook is, [!DNL Data Science Workspace] helpt het proces van het vinden van inzichten in data en het toepassen ervan op digitale ervaringen te vereenvoudigen en te versnellen.

### Data-exploratie

Het vinden van de juiste gegevens en het voorbereiden ervan is het meest arbeidsintensieve onderdeel van het opbouwen van een effectief recept. [!DNL Data Science Workspace] en Adobe Experience Platform helpen u sneller van gegevens naar inzichten te gaan.

Op Adobe Experience Platform worden uw gegevens over meerdere kanalen gecentraliseerd en opgeslagen in het gestandaardiseerde XDM-schema, zodat gegevens eenvoudiger te vinden, te begrijpen en schoon zijn. Één enkele opslag van gegevens die op een gemeenschappelijk schema worden gebaseerd kan u ontelbare uren van gegevensexploratie en voorbereiding besparen.

Terwijl u bladert, gebruikt u R, [!DNL Python] of Scala met de geïntegreerde, gehoste [!DNL Jupyter Notebook] om door de gegevenscatalogus op [!DNL Platform] te bladeren. Als u een van deze talen gebruikt, kunt u ook gebruikmaken van [!DNL Spark] ML en TensorFlow. Begin helemaal opnieuw of gebruik een van de laptopsjablonen voor specifieke bedrijfsproblemen.

Als onderdeel van de workflow voor gegevensverkenning kunt u ook nieuwe gegevens invoeren of bestaande functies gebruiken voor de voorbereiding van gegevens.

### Authoring

Met [!DNL Data Science Workspace] bepaalt u hoe u recepten wilt ontwerpen.

- Bespaar tijd door te bladeren naar een vooraf samengesteld recept dat aan uw bedrijfsbehoeften voldoet, dat u kunt gebruiken zoals is of vormen om aan uw specifieke vereisten te voldoen.
- Maak een geheel nieuw recept en gebruik de ontwerpruntime in Jupyter Notebook om het recept te ontwikkelen en te registreren.
- Upload een recept dat buiten Adobe Experience Platform is geschreven naar [!DNL Data Science Workspace] of importeer recept-code uit een opslagplaats, zoals [!DNL Git] , met behulp van de verificatie en integratie die beschikbaar zijn tussen [!DNL Git] en [!DNL Data Science Workspace] .

### Experimentatie

Data Science Workspace biedt een enorme flexibiliteit aan het experimentatieproces. Begin met je recept. Maak vervolgens een aparte instantie met hetzelfde kernalgoritme en unieke kenmerken, zoals hyper-tuning-parameters. U kunt zo veel instanties maken als u nodig hebt, elke instantie zo vaak trainen en scoren als u wilt. Terwijl u ze traint, houdt [!DNL Data Science Workspace] recepten, receptenvarianten en getrainde varianten bij, samen met evaluatiemetriek, zodat u dat niet hoeft te doen.

### Operationalisatie

Als je tevreden bent met je recept, is het slechts een paar klikken om een intelligente dienst te creëren. Geen codering vereist - je kunt het zelf doen, zonder een ontwikkelaar of ingenieur in te schrijven. Ten slotte publiceer de intelligente service naar Adobe IO en is deze klaar voor gebruik door je team voor digitale ervaringen.

<!--You can also publish your intelligent service to the Service Gallery, where it's available to specific people, specific organizations, or everyone who develops data solutions on Adobe Experience Platform. You can even share it with your external partners, and they can share their intelligent service with you. And the next time you're starting a new recipe, you can check the Service Gallery to see if there's a similar intelligent service you can use to get started. -->

### Voortdurende verbetering

[!DNL Data Science Workspace] houdt bij waar intelligente services worden aangeroepen en hoe ze presteren. Als data wordt ingevoerd, kun je de nauwkeurigheid van intelligente services evalueren om de lus te sluiten en de formules waar nodig omscholen om de prestaties te verbeteren. Het resultaat is een voortdurende verfijning van de precisie van klantpersonalisatie.

### Toegang tot nieuwe functies en gegevenssets

Datawetenschappers kunnen profiteren van nieuwe technologieën en datasets zodra ze beschikbaar zijn via Adobe-services. Door regelmatige updates, doen wij het werk van het integreren van datasets en technologieën in het platform, zodat moet u niet.

### Veiligheid en gemoedsrust

Het beveiligen van je data is een topprioriteit voor Adobe. Adobe beschermt je data met beveiligingsprocessen en -controles die zijn ontwikkeld om te voldoen aan door de industrie geaccepteerde standaarden, voorschriften en certificeringen.

De beveiliging is ingebouwd in software en services als onderdeel van de levenscyclus van veilige producten in de Adobe.
Ga naar de beveiligingspagina op https://www.adobe.com/security.html voor meer informatie over Adobe- en softwarebeveiliging, compliance en meer.

## [!DNL Data Science Workspace] in actie

Voorspellen en inzichten bieden de informatie die je nodig hebt om elke klant die je website bezoekt, contact opneemt met je callcenter of andere digitale ervaringen een gepersonaliseerde ervaring te bieden. Zo ontstaat je dagelijks werk met [!DNL Data Science Workspace] .

### Het probleem definiëren

Het begint allemaal met een bedrijfsprobleem. Bijvoorbeeld, heeft een online callcenter context nodig om hen te helpen een negatief klantensentiment positief veranderen.

Er zijn genoeg gegevens over de klant. Ze hebben de site bezocht, items in hun winkelwagentje gezet en zelfs bestellingen geplaatst. Ze hebben mogelijk eerder e-mails ontvangen, coupons gebruikt of contact opgenomen met het callcenter. Het recept moet daarom de beschikbare data over de klant en hun activiteiten gebruiken om de neiging te bepalen om een aanbieding te kopen en aan te bevelen die de klant waarschijnlijk zal waarderen en gebruiken.

![](./images/home/example_problem.png)

Op het tijdstip van het contact van het callcenter, heeft de klant nog twee paar schoenen in de kar, maar verwijderde een shirt. Met deze informatie, zou de intelligente dienst kunnen adviseren dat de agent van het callcenter een coupon voor 20% van schoenen tijdens de vraag aanbiedt. Als de klant de coupon gebruikt, wordt die informatie aan de dataset toegevoegd en worden de voorspellingen nog beter de volgende keer dat de klant roept.

### De data verkennen en voorbereiden

Op basis van het gedefinieerde bedrijfsprobleem, weet je dat het recept alle webtransacties van de klant moet bekijken, inclusief sitebezoeken, zoekopdrachten, paginaweergaven, geklikte koppelingen, winkelacties, ontvangen aanbiedingen, ontvangen e-mails, interacties met callcenters enzovoort.

Een datawetenschapper besteedt doorgaans tot 75% van de tijd die nodig is om een recept te creëren voor het verkennen en transformeren van de data. Gegevens komen vaak uit meerdere opslagplaatsen en worden opgeslagen in verschillende schema&#39;s. Deze gegevens moeten worden gecombineerd en toegewezen voordat ze kunnen worden gebruikt om een recept te maken.

[//]: # (Your first step is to check the recipe gallery to see if an existing recipe meets your needs, or comes close. An alternative is to import a recipe you created outside of Adobe Experience Platform. Starting with an existing recipe often streamlines the data exploration phase and makes it easier for a data scientist.)

Als je een geheel nieuw recept start of een bestaand recept configureert, begin je met je datazoekopdracht in een gecentraliseerde en gestandaardiseerde datatatatalogus voor je organisatie, waardoor de zoekactie aanzienlijk wordt vereenvoudigd. Je zou zelfs kunnen ontdekken dat een andere datawetenschapper in je organisatie al een vergelijkbare dataset heeft geïdentificeerd, en ervoor kiezen om die dataset te verfijnen in plaats van helemaal opnieuw te beginnen.
Alle gegevens in Adobe Experience Platform voldoen aan een gestandaardiseerd XDM-schema, zodat er geen complex model hoeft te worden gemaakt voor het samenvoegen van data of om hulp te krijgen van een datatechnicus.

Als u niet onmiddellijk de gegevens vindt u nodig hebt, maar het bestaat buiten Adobe Experience Platform, is het een vrij eenvoudige taak om extra datasets op te nemen, die ook in het gestandaardiseerde XDM schema zal omzetten.\
U kunt [!DNL Jupyter Notebook] gebruiken om de verwerking van gegevens te vereenvoudigen - mogelijk te beginnen met een laptopsjabloon of een notebook dat u eerder hebt gebruikt voor koopneiging.

![](./images/home/notebook_templates-new.png)

### Ontwerp het recept

Als je al een recept hebt gevonden dat aan al je behoeften voldoet, kun je verder experimenteren. U kunt het recept ook een beetje wijzigen of helemaal zelf een recept maken - u kunt profiteren van de [!DNL Data Science Workspace] -ontwerpruntime in [!DNL Jupyter Notebook] . Als u de ontwerpruntime gebruikt, weet u zeker dat u de [!DNL Data Science Workspace] -workflow voor training en scores kunt gebruiken en het recept later kunt omzetten, zodat het kan worden opgeslagen en hergebruikt door anderen in uw organisatie.

U kunt ook een recept importeren in [!DNL Data Science Workspace] en profiteren van de workflows voor experimenten terwijl u de intelligente service maakt.

### Experimenteer met het recept

Met een recept dat je kernalgoritmen voor machine learning omvat, kunnen veel recept-varianten worden gemaakt met één recept. Deze recept-instanties worden modellen genoemd. Een model vereist training en evaluatie om de operationele efficiëntie en effectiviteit ervan te optimaliseren, een proces dat doorgaans bestaat uit vallen en opstaan.

![](./images/home/recipe_hiearchy_ui.png)

Terwijl je je modellen traint, worden trainingsruns en evaluaties gegenereerd. [!DNL Data Science Workspace] houdt evaluatiemetrieken bij voor elk uniek model en de bijbehorende trainingen. Met evaluatiemetrieken die via experimenteren worden gegenereerd, kunt u bepalen welke trainingsrun het best presteert.

![](./images/home/evaluation_metrics.png)

Bezoek of [ API ](./models-recipes/train-evaluate-model-api.md) of [ UI ](./models-recipes/train-evaluate-model-ui.md) leerprogramma op om modellen in [!DNL Data Science Workspace] te trainen en te evalueren.

### Het model laten werken

Wanneer u het beste getrainde recept hebt gekozen om aan uw bedrijfsbehoeften te voldoen, kunt u zonder hulp van de ontwikkelaar een intelligente service maken in [!DNL Data Science Workspace] . Het is maar een paar klikken - geen codering vereist. Een gepubliceerde intelligente service is toegankelijk voor andere leden van uw organisatie zonder dat u het model opnieuw hoeft te maken.

Een gepubliceerde intelligente service is configureerbaar om zichzelf automatisch van tijd tot tijd op te leiden met behulp van nieuwe data zodra deze beschikbaar zijn. Dit zorgt ervoor dat uw service efficiënt en efficiënt blijft wanneer de tijd doorgaat.

## Volgende stappen

[!DNL Data Science Workspace] stroomlijnt en vereenvoudigt de datawetenschapsworkflow, van dataverzameling tot algoritmen en intelligente services voor datawetenschappers van alle vaardigheidsniveaus. Met de geavanceerde gereedschappen die [!DNL Data Science Workspace] biedt, kunt u de tijd aanzienlijk verkorten van gegevens naar inzichten.

Nog belangrijker is dat [!DNL Data Science Workspace] de mogelijkheden voor gegevenswetenschap en algoritmische optimalisatie van het toonaangevende marketingplatform van Adobe in handen legt van wetenschappers op het gebied van bedrijfsgegevens. Voor het eerst kunnen bedrijven bedrijfseigen algoritmen aan het platform aanbieden, waarbij ze profiteren van de krachtige computervaardigheden van Adobe en AI-mogelijkheden om op grote schaal zeer persoonlijke klantervaringen te bieden.

Met het huwelijk van merkenkennis en het machineonderwijs van Adobe en AI-processen hebben bedrijven de macht om meer bedrijfswaarde en merktrouw te drijven door klanten te geven wat ze willen, voordat ze erom vragen.

Voor extra informatie, zoals een volledig dagelijks werkschema, gelieve te beginnen door de [ looppas-door ](./walkthrough.md) documentatie van Workspace van de Wetenschap van Gegevens te lezen.

## Aanvullende bronnen

De volgende video is ontworpen om uw begrip van [!DNL Data Science Workspace] te steunen.

>[!VIDEO](https://video.tv.adobe.com/v/30567?quality=12&amp;enable10seconds=on&amp;speedcontrol=on)