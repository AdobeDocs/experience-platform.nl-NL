---
keywords: Experience Platform;home;Data Science Workspace;populaire onderwerpen;data science workspace;data science
solution: Experience Platform
title: Overzicht van de Data Science Workspace
topic-legacy: overview
description: Deze handleiding biedt een overzicht van de belangrijkste concepten met betrekking tot de Data Science Workspace in Adobe Experience Platform.
exl-id: bef25073-0dfb-453d-8c32-7f44d917d62d
source-git-commit: b30700fde3ce75cc4f66343c8d37d3e731775627
workflow-type: tm+mt
source-wordcount: '2388'
ht-degree: 0%

---

# Overzicht van de Data Science Workspace

Adobe Experience Platform [!DNL Data Science Workspace] maakt gebruik van machinaal leren en kunstmatige intelligentie om inzichten van uw gegevens te onthullen. geïntegreerd in Adobe Experience Platform, [!DNL Data Science Workspace] helpt u om voorspellingen te maken gebruikend uw inhoud en gegevensactiva over Adobe oplossingen.

Gegevenswetenschappers van alle vaardigheidsniveaus zullen geavanceerde, makkelijk te gebruiken hulpmiddelen vinden die snelle ontwikkeling, opleiding, en het stemmen van machine het leren recepten steunen - alle voordelen van AI technologie, zonder de ingewikkeldheid.

Met [!DNL Data Science Workspace]Gegevenswetenschappers kunnen gemakkelijk intelligente services-API&#39;s maken, aangedreven door machinaal leren. Deze services werken samen met andere Adobe-services, waaronder Adobe Target en Adobe Analytics Cloud, om u te helpen persoonlijke, doelgerichte digitale ervaringen te automatiseren voor web-, desktop- en mobiele apps.

Deze handleiding biedt een overzicht van de belangrijkste concepten met betrekking tot [!DNL Data Science Workspace].

## Inleiding

De onderneming van vandaag plaatst een hoge prioriteit op het ontginnen van grote gegevens voor voorspellingen en inzichten die hen zullen helpen klantenervaringen personaliseren en meer waarde aan klanten - en aan de zaken leveren.
Hoe belangrijk het ook is, het overstappen van gegevens naar inzichten kan hoge kosten met zich meebrengen. Meestal vereist het deskundige gegevenswetenschappers die intensief en tijdrovend gegevensonderzoek uitvoeren om machinaal leermodellen te ontwikkelen, of recepten, die intelligente diensten aandrijven. Het proces is lang, de technologie is complex, en deskundige gegevenswetenschappers kunnen moeilijk te vinden zijn.

Met [!DNL Data Science Workspace], Adobe Experience Platform biedt u de mogelijkheid om ervaren AI in de hele onderneming te introduceren, gegevens-naar-inzichten-naar-code te stroomlijnen en te versnellen met:
- Een framework voor machinetlering en runtime
- Geïntegreerde toegang tot uw gegevens die in Adobe Experience Platform zijn opgeslagen
- Geïntegreerd gegevensschema gebaseerd op [!DNL Experience Data Model] (XDM)
- De verwerkingskracht die essentieel is voor het leren van machines/AI en het beheren van grote datasets
- Prebuilt machine het leren recepten om de sprong in AI gedreven ervaringen te versnellen
- Vereenvoudigd ontwerp, hergebruik en wijziging van recepten voor gegevenswetenschappers met verschillende vaardigheidsniveaus
- Intelligente het de dienstpubliceren en delen in slechts een paar klikken - zonder een ontwikkelaar - en controle en herscholing voor ononderbroken optimalisering van gepersonaliseerde klantenervaringen

Gegevenswetenschappers van alle vaardigheidsniveaus zullen sneller en effectievere digitale ervaringen bereiken.

## Aan de slag

Voordat u in de details van [!DNL Data Science Workspace]Hier volgt een korte samenvatting van de belangrijkste termen:

