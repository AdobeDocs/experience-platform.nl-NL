---
title: Packaging van Query Service
description: Het volgende document schetst de verpakking van mogelijkheden en producten beschikbaar voor de Dienst van de Vraag en benadrukt de verschillen tussen ad hoc en partijvragen.
exl-id: ba472d9e-afe6-423d-9abd-13ecea43f04f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 0%

---

# Query Service verpakken

Dit document schetst de verschillende soorten verpakking en de mogelijkheden van de vraaguitvoering beschikbaar in de Dienst van de Vraag.

Adobe Experience Platform Query Service kan worden onderverdeeld in twee mogelijkheden op basis van de querypatronen die kunnen worden uitgevoerd:

- **Ad hoc vragen** zijn SQL vragen die worden gebruikt om ingebedde datasets voor controle, bevestiging, experimenteren, etc. te onderzoeken. Deze query&#39;s schrijven geen gegevens terug naar het Experience Platform data Lake.
- **de vragen van de Partij** zijn SQL vragen die worden gebruikt om de post-ingestitieverwerking van ingebedde datasets uit te voeren. Deze vragen schoonmaken, vormen, manipuleren, en verrijken gegevens, waarvan de resultaten terug naar het gegevensmeer van Experience Platform worden geschreven. Deze vragen kunnen als partijbanen worden gepland, worden beheerd en worden gecontroleerd.

De mogelijkheden van de Dienst van de vraag worden verpakt met de volgende producten en toe:voegen-ons:

- **op Experience Platform-Gebaseerde toepassingen** (Adobe Real-Time Customer Data Platform, Adobe Customer Journey Analytics, en Adobe Journey Optimizer): De toegang van de Dienst van de vraag om ad hoc vragen uit te voeren wordt verstrekt van het begin met elke variatie en rij van op Experience Platform-Gebaseerde toepassingen.
- **[!DNL Data Distiller]** (add-on-pakket dat u kunt kopen met Adobe Real-Time CDP, Customer Journey Analytics en Adobe Journey Optimizer): toegang tot Query Service voor het uitvoeren van batchquery&#39;s wordt geleverd bij [!DNL Data Distiller] .

## Rechten {#entitlements}

De volgende lijst schetst de belangrijkste die de dienstrechten van de Vraag op hoe worden gebaseerd zij verpakt:

