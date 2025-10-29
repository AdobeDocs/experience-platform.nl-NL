---
description: Adobe Experience Platform Destination SDK is een reeks configuratie APIs die u toestaan om bestemmingsintegratiepatronen voor Experience Platform te vormen om publiek en profielgegevens aan uw eindpunt of opslagplaats te leveren, die op gegevens en authentificatieformaten van uw keus wordt gebaseerd. De configuraties worden opgeslagen in Experience Platform en kunnen via API worden opgehaald voor extra updates.
title: Adobe Experience Platform Destination SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 0%

---

# Adobe Experience Platform Destination SDK

Adobe Experience Platform Destination SDK is een reeks configuratie-API&#39;s waarmee u bestemmingsintegratiepatronen voor Experience Platform kunt configureren om gebruikers- en profielgegevens te leveren aan uw eindpunt of opslaglocatie, op basis van de gegevens- en verificatieformaten van uw keuze. De configuraties worden opgeslagen in Experience Platform en kunnen via API worden opgehaald voor extra updates.

De documentatie van Destination SDK verstrekt instructies voor u om Adobe Experience Platform Destination SDK te gebruiken om een productievere bestemmingsintegratie met Adobe Experience Platform te vormen, te testen en vrij te geven, en uw bestemming te hebben deel van de steeds groeiende bestemmingscatalogus worden. Met Destination SDK kunt u ook uw eigen aangepaste persoonlijke bestemming maken om gegevens te exporteren die op uw behoeften zijn afgestemd.

