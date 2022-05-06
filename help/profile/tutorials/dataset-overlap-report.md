---
keywords: Experience Platform;profiel;real-time klantprofiel;problemen;API;rapportering;dataset overlapt rapport;profiel gegevens
title: Het rapport Gegevensset-overlap genereren
type: Tutorial
description: In deze zelfstudie worden de stappen beschreven die nodig zijn om het overlappingsrapport van de gegevensset te genereren met behulp van de Real-time Customer Profile API.
exl-id: 90894ed3-b09e-435d-a9e3-18fd6dc8e907
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 1%

---

# Genereer het overlappingsrapport voor de gegevensset

Het rapport van de datasetoverlapping verstrekt zicht in de samenstelling van uw organisatie [!DNL Profile] opslag door de datasets bloot te stellen die het meest aan uw adresseerbare publiek (profielen) bijdragen.

Dit rapport biedt niet alleen inzichten in uw gegevens, maar kan u ook helpen bij het nemen van acties om uw licentiegebruik te optimaliseren, zoals het instellen van een limiet voor de levensduur van bepaalde gegevens.

In deze zelfstudie worden de stappen beschreven die nodig zijn om het overlappende rapport voor de gegevensset te genereren met behulp van [!DNL Real-time Customer Profile] API en interpreteer de resultaten voor uw organisatie.

## Aan de slag

Als u Adobe Experience Platform API&#39;s wilt gebruiken, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en) om de waarden te verzamelen die u voor de vereiste kopballen nodig hebt. Raadpleeg voor meer informatie over Experience Platform-API&#39;s de [aan de slag met Platform APIs documentatie](../../landing/api-guide.md).

De vereiste kopballen voor alle API vraag in dit leerprogramma zijn:

* `Authorization: Bearer {ACCESS_TOKEN}`: De `Authorization` header vereist een toegangstoken die wordt voorafgegaan door het woord `Bearer`. Elke 24 uur moet een nieuwe toegangstoken-waarde worden gegenereerd.
* `x-api-key: {API_KEY}`: De `API Key` ook bekend als a `Client ID` en is een waarde die slechts eenmaal hoeft te worden gegenereerd.
* `x-gw-ims-org-id: {ORG_ID}`: De `IMS Org` staat ook bekend als een `Organization ID` en hoeft slechts eenmaal te worden gegenereerd.

Na de voltooiing van de authentificatiezelfstudie en het verzamelen van de waarden voor de vereiste kopballen, bent u bereid beginnen het richten vraag aan de Klant API in real time.

## Gegevenssetoverlapping genereren met gebruik van de opdrachtregel

Als u vertrouwd bent met het gebruiken van de bevellijn, kunt u het volgende cURL- verzoek gebruiken om het rapport van de datasetoverlapping te produceren door een verzoek van de GET uit te voeren om `/previewsamplestatus/report/dataset/overlap`.

**Verzoek**

In het volgende verzoek wordt het `date` parameter om het meest recente rapport voor de gespecificeerde datum terug te keren.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-04-19 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

| Parameter | Beschrijving |
|---|---|
| `date` | Geef de datum op van het rapport dat moet worden geretourneerd. Als er meerdere rapporten op de datum werden uitgevoerd, wordt het meest recente rapport voor die datum geretourneerd. Wanneer een rapport niet bestaat voor de opgegeven datum, wordt een HTTP status 404 (Not Found)-fout geretourneerd. Als er geen datum is opgegeven, wordt het meest recente rapport geretourneerd. Indeling: YYYY-MM-DD. Voorbeeld: `date=2024-12-31` |

**Antwoord**

Een succesvol verzoek keert HTTP status 200 (OK) en de dataset overlappen rapport terug. Het verslag bevat een `data` object, met door komma&#39;s gescheiden lijsten met gegevenssets en het respectievelijke aantal profielen. Voor meer informatie over het lezen van het rapport raadpleegt u de sectie over [het interpreteren van de dataset overlappen rapportgegevens](#interpret-the-report) later in deze zelfstudie.

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