| Term | Definitie |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [!DNL Data Science Workspace] | [!DNL Data Science Workspace] binnen [!DNL Experience Platform] stelt klanten in staat modellen voor het leren van machines te maken met behulp van gegevens over [!DNL Experience Platform] en Adobe Oplossingen om intelligente inzichten en voorspellingen te produceren om prachtige digitale ervaringen van eindgebruikers te wekken. |
| Kunstmatige intelligentie | Kunstmatige intelligentie is een theorie en ontwikkeling van computersystemen die taken kunnen uitvoeren die normaal menselijke intelligentie vereisen, zoals visuele waarneming, spraakherkenning, besluitvorming en vertaling tussen talen. |
| Machine leren | Het leren van de machine is het gebied van studie dat computers de capaciteit toelaat om te leren zonder uitdrukkelijk geprogrammeerd te zijn. |
| [!DNL Sensei] ML Framework | [!DNL Sensei] Het Kader van ML is een verenigd machine het leren kader over Adobe dat hefboomwerkingen gegevens over [!DNL Experience Platform] gegevenswetenschappers in staat te stellen sneller, schaalbaar en herbruikbaar gebruik te maken van computerleergestuurde inlichtingendiensten. |
| [!DNL Experience Data Model] | [!DNL Experience Data Model] (XDM) is de normalisatieinspanning die door Adobe wordt geleid om standaardschema&#39;s zoals te bepalen [!DNL Profile] en [!DNL ExperienceEvent], voor Customer Experience Management. |
| [!DNL JupyterLab] | [!DNL JupyterLab] is een open-bron web-based interface voor Project Jupyter en is strak geïntegreerd in [!DNL Experience Platform]. |
| Ontvangers | Een recept is Adobe term voor een modelspecificatie en is een top-level container die een specifiek machine het leren, AI algoritme of een samenstel van algoritmen, verwerkingslogica, en configuratie vertegenwoordigt die wordt vereist om een opgeleid model te bouwen en uit te voeren en vandaar helpen specifieke bedrijfsproblemen oplossen. |
| Model | Een model is een geval van een machine het leren recept dat gebruikend historische gegevens en configuraties wordt opgeleid om voor een bedrijfs geval op te lossen. |
| Training | Training is het proces van leerpatronen en inzichten van gelabelde gegevens. |
| Gevolgd model | Een getraind model vertegenwoordigt de uitvoerbare output van een model opleidingsproces, waarin een reeks opleidingsgegevens werd toegepast op de modelinstantie. Een getraind model zal een verwijzing naar om het even welke intelligente Webdienst handhaven die van het wordt gecreeerd. Het getrainde model is geschikt voor het scoren en maken van een intelligente webservice. Wijzigingen in een getraind model kunnen als een nieuwe versie worden bijgehouden. |
| Scores | Scores is het proces om inzichten van gegevens te produceren gebruikend een opgeleid model. |
| Service | Een geïmplementeerde service stelt functies van een kunstmatige intelligentie, een model voor machinaal leren of een geavanceerd algoritme via een API beschikbaar, zodat het door andere services of toepassingen kan worden gebruikt om intelligente apps te maken. |

De volgende grafiek schetst de hiërarchische verhouding tussen Ontvangers, Modellen, de Looppas van de Opleiding, en het Scorelooppas.

![](./images/home/recipe_hiearchy_ui.png)

## [!DNL Data Science Workspace] begrijpen

Met [!DNL Data Science Workspace]Uw gegevenswetenschappers kunnen het lastige proces stroomlijnen om inzichten in grote datasets te ontdekken. Gebaseerd op een gemeenschappelijk computerleerkader en runtime, [!DNL Data Science Workspace] biedt geavanceerd workflowbeheer, modelbeheer en schaalbaarheid. De intelligente diensten steunen hergebruik van machine het leren recepten om een verscheidenheid van toepassingen tot stand te brengen die gebruikend Adobe producten en oplossingen worden gecreeerd.

### Toegang tot gegevens met één stop

Gegevens zijn de hoeksteen van het leren van AI en machines.

[!DNL Data Science Workspace] volledig geïntegreerd is met Adobe Experience Platform, met inbegrip van het Data Lake, [!DNL Real-time Customer Profile], en [!DNL Unified Edge]. Ontdek al uw organisatiegegevens die in Adobe Experience Platform tegelijk zijn opgeslagen, samen met veelgebruikte gegevens en uitgebreide leerbibliotheken, zoals [!DNL Spark] ML en [!DNL TensorFlow]. Als u niet vindt wat u nodig hebt, neemt uw eigen datasets op gebruikend het XDM gestandaardiseerde schema.

### Prebuilt machine het leren recepten

[!DNL Data Science Workspace] omvat prebuilt machine het leren recepten voor gemeenschappelijke bedrijfsbehoeften, zoals kleinhandelsverkoop voorspellen en anomalieopsporing, zodat gegevenswetenschappers en ontwikkelaars niet van kras hoeven te beginnen. Er worden momenteel drie recepten aangeboden, [productaankoopvoorspelling](./pre-built-recipes/product-purchase-prediction.md), [productaanbevelingen](./pre-built-recipes/product-recommendations.md), en [detailverkoop](./pre-built-recipes/retail-sales.md).

