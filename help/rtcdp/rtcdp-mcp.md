---
solution: Real-Time Customer Data Platform
product: real-time customer data platform
title: Werken met MCP-clients (Beta)
description: Leer hoe u Adobe Real-Time CDP met MCP-clients verbindt via de MCP-server
feature: Integrations
topic: Content Management, Artificial Intelligence
badge: label="Beta" type="Informative"
role: User, Developer
level: Beginner, Intermediate
hide: true
hidefromtoc: true
exl-id: 48dba0d2-7df9-4d76-bc87-5af49a8a40cc
source-git-commit: b340d118051e2c38e1098b601e9944a7029129dc
workflow-type: tm+mt
source-wordcount: '2379'
ht-degree: 0%

---

# Werken met MCP-clients (Beta) {#rtcdp-mcp}

U kunt de integratie van Adobe Real-Time CDP MCP gebruiken om publiek, bestemmingen, en activeringsgezondheid te vragen gebruikend duidelijk-taalherinneringen - zonder API vraag te schrijven of productschermen te navigeren. Op deze pagina wordt uitgelegd hoe de integratie werkt, wat u ermee kunt doen en hoe u aan de slag kunt.

>[!AVAILABILITY]
>
>De server van Real-Time CDP MCP wordt gedistribueerd als a **verre het vervoerserver van HTTP** die de gebruikers installeren en in gesteunde cliënten MCP en app platforms (bijvoorbeeld, Claude, ChatGPT, de Code van Claude, Codex, Cursor, of de Code van VS) vormen. De authentificatie wordt behandeld door a **op browser-gebaseerde login stroom** — wanneer uw cliënt eerst met de server verbindt, opent het uw standaardbrowser zodat kunt u binnen met uw geloofsbrieven van Adobe ondertekenen en toegang machtigen. Neem contact op met uw Adobe-vertegenwoordiger voor toegang tot dit Beta-programma.

## Beta, beveiliging en juridische kennisgevingen {#mcp-notices}

**de documentatiebericht van Beta:** Deze documentatie behandelt een eigenschap van Beta en vormt geen definitieve documentatie. De inhoud die hier wordt beschreven, heeft betrekking op een Beta-release en kan worden gewijzigd voordat de inhoud algemeen beschikbaar is. Adobe geeft geen weergaven van de volledigheid of nauwkeurigheid van deze documentatie.

Door Adobe Real-Time CDP MCP Server (Beta) (&quot;Beta&quot;) te gebruiken, bevestigt u hierbij dat Beta **&quot;zoals is&quot;zonder enige garantie van welke aard ook wordt verstrekt**. Adobe is niet verplicht de Beta te onderhouden, te corrigeren, bij te werken, te wijzigen, te wijzigen of anderszins te ondersteunen. U wordt aangeraden voorzichtig te zijn en op geen enkele wijze te vertrouwen op de juiste werking of prestaties van dergelijke Beta en/of begeleidende materialen. De Beta wordt beschouwd als vertrouwelijke informatie van Adobe. Alle &quot;Feedback&quot; (informatie over de Beta, inclusief maar niet beperkt tot problemen of defecten die u tegenkomt bij het gebruik van de Beta, suggesties, verbeteringen en aanbevelingen) die u aan Adobe verstrekt, worden hierbij aan Adobe toegewezen, inclusief alle rechten, titel en interesse in en voor dergelijke feedback.

