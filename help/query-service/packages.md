---
title: Query Service-pakketten
description: Het volgende document schetst de pakketten mogelijkheden en producten beschikbaar voor de Dienst van de Vraag en benadrukt de verschillen tussen ad hoc en partijvragen.
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '720'
ht-degree: 2%

---

# Query Service-pakketten

Dit document schetst de verschillende soorten verpakking en de mogelijkheden van de vraaguitvoering beschikbaar in de Dienst van de Vraag.

Adobe Experience Platform Query Service kan worden onderverdeeld in twee mogelijkheden op basis van de querypatronen die kunnen worden uitgevoerd:

- **Ad-hocquery&#39;s** zijn SQL vragen die worden gebruikt om ingebedde datasets voor controle, bevestiging, experimenteren, etc. te onderzoeken. Deze vragen schrijven geen gegevens terug naar het meer van de gegevens van het Platform.
- **Batchquery&#39;s** zijn SQL vragen die worden gebruikt om de post-ingestitieverwerking van ingebedde datasets uit te voeren. Deze vragen schoonmaken, vormen, manipuleren, en verrijken gegevens, waarvan de resultaten terug naar het Platform gegevensmeer worden geschreven. Deze vragen kunnen als partijbanen worden gepland, worden beheerd en worden gecontroleerd.

De mogelijkheden van de Dienst van de vraag worden verpakt met de volgende producten en toe:voegen-ons:

- **Toepassingen op basis van Platforms** (Adobe Real-time Customer Data Platform, Adobe Customer Journey Analytics en Adobe Journey Optimizer): De toegang van de Dienst van de vraag om ad hoc vragen uit te voeren wordt verleend vanaf het begin met elke variatie en rij van op Platform-gebaseerde toepassingen.
- **[!DNL Data Distiller]** (add-onpakket dat u kunt kopen met Adobe Real-Time CDP, Customer Journey Analytics en Adobe Journey Optimizer): De toegang van de Dienst van de vraag om partijvragen uit te voeren wordt verleend met [!DNL Data Distiller].

De volgende lijst schetst de belangrijkste die de dienstrechten van de Vraag op hoe worden gebaseerd zij verpakt:

| Query Service Entitlement | Verpakt met op Platform-gebaseerde toepassingen | Verpakt met [!DNL Data Distiller] |
|---|---|---|
| Ondersteund querypatroon | Alleen ad-hocquery | Batchquery |
| Ondersteuning voor hoofdletters en kleine letters gebruiken | <ul><li>&#x200B;</li><li>&#x200B; voor gegevensdetectie</li><li>Gegevensvalidatie</li><li>Experimentatie</li></ul> | <ul><li>Reiniging</li><li>Vorm</li><li>Bewerken</li><li>Verrijken</li></ul> |
| Ondersteunde semantiek | <ul><li>Vragen SELECTEREN</li></ul> | <ul><li>CTAS- en ITAS-query&#39;s</li></ul> |
| Maximale uitvoeringstijd | 10 minuten | 24 uur |
| Licentiemetrisch | **Vraag gebruiker gelijktijdig**: <ul><li>1 gelijktijdige gebruiker (Real-Time CDP, Adobe Journey Optimizer) &#x200B;</li><li>5 gelijktijdige gebruikers (Customer Journey Analytics) &#x200B;</li></ul> **Query gelijktijdig**: <ul><li>1 gelijktijdige uitgevoerde vraag (alle toepassingen) &#x200B;</li></ul> **Extra add-on voor gebruikers van ad-hocquery&#39;s** kan worden aangeschaft om de geautoriseerde ad-hocqueryrechten van klanten te verhogen. <ul><li>+5 extra gebruikers per verpakking</li><li>+1 extra gelijktijdige lopende vraag per pak</li></ul> | **Rekenuren**: <ul><li>Variabele (bereik gebaseerd op de rechten van de klant)</li></ul> **Rekenuren** is een maatregel van de hoeveelheid tijd die door de motor van de Dienst van de Vraag wordt genomen om, gegevens terug in het gegevensmeer te lezen te verwerken en te schrijven wanneer een partijvraag wordt uitgevoerd. |
| Interface voor query-uitvoering | <ul><li>Gebruikersinterface Query Service</li><li>Gebruikersinterface van externe clients</li><li>[!DNL PostgresSQL] clientinterface</li></ul> | <ul><li>Query-interface </li><li>Gebruikersinterface van externe clients</li><li>[!DNL PostgresSQL] clientinterface</li><li>REST-API’s </li></ul> |
| Zoekresultaten geretourneerd via | Gebruikersinterface client | Afgeleide dataset die in het gegevensmeer wordt opgeslagen |
| Resultaatlimiet | <ul><li>Query-gebruikersinterface - 100 rijen</li><li>Client van derden - 50.000</li><li>[!DNL PostgresSQL] client - 50.000</li></ul> | <ul><li>Query-gebruikersinterface (geen bovenlimiet voor rijen)</li><li>Externe clients (geen bovengrens voor rijen)</li><li>[!DNL PostgresSQL] client (geen bovenlimiet voor rijen)</li><li>REST API&#39;s (geen bovengrens voor rijen)</li></ul> |
| Datasetcapaciteit lezen | Ja | Ja |
| Gegevenscapaciteit schrijven | Nee | Ja |
| Planningscapaciteit | Nee | Ja |
| Bewakingscapaciteit | Ja | Ja |
| Setup-capaciteit voor query-waarschuwingen | Nee | Ja |

