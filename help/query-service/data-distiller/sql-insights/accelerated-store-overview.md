---
title: Versnelde winkeloverzicht
description: Leer hoe u de versnelde winkel in Adobe Experience Platform kunt gebruiken voor snelle, op SQL gebaseerde inzichten met behulp van geaggregeerde gegevens. Deze pagina beschrijft het beoogde gebruik, de beperkingen op identiteits- en BI-gegevens en de beste praktijken om ervoor te zorgen dat het beleid voor gegevensbeheer van Adobe wordt nageleefd.
source-git-commit: 5e8dccf91e8c83b4734b363539cfb911b5c2ae29
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---

# Overzicht van versnelde opslag

De versnelde opslag in Adobe Experience Platform is een voor prestaties geoptimaliseerde opslaglaag die beschikbaar is via de Data Distiller SKU. Het wordt ontworpen om pre-bijeengevoegde datasets te houden, toelatend snelle, op SQL-Gebaseerde inzichten en dashboard teruggeven.

In dit document wordt beschreven hoe u de versnelde opslag correct kunt gebruiken, wordt uitgelegd waarom geaggregeerde gegevenssets zijn vrijgesteld van de standaardprocessen voor gegevenshygiëne en wordt benadrukt dat identiteitsgegevens niet mogen worden opgeslagen. Als u wilt blijven voldoen aan de Adobe-richtlijnen, moet u zich houden aan het beleid voor gegevensbeheer en de gebruiksbeperkingen die in dit document worden beschreven.

## Belangrijkste mogelijkheden {#key-capabilities}

De versnelde opslag is speciaal ontwikkeld voor prestaties en efficiëntie. Het maakt gestroomlijnde het vragen en het melden van werkschema&#39;s door zich op geaggregeerde gegevens te concentreren mogelijk. In de onderstaande lijst worden de belangrijkste mogelijkheden van de component beschreven:

- Serveer krachtige dashboards en widgets gebruikend SQL vragen
- Vooraf geaggregeerde gegevenssets opslaan die zijn ontworpen voor terugkerende inzichten
- Aangepaste gegevensmodellen maken voor het rapporteren van gebruiksgevallen

## Beoogd gebruik {#intended-use}

De versnelde opslag wordt ontworpen **alleen** voor het opslaan van samengevoegde gegevens die gestroomlijnd dashboarding en visualisatie toelaat. De architectuur is niet bedoeld om complexe werklasten te ondersteunen, zoals de verwerking van bedrijfsinformatie of gegevensopslag.

>[!IMPORTANT]
>
>De versnelde opslag is geen vervanging voor het gegevensmeer of een opslagoplossing voor algemeen gebruik.

## Gebruiksbeperkingen {#usage-restrictions}

Om ervoor te zorgen dat het Adobe-model voor gegevensbeheer en de licentievoorwaarden worden nageleefd, gelden de volgende beperkingen:

- **slaat geen ruwe gebeurtenisgegevens op**
- **opslag geen identiteitsgegevens**
- **slaat persoonlijk identificeerbare informatie (PII) niet op** zoals e-mailadressen, gezondheidsgegevens, of klantenherkenningstekens
- **gebruikt niet de versnelde opslag om uw volledig gegevenspeer te herhalen**

Alleen geaggregeerde, niet-identificeerbare gegevens mogen worden opgeslagen in de versnelde opslag. Samengevoegde gegevenssets kunnen niet omgekeerd worden ontworpen om de oorspronkelijke brongegevens te onthullen, waardoor ze worden vrijgesteld van de gecentraliseerde gegevenshygiëneprocessen van Experience Platform.

## Bestuur en naleving {#governance-and-compliance}

Als u de versnelde opslag buiten het beoogde doel gebruikt, loopt uw organisatie het risico dat de licentieovereenkomst van Adobe en de grenzen voor gegevensbeheer worden geschonden. Als gegevensbeheerincidenten optreden als gevolg van niet-ondersteunde gebruikspatronen, neemt uw organisatie de volledige verantwoordelijkheid op zich.

Adobe is niet aansprakelijk voor gevolgen die voortvloeien uit misbruik van deze functie.

Meer over leren hoe te om gegevens in Experience Platform verantwoordelijk te beheren, zie [&#x200B; Bestuur, privacy, en veiligheid in Experience Platform &#x200B;](../../../landing/governance-privacy-security/overview.md). Deze pagina schetst de diensten en de hulpmiddelen die u helpen uw ervaringsgegevens controleren in overeenstemming met bedrijfsbeleid, wettelijke vereisten, en ontwikkelingsnormen. Voor verbindingen aan meer gedetailleerde begeleiding op gebruiksetikettering en beleidshandhaving, bezoek het [&#x200B; overzicht van het Beleid van Gegevens &#x200B;](../../../data-governance/home.md).

## Best practices {#best-practices}

Om efficiënt en volgzaam gebruik van de versnelde opslag te verzekeren, volg deze geadviseerde beste praktijken:

- Gebruik afgeleide datasets om vooraf samengevoegde lijsten tot stand te brengen die specifiek aan uw dashboardbehoeften worden aangepast
- Vermijd het gebruik van de versnelde opslagruimte als ophalings- of back-uplocatie voor onbewerkte gegevenssets
- Controleer regelmatig uw gebruik om ervoor te zorgen dat deze is afgestemd op de door Adobe aanbevolen hulplijnen

## Volgende stappen

Door dit document te lezen, hebt u geleerd wat de versnelde opslag is, zijn voorgenomen gebruik voor samengevoegde gegevens in rapporteringsscenario&#39;s, en de governanceregels die moeten worden gevolgd om volgzaam gebruik te verzekeren. Om uw begrip te verdiepen en deze richtlijnen effectief toe te passen, verken de volgende middelen:

- [&#x200B; SQL overzicht van Inzichten &#x200B;](./overview.md): Leer hoe SQL Inzichten prestaties-geoptimaliseerde rapportering gebruikend samengevoegde datasets toelaat.
- [&#x200B; verzendt versnelde vragen &#x200B;](./send-accelerated-queries.md): Begrijp hoe te vragen tegen de versnelde opslag aan machtsafdashboards en widgets in werking te stellen.
- [&#x200B; het bestuur en de hygiëne van Gegevens &#x200B;](../../data-governance/overview.md): Herzie het beleid van de gegevenshygiëne van Adobe en governancerichtlijnen om volgzaam gebruik te verzekeren.