>[!WARNING]
>
>Het ModelContextprotocol (MCP) is een nieuwe open-bronnorm en kan veiligheid of betrouwbaarheidsrisico&#39;s voorstellen. Adobe MCP server integrations en verwante documentatie worden verstrekt &quot;zoals is,&quot;zonder enige garanties van welke aard ook.
>
>Het verbinden van cliënten MCP of servers met de producten van Adobe is een klant-verkozen configuratie. De klanten zijn verantwoordelijk voor het evalueren van de veiligheid en de geschiktheid van om het even welke integratie MCP. Adobe is niet verantwoordelijk voor problemen die voortvloeien uit verkeerde configuratie, misbruik van MCP, kwetsbaarheden in derdeimplementaties, of onbedoelde acties die via MCP-Toegelaten werkschema&#39;s worden uitgevoerd.
>
>Om risico&#39;s te verminderen, moedigt Adobe het testen van integratie in een zandbakmilieu voorafgaand aan productief gebruik aan, en zorgvuldig het herzien en het bevestigen van alle MCP-Gerichte acties en reacties alvorens hen te bevestigen of te vertrouwen.

## Wat is het modelcontextprotocol? {#mcp-overview}

De marketing, gegevens, en klant-ervaring teams vertrouwen meer en meer op op praatjegebaseerde toepassingen en ontwikkelaarshulpmiddelen - zoals Anthropic Claude, OpenAI ChatGPT, Cursor, en Microsoft Copilot Studio - om hun dagelijks werk te stroomlijnen. Deze toepassingen steunen het **ModelProtocol van de Context (MCP)**, een open norm die toepassingen achterste deelhulpmiddelen aan grote taalmodellen (LLMs) op een eenvormige manier laat blootstellen.

Real-Time CDP biedt nu een MCP-server waarmee publiek-, doel- en activeringsbewerkingen direct binnen een MCP-compatibele toepassing worden uitgevoerd. Met de integratie van Real-Time CDP MCP, kunnen de verschillende individuen rond de zelfde segmentatie en activeringsgegevens samenwerken - zonder vragen tegen Adobe Experience Platform REST APIs te schrijven of veelvoudige schermen UI te navigeren. De klanten kunnen hun intent gespreksbeschrijving beschrijven en LLM laten de aangewezen hulpmiddelen aanhalen MCP.

## Belangrijkste mogelijkheden {#mcp-capabilities}

De server van Real-Time CDP MCP laat u, publiek en bestemmingen direct van uw AI medewerker inspecteren samenvatten en problemen oplossen. Alle verrichtingen zijn **read-only** — de MCP serveroppervlakten winnen APIs als duidelijk-taalantwoorden terug zodat kunt u:

* **krijgt onmiddellijk publiekszicht** — Vraag over publieksdefinities, levenscyclusstaat, en namespace in gewone taal zonder menu&#39;s te navigeren of rapporten manueel te trekken.
* **schat publieksgrootte vóór activering** - de tellingen van het lidmaatschapslidmaatschap van de voorproef en betrouwbaarheidsintervallen voor een PQL of SDD segmentvraag alvorens u aan de bouw van een publiek begaat.
* **controleer uw activeringsportefeuille** — Overzicht gevormde bestemmingen, dataflows die hen, en de bron/doelverbindingen achter elke stroom voeren — zonder JSON te ontleden of over productschermen te springen.
* **de activeringsproblemen van de Steun vroeg** — Oppervlak ontbrak of in uitvoering de bestemmingslooppas het ogenblik u vraagt, zodat kan uw team snel handelen.
* **werkt rond levende gegevens** samen - de Marketers, de gegevensingenieurs, en de belanghebbenden kunnen allen de zelfde levende gegevens van Real-Time CDP door hun AI medewerker vragen, makend het gemakkelijker te richten, te besluiten en samen te bewegen.

## Beschikbare gereedschappen {#mcp-tools}

De beschikbaarheid van gereedschappen verandert snel naarmate nieuwe gereedschappen worden ingeschakeld. Neem contact op met uw Adobe-vertegenwoordiger voor een lijst met de nieuwste beschikbare tools.

>[!NOTE]
>
>Alle hulpmiddelen zijn **read-only**. Schrijfbewerkingen (maken, bijwerken of verwijderen van soorten publiek, doelen of dataflows) worden niet ondersteund in de huidige Beta-versie.

## Gebruiksscenario&#39;s {#mcp-use-cases}