{style=&quot;table-layout:auto&quot;}

## Toegangsbeheer

Toegangscontrole voor Experience Platform wordt beheerd via [Adobe Admin Console](https://adminconsole.adobe.com/) waarin productprofielen gebruikers met machtigingen en sandboxen koppelen. Zie de [toegangsbeheeroverzicht](../access-control/home.md) voor meer informatie .

Om de Dienst van de Vraag te gebruiken, [!DNL Manage Queries] de toestemming moet binnen admin console worden toegelaten. Met deze machtiging kunnen gebruikers ad-hocquery&#39;s en batchquery&#39;s uitvoeren. Gedetailleerde instructies voor het aanvragen van toegang tot het productprofiel [!DNL Manage Queries] Deze machtiging is beschreven in het gedeelte [machtigingen voor een productprofiel beheren](../access-control/ui/permissions.md) en [gebruikers beheren voor een productprofiel](../access-control/ui/users.md) documenten.

Nadat u de [!DNL Data Distiller] invoegtoepassing, de [!DNL Write Dataset] toestemming moet worden verleend. Deze machtiging staat [!DNL Data Distiller] gebruikers om batchquery&#39;s uit te voeren.

In de volgende tabel worden de effecten van de [!DNL Manage Queries] machtiging:

| Machtiging | -functie |
|---|---|
| [!DNL Manage Queries] (zonder toestemming voor schrijven van gegevens) | Biedt toegang tot ad-hocquery&#39;s |
| [!DNL Manage Queries] (met machtiging voor schrijven van gegevens) | Biedt toegang tot het uitvoeren van batchquery&#39;s |

{style=&quot;table-layout:auto&quot;}

## Sandbox-ondersteuning

Sandboxen zijn virtuele partities binnen één instantie van Experience Platform. Elke instantie van het Platform steunt veelvoudige productie en niet productie zandbakken, elk handhaven zijn eigen bibliotheek van Platform middelen. Met niet-productiesandboxen kunt u functies testen, experimenten uitvoeren en aangepaste configuraties maken zonder dat dit invloed heeft op uw productiesandboxen. Zie voor meer informatie over sandboxen de [sandboxen, overzicht](../sandboxes/home.md). Alle rechten van de Dienst van de Vraag worden gedeeld over alle zandbakken

## Volgende stappen

Door dit document te lezen zou u een beter inzicht in de verschillende pakkettypes en mogelijkheden van de vraaguitvoering beschikbaar in de Dienst van de Vraag moeten hebben. Om meer over de Dienst van de Vraag, zoals bekende de dienstgevallen van het de industrietak te leren, te lezen gelieve [case-documentatie gebruiken](./use-cases/abandoned-browse.md). Ga voor meer algemene informatie naar de [Overzicht van Query Service](./home.md).
