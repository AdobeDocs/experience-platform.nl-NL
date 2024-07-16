---
title: Foutafhandeling
description: Leer hoe de fout wordt behandeld in de Reactor-API.
exl-id: 336c0ced-1067-4519-94e1-85aea700fce6
source-git-commit: f3c23665229a83d6c63c7d6026ebf463069d8ad9
workflow-type: tm+mt
source-wordcount: '1057'
ht-degree: 0%

---

# Foutafhandeling

Wanneer een probleem optreedt tijdens het aanroepen van de Reactor-API, kan een fout op een van de volgende manieren worden geretourneerd:

* **Onmiddellijke fouten**: Wanneer het uitvoeren van een verzoek dat in een directe fout resulteert, is een foutenreactie teruggekeerd door API, met de status van HTTP die op het algemene type van fout wijzen die voorkwam.
* **Vertraagde fouten**: Wanneer het uitvoeren van een API verzoek dat in een vertraagde fout (zoals een asynchrone activiteit) resulteert, kan een fout door API in `meta.status_details` van een verwante middel zijn teruggekeerd.

## Foutindeling

De reacties van de fout zijn bedoeld om met [ JSON in overeenstemming te zijn:API foutenspecificatie ](http://jsonapi.org/format/#errors), en over het algemeen aan de volgende structuur te houden:

```json
{
  "errors": [
    {
      "id": "8a5526da-ab12-4be9-b084-2efe537f388c",
      "status": "404",
      "code": "not-found",
      "title": "Record Not Found",
      "meta": {
        "request_id": "jfb0dQ2e0XVTkQ6AOfEJFfTDjguw9x3d"
      },
      "source": {
        "pointer": "/data"
      }
    }
  ]
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `id` | Een unieke id voor dit specifieke exemplaar van het probleem. |
| `status` | De HTTP-statuscode die op dit probleem van toepassing is, uitgedrukt als een tekenreekswaarde. |
| `code` | Een toepassingsspecifieke foutcode, uitgedrukt als tekenreekswaarde. |
| `title` | Een korte, mens-leesbare samenvatting van het probleem dat **** van voorkomen aan voorkomen, behalve voor localisatie niet zou moeten veranderen. |
| `detail` | Een door de mens leesbare verklaring specifiek voor dit voorkomen van het probleem. Net als `title` kan de waarde van dit veld worden gelokaliseerd. |
| `source` | Een object met verwijzingen naar de bron van de fout, eventueel inclusief een van de volgende leden:<ul><li>`pointer`: a [ JSON Aanwijzer (RFC6901) ](https://datatracker.ietf.org/doc/html/rfc6901) koord dat verwijzingen de bijbehorende entiteit in het verzoekdocument (zoals `/data` voor een primair gegevensvoorwerp, of `/data/attributes/title` voor een specifiek attribuut).</li></ul> |
| `meta` | Een object dat niet-standaard metagegevens over de fout bevat. |

{style="table-layout:auto"}

## Verwijzing fout

In de volgende tabel worden de verschillende fouten weergegeven die de API kan retourneren.

| Fouttitel | Beschrijving |
| --- | --- |
| `authentication-failure` | Uw IMS-toegangstoken is ongeldig. U kunt een nieuw toegangstoken krijgen door u opnieuw aan te melden. Of voor technische accounts, een nieuwe JWT genereren en een toegangstoken voor IMS wisselen. |
| `connection-refused` | Kan geen verbinding maken met de server. |
| `decrypt-bad-passphrase` | De gegevens konden niet met verstrekte passphrase worden gedecrypteerd. |
| `decrypt-failed` | De gegevens kunnen niet worden gedecodeerd met de opgegeven persoonlijke sleutel. Controleer of de sleutel lokaal werkt en of witruimte is weggesneden. |
| `decrypt-no-data` | De gegevens kunnen niet zonder een persoonlijke sleutel worden gedecodeerd. Geef een gecodeerde persoonlijke sleutel op. |
| `delegate-descriptor-unresolved` | De extensie bevatte niet de verwachte definitie van deze gedelegeerde descriptor. De extensie moet mogelijk worden bijgewerkt. |
| `deleted-resources` | De bronnen die u wilt toevoegen aan uw bibliotheek zijn verwijderd. |
| `environment-in-use` | Een omgeving kan slechts aan één bibliotheek tegelijk worden toegewezen. Optie 1 is een andere omgeving te kiezen. Optie 2 is deze omgeving vrij te maken door de bibliotheek naar een andere omgeving te verplaatsen of de bibliotheek te verwijderen. |
| `environment-required` | Er moet een omgeving zijn toegewezen aan uw bibliotheek voordat u een build kunt maken. |
| `extension-not-found` | De extensie die een gegevenselement of regelcomponent definieert, is niet opgenomen in de bibliotheek. Controleer of alle vereiste extensies zijn toegevoegd aan uw bibliotheek. |
| `extension-package-path-error` | Een pad dat is gedefinieerd in extension.json is onjuist geconstrueerd. |
| `extension-package-transform-definition-error` | U hebt een ongeldige transformatie voor een objecteigenschap gedefinieerd. Voor elke objecteigenschap kan één transformatie worden gedefinieerd en dit moet een bestandstransformatie of een functie-transformatie zijn. |
| `extension-package-zip-error` | Er is een fout opgetreden tijdens het uitpakken van het ExtensionPackage of het comprimeren van de bestanden voor distributie. |
| `host-in-use` | Een host kan niet worden verwijderd als een of meer omgevingen deze gebruiken. |
| `host-required` | De omgeving die aan deze bibliotheek is toegewezen, heeft geen geldige host. Controleer welke omgeving aan uw bibliotheek is toegewezen. Wijs vervolgens een geldige host toe aan die omgeving. |
| `host-type-error` | Alleen SFTP-hosts moeten verificatiegegevens hebben voordat ze kunnen worden gebruikt, zodat de voortest alleen beschikbaar is voor dat type host. |
| `illegal-custom-code-transform` | U mag de transformatie customCode niet gebruiken. Geef een functie of bestandstransformatie op. |
| `ims-not-authorized` | Er is een onbekende fout opgetreden bij het autoriseren van uw account. Probeer het later opnieuw. |
| `ims-session-error` | Er is een probleem met de aanmeldingssessie. Log uit en meld u opnieuw aan. |
| `internal-error` | Er is een interne fout opgetreden. Wacht een paar minuten en probeer het opnieuw. Neem contact op met de klantenservice als het probleem zich blijft voordoen. |
| `invalid-data_element` | Een ongeldig gegevenselement kan niet aan een bibliotheek worden toegevoegd. |
| `invalid-embed_code` | Dit is geen geldige insluitcode of u probeert deze te koppelen aan een ontwikkelings- of testomgeving. Dynamic Tag Management (DTM)-insluitcodes kunnen alleen worden gekoppeld aan productieomgevingen. |
| `invalid-extension` | Een ongeldige extensie kan niet worden toegevoegd aan een bibliotheek. |
| `invalid-extension_package_id` | U kunt slechts enkele objecteigenschappen van een extensiepakket wijzigen. U hebt geprobeerd een van de toegestane wijzigingen aan te brengen. |
| `invalid-new-owner-org-id` | De organisatie-id die u wilt toewijzen, is geen geldige organisatie-id. |
| `invalid-org` | Uw actieve organisatie heeft geen toegang tot de API. Controleer of je de juiste Org gebruikt. |
| `invalid-rule` | Een ongeldige regel kan niet worden toegevoegd aan een bibliotheek. |
| `invalid-settings-syntax` | Er is een syntaxisfout aangetroffen tijdens het parseren van de JSON-instellingen. |
| `library-file-not-found` | Een vereist bestand dat is gedefinieerd in extension.json kan niet worden gevonden in het ZIP-pakket. |
| `minification-error` | De code kan niet worden gecompileerd vanwege ongeldige code. |
| `multiple-revisions` | Slechts één revisie van elke bron kan in een bibliotheek worden opgenomen. |
| `no-available-orgs` | Deze gebruikersaccount behoort niet tot een productprofiel dat toegang heeft tot tags. Gebruik de Admin Console om deze gebruiker toe te voegen aan een productprofiel met tagrechten. |
| `not-authorized` | Deze gebruikersaccount beschikt niet over de benodigde rechten om deze handeling uit te voeren. |
| `not-found` | De record kan niet worden gevonden. Controleer de id van het object dat u wilt ophalen. |
| `not-unique` | De naam die u wilt gebruiken, is al in gebruik. Voor deze resource moet de eigenschap &#39;name&#39; uniek zijn. |
| `public-release-not-authorized` | De openbare release van extensies wordt gecoördineerd door `launch-ext-dev@adobe.com` . Zie het document op [ het vrijgeven van uitbreidingen ](../../extension-dev/submit/release.md) voor meer informatie. |
| `read-only` | Deze bron is alleen-lezen en kan niet worden gewijzigd. |
| `session-timeout` | De gebruikerssessie is verlopen. Log uit en meld u opnieuw aan. |
| `sftp-authentication-failed` | Verificatie is mislukt voor de SFTP-verbinding. |
| `sftp-connection-timeout` | Er is een time-out opgetreden voor de SFTP-verbinding. |
| `sftp-exception` | Er is een uitzondering aangetroffen bij het gebruik van SFTP om verbinding te maken met de server. |
| `sftp-status-exception` | Er is een SFTP-uitzondering aangetroffen tijdens de communicatie met de server. |
| `socket-error` | Er is een socketfout aangetroffen tijdens de communicatie met de server. |
| `ssh-disconnect` | De SSH-sessie is verbroken. |
| `timeout-error` | Time-out voor verbinding met de server. |
| `unknown-error` | Er is een onverwachte fout opgetreden. U kunt het later opnieuw proberen of de Zorg van de Klant een vraag geven en verklaren wat u toen het gebeurde deed. |
| `unsupported-custom-code-language` | Er is een aangepaste codetaal opgegeven die niet wordt ondersteund. |
| `upgraded-extension-required` | Nadat u een extensie-upgrade hebt geïnstalleerd, moet u deze in alle bibliotheken opnemen totdat de upgrade naar Productie gaat. De enige uitzondering is als de extensie nog niet is gepubliceerd. |
| `upstream-build-required` | Een geslaagde build voor de upstream-bibliotheek is vereist voordat u deze kunt maken. |

{style="table-layout:auto"}
