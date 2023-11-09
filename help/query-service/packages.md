---
title: Query Service-pakketten
description: Het volgende document schetst de pakketten mogelijkheden en producten beschikbaar voor de Dienst van de Vraag en benadrukt de verschillen tussen ad hoc en partijvragen.
exl-id: ba472d9e-afe6-423d-9abd-13ecea43f04f
source-git-commit: 4fb755d8936a6c2019421a064e29ab403092cf77
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 1%

---

# Query Service-pakketten

Dit document schetst de verschillende soorten verpakking en de mogelijkheden van de vraaguitvoering beschikbaar in de Dienst van de Vraag.

Adobe Experience Platform Query Service kan worden onderverdeeld in twee mogelijkheden op basis van de querypatronen die kunnen worden uitgevoerd:

- **Ad-hocquery&#39;s** zijn SQL vragen die worden gebruikt om ingebedde datasets voor controle, bevestiging, experimenteren, etc. te onderzoeken. Deze vragen schrijven geen gegevens terug naar het de gegevensmeer van het Platform.
- **Batchquery&#39;s** zijn SQL vragen die worden gebruikt om de post-ingestitieverwerking van ingebedde datasets uit te voeren. Deze vragen schonen, vormen, manipuleren, en verrijken gegevens, waarvan de resultaten terug naar het de gegevensmeer van het Platform worden geschreven. Deze vragen kunnen als partijbanen worden gepland, worden beheerd en worden gecontroleerd.

De mogelijkheden van de Dienst van de vraag worden verpakt met de volgende producten en toe:voegen-ons:

- **Platformgebaseerde toepassingen** (Adobe Real-time Customer Data Platform, Adobe Customer Journey Analytics en Adobe Journey Optimizer): toegang tot Query Service voor het uitvoeren van ad-hocquery&#39;s wordt vanaf het begin geboden bij elke variatie en elk niveau van platformgebaseerde toepassingen.
- **[!DNL Data Distiller]** (add-on-pakket dat u kunt kopen met Adobe Real-Time CDP, Customer Journey Analytics en Adobe Journey Optimizer): toegang tot Query Service voor het uitvoeren van batchquery&#39;s wordt geleverd bij [!DNL Data Distiller].

## Terminologie {#terminology}

De volgende sectie verstrekt definities voor zeer belangrijke termijnen met betrekking tot de pakketten van de Dienst van de Vraag:

- **Opslag gegevensopslag**: Het datumpeer dient hoofdzakelijk de volgende doeleinden:
   - fungeert als testgebied voor gegevens aan boord in Experience Platform;
   - fungeert als de gegevensopslag op lange termijn voor alle gegevens van het Experience Platform;
   - Hiermee worden gebruiksgevallen ingeschakeld, zoals gegevensanalyse en gegevenswetenschap.
- **Gegevens exporteren**: De [gegevensset](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html) Welke typen u kunt exporteren, is afhankelijk van uw toepassing, productlaag en eventuele aangeschafte invoegtoepassingen. De afgeleide datasets kunnen door de Gegevens Distiller van de Dienst van de Vraag worden gecreeerd toe:voegen-on, en kunnen worden [geëxporteerd uit Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activation-overview.html) tot een groot aantal bestemmingen, waaronder [cloudopslagbestemmingen](/help/destinations/ui/export-datasets.md).
- **Versnelde query&#39;s**: Versnelde query&#39;s retourneren resultaten op basis van geaggregeerde gegevens om de wachttijd voor de resultaten te verminderen en een meer interactieve uitwisseling van informatie te bieden. Stateless query&#39;s die aan de accelerated store zijn gemaakt, zijn alleen beschikbaar als onderdeel van de Data Distiller-add-on.
- **Rekenuren**: De rekenuren zijn metrisch gebruikt om het aftasten en het schrijven van gegevens met partijvragen te volgen gebruikend de Dienst API van de Vraag. Het wordt berekend in uren per jaar en wordt gemeten over alle zandbakken. Het aantal Compute uren die aan uw organisatie wordt verstrekt wordt bepaald in het overeenkomst scoping proces.