![&#x200B; Screenshot van Experience Platform UI, die de bestemmingscatalogus toont.](assets/destinations-catalog-overview.png)

## Snel starten - essentiële informatie verkennen {#quick-start}

Controleer de documentatie in de onderstaande koppelingen om snel aan de slag te gaan met het configureren en verzenden van uw bestemming via Destination SDK.

>[!BEGINSHADEBOX]

<table style="border: 0;">
  <tbody>
    <tr>
        <td>
            <p><b>Configuratiepagina</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/functionality/configuration-options.md">Alle configuratieopties worden beschreven</a></li>
                <li> De serverconfiguratie van de bestemming - <a href="/help/destinations/destination-sdk/functionality/destination-server/server-specs.md"> server specs </a> en <a href="/help/destinations/destination-sdk/functionality/destination-server/templating-specs.md"> het templating specs </a></li>
                <li><a href="/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md">Gegevensvelden van de klant en andere onderdelen van de doelconfiguratie</a></li>
                <li><a href="https://experienceleague.adobe.com/en/docs/experience-platform/destinations/destination-sdk/functionality/destination-server/message-format">Sjablonen en macro's</a></li>
            </ul>
        </td>
        <td>
            <p><b>Handleidingen</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/overview.md#process">Integratieproces op hoog niveau</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/configure-destination-instructions.md">Een streamingbestemming configureren</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/configure-file-based-destination-instructions.md">Een op een bestand gebaseerde bestemming configureren</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/batch/configure-prospect-audience-destination.md">Vorm een bestemming om perspectiefprofielen uit te voeren</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/submit-destination.md">Doel verzenden voor publicatie</a></li>
            </ul>
        </td>
                <td>
            <p><b>API-verwijzingen</b></p>
            <ul>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Destination-servers-and-templates">API-referentie voor eindpunt doelserver</a></li>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Destination-configurations">Referentie voor eindpunt-API van bestemming</a></li>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Audience-metadata-templates">Referentie voor API van audiometagegevens</a></li>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Destination-testing">Referentie voor API testen</a></li>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Destination-publishing">Referentie voor publicatie-API van bestemming</a></li>
            </ul>
        </td>
    </tr>
  </tbody>
</table>

<table style="border: 0;">
  <tbody>
    <tr>
        <td>
            <p><b>Een streamingdoel configureren - een bedriegblad</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/guides/configure-destination-instructions.md">Vorm een het stromen bestemmingsgids van begin tot eind</a></li>
                <li><a href="/help/destinations/destination-sdk/functionality/destination-server/message-format.md"> Begrijp gegevenstransformatie door de malplaatjes van de Kiezelaar </a> en <a href="/help/destinations/destination-sdk/functionality/destination-server/supported-functions.md"> mening gesteunde het templating functies </a></li>
                <li><a href="/help/destinations/destination-sdk/functionality/destination-configuration/aggregation-policy.md">Beleid voor gegevenssamenvoeging begrijpen</a></li>
                <li><a href="https://experienceleague.adobe.com/en/docs/experience-platform/destinations/destination-sdk/functionality/destination-server/message-format">Voorbeeld van actieve configuratie</a></li>
                <li><a href="/help/destinations/destination-sdk/testing-api/streaming-destinations/streaming-destination-testing-overview.md">Streaming doel testen</a></li>
            </ul>
        </td>
        <td>
            <p><b>Een op een bestand gebaseerde bestemming configureren - voorblad</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/guides/configure-file-based-destination-instructions.md">Vorm een op dossier-gebaseerde bestemmingsgids van begin tot eind</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/batch/configure-file-formatting-options.md">Bestandsindelingen configureren voor de geëxporteerde bestanden</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/batch/configure-amazon-s3-destination-with-predefined-file-formatting.md">Live-configuratievoorbeeld voor een Amazon S3-bestemming</a></li>
                <li><a href="/help/destinations/destination-sdk/functionality/destination-configuration/batch-configuration.md"> Configuratie van de Partij </a> voor dossier de uitvoerprogramma en dossier het noemen</li>
                <li><a href="/help/destinations/destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md">Bestandsgebaseerde bestemming testen</a></li>
            </ul>
        </td>
        <td>
            <p><b>Overige essentiële informatie</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/getting-started.md#obtain-authentication-credentials">Verkrijg vereiste authentificatiegeloofsbrieven om API te gebruiken</a></li>
                <li><a href="/help/destinations/destination-sdk/integration-prerequisites.md">Integratievereisten</a></li>
                <li><a href="/help/destinations/destination-sdk/glossary.md">Woordenlijst met Destination SDK-termen</a></li>                
                <li><a href="/help/destinations/destination-sdk/functionality/rate-limiting-retry-policy.md">Tarieflimieten en beleid voor opnieuw uitproberen</a></li>
                <li><a href="/help/destinations/destination-sdk/docs-framework/self-service-template.md">Zelfbedieningssjabloon om uw doel te documenteren</a></li>
            </ul>
        </td>
    </tr>
  </tbody>
</table>


>[!ENDSHADEBOX]

## Productie- en aangepaste integratie {#productized-custom-integrations}

>[!IMPORTANT]
>
> Deze functionaliteit om privé douanebestemmingen tot stand te brengen is beschikbaar slechts aan [&#x200B; Adobe Real-Time Customer Data Platform Ultimate &#x200B;](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) klanten.

Als partner van Destination SDK, kunt u van het toevoegen van uw geproduceerde bestemming aan de [&#x200B; catalogus van Experience Platform &#x200B;](../catalog/overview.md) profiteren:

1. Standaardiseer integratieconfiguraties voor alle klanten met vooraf geconfigureerde parameters en vereenvoudig de installatie-ervaring voor klanten.
2. Introduceer een merkgebonden bestemmingskaart in de de bestemmingscatalogus van Experience Platform voor vereenvoudigde klantenopstelling en bewustzijn.
3. Wees uitgerust met een productieve bestemmingsintegratie met Adobe Experience Platform en Adobe Real-Time Customer Data Platform.

Als Experience Platform-klant kunt u ook uw eigen aangepaste privébestemming maken. Deze bestemming is het meest geschikt voor uw activeringsbehoeften.

![&#x200B; diagram dat van het Overzicht toont hoe de bestemmingsontwikkelaars met Destination SDK in wisselwerking staan en hoe de klanten van Real-Time CDP van productiviteit en privé bestemmingen profiteren.](assets/destination-sdk-visual.png)

## Ondersteunde integratietypen {#supported-integration-types}

### Integraties in realtime (streaming) {#real-time-integrations}

Via Destination SDK biedt Adobe Experience Platform ondersteuning voor realtime (ook wel streaming genoemd) integratie met doelen die een REST API-eindpunt hebben. De real-time integratie met Experience Platform ondersteunt mogelijkheden zoals:

* Berichtentransformatie en -aggregatie
* Profiel terugzetten
* Configureerbare metagegevensintegratie om de publieksinstellingen en gegevensoverdracht te initialiseren
* Configureerbare verificatie
* Een pakket test- en validatie-API&#39;s waarmee u uw doelconfiguraties kunt testen en doorlopen

### Bestandsgebaseerde integratie {#file-based-integrations}

Via Destination SDK kunt u ook integratie instellen om bestanden periodiek naar de gewenste opslaglocatie te exporteren. De op dossier-gebaseerde integratie met Experience Platform steunt mogelijkheden zoals:

* Bestand exporteren in verschillende ondersteunde indelingen (CSV, Parquet, JSON)
* Configureerbare opties voor bestandsindeling waarmee u de indeling van de geëxporteerde bestanden kunt structureren en aan uw downstreamvereisten kunt voldoen.

Lees over de technische vereisten aan de bestemmingskant in het [&#x200B; artikel van de integratieeerste vereisten &#x200B;](integration-prerequisites.md) en lees over alle gesteunde configuraties in het [&#x200B; configuratieopties &#x200B;](functionality/configuration-options.md) artikel

## Toegang tot Destination SDK krijgen {#get-access}

Destination SDK-toegang is afhankelijk van uw status als partner of Experience Platform, Real-Time CDP-klant. Zie de onderstaande tabel voor meer informatie.

| Type van partner of klant | Toegang tot Destination SDK |
|---------|----------|
| Independent Software Vendor (ISV) | Sluit me aan bij het [&#x200B; Programma van de Partner van de Technologie van Adobe &#x200B;](https://partners.adobe.com/technologyprogram/experiencecloud.html) en verzoek om een zandbak van Experience Platform te krijgen die wordt voorzien om tot Destination SDK toegang te hebben. |
| Systeemintegrator (SI) | U moet op of het Niveau van het Goud of Platina in het [&#x200B; Programma van de Partner van de Oplossing van Adobe &#x200B;](https://solutionpartners.adobe.com/home.html) zijn om een zandbak van Experience Platform te krijgen provisioned en toegang tot Destination SDK. |
| De klant van Experience Platform op het [&#x200B; pakket van Ultimate van Real-Time CDP &#x200B;](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) | Standaard hebt u toegang tot Experience Platform-sandboxen en Destination SDK, zodat u persoonlijke doelen voor uw organisatie kunt maken. |

{style="table-layout:auto"}

## Proces op hoog niveau {#process}

Het proces voor het configureren van uw bestemming in Experience Platform wordt hieronder beschreven:

1. Als u ISV of SI bent, zie [&#x200B; het krijgen van toegang &#x200B;](#get-access) informatie in de sectie hierboven. [&#x200B; het pakket van Real-Time CDP Ultimate &#x200B;](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) klanten kunnen deze stap overslaan.
2. [&#x200B; Verzoek aan voorziening een zandbak van Experience Platform &#x200B;](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) en laat de toestemming van de bestemmingscreatie toe.
3. Bouw uw integratie op. Volg de instructies in de productdocumentatie om [&#x200B; het stromen bestemmingen &#x200B;](guides/configure-destination-instructions.md) of [&#x200B; op dossier-gebaseerde bestemmingen &#x200B;](guides/configure-file-based-destination-instructions.md) te vormen.
4. Test uw integratie. Volg de instructies in de productdocumentatie om [&#x200B; het stromen bestemmingen &#x200B;](testing-api/streaming-destinations/streaming-destination-testing-overview.md) of [&#x200B; op dossier-gebaseerde bestemmingen &#x200B;](testing-api/batch-destinations/file-based-destination-testing-overview.md) te testen.
5. Als u ISV of SI creërend a [&#x200B; geproduceerde integratie &#x200B;](./overview.md#productized-custom-integrations) bent, [&#x200B; voorlegt uw integratie &#x200B;](guides/submit-destination.md) voor het overzicht van Adobe (de standaardreactietijd is vijf werkdagen).
6. Als u ISV of SI creërend een geproduceerde integratie bent, gebruik het [&#x200B; zelfbediening documentatieproces &#x200B;](docs-framework/documentation-instructions.md) om een pagina van de productdocumentatie op Experience League voor uw bestemming tot stand te brengen.
7. Voor geproduceerde integratie, zodra goedgekeurd door Adobe, zal uw integratie in de [&#x200B; catalogus van Experience Platform &#x200B;](../catalog/overview.md) verschijnen.
8. Volg hetzelfde proces als u uw integratie wilt bijwerken.

## Referentie {#reference}

Adobe raadt u aan de volgende Experience Platform-documentatie te lezen en te begrijpen:

* [&#x200B; de bestemmingen van Adobe Experience Platform overzicht &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=nl)
* [&#x200B; Basis van XDM schemacompositie &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html)
* [&#x200B; Overzicht van identiteitskaart namespace &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=nl)