In de volgende voorbeelden ziet u hoe u communiceert met de [!DNL Adobe Real-Time CDP] MCP-server in natuurlijke taal:

| Goal | Voorbeeldprompt |
| --- | --- |
| **de catalogusontdekking van de Bestemming** | &quot;Is TikTok beschikbaar als een doel in mijn sandbox?&quot; / &quot;Welke bestemmingstypes heb ik reeds rekeningen die voor worden gevormd?&quot; |
| **inventaris van de Bestemming door type** | &quot;Maak een lijst van al mijn Amazon S3 bestemmingen.&quot; / &quot;Heb ik gegevensreeks uitvoerbestemmingen opstelling?&quot; |
| **de configuratiecontrole van de Bestemming** | &quot;Aan welk emmertje is mijn `Loyalty S3 Export` bestemming die schrijft?&quot; / &quot;toon me de doelweg en dossierformaat voor dataflow [ identiteitskaart ].&quot; |
| **gezondheid van de Rekening** | &quot;Welke van mijn bestemmingsrekeningen zijn geloofsbrieven verlopen?&quot; / &quot;Zijn er Pinterest- of Facebook-accounts in een foutstatus?&quot; |
| **gezondheid van de Activering — laatste 24 uren** | &quot;Maak een lijst van elke bestemming met een ontbroken looppas in de laatste 24 uren.&quot; / &quot;Heeft mijn gegevensset-exportbestemming in de afgelopen 24 uur gegevens verzonden?&quot; |
| **geschiedenis van de Activering door bestemming** | &quot;Heeft `Weekly Loyalty Export` de afgelopen 30 dagen iets geëxporteerd?&quot; / &quot;Toon me de volledige looppasgeschiedenis voor bestemming {NAME}.&quot; |
| **analyse van de Mislukking** | &quot;Wat is de gemeenschappelijkste mislukkingsreden over mijn op dossier-gebaseerde bestemmingen deze week?&quot; / &quot;Recente mislukte uitvoering groeperen op basis van fouttype.&quot; |
| **Ontdekking &amp; het filtreren van het publiek** | &quot;Maak een lijst van elk op CSV gebaseerd publiek in de `marketing-prod` zandbak.&quot; / &quot;Welk publiek heeft een externe publiek-id gedefinieerd?&quot; |
| **Publiek rangschikkend controle** | &quot;Toon me elk publiek met grootte 0.&quot; / &quot;Welk publiek is groter dan 1.000 profielen?&quot; |
| **controle van de vervaldatum van het publiek** | &quot;Welke bestemmingen hebben publiek waarvan einddatum reeds voorbij is gegaan?&quot; / &quot;Lijstpubliek dat in de komende 7 dagen vervalt.&quot; |
| **de activeringsvoetafdruk van het publiek** | &quot;Welke bestemmingen hebben meer dan 10 publiek geactiveerd aan hen?&quot; / &quot;Welk publiek wordt geactiveerd aan de meeste bestemmingen?&quot; |
| **dwars-filter: publiek × activering** | &quot;Toon me publiek met grootte groter dan 1.000 die op minstens 2 bestemmingen worden geactiveerd.&quot; / &quot;Groot publiek dat slechts aan één bestemming wordt geactiveerd.&quot; |
| **de lidmaatschapsvoorproef van het publiek** | &quot;Geef een voorvertoning van de lidmaatschapsgrootte voor het publiek weer `High-Value Loyalty Members`.&quot; / &quot;Maak een schatting van de grootte van deze PQL-query voordat ik deze opsla: {EXPRESSION}.&quot; |

## Vereisten {#mcp-prerequisites}

Controleer het volgende voordat u de Real-Time CDP MCP-server aansluit op uw MCP-client:

* U hebt een actieve Real-Time CDP-licentie.
* U hebt toegang tot een ondersteunde client die verbinding kan maken met een externe MCP-server of aangepaste MCP-app, zoals Claude, ChatGPT, Claude Code, Codex, Cursor of VS-code.
* U hebt uw organisatie-id en de naam van de sandbox waarop u een query wilt uitvoeren.
* U hebt de noodzakelijke toestemmingen in Adobe Experience Platform om publiek, bestemmingen, en de entiteiten van de stroomdienst te bekijken.