| Query Service Entitlement | Verpakt met op Experience Platform gebaseerde toepassingen | Verpakt met [!DNL Data Distiller] |
|---|---|---|
| Ondersteund querypatroon | Alleen ad-hocquery&#39;s | Batchquery |
| Ondersteuning voor hoofdletters en kleine letters gebruiken | <ul><li>&#x200B;</li><li>&#x200B; voor gegevensdetectie</li><li>Gegevensvalidatie</li><li>Experimentatie</li></ul> | <ul><li>Reiniging</li><li>Vorm</li><li>Bewerken</li><li>Verrijken</li></ul> |
| Ondersteunde semantiek | <ul><li>Vragen SELECTEREN</li></ul> | <ul><li>CTAS- en ITAS-query&#39;s</li></ul> |
| Maximale uitvoeringstijd | 10 minuten | 24 uur |
| Licentiemetrisch | **Gelijktijdige van de Gebruiker van de Vraag**: <ul><li>1 gelijktijdige gebruiker (Real-Time CDP, Adobe Journey Optimizer) &#x200B;</li><li>5 gelijktijdige gebruikers (Customer Journey Analytics) &#x200B;</li></ul> **vraag gelijktijdig**: <ul><li>1 gelijktijdige uitgevoerde vraag (alle toepassingen) &#x200B;</li></ul> **een extra ad hoc pakket add-on van vraaggebruikers** kan worden gekocht om uw geoorloofde ad hoc vraagbevoegdheid te verhogen. <ul><li>+5 extra gebruikers per verpakking</li><li>+1 extra gelijktijdige lopende vraag per pak</li></ul> | **rekenuren**: <ul><li>Variabele (bereik gebaseerd op toepassingsmachtiging)</li></ul> **rekent Uren** is een maatregel van de hoeveelheid tijd die door de motor van de Dienst van de Vraag wordt genomen om, gegevens terug in het gegevensmeer te lezen te verwerken en te schrijven wanneer een partijvraag wordt uitgevoerd. <br> met Gegevens Distiller SKU, krijgt u ook een extra gebruiker en vraaggelijktijdig, die aan de uitvoering van ad hoc vragen kan worden gebruikt.  De gegevens Distiller SKU omvat:<br><ul><li>+5 extra gelijktijdige gebruikers</li><li>+1 extra gelijktijdige uitvoering van query</li></ul> |
| Versneld vraag en rapporteringsgebruik | Nee | Ja - Met gelijktijdige versnelde query&#39;s kunt u gegevens lezen uit de versnelde opslag en weergave in uw dashboards. Er wordt ook een speciale machtiging voor het opslaan van rapportagemodellen en gegevenssets in de versnelde opslag verstrekt. |
| Opslagcapaciteit gegevensopslag | Uw totale opslagrechten zijn afhankelijk van uw platformgebaseerde toepassingslicenties. Bijvoorbeeld Real-Time CDP, AJO, CJA enzovoort. | Ja - Er is een extra opslagmachtiging opgegeven om uw onbewerkte en afgeleide gegevenssets voor Data Distiller te behouden voor gebruik van gegevensgevallen na een vervaldatum van zeven dagen voor gegevens.<br> de opslagcapaciteit van uw gegevensmeeropslag wordt gemeten in terabytes (TB) en hangt van de hoeveelheid Rekenuren af die u hebt gekocht. Raadpleeg de productbeschrijving voor meer informatie. |
| Exportrecht voor gegevens | Uw totale exportmachtiging is afhankelijk van uw platformgebaseerde toepassingslicenties. Bijvoorbeeld Real-Time CDP, AJO, CJA enzovoort. | Ja - Er is een extra exportrecht om de uitvoer van afgeleide gegevenssets die zijn gemaakt met Data Distiller mogelijk te maken.<br> Uw jaarlijkse toelage van de gegevensuitvoer wordt gemeten in terabytes (TB) en hangt van de hoeveelheid Rekenuren af die u hebt gekocht. Zie de productbeschrijving voor meer informatie. |
| Interface voor query-uitvoering | <ul><li>Gebruikersinterface Query Service</li><li>Gebruikersinterface van externe clients</li><li>[!DNL PostgresSQL] clientinterface</li></ul> | <ul><li>Gebruikersinterface Query Service </li><li>Gebruikersinterface van externe clients</li><li>[!DNL PostgresSQL] clientinterface</li><li>REST API&#39;s</li></ul> |
| Zoekresultaten geretourneerd via | Gebruikersinterface client | Afgeleide dataset die in het gegevensmeer wordt opgeslagen |
| Resulterende limiet | <ul><li>De Dienst UI van de vraag - het aantal outputrijen kan [&#x200B; met een UI worden gevormd die &#x200B;](./ui/user-guide.md#result-count) aan tussen 50-500 rijen plaatsen.</li><li>Externe klanten - 50.000</li><li>[!DNL PostgresSQL] client - 50.000</li></ul> | CTAS en ITAS de vragen produceren slechts succesberichten aangezien de vraagoutput in afgeleide datasets wordt opgeslagen. |
| Dataset-capaciteit lezen | Ja | Ja |
| Gegevenscapaciteit schrijven | Nee | Ja |
| Planningscapaciteit | Nee | Ja |
| Bewakingscapaciteit | Ja | Ja |
| Setup-capaciteit voor query-waarschuwingen | Nee | Ja |

{style="table-layout:auto"}

## Toegangsbeheer {#access-control}

De controle van de toegang voor Experience Platform wordt beheerd door [&#x200B; Adobe Admin Console &#x200B;](https://adminconsole.adobe.com/) waar de productprofielen gebruikers met toestemmingen en zandbakken verbinden. Zie het [&#x200B; overzicht van de toegangscontrole &#x200B;](../access-control/home.md) voor meer informatie.

Zie [&#x200B; toestemmingen voor een productprofiel &#x200B;](../access-control/ui/permissions.md) beheren en [&#x200B; gebruikers voor een document van het productprofiel &#x200B;](../access-control/ui/users.md) voor gedetailleerde instructies bij het verzoeken van toegang tot de toestemmingen van het productprofiel

### De relevante toestemmingen van de Dienst van de Vraag {#query-service-permissions}

Als u Query Service wilt gebruiken, moet de machtiging **[!DNL Manage Queries]** zijn ingeschakeld in Admin Console. Met deze machtiging kunnen gebruikers ad-hoc- en batchquery&#39;s uitvoeren.

In de volgende tabel worden de effecten van de machtiging [!DNL Manage Queries] weergegeven:

| Machtiging | Functie |
|---|---|
| [!DNL Manage Queries] (zonder machtiging voor schrijven van gegevens) | Biedt toegang tot ad-hocquery&#39;s |
| [!DNL Manage Queries] (met schrijfmachtiging) | Biedt toegang tot het uitvoeren van batchquery&#39;s |

{style="table-layout:auto"}

### Relevante SQL Insights-machtigingen {#sql-insights-permissions}

Om de Gegevens Distiller [&#x200B; SQL Inzichten &#x200B;](./data-distiller/sql-insights/overview.md) binnen dashboards tot stand te brengen, moeten de volgende toestemmingen **&#x200B;**&#x200B;binnen Admin Console worden toegelaten.

| Machtiging | Functie |
|---|---|
| [!DNL View Custom Dashboard] | Biedt toegang tot door de gebruiker gedefinieerde dashboards |
| [!DNL Manage Custom Dashboard] | Biedt beheertoegang voor door de gebruiker gedefinieerde dashboards |

{style="table-layout:auto"}

## Sandbox-ondersteuning {#sandbox-support}

Sandboxen zijn virtuele partities binnen één instantie van Experience Platform. Elke Experience Platform-instantie ondersteunt meerdere productie- en niet-productie sandboxen, elk met een eigen bibliotheek met Experience Platform-bronnen. Met niet-productiesandboxen kunt u functies testen, experimenten uitvoeren en aangepaste configuraties maken zonder dat dit invloed heeft op uw productiesandboxen. Voor meer informatie over zandbakken, zie het [&#x200B; overzicht van zandbakken &#x200B;](../sandboxes/home.md). Alle rechten van de Dienst van de Vraag worden gedeeld over alle zandbakken.

## Volgende stappen

Door dit document te lezen, zou u een beter inzicht in de verschillende pakkettypes en mogelijkheden van de vraaguitvoering beschikbaar in de Dienst van de Vraag moeten hebben. Om meer over de Dienst van de Vraag, zoals bekende de gebruikscase van de industrie te leren, lees de [&#x200B; documentatie van het gebruiksgeval &#x200B;](./use-cases/abandoned-browse.md). Voor meer algemene informatie, bezoek het [&#x200B; overzicht van de Dienst van de Vraag &#x200B;](./home.md).