## Rechten {#entitlements}

De volgende lijst schetst de belangrijkste die de dienstrechten van de Vraag op hoe worden gebaseerd zij verpakt:

| Query Service Entitlement | Verpakt met op platform-gebaseerde toepassingen | Verpakt met [!DNL Data Distiller] |
|---|---|---|
| Ondersteund querypatroon | Alleen ad-hocquery&#39;s | Batchquery |
| Ondersteuning voor hoofdletters en kleine letters gebruiken | <ul><li>&#x200B;</li><li>&#x200B; voor gegevensdetectie</li><li>Gegevensvalidatie</li><li>Experimentatie</li></ul> | <ul><li>Reiniging</li><li>Vorm</li><li>Bewerken</li><li>Verrijken</li></ul> |
| Ondersteunde semantiek | <ul><li>Vragen SELECTEREN</li></ul> | <ul><li>CTAS- en ITAS-query&#39;s</li></ul> |
| Maximale uitvoeringstijd | 10 minuten | 24 uur |
| Licentiemetrisch | **Query-gebruiker gelijktijdig**: <ul><li>1 gelijktijdige gebruiker (Real-Time CDP, Adobe Journey Optimizer) &#x200B;</li><li>5 gelijktijdige gebruikers (Customer Journey Analytics) &#x200B;</li></ul> **Query gelijktijdig**: <ul><li>1 gelijktijdige uitgevoerde vraag (alle toepassingen) &#x200B;</li></ul> **Extra add-on voor gebruikers van ad-hocquery&#39;s** kan worden aangeschaft om de geautoriseerde ad-hocqueryrechten van klanten te verhogen. <ul><li>+5 extra gebruikers per verpakking</li><li>+1 extra gelijktijdige lopende vraag per pak</li></ul> | **Rekenuren**: <ul><li>Variabele (bereik gebaseerd op de rechten van de klant)</li></ul> **Rekenuren** is een maatregel van de hoeveelheid tijd die door de motor van de Dienst van de Vraag wordt genomen om, gegevens terug in het gegevensmeer te lezen te verwerken en te schrijven wanneer een partijvraag wordt uitgevoerd. |
| Versneld vraag en rapporteringsgebruik | Nee | Ja - Met gelijktijdige versnelde query&#39;s kunt u gegevens lezen uit de versnelde opslag en weergave in uw dashboards. Er wordt ook een speciale machtiging voor het opslaan van rapportagemodellen en gegevenssets in de versnelde opslag verstrekt. |
| Opslagcapaciteit gegevensopslag | Ja - Uw totale opslagrechten zijn afhankelijk van uw platformgebaseerde licenties voor toepassingen. Bijvoorbeeld Real-Time CDP, AJO, CJA enzovoort. | Ja - Er is een extra opslagmachtiging opgegeven om uw onbewerkte en afgeleide gegevenssets voor Data Distiller te behouden voor gebruik van gegevensgevallen na een vervaldatum van zeven dagen voor gegevens.<br>De opslagcapaciteit van het gegevensmeergeheugen wordt gemeten in terabytes (TB) en hangt af van de hoeveelheid Rekenuren die u hebt gekocht. |
| Exportrecht voor gegevens | Ja - Uw totale exportmachtiging is afhankelijk van uw platformgebaseerde toepassingslicenties. Bijvoorbeeld Real-Time CDP, AJO, CJA enzovoort. | Ja - Er worden aanvullende uitvoerrechten verleend om de uitvoer van afgeleide gegevenssets die met Data Distiller zijn gemaakt, mogelijk te maken.<br>Uw jaarlijkse toelage voor het exporteren van gegevens wordt gemeten in terabytes (TB) en hangt af van de hoeveelheid Rekenuren die u hebt gekocht. |
| Interface voor query-uitvoering | <ul><li>Gebruikersinterface Query Service</li><li>Gebruikersinterface van externe clients</li><li>[!DNL PostgresSQL] clientinterface</li></ul> | <ul><li>Gebruikersinterface Query Service </li><li>Gebruikersinterface van externe clients</li><li>[!DNL PostgresSQL] clientinterface</li><li>REST-API’s </li></ul> |
| Zoekresultaten geretourneerd via | Gebruikersinterface client | Afgeleide dataset die in het gegevensmeer wordt opgeslagen |
| Resulterende limiet | <ul><li>Gebruikersinterface van Query-service - 100 rijen</li><li>Externe klanten - 50.000</li><li>[!DNL PostgresSQL] client - 50.000</li></ul> | <ul><li>De Dienst UI van de vraag - het aantal outputrijen kan zijn [geconfigureerd met een interface-instelling](./ui/user-guide.md#result-count) tot tussen 50-500 rijen.</li><li>Externe clients (geen bovengrens voor rijen)</li><li>[!DNL PostgresSQL] client (geen bovenlimiet voor rijen)</li><li>REST API&#39;s (geen bovengrens voor rijen)</li></ul> |
| Dataset-capaciteit lezen | Ja | Ja |
| Gegevenscapaciteit schrijven | Nee | Ja |
| Planningscapaciteit | Nee | Ja |
| Bewakingscapaciteit | Ja | Ja |
| Setup-capaciteit voor query-waarschuwingen | Nee | Ja |

{style="table-layout:auto"}

## Toegangsbeheer {#access-control}

Toegangscontrole voor Experience Platform wordt beheerd via [Adobe Admin Console](https://adminconsole.adobe.com/) waarin productprofielen gebruikers met machtigingen en sandboxen koppelen. Zie de [toegangsbeheeroverzicht](../access-control/home.md) voor meer informatie .

Voor het gebruik van Query Service [!DNL Manage Queries] De toestemming moet binnen Admin Console worden toegelaten. Met deze machtiging kunnen gebruikers ad-hoc- en batchquery&#39;s uitvoeren. Gedetailleerde instructies voor het aanvragen van toegang tot het productprofiel [!DNL Manage Queries] Deze machtiging is beschreven in het gedeelte [machtigingen voor een productprofiel beheren](../access-control/ui/permissions.md) en [gebruikers beheren voor een productprofiel](../access-control/ui/users.md) documenten.

Nadat u de [!DNL Data Distiller] toe:voegen-aan, [!DNL Write Dataset] toestemming moet worden verleend. Deze machtiging staat [!DNL Data Distiller] gebruikers om partijvragen uit te voeren.

In de volgende tabel worden de effecten van de [!DNL Manage Queries] machtiging:

| Machtiging | -functie |
|---|---|
| [!DNL Manage Queries] (zonder toestemming voor schrijven van gegevens) | Biedt toegang tot ad-hocquery&#39;s |
| [!DNL Manage Queries] (met schrijfmachtiging) | Biedt toegang tot het uitvoeren van batchquery&#39;s |

{style="table-layout:auto"}

## Sandbox-ondersteuning {#sandbox-support}

Sandboxen zijn virtuele partities binnen één instantie van Experience Platform. Elke instantie van het Platform steunt veelvoudige productie en niet productie zandbakken, elk die zijn eigen bibliotheek van de middelen van het Platform handhaven. Met niet-productiesandboxen kunt u functies testen, experimenten uitvoeren en aangepaste configuraties maken zonder dat dit invloed heeft op uw productiesandboxen. Zie voor meer informatie over sandboxen de [sandboxen, overzicht](../sandboxes/home.md). Alle rechten van de Dienst van de Vraag worden gedeeld over alle zandbakken.

## Volgende stappen

Door dit document te lezen, zou u een beter inzicht in de verschillende pakkettypes en mogelijkheden van de vraaguitvoering beschikbaar in de Dienst van de Vraag moeten hebben. Om meer over de Dienst van de Vraag, zoals bekende de gebruiksgevallen van de industrie te leren, lees [case-documentatie gebruiken](./use-cases/abandoned-browse.md). Voor meer algemene informatie gaat u naar de [Overzicht van Query Service](./home.md).
