---
keywords: Experience Platform;profiel;real-time klantprofiel;problemen;API;rapportering;dataset overlapt rapport;profiel gegevens
title: Het rapport Gegevensset-overlap genereren
type: Tutorial
description: In deze zelfstudie worden de stappen beschreven die nodig zijn om het overlappingsrapport van de gegevensset te genereren met behulp van de Real-time Customer Profile API.
source-git-commit: f30f87527f5e903c851a140e7cbaad1964a48803
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 1%

---


# Genereer het overlappingsrapport voor de gegevensset

Het rapport van de overlapping van de dataset verstrekt zicht in de samenstelling van [!DNL Profile] opslag van uw organisatie door de datasets bloot te stellen die het meest aan uw adresseerbare publiek (profielen) bijdragen.

Dit rapport biedt niet alleen inzichten in uw gegevens, maar kan u ook helpen bij het nemen van acties om uw licentiegebruik te optimaliseren, zoals het instellen van een limiet voor de levensduur van bepaalde gegevens.

In deze zelfstudie worden de stappen beschreven die nodig zijn om het overlappende rapport van de gegevensset te genereren met de API [!DNL Real-time Customer Profile] en worden de resultaten voor uw organisatie geïnterpreteerd.

## Aan de slag

Als u Adobe Experience Platform API&#39;s wilt gebruiken, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en) voltooien om de waarden te verzamelen die u nodig hebt voor de vereiste headers. Voor meer informatie over Experience Platform APIs, gelieve te verwijzen naar [begonnen met Platform APIs documentatie](../../landing/api-guide.md).

De vereiste kopballen voor alle API vraag in dit leerprogramma zijn:

* `Authorization: Bearer {ACCESS_TOKEN}`: Voor de  `Authorization` koptekst is een toegangstoken vereist, voorafgegaan door het woord  `Bearer`. Elke 24 uur moet een nieuwe toegangstoken-waarde worden gegenereerd.
* `x-api-key: {API_KEY}`: Het  `API Key` wordt ook wel een waarde genoemd  `Client ID` en deze waarde hoeft maar één keer te worden gegenereerd.
* `x-gw-ims-org-id: {IMS_ORG}`: Het  `IMS Org` is ook bekend als een  `Organization ID` en moet slechts eenmaal worden gegenereerd.

Na de voltooiing van de authentificatiezelfstudie en het verzamelen van de waarden voor de vereiste kopballen, bent u bereid beginnen het richten vraag aan de Klant API in real time.

## Gegevenssetoverlapping genereren met gebruik van de opdrachtregel

Als u vertrouwd bent met het gebruiken van de bevellijn, kunt u het volgende cURL- verzoek gebruiken om het rapport van de datasetoverlapping te produceren door een verzoek van de GET aan `/previewsamplestatus/report/dataset/overlap` uit te voeren.

**Verzoek**

In het volgende verzoek wordt de parameter `date` gebruikt om het meest recente rapport voor de opgegeven datum te retourneren.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-04-19 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

| Parameter | Beschrijving |
|---|---|
| `date` | Geef de datum op van het rapport dat moet worden geretourneerd. Als er meerdere rapporten op de datum werden uitgevoerd, wordt het meest recente rapport voor die datum geretourneerd. Wanneer een rapport niet bestaat voor de opgegeven datum, wordt een HTTP status 404 (Not Found)-fout geretourneerd. Als er geen datum is opgegeven, wordt het meest recente rapport geretourneerd. Indeling: YYYY-MM-DD. Voorbeeld: `date=2024-12-31` |

**Antwoord**

Een succesvol verzoek keert HTTP status 200 (OK) en de dataset overlappen rapport terug. Het rapport bevat een `data`-object, dat door komma&#39;s gescheiden lijsten met gegevenssets en hun respectievelijke aantal profielen bevat. Voor details op hoe te om het rapport te lezen, zie de sectie over [het interpreteren van de dataset overlappen rapportgegevens](#interpret-the-report) later in dit leerprogramma.

```json
{
    "data": {
        "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
        "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
        "5eeda0032af7bb19162172a7": 107
    },
    "reportTimestamp": "2021-04-19T19:55:31.147"
}
```

### Gegevenssetoverlap genereren met Postman