### Rapport voor overlapping van gegevenssets genereren met Postman

Postman is een samenwerkingsplatform voor API-ontwikkeling en is handig voor het visualiseren van API-aanroepen. Het kan gratis worden gedownload vanaf het tabblad [Postman-website](https://www.postman.com) en biedt een gebruiksvriendelijke gebruikersinterface voor het uitvoeren van API-aanroepen. In de volgende schermafbeeldingen wordt de Postman-interface gebruikt.

**Verzoek**

Voer de volgende stappen uit om het rapport voor gegevenssetoverlapping met Postman aan te vragen:

* Selecteer GET als aanvraagtype met behulp van het vervolgkeuzemenu.
* Voer de vereiste kopteksten in het dialoogvenster `KEY` kolom:
   * `Authorization`
   * `x-api-key`
   * `x-gw-ims-org-id`
* Voer de waarden die u tijdens de verificatie hebt gegenereerd in het dialoogvenster `VALUE` kolom, accolades vervangen (`{{ }}`) en alle inhoud binnen de accolades.
* Voer het aanvraagpad in met of zonder de optionele `date` parameter:
   `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap`\
   of
   `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=YYYY-MM-DD`

| Parameter | Beschrijving |
|---|---|
| `date` | Geef de datum op van het rapport dat moet worden geretourneerd. Als er meerdere rapporten op de datum werden uitgevoerd, wordt het meest recente rapport voor die datum geretourneerd. Wanneer een rapport niet bestaat voor de opgegeven datum, wordt een HTTP status 404 (Not Found)-fout geretourneerd. Als er geen datum is opgegeven, wordt het meest recente rapport geretourneerd. <br/>Indeling: YYYY-MM-DD. Voorbeeld: `date=2024-12-31` |

Nadat het aanvraagtype, de kopteksten, de waarden, en de weg volledig zijn, uitgezocht **Verzenden** om de API-aanvraag te verzenden en het rapport te genereren.

![](../images/dataset-overlap-report/postman-request.png)

**Antwoord**

Een succesvol verzoek keert HTTP status 200 (OK) en de dataset overlappen rapport terug. Het verslag bevat een `data` object, met door komma&#39;s gescheiden lijsten met gegevenssets en het respectievelijke aantal profielen. Voor meer informatie over het lezen van het rapport raadpleegt u de sectie over [het interpreteren van de dataset overlappen rapportgegevens](#interpret-the-report).

![](../images/dataset-overlap-report/postman-response.png)

## Interpreteer de gegevens van het datasetoverlapping rapport {#interpret-the-report}

Het gegenereerde rapport voor de overlapping van gegevenssets bevat een tijdstempel met de datum en tijd van het rapport en een gegevensobject met unieke combinaties van id&#39;s voor gegevenssets als door komma&#39;s gescheiden lijsten. De volgende secties verstrekken extra informatie betreffende de componenten van het rapport.

### Tijdstempel rapporteren

De `reportTimestamp` komt overeen met de datum die is opgegeven in de API-aanvraag of, als er geen datum is opgegeven, met de tijdstempel van het meest recente rapport.

### Lijst met gegevensset-id&#39;s

De `data` Het object bevat unieke combinaties van id&#39;s van gegevenssets als door komma&#39;s gescheiden lijsten met het respectieve aantal profielen voor die combinatie van gegevenssets.

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
* Er zijn 107 profielen die slechts van gegevens van dataset worden samengesteld `5eeda0032af7bb19162172a7`.
* Er zijn in totaal 454.642 profielen in de organisatie.

## Volgende stappen

Na het voltooien van deze zelfstudie kunt u nu het rapport voor de overlapping van gegevenssets genereren met behulp van de Real-Time Customer Profile API. Als u meer wilt weten over het werken met profielgegevens in zowel de API als de interface van het Experience Platform, leest u eerst de [Profieloverzicht, documentatie](../home.md).
