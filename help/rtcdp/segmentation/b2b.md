---
title: Gebruiksscenario's voor segmentatie voor Real-time Customer Data Platform B2B Edition
description: Een overzicht van de verschillende beschikbare Adobe Real-time Customer Data Platform B2B Edition-gebruiksgevallen.
feature: Get Started, Audiences, Segments, B2B
badgeB2B: label="B2B Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 2a99b85e-71b3-4781-baf7-a4d5436339d3
source-git-commit: 8a487d948d2eb7db167298b61045ef8dd2099da6
workflow-type: tm+mt
source-wordcount: '1330'
ht-degree: 0%

---

# Gebruiksscenario&#39;s voor segmentatie voor Real-time Customer Data Platform B2B Edition

Dit document bevat voorbeelden van segmentdefinities in Adobe Real-time Customer Data Platform B2B Edition en hoe verschillende typen kenmerken kunnen worden gecombineerd voor veelgebruikte B2B-toepassingen. Om te begrijpen hoe de bestemmingen in uw B2B- werkschema passen, gelieve te zien [ leerprogramma van begin tot eind ](../b2b-tutorial.md#create-a-segment-to-evaluate-your-data).

>[!NOTE]
>
>De kenmerken die vereist zijn voor deze segmentatieuse-gevallen zijn alleen beschikbaar voor Real-time Customer Data Platform B2B Edition-klanten. Als u Real-time Customer Data Platform B2B Uitgave niet gebruikt, zie in plaats daarvan het [ segmentatieoverzicht ](./segmentation-overview.md).

## Vereisten {#prerequisites}

Voordat u de segmentatiekenmerken voor B2B-klassen kunt gebruiken, moet u de volgende stappen uitvoeren:

1. Maak schema&#39;s waarin de B2B-klassen worden gebruikt. De klassen B2B Edition omvatten Account, Campagne, Opportunity, Marketing List en meer. Voor informatie over [ hoe te opstellingsschema&#39;s voor gebruik met B2B klassen ](../schemas/b2b.md) gelieve te zien de schemadocumentatie.
2. Maak relaties tussen uw XDM- (Experience Data Model) B2B-schema&#39;s. Het publiek dat op de attributen van de Uitgave B2B wordt gebaseerd vereist verband tussen de klassen om de uitgebreide functionaliteit van de Segmentatie B2B volledig te gebruiken. Zie de documentatie op [ hoe te om een verband tussen twee schema&#39;s te bepalen B2B ](../../xdm/tutorials/relationship-b2b.md) voor meer informatie.
3. Samenvatting gegevens gebruikend datasets die op uw B2B- schema&#39;s worden gebaseerd. Zie de brondocumentatie voor [ informatie over hoe te om gegevens ](../../sources/connectors/adobe-applications/marketo/marketo.md) in te voeren.
4. Lees de [ gebruikersgids van de Bouwer van het Segment ](../../segmentation/ui/segment-builder.md) voor een meer gedetailleerde begeleiding op hoe te om publiek te bouwen.

Als aan deze vereisten is voldaan, kunt u deze kenmerken combineren voor algemene B2B-gebruiksgevallen.

## Aan de slag {#getting-started}

Zodra de unieschema&#39;s voor de B2B-klassen relaties hebben vastgesteld en zijn gebruikt om gegevens in te voeren, worden hun kenmerken beschikbaar gesteld in de linkerspoorlijn van de Segment Builder.

B2B-klassen en hun kenmerken worden toegevoegd met een `B2B` -label in de segmentatiewerkruimte om ze te onderscheiden van de standaardklassen in Real-time Customer Data Platform.

Om een publiek voor B2B gebruiksgevallen effectief tot stand te brengen, is het belangrijk om een intieme kennis van het schema te hebben en te begrijpen hoe het gegevensmodel eruit ziet. Het is ook handig om rekening te houden met het pad dat de gegevens van het ene gegevensobject naar het andere overnemen.

De onderstaande afbeelding illustreert de relaties tussen de B2B-klassen die beschikbaar zijn in Real-Time CDP B2B Edition.

![ B2B klasse ERD ](../assets/segmentation/b2b-classes.png)

Aangezien uw gegevensmodel gecompliceerd kan zijn, kunt u de interface van het Platform gebruiken om een meer gedetailleerde visuele vertegenwoordiging van uw gegevensmodel te bekijken om de relevante attributen voor uw gebruiksgeval te vinden. Ga om te beginnen naar de interface van het platform en selecteer Schema&#39;s in de linkernavigatie.

Selecteer het gewenste schema in de beschikbare lijst en selecteer de gewenste relatie in de [!UICONTROL Composition] side rail. In het onderstaande voorbeeld wordt door het selecteren van de relatie &quot;Persoon&quot; duidelijk welk kenmerk in het huidige schema verwijst naar het gerelateerde schema &quot;Persoon&quot; (als dit het bronschema in de relatie is) of dat naar het schema &quot;Persoon&quot; wordt verwezen (als dit het referentieschema in de relatie is).

![ bron-zeer belangrijk voorbeeld gebruikend de personenverhouding in de schemawerkruimte ](../assets/segmentation/source-key-schema-relationship-example.png)

Deze relatie wordt weerspiegeld in de Segment Builder door het gebruik van `Key` mappen, zoals in de onderstaande afbeelding wordt getoond.

![ bron-zeer belangrijk voorbeeld gebruikend de segmentbouwer in de segmentatiewerkruimte ](../assets/segmentation/source-key-segmentation-example.png)

Gelieve te verwijzen naar de [ schema&#39;s in de documentatie van de Uitgave van Real-time Customer Data Platform B2B ](../schemas/b2b.md) voor meer informatie over de beschikbare B2B klassen.

De onderstaande gebruiksgevallen bevatten informatie over de klassen die worden gebruikt om relaties tussen de verschillende schema&#39;s tot stand te brengen om deze resultaten te bereiken. Deze voorbeelden kunnen u helpen uw eigen publiek tot stand brengen.

## Voorbeelden van gebruiksgevallen van verschillende segmentaties {#use-cases}

De volgende gebruiksgevallen zijn beschikbaar voor segmentatie met de B2B Edition. Elk voorbeeld bevat een beschrijving van wat de doelgroep doet en een beschrijving van de klassen die zijn gebruikt om deze te maken. De geleverde afbeeldingen markeren het bestandspad in de [!UICONTROL Attributes] side rail die de structuur van het schema weerspiegelt. De sectie [!UICONTROL Segment properties] rechts van de weergave bevat een schriftelijke uitsplitsing van de attributen van het publiek.

### Voorbeeld 1: Zoek naar &quot;besluitvormers&quot; voor B2B-mogelijkheden {#find-decision-maker}

Vind alle mensen die de &quot;Beslissingsmaker&quot;van om het even welke kans zijn. Dit publiek heeft een koppeling nodig tussen de klasse [!UICONTROL XDM Individual Profile] en de klasse [!UICONTROL XDM Business Opportunity Person Relation] .

![ UI die voorbeeld 1 montages ](../assets/segmentation/example-1.png) toont

### Voorbeeld 2: B2B-profielen zoeken die zijn toegewezen aan mogelijkheden boven een bepaald dollarbedrag {#find-opportunities-amount}

Zoek alle mensen die rechtstreeks zijn toegewezen aan kansen waarvan het opportuniteitsbedrag hoger is dan het opgegeven bedrag ($ 1 miljoen). Dit publiek heeft een koppeling nodig tussen de klasse [!UICONTROL XDM Individual Profile] , de klasse [!UICONTROL XDM Business Opportunity Person Relation] en de klasse [!UICONTROL XDM Business Opportunity] .

![ UI die voorbeeld 2 montages ](../assets/segmentation/example-2.png) toont

### Voorbeeld 3: B2B-profielen zoeken die zijn toegewezen aan mogelijkheden per locatie {#find-opportunities-location}

Zoek alle personen die rechtstreeks zijn toegewezen aan kansen waar de account zich op een bepaalde locatie bevindt (Canada). Dit publiek heeft een koppeling nodig tussen de klasse [!UICONTROL XDM Individual Profile] , de klasse [!UICONTROL XDM Business Opportunity Person Relation] , de klasse [!UICONTROL XDM Business Opportunity] en de klasse [!UICONTROL XDM Business Account] .

![ UI die voorbeeld 3 montages ](../assets/segmentation/example-3.png) toont

### Voorbeeld 4: Zoek naar &quot;besluitvormers&quot; voor mogelijkheden per bedrijfstak en browsergedrag {#find-industry-browsing-behavior}

Vind alle mensen die een &quot;Beslissingsmaker&quot;van om het even welke kans zijn waar de rekening in de &quot;Financiën&quot;industrie is, en bezocht de het tarief pagina in de laatste drie dagen. Dit publiek heeft een koppeling nodig tussen de klasse [!UICONTROL XDM Individual Profile] , de klasse [!UICONTROL XDM Business Opportunity Person Relation] , de klasse [!UICONTROL XDM Business Opportunity] en de klasse [!UICONTROL XDM Business Account] en de klasse [!UICONTROL XDM ExperienceEvent] .

![ UI die voorbeeld 4 montages ](../assets/segmentation/example-4.png) toont

### Voorbeeld 5: Zoek B2B-profielen voor mogelijkheden per afdelingsnaam en opportuniteitsbedrag {#find-department-opportunity-amount}

Vind alle mensen die in een afdeling van het Personeel (HR) werken en om het even welke rekening hebben die minstens één open kans heeft die het bepaalde bedrag ($1 miljoen) of meer waard is. Dit publiek heeft een koppeling nodig tussen de klasse [!UICONTROL XDM Individual Profile] , de klasse [!UICONTROL XDM Business Account] en de klasse [!UICONTROL XDM Business Opportunity] .

![ UI die voorbeeld 5 montages ](../assets/segmentation/example-5.png) toont

### Voorbeeld 6: Zoek naar B2B-profielen per functie en jaarrekening {#find-by-job-title-and-revenue}

Zoek alle personen van wie de functie Vice President is en die een rekening hebben met jaarinkomsten van het gegeven bedrag ($ 100 miljoen) of meer, en de prijspagina ten minste drie keer in de afgelopen maand hebben bezocht. Dit publiek heeft een koppeling nodig tussen de klasse [!UICONTROL XDM Individual Profile] , de klasse [!UICONTROL XDM Business Account] en de klasse [!UICONTROL XDM ExperienceEvent] .

![ UI die voorbeeld 6 montages ](../assets/segmentation/example-6.png) toont

### Voorbeeld 7: Zoek naar &quot;besluitvormers&quot; op opportuniteitsstatus en blader gedrag {#find-by-opportunity-status-and-browsing-behavior}

Zoek alle mensen die een &quot;Beslissingsmaker&quot;van om het even welke gesloten-verloren kans zijn, en bezocht de het tarief pagina in de vorige week. Dit publiek heeft een koppeling nodig tussen de klasse [!UICONTROL XDM Individual Profile] , de klasse [!UICONTROL XDM Business Opportunity Person Relation] , de klasse [!UICONTROL XDM Business Opportunity] en de klasse [!UICONTROL XDM ExperienceEvent] .

![ UI die voorbeeld 7 montages ](../assets/segmentation/example-7.png) toont

### Voorbeeld 8: Verwante accounts gebruiken om het segmentatiebereik uit te breiden {#related-accounts}

Vind alle mensen die in een afdeling van het Personeel (HR) werken en met om het even welke rekening *of om het even welke verwante rekeningen van de rekening* verwant zijn die minstens één open kans de bepaalde hoeveelheid ($1 miljoen) of meer heeft. Dit publiek heeft een koppeling nodig tussen de klasse [!UICONTROL XDM Individual Profile] , de klasse [!UICONTROL XDM Business Account] en de klasse [!UICONTROL XDM Business Opportunity] .

![ UI tonend segmentatie voor verwante rekeningen ](../assets/segmentation/example-8.png)

### Voorbeeld 9: Gebruik loodscores en/of accountscores om een profiel te kwalificeren {#account-scoring}

Alle profielen zoeken met een hoofdscore van meer dan 80.

![ UI tonend segmentatie voor het vooruitlopende lood en rekening die ](../assets/segmentation/example-9.png) scoren

### Voorbeeld 10: B2B-profielen zoeken die zijn gekoppeld aan accounts waarvan de bovenliggende org inkomsten heeft boven een bepaald dollarbedrag {#find-parent-org-amount}

Vind alle mensen die met rekeningen worden geassocieerd waarvan Parent Org een opbrengst meer dan het bepaalde bedrag ($100.000.000) heeft.

![ UI tonend segmentatie ouder org ](../assets/segmentation/example-10.png)

### Voorbeeld 11: B2B-profielen zoeken op basis van functie- en accountnaam met een actieve relatie {#find-by-job-title-and-account-name}

Vind alle mensen die een &quot;Manager&quot;op de rekening &quot;Acme&quot;zijn, waar de rekeningsverhouding &quot;Actief is.

![ UI tonend segmentatie ouder org ](../assets/segmentation/example-11.png)

### Voorbeeld 12: Zoek naar B2B-profielen voor campagnes waarbij de werkelijkeKosten hoger is dan de gebudgetteerdeKosten {#find-actualcost-exceed-budgetcost}

Vind alle mensen die voor campagnes worden gericht waar actualCost de budgetedCost overtrof.

![ UI tonend segmentatie ouder org ](../assets/segmentation/example-12.png)

### Voorbeeld 13: zoek B2B-profielen die bij een statische lijst van Marketo horen en isDelette=false {#find-marketo-static-list}

Vind alle mensen die tot de Statische lijst van Marketo &quot;Verherende gebruikers&quot;behoren waar isDelette=false.

![ UI tonend segmentatie ouder org ](../assets/segmentation/example-13.png)

## Volgende stappen {#next-steps}

Na het lezen van dit overzicht hebt u nu inzicht in de segmentatiemogelijkheden die beschikbaar zijn met Real-Time CDP, B2B Edition. Voor meer informatie over de Dienst van de Segmentatie, te lezen gelieve de [ documentatie van de Segmentatie ](../../segmentation/home.md).