## De Real-Time CDP MCP-server verbinden {#mcp-connect}

>[!NOTE]
>
>Deze integratie vindt plaats in Beta. Clientmenu&#39;s, planvereisten en beheerbesturingselementen kunnen per toepassing en versie verschillen.

Voordat u begint, moet u het volgende doen:

* Het MCP servereindpunt URL: `Available to Beta customers through your Adobe representative`.
* Bevestiging dat uw Adobe-gebruiker toegang heeft tot de Experience Platform-doelorganisatie en -sandbox.

De server van Real-Time CDP MCP is a **verre server MCP van HTTP**. Voor elke client geldt hetzelfde patroon:

1. Voeg de URL van de server toe.
2. Sla de verbinding op of schakel deze in.
3. Voltooi **op browser-gebaseerde login van Adobe** de eerste keer de cliënt een hulpmiddel aanhaalt.
4. Geef `imsOrgId` en `sandboxName` elk verzoek.

### Installeren in op UI gebaseerde clients {#mcp-connect-ui}

#### Claude

Voor `claude.ai` en de Desktop van Claude, voeg de server van Real-Time CDP MCP als a **douaneschakelaar** toe gebruikend het eindpunt dat door uw vertegenwoordiger van Adobe wordt verstrekt. In individuele Claude plannen, voeg het onder **toe Aanpassen > Schakelaars**. In de plannen van het Team en van de Onderneming, kan een eigenaar het eerst onder **montages van de Organisatie > Schakelaars** moeten toevoegen, waarna elke gebruiker het in hun eigen Claude montages verbindt. Zodra gevormd, laat de schakelaar in een gesprek toe en voltooi browser Adobe login bij eerste gebruik.

#### ChatGPT

In ChatGPT, voeg de server van Real-Time CDP MCP als a **douane app/schakelaar** toe gebruikend het eindpunt dat door uw vertegenwoordiger van Adobe wordt verstrekt. Afhankelijk van uw plan ChatGPT, kan dit **wijze van de Ontwikkelaar** en werkruimte vereisen admin goedkeuring. Nadat app/de schakelaar wordt gecreeerd of toegelaten, verbind het van **Montages > Apps** of **Montages > Apps &amp; Connectors**, dan verifieer door browser van Adobe login wanneer ertoe aangezet.

#### Cursor

Voeg in Cursor de Real-Time CDP MCP-server toe als een externe MCP-server met behulp van het eindpunt dat door uw Adobe-vertegenwoordiger is opgegeven. Open **Montages > MCP**, voeg een nieuwe server toe, en kleef het eindpunt URL. Zodra toegevoegd, laat de server voor uw werkruimte toe door **te selecteren verbind** om via browser voor authentiek te verklaren.

#### Andere op UI gebaseerde cliënten

Voor cliënten zoals de Code van VS of andere Desktop en Webtoepassingen met verre steun MCP, voeg de server van Real-Time CDP MCP als a **verre server van HTTP** toe gebruikend het eindpunt dat door uw vertegenwoordiger van Adobe wordt verstrekt. Als de client optionele kopteksten of tokens voor toonder ondersteunt, laat u deze leeg, tenzij Adobe anders opgeeft. De verificatie wordt bij het eerste gebruik afgehandeld via de Adobe-aanmeldstroom op basis van de browser.

### Installeren in technische clients {#mcp-connect-technical}

#### Claude Code

Voeg de server van de terminal toe:

```bash
claude mcp add --transport http rtcdp <endpoint provided by your Adobe representative>
```

Start vervolgens Claude Code en voer de volgende stappen uit:

```text
/mcp
```