Postman is een samenwerkingsplatform voor API-ontwikkeling en is handig voor het visualiseren van API-aanroepen. Deze kan gratis worden gedownload van de [Postman-website](https://www.postman.com) en biedt een gebruiksvriendelijke gebruikersinterface voor het uitvoeren van API-aanroepen. De volgende schermafbeeldingen gebruiken de interface Postman.

**Verzoek**

Voer de volgende stappen uit om het rapport voor gegevenssetoverlapping met Postman aan te vragen:

* Selecteer GET als aanvraagtype met behulp van het vervolgkeuzemenu.
* Voer de vereiste kopteksten in de kolom `KEY` in:
   * `Authorization`
   * `x-api-key`
   * `x-gw-ims-org-id`
* Voer de waarden die u tijdens de verificatie hebt gegenereerd in de `VALUE`-kolom in, waarbij u de accolades (`{{ }}`) en alle inhoud binnen de accolades vervangt.
* Voer het aanvraagpad met of zonder de optionele parameter `date` in:
   `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap`\
   of
   `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=YYYY-MM-DD`

| Parameter | Beschrijving |
|---|---|
| `date` | Geef de datum op van het rapport dat moet worden geretourneerd. Als er meerdere rapporten op de datum werden uitgevoerd, wordt het meest recente rapport voor die datum geretourneerd. Wanneer een rapport niet bestaat voor de opgegeven datum, wordt een HTTP status 404 (Not Found)-fout geretourneerd. Als er geen datum is opgegeven, wordt het meest recente rapport geretourneerd. <br/>Indeling: YYYY-MM-DD. Voorbeeld: `date=2024-12-31` |

Nadat het verzoektype, de kopballen, de waarden, en de weg volledig zijn, uitgezocht **verzend** om het API verzoek te verzenden en het rapport te produceren.

![](../images/dataset-overlap-report/postman-request.png)

**Antwoord**

Een succesvol verzoek keert HTTP status 200 (OK) en de dataset overlappen rapport terug. Het rapport bevat een `data`-object, dat door komma&#39;s gescheiden lijsten met gegevenssets en hun respectievelijke aantal profielen bevat. Voor details op hoe te om het rapport te lezen, zie de sectie over [het interpreteren van de dataset overlappen rapportgegevens](#interpret-the-report).

![](../images/dataset-overlap-report/postman-response.png)

## De rapportgegevens van de gegevensset overlappen {#interpret-the-report} interpreteren

Het gegenereerde rapport voor de overlapping van gegevenssets bevat een tijdstempel met de datum en tijd van het rapport en een gegevensobject met unieke combinaties van id&#39;s voor gegevenssets als door komma&#39;s gescheiden lijsten. De volgende secties verstrekken extra informatie betreffende de componenten van het rapport.

### Tijdstempel rapporteren

De `reportTimestamp` komt overeen met de datum die is opgegeven in de API-aanvraag of, als er geen datum is opgegeven, met de tijdstempel van het meest recente rapport.

### Lijst met gegevensset-id&#39;s

Het `data` voorwerp omvat unieke combinaties dataset IDs als komma-gescheiden lijsten met de respectieve profieltelling voor die combinatie datasets.

>[!NOTE]
>
>De som van alle profieltellingen verbonden aan elke rij van de datasetoverlapping rapport zou het totale aantal profielen in uw organisatie moeten gelijk stellen.

Om de resultaten van het rapport te interpreteren, overweeg het volgende voorbeeld:

```json
  "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
  "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
  "5eeda0032af7bb19162172a7": 107
```

Dit rapport bevat de volgende informatie:
* Er zijn 123 profielen die van gegevens uit de volgende datasets worden samengesteld: `5d92921872831c163452edc8`, `5da7292579975918a851db57`, `5eb2cdc6fa3f9a18a7592a98`.
* Er zijn 454.412 profielen samengesteld uit gegevens die uit deze twee datasets komen: `5d92921872831c163452edc8` en `5eb2cdc6fa3f9a18a7592a98`.
* Er zijn 107 profielen die slechts van gegevens uit dataset `5eeda0032af7bb19162172a7` worden samengesteld.
* Er zijn in totaal 454.642 profielen in de organisatie.

## Volgende stappen

Na het voltooien van deze zelfstudie kunt u nu het rapport voor de overlapping van gegevenssets genereren met behulp van de Real-Time Customer Profile API. Als u meer wilt weten over het werken met profielgegevens in zowel de API als de interface van het Experience Platform, leest u eerst de [Documentatieoverzicht profiel](../home.md).