[//]: # (The built-in recipe gallery offers recommendations for prebuilt recipes based on your business needs.)

U kunt desgewenst een vooraf samengesteld recept aanpassen aan uw behoeften, een recept importeren of helemaal opnieuw beginnen om een aangepast recept te maken. Maar als je eenmaal begint met het trainen en afstemmen van een recept, is het maken van een aangepaste intelligente service geen ontwikkelaar nodig - slechts een paar klikken en je bent klaar om een gerichte, gepersonaliseerde digitale ervaring op te bouwen.

### Werkschema gericht op de gegevenswetenschapper

Ongeacht uw niveau van deskundigheid op het gebied van gegevenswetenschap, [!DNL Data Science Workspace] helpt u het zoeken naar inzichten in gegevens te vereenvoudigen en te versnellen en deze toe te passen op digitale ervaringen.

### Gegevensexploratie

Het vinden van de juiste gegevens en het voorbereiden ervan is het meest arbeidsintensieve onderdeel van het opbouwen van een effectief recept. [!DNL Data Science Workspace] en Adobe Experience Platform helpt u sneller van gegevens naar inzichten te gaan.

Op Adobe Experience Platform worden uw gegevens over meerdere kanalen gecentraliseerd en opgeslagen in het gestandaardiseerde XDM-schema, zodat gegevens eenvoudiger te vinden, te begrijpen en schoon zijn. Één enkele opslag van gegevens die op een gemeenschappelijk schema worden gebaseerd kan u ontelbare uren van gegevensexploratie en voorbereiding besparen.

Als u bladert, gebruikt u R [!DNL Python]of Scala met de geïntegreerde, gehoste [!DNL Jupyter Notebook] om door de gegevenscatalogus te bladeren [!DNL Platform]. Als u een van deze talen gebruikt, kunt u ook gebruikmaken van [!DNL Spark] ML en TensorFlow. Begin helemaal opnieuw of gebruik een van de laptopsjablonen voor specifieke bedrijfsproblemen.

Als onderdeel van de workflow voor gegevensverkenning kunt u ook nieuwe gegevens invoeren of bestaande functies gebruiken voor de voorbereiding van gegevens.

### Authoring

Met [!DNL Data Science Workspace], bepaalt u hoe u recepten wilt ontwerpen.

- Bespaar tijd door te bladeren naar een vooraf samengesteld recept dat aan uw bedrijfsbehoeften voldoet, dat u kunt gebruiken zoals is of vormen om aan uw specifieke vereisten te voldoen.
- Maak een geheel nieuw recept en gebruik de ontwerpruntime in Jupyter Notebook om het recept te ontwikkelen en te registreren.
- Een buiten Adobe Experience Platform ontworpen recept uploaden naar [!DNL Data Science Workspace] of importeer recept-code uit een gegevensopslagruimte, zoals [!DNL Git], met behulp van de verificatie en integratie die beschikbaar zijn tussen [!DNL Git] en [!DNL Data Science Workspace].

### Experimentatie

De Werkruimte van de Wetenschap van gegevens brengt enorme flexibiliteit aan het experimentatieproces. Begin met je recept. Maak vervolgens een aparte instantie met hetzelfde kernalgoritme en unieke kenmerken, zoals hyper-tuning-parameters. U kunt zo veel instanties maken als u nodig hebt, elke instantie zo vaak trainen en scoren als u wilt. Terwijl je ze traint, [!DNL Data Science Workspace] volgt recepten, recept instanties, en getrainde instanties, samen met evaluatiemetriek, zodat moet u niet.

### Operationalisatie

Als je tevreden bent met je recept, is het slechts een paar klikken om een intelligente dienst te creëren. Geen codering vereist - u kunt het zelf doen zonder een ontwikkelaar of technicus in te schrijven. Tot slot publiceert u de intelligente service naar Adobe IO en is deze klaar voor gebruik door uw team voor digitale ervaring.

<!--You can also publish your intelligent service to the Service Gallery, where it's available to specific people, specific organizations, or everyone who develops data solutions on Adobe Experience Platform. You can even share it with your external partners, and they can share their intelligent service with you. And the next time you're starting a new recipe, you can check the Service Gallery to see if there's a similar intelligent service you can use to get started. -->

### Continue verbetering

[!DNL Data Science Workspace] sporen waar de intelligente diensten worden aangehaald en hoe zij presteren. Terwijl de gegevens worden doorgegeven, kunt u de nauwkeurigheid van de intelligente service beoordelen om de lus te sluiten en de recepten zo nodig opnieuw trainen om de prestaties te verbeteren. Het resultaat is een voortdurende verfijning van de nauwkeurigheid van klantpersonalisatie.

### Toegang tot nieuwe functies en datasets

Gegevenswetenschappers kunnen profiteren van nieuwe technologieën en datasets zodra deze beschikbaar zijn via Adobe-services. Door regelmatige updates, doen wij het werk om datasets en technologieën in het platform te integreren, zodat moet u niet.

### Veiligheid en gemoedsrust

Het beveiligen van uw gegevens is een topprioriteit voor Adobe. Adobe beschermt uw gegevens met beveiligingsprocessen en -besturingselementen die zijn ontwikkeld om te helpen voldoen aan door de branche aanvaarde standaarden, regels en certificeringen.

De veiligheid wordt ingebouwd in software en de diensten als deel van de Levenscyclus van het Product van de Adobe Veilige.
Ga naar de beveiligingspagina op https://www.adobe.com/security.html voor meer informatie over de beveiliging van Adobe-gegevens en -software, compatibiliteit en meer.

## [!DNL Data Science Workspace] in actie

De voorspellingen en de inzichten verstrekken de informatie u nodig hebt om een hoogst gepersonaliseerde ervaring aan elke klant te leveren die uw website bezoekt, uw callcenter contacteert, of aan andere digitale ervaringen aangaat. Zo ziet u hoe uw dagelijkse werk er uitziet [!DNL Data Science Workspace].

### Het probleem definiëren

Het begint allemaal met een bedrijfsprobleem. Bijvoorbeeld, heeft een online callcenter context nodig om hen te helpen een negatief klantensentiment positief veranderen.

Er zijn genoeg gegevens over de klant. Ze hebben op de site gebladerd, items in hun winkelwagentje gezet en zelfs bestellingen geplaatst. Ze hebben mogelijk eerder e-mails ontvangen, coupons gebruikt of contact opgenomen met het callcenter. Het recept moet dan de beschikbare gegevens over de klant en zijn activiteiten gebruiken om te bepalen of hij geneigd is een aanbod te kopen en aan te bevelen dat de klant waarschijnlijk zal waarderen en gebruiken.

![](./images/home/example_problem.png)

Op het tijdstip van het contact van het callcenter, heeft de klant nog twee paar schoenen in de kar, maar verwijder een shirt. Met deze informatie, zou de intelligente dienst kunnen adviseren dat de agent van het vraagcentrum een coupon voor 20% van schoenen tijdens de vraag aanbiedt. Als de klant de coupon gebruikt, wordt die informatie toegevoegd aan de dataset en worden de voorspellingen nog beter de volgende keer de klantenvraag.

### De gegevens verkennen en voorbereiden

Op basis van het gedefinieerde bedrijfsprobleem weet u dat het recept alle webtransacties van de klant moet bekijken, zoals bezoeken op de site, zoekopdrachten, paginaweergaven, geklikte koppelingen, cartacties, ontvangen aanbiedingen, ontvangen e-mails, interacties tussen callcenters enzovoort.

Een gegevenswetenschapper besteedt doorgaans tot 75% van de tijd die nodig is om een recept te maken voor het verkennen en transformeren van de gegevens. De gegevens komen vaak uit veelvoudige bewaarplaatsen en worden bewaard in verschillende schema&#39;s - het moet worden gecombineerd en in kaart gebracht alvorens het kan worden gebruikt om een recept tot stand te brengen.

[//]: # (Your first step is to check the recipe gallery to see if an existing recipe meets your needs, or comes close. An alternative is to import a recipe you created outside of Adobe Experience Platform. Starting with an existing recipe often streamlines the data exploration phase and makes it easier for a data scientist.)

Als u van kras begint of een bestaand recept vormt, begint u uw gegevensonderzoek in een gecentraliseerde en gestandaardiseerde gegevenscatalogus voor uw organisatie, die de jacht aanzienlijk vereenvoudigt. Misschien zult u zelfs zien dat een andere gegevenswetenschapper in uw organisatie al een vergelijkbare dataset heeft geïdentificeerd, en verkiest om die dataset te verfijnen eerder dan van kras te beginnen.
Alle gegevens in Adobe Experience Platform voldoen aan een gestandaardiseerd XDM-schema, waardoor het niet nodig is om een complex model te maken voor het samenvoegen van gegevens of hulp te krijgen van een gegevensengineer.

Als u niet onmiddellijk de gegevens vindt u wenst, maar het bestaat buiten Adobe Experience Platform, is het een vrij eenvoudige taak om extra datasets in te voeren, die ook in het gestandaardiseerde XDM schema zal omzetten.\
U kunt [!DNL Jupyter Notebook] om de verwerking van gegevens te vereenvoudigen - mogelijk te beginnen met een laptopsjabloon of een laptop die u eerder hebt gebruikt voor koopkracht.

![](./images/home/notebook_templates.png)

### Auteur van het recept

Als u al een recept hebt gevonden dat aan al uw behoeften voldoet, kunt u verdergaan met experimenteren. Of u kunt het recept een beetje wijzigen of een geheel nieuw recept maken, zodat u profiteert van de [!DNL Data Science Workspace] ontwerpruntime in [!DNL Jupyter Notebook]. Wanneer u de ontwerpruntime gebruikt, weet u zeker dat u de [!DNL Data Science Workspace] training en scoring en zet het recept later om, zodat het kan worden opgeslagen en hergebruikt door anderen in uw organisatie.

U kunt ook een recept importeren in [!DNL Data Science Workspace] en maak gebruik van de workflows voor experimenteren terwijl u de intelligente service creëert.

### Experimenteer met het recept

Met een recept dat uw kernalgoritmen voor machinaal leren omvat, kunnen vele recept instanties met één enkel recept worden gecreeerd. Deze recept-varianten worden modellen genoemd. Een model vereist training en evaluatie om de operationele efficiëntie en effectiviteit ervan te optimaliseren, een proces dat meestal bestaat uit vallen en fouten.

![](./images/home/recipe_hiearchy_ui.png)

Tijdens het trainen van uw modellen worden trainingsreeksen en evaluaties gegenereerd. [!DNL Data Science Workspace] houdt het overzicht van evaluatiemetriek voor elk uniek model en hun trainingslooppas bij. De metriek van de evaluatie die door experimentatie wordt geproduceerd zal u toestaan om de trainingslooppas te bepalen die het best presteert.

![](./images/home/evaluation_metrics.png)

Bezoek de [API](./models-recipes/train-evaluate-model-api.md) of [UI](./models-recipes/train-evaluate-model-ui.md) zelfstudie over het trainen en evalueren van modellen in [!DNL Data Science Workspace].

### Het model opereren

Wanneer u het best opgeleide recept hebt geselecteerd om aan uw bedrijfsbehoeften te voldoen, kunt u een intelligente dienst tot stand brengen in [!DNL Data Science Workspace] zonder hulp van de ontwikkelaar. Het is slechts een paar klikken - geen codering vereist. Een gepubliceerde intelligente dienst is toegankelijk voor andere leden van uw organisatie zonder de behoefte om het model te ontspannen.

Een gepubliceerde intelligente dienst is configureerbaar om zich van tijd tot tijd automatisch op te leiden gebruikend nieuwe gegevens aangezien zij beschikbaar worden. Dit zorgt ervoor dat uw service efficiënt en efficiënt blijft wanneer de tijd doorgaat.

## Volgende stappen

[!DNL Data Science Workspace] helpt de workflow voor gegevenswetenschap te stroomlijnen en te vereenvoudigen, van gegevensverzameling tot algoritmen tot intelligente services voor gegevenswetenschappers van alle vaardigheidsniveaus. Met de geavanceerde gereedschappen [!DNL Data Science Workspace] biedt, kunt u de tijd aanzienlijk verkorten van gegevens naar inzichten.

Belangrijker nog, [!DNL Data Science Workspace] zet de mogelijkheden voor gegevenswetenschappen en algoritmische optimalisatie van het toonaangevende marketingplatform in de handen van wetenschappers op het gebied van bedrijfsgegevens. Voor de eerste keer kunnen bedrijven bedrijfseigen algoritmen aan het platform aanbieden, waarbij ze profiteren van krachtige machinemogelijkheden en AI-mogelijkheden om zeer gepersonaliseerde klantervaringen op grote schaal te bieden.

Met het huwelijk van merkenkennis en Adobe-machinedragers en AI-processen hebben bedrijven de macht om meer bedrijfswaarde en merkloyaliteit te drijven door klanten te geven wat ze willen, voordat ze hierom vragen.

Voor aanvullende informatie, zoals een volledige dagelijkse workflow, begint u met het lezen van de [Doorloop van de Data Science Workspace](./walkthrough.md) documentatie.

## Aanvullende bronnen

De volgende video is ontworpen om uw begrip van [!DNL Data Science Workspace].

>[!VIDEO](https://video.tv.adobe.com/v/30567?quality=12&amp;enable10seconds=on&amp;speedcontrol=on)