Selecteer de `rtcdp` -server en voltooi de Adobe-aanmeldstroom in uw browser. Als u de server al hebt toegevoegd in `claude.ai` , kan deze ook automatisch worden weergegeven in Claude Code wanneer beide gebruikers hetzelfde account gebruiken.

#### Codex

Voeg de server van de terminal toe:

```bash
codex mcp add rtcdp --url <endpoint provided by your Adobe representative>
```

Verifieer de server:

```bash
codex mcp login rtcdp
```

Controleer de configuratie:

```bash
codex mcp list
```

U kunt de server ook rechtstreeks toevoegen aan `~/.codex/config.toml` :

```toml
[mcp_servers.rtcdp]
url = "<endpoint provided by your Adobe representative>"
```

### Vereiste parameters voor aanvragen {#mcp-connect-params}

Elke hulpmiddelvraag vereist twee parameters die het verzoek omvatten:

* `imsOrgId` — uw organisatie-id is toegewezen aan de `x-gw-ims-org-id` -header op Experience Platform API-aanroepen.
* `sandboxName` — De naam van de Experience Platform-sandbox, toegewezen aan de `x-sandbox-name` -header.

## Bekende beperkingen (Beta) {#mcp-limitations}

De volgende beperkingen gelden voor de huidige Beta-versie van de [!DNL Adobe Real-Time CDP] MCP-server:

| Beperking | Beschrijving | Workaround |
| --- | --- | --- |
| **read-only oppervlakte** | De MCP-server stelt alleen ophalen API&#39;s beschikbaar. U kunt geen publiek, bestemmingen, of gegevensstromen tot stand brengen, bijwerken, activeren of schrappen. | Gebruik de Real-Time CDP-gebruikersinterface of de AEP REST-API&#39;s voor schrijfbewerkingen. |
| **Geen overeenkomst of leveringsmetriek** | De server MCP keert stroomafwaartse leveringsstaten, geen overeenkomst, of omzettingsmetriek van bestemmingsplatforms terug. | Gebruik de eigen rapportage van het doelplatform, Customer Journey Analytics MCP of Adobe Analytics MCP voor service- en conversiegegevens. |
| **vraag van het Segment moet extern worden ontworpen** | `Preview Audience Membership` vereist een geldige PQL- of SDD-expressie als invoer; de MCP-server stelt de query niet voor u samen. | Auteur de uitdrukking PQL/SDD in de Bouwer van het Segment of via de Dienst API van de Segmentatie, dan deeg in de herinnering MCP. |
| **Paginering via voortzettokens** | Lijstgereedschappen retourneren gepagineerde resultaten. Voor volledige opsomming van zeer grote sandboxen is een keten van `continuationToken` -aanroepen vereist. | De smalle vragen die filters (naam, staat, verbindingsspecificatie, tijdwaaier) eerder gebruiken dan het opsommen van de volledige lijst. |
| **de looppas van de Activering het filtreren is op tijd-gebaseerd slechts** | `Inspect Activation Runs` ondersteunt filtering op basis van status en voltooiingstijd (epoch ms UTC), maar niet rechtstreeks op basis van fouttype of doelplatform. | Filteren op `flowId` eerst (verkregen uit `List Configured Destinations` ) om het bereik uit te voeren naar een specifiek doel. |
| **vereiste configuratie van het Gebied** | De vraag van het hulpmiddel zal met HTTP 403 &quot;gebied van de Gebruiker ontbreken&quot;als de gateway MCP niet voor het gebied van uw gebruiker wordt gevormd. | Neem contact op met uw Adobe-vertegenwoordiger om te bevestigen dat de gateway voor uw regio is geconfigureerd voordat u het product voor het eerst gebruikt. |

## Veelgestelde vragen {#mcp-faq}

+++Welke cliënten MCP worden gesteund?

