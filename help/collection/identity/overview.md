---
title: Identiteit in gegevensverzameling
description: Leer hoe de Inzameling van Gegevens ECIDs, CORE IDs, eerste-partijpersistentie, en identityMap over Webimplementaties gebruikt.
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---

# Identiteit in gegevensverzameling

Adobe Data Collection gebruikt identiteitssignalen om terugkerende bezoekers te erkennen en context over ervaringen te dragen. Wanneer een bezoeker uw site bereikt, genereert de Edge Network een Experience Cloud-id (ECID) en wordt deze gebruikt in een cookie van de eerste partij. Die ECID is de primaire apparaat-id die in Adobe Experience Cloud-toepassingen wordt gebruikt en vormt de basis waarop analyses, personalisatie en publieksactivering voortbouwen. In uw implementatie hebt u via de opdracht [`getIdentity`](/help/collection/js/commands/getidentity.md) toegang tot de ECID van de bezoeker op de client. Op het gegevensstroomniveau, kunt u [&#x200B; Prep van Gegevens voor de Inzameling van Gegevens &#x200B;](/help/datastreams/data-prep.md) gebruiken om ECID in een douaneXDM gebied in kaart te brengen alvorens het stroomafwaartse diensten bereikt.

De ECID identificeert een apparaat, niet een persoon. Om activiteit aan een gekende persoon te binden, kunt u extra herkenningstekens, zoals een identiteitskaart van CRM of gehakt e-mail, naast ECID verzenden gebruikend XDM [`identityMap`](./identity-map.md). Adobe adviseert het plaatsen van een persoon-vlakke namespace als [&#x200B; primaire identiteit &#x200B;](/help/tags/extensions/client/web-sdk/data-element-types.md#identity-map) wanneer één beschikbaar is.

Buiten standaard ECID, steunt de Inzameling van Gegevens extra identiteitssignalen afhankelijk van uw implementatie:

* **Eerste partij apparaat IDs (FPIDs)**: De herkenningstekens van het apparaat die u op infrastructuur produceert en beheert u controleert. Edge Network gebruikt FPID aan [&#x200B; zaait ECID &#x200B;](./fpid.md), die u sterkere koekjespersistentie op bezeten eigenschappen geven wanneer browser beperkingen het leven van Adobe-Beheerde koekjes verkorten.
* **KERN IDs**: Een afzonderlijk, op demdex-Gebaseerd herkenningsteken dat aan de werkschema&#39;s van de dersidentiteit deelneemt wanneer de derdekoekjes beschikbaar zijn. De CORE-id verschilt van de ECID en kan worden opgehaald via [`getIdentity`](/help/collection/js/commands/getidentity.md) . Voor details op hoe de context van de eerste partij en van de derdenidentiteit samen werken, zie [&#x200B; Verenigde identiteitssteun &#x200B;](./unified-identity-support.md).

Zie [`idMigrationEnabled`](/help/collection/js/commands/configure/idmigrationenabled.md) voor het migreren van bestaande AMCV-cookies als u een upgrade uitvoert van de Bezoeker-API of het oude identiteitsgedrag van de gebruiker in overeenstemming brengt.

## Eerste partij en collectie van derden {#first-party-and-third-party-collection}

SDK van het Web plaatst altijd identiteit [&#x200B; koekjes &#x200B;](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/cookies/web-sdk) (zoals `kndctr_` koekjes) als eerstepartijkoekjes op uw domein, ongeacht welk eindpunt het verzoek van de gegevensinzameling ontvangt. Het inzamelingseindpunt (het domein dat uw implementatie gegevens naar) verzendt is een afzonderlijke keus die beïnvloedt hoe browsers en netwerkbeleid het verzoek zelf behandelen.

**van de de inzameling van de eerste partij 1&rbrace; routes gegevensverzamelingsverzoeken door een domein dat uw organisatie (bijvoorbeeld,**) controleert, gebruikend een NAAM die aan Adobe Edge Network richt. `data.example.com` Omdat het verzoek op uw domein blijft, is het minder waarschijnlijk om door ad blokkers of browser netwerkbeperkingen worden geblokkeerd. De inzameling van de eerste partij is ook een eerste vereiste voor het plaatsen van [&#x200B; eerste-partij apparaat IDs &#x200B;](./fpid.md) van uw eigen serverinfrastructuur, die de duurste beschikbare identiteitsstrategie is. Adobe adviseert gebruikend het [&#x200B; Adobe-Beheerde certificaatprogramma &#x200B;](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/adobe-managed-cert) om eerste-partijinzameling voor uw implementatie te vormen.

**de inzameling van de Derde** verzendt verzoeken rechtstreeks naar Adobe-Bezit [`edgeDomain`](/help/collection/js/commands/configure/edgedomain.md) (zoals `example.data.adobedc.net`). Hoewel identiteitscookies nog steeds zijn ingesteld als eerste partij op uw domein, gaat de aanvraag zelf naar een domein van een derde partij, dat door sommige browsers en adverteerders kan worden beperkt.

## Het juiste identiteitspatroon kiezen {#choose-your-path}

* **verbeter identiteitspersistentie op bezeten eigenschappen**: Gebruik [&#x200B; eerste-partijapparaat IDs &#x200B;](./fpid.md) wanneer browser de beperkingen kookieleven verkorten en u sterkere continuïteit voor analyses en verpersoonlijking op plaatsen hebt u controleert.
* **Handje van identiteit van een app aan mobiel Web**: Gebruik [&#x200B; mobiel-aan-Web identiteit het delen &#x200B;](./mobile-to-web.md) wanneer de bezoeker in uw mobiele app begint en in een WebView of mobiele Web-pagina verdergaat.
* **houd identiteit ononderbroken over uw domeinen**: Gebruik [&#x200B; dwars-domein het delen &#x200B;](./cross-domain-sharing.md) wanneer de bezoekers zich tussen Webeigenschappen bewegen die uw organisatie bezit en u verenigbare rapportering en verpersoonlijking wilt.
* **combineer eerste-partijpersistentie met derdenactivering**: [&#x200B; Verenigde identiteitssteun van het gebruik &#x200B;](./unified-identity-support.md) wanneer u duurzame eersteidentificatie naast gesteunde derdesactiveringsstromen nodig hebt.
* **verzend persoon-vlakke herkenningstekens**: Gebruik [`identityMap`](./identity-map.md) om CRM IDs, gehakte e-mail, en andere persoon-vlakke herkenningstekens naast ECID te verzenden zodat de stroomafwaartse diensten activiteit aan een bekende persoon kunnen hechten.
* **Begrijp hoe de toestemming identiteit** beïnvloedt: Lees [&#x200B; Toestemming en identiteit &#x200B;](./consent.md) om te leren hoe `defaultConsent` en `setConsent` controle wanneer het Web SDK ECID produceert, koekjes plaatst, en gegevens verzendt.

Voor hulp die identiteitskwesties zoals bezoekersinflatie diagnostiseren, ECID inconsistenties, of FPID problemen, zie {de identiteit van het Oplossen van problemen 0} [.](./troubleshooting.md)