De Real-Time CDP MCP-server werkt met ondersteunde clients die verbinding kunnen maken met externe MCP-servers of aangepaste MCP-apps, zoals Claude, ChatGPT, Claude Code, Codex, Cursor en VS-code. De opstellingsstroom hangt van de cliënt af: Op UI gebaseerde cliënten voegen typisch de server van montages toe, terwijl de technische cliënten zoals de Code van Claude en de Codex het van de bevellijn of configuratiedossiers kunnen toevoegen.
+++

+++Hoe werkt verificatie?

De authentificatie wordt behandeld door op browser-gebaseerde login van a ****. Wanneer uw MCP cliënt eerst een hulpmiddel aanhaalt, opent het uw standaardbrowser aan Adobe login pagina. Nadat u de client hebt geverifieerd en geautoriseerd, wordt de sessie tot stand gebracht en worden de volgende gereedschapsaanroepen opnieuw gebruikt. Geen API sleutels of lange-levende geloofsbrieven moeten in uw cliëntconfiguratie worden opgeslagen.
+++

+++Welke voorwerpen van Real-Time CDP kan ik via MCP toegang hebben?

U kunt tot publiek, bestemmingstypes, gevormde bestemmingsrekeningen, bestemmingsdataflows, bron en doelverbindingen, en activeringsloopingstijd toegang hebben. Bewerkingen zijn alleen-lezen (ophalen API&#39;s); schrijfbewerkingen worden niet ondersteund in de huidige release.
+++

+++Heb ik toegang tot ontwikkelaars nodig om de server van Real-Time CDP MCP te gebruiken?

Nee. De server MCP wordt ontworpen voor zowel marketing als technische karakters. De verkopers kunnen met het in wisselwerking staan gebruikend natuurlijke taalherinneringen in om het even welke gesteunde cliënt MCP, terwijl de gegevensingenieurs en de ontwikkelaars het in ontwikkelaarshulpmiddelen kunnen gebruiken die MCP steunen.
+++

+++Wordt mijn gegevens verzonden naar de MCP cliëntleverancier?

Wanneer u een herinnering voorlegt, kan de cliënt MCP relevante context (met inbegrip van de gegevens van Real-Time CDP die door de server MCP zijn teruggekeerd) naar zijn model voor verwerking verzenden. Controleer het privacybeleid en het beleid voor gegevensverwerking van uw MCP cliëntleverancier alvorens met productiegegevens te verbinden.
+++

+++Welke machtigingen heb ik in Real-Time CDP nodig?

U hebt bij minimum **toestemmingen van de Mening** voor de voorwerpen nodig u wilt vragen — publiek, bestemmingen, en de entiteiten van de stroomdienst. Er zijn geen schrijfmachtigingen vereist omdat de MCP-server alleen leesbewerkingen uitvoert. Neem contact op met de [!DNL Adobe Experience Platform] -beheerder als u niet zeker bent over het huidige toegangsniveau.
+++

+++Kan ik de server MCP in zandbakmilieu&#39;s gebruiken?

Ja. Voor elke gereedschapsaanroep is een parameter `sandboxName` vereist, zodat de MCP-server altijd de configuratie van de [!DNL Adobe Experience Platform] -sandbox volgt. U kunt elke sandbox waartoe u toegang hebt, opvragen door de naam ervan op te geven in de vraag.
+++

+++Wat is het verschil tussen de Lidmaatschap van het publiek van de Voorproef en Onderzoek Bestaande Publiek?

`Search Existing Audiences` geeft een publiek weer dat al is ontworpen en opgeslagen in uw sandbox. `Preview Audience Membership` neemt een ruwe PQL of SDD segmentuitdrukking en keert een grootteschatting voor het terug — nuttig om een vraag *te rangschikken alvorens* u het als publiek opslaat.
+++

+++Kan ik een query uitvoeren op het publiek van de account en op het publiek van het profiel?

Ja. Zowel `Search Existing Audiences` als `Preview Audience Membership` ondersteunen een parameter van het entiteitstype. Het publiek van het profiel kan worden uitgedrukt in PQL of SDD; het publiek van de rekening gebruikt altijd (relationele) syntaxis SDD.
+++
