---
keywords: Experience Platform;profiel;real-time klantprofiel;problemen;API;rapportage;gegevensset overlapt rapport;profielgegevens
title: Het rapport Gegevensset-overlap genereren
type: Tutorial
description: In deze zelfstudie worden de stappen beschreven die nodig zijn om het overlappingsrapport van de gegevensset te genereren met behulp van de Real-Time Customer Profile API.
exl-id: 90894ed3-b09e-435d-a9e3-18fd6dc8e907
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 0%

---

# Genereer het overlappingsrapport voor de gegevensset

Het rapport van de overlapping van datasets verstrekt zicht in de samenstelling van de [!DNL Profile] opslag van uw organisatie door de datasets bloot te stellen die het meest aan uw adresseerbare publiek (profielen) bijdragen.

Dit rapport biedt niet alleen inzichten in uw gegevens, maar kan u ook helpen bij het nemen van acties om uw licentiegebruik te optimaliseren, zoals het instellen van een limiet voor de levensduur van bepaalde gegevens.

In deze zelfstudie worden de stappen beschreven die nodig zijn om het rapport voor de overlapping van gegevenssets te genereren met de API [!DNL Real-Time Customer Profile] en de resultaten voor uw organisatie te interpreteren.

## Aan de slag

Om Adobe Experience Platform APIs te gebruiken, moet u het [&#x200B; authentificatieleerprogramma &#x200B;](https://www.adobe.com/go/platform-api-authentication-en) eerst voltooien om de waarden te verzamelen die u voor de vereiste kopballen nodig hebt. Meer over Experience Platform APIs leren, gelieve te verwijzen naar [&#x200B; begonnen wordt met de documentatie van Experience Platform APIs &#x200B;](../../landing/api-guide.md).

De vereiste kopballen voor alle API vraag in dit leerprogramma zijn:

* `Authorization: Bearer {ACCESS_TOKEN}`: Voor de `Authorization` -header is een toegangstoken vereist, voorafgegaan door het woord `Bearer` . Elke 24 uur moet een nieuwe toegangstoken-waarde worden gegenereerd.
* `x-api-key: {API_KEY}`: De `API Key` wordt ook wel een `Client ID` -waarde genoemd en is een waarde die slechts eenmaal hoeft te worden gegenereerd.
* `x-gw-ims-org-id: {ORG_ID}`: De organisatie-id hoeft slechts eenmaal te worden gegenereerd.

Na de voltooiing van de authentificatiezelfstudie en het verzamelen van de waarden voor de vereiste kopballen, bent u bereid beginnen het maken van vraag aan Real-Time Klant API.

## Gegevenssetoverlapping genereren met gebruik van de opdrachtregel

Als u vertrouwd bent met het gebruiken van de bevellijn, kunt u het volgende cURL- verzoek gebruiken om het rapport van de datasetoverlapping te produceren door een GET verzoek aan `/previewsamplestatus/report/dataset/overlap` uit te voeren.

**Verzoek**

In het volgende verzoek wordt de parameter `date` gebruikt om het meest recente rapport voor de opgegeven datum te retourneren.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-04-19 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

| Parameter | Beschrijving |
|---|---|
| `date` | Geef de datum op van het rapport dat moet worden geretourneerd. Als er meerdere rapporten op de datum werden uitgevoerd, wordt het meest recente rapport voor die datum geretourneerd. Wanneer een rapport niet bestaat voor de opgegeven datum, wordt een HTTP status 404 (Not Found)-fout geretourneerd. Als er geen datum is opgegeven, wordt het meest recente rapport geretourneerd. Indeling: JJJ-MM-DD. Voorbeeld: `date=2024-12-31` |

**Reactie**

Een succesvol verzoek keert HTTP status 200 (OK) en de dataset overlappen rapport terug. Het rapport bevat een `data` -object, dat door komma&#39;s gescheiden lijsten met gegevenssets en hun respectievelijke aantal profielen bevat. Voor details op hoe te om het rapport te lezen, zie de sectie over [&#x200B; het interpreteren van de dataset overlappen rapportgegevens &#x200B;](#interpret-the-report) later in dit leerprogramma.

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

Postman is een samenwerkingsplatform voor API-ontwikkeling en is handig voor het visualiseren van API-aanroepen. Het kan gratis van de [&#x200B; website van Postman &#x200B;](https://www.postman.com) worden gedownload en verstrekt gemakkelijk om UI voor het uitvoeren van API vraag te gebruiken. In de volgende schermafbeeldingen wordt de Postman-interface gebruikt.

**Verzoek**

Voer de volgende stappen uit om het rapport voor gegevenssetoverlapping met Postman aan te vragen:

* Selecteer GET als aanvraagtype in het vervolgkeuzemenu.
* Voer de vereiste kopteksten in de kolom `KEY` in:
   * `Authorization`
   * `x-api-key`
   * `x-gw-ims-org-id`
* Voer in de kolom `VALUE` de waarden in die u tijdens de verificatie hebt gegenereerd en vervang de accolades ( `{{ }}` ) en eventuele inhoud binnen de accolades.
* Voer het aanvraagpad in met of zonder de optionele parameter `date` :
  `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap`\
  of
  `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=YYYY-MM-DD`

| Parameter | Beschrijving |
|---|---|
| `date` | Geef de datum op van het rapport dat moet worden geretourneerd. Als er meerdere rapporten op de datum werden uitgevoerd, wordt het meest recente rapport voor die datum geretourneerd. Wanneer een rapport niet bestaat voor de opgegeven datum, wordt een HTTP status 404 (Not Found)-fout geretourneerd. Als er geen datum is opgegeven, wordt het meest recente rapport geretourneerd. <br/> Formaat: JJJ-MM-DD. Voorbeeld: `date=2024-12-31` |

Nadat het verzoektype, de kopballen, de waarden, en de weg volledig zijn, verzenden de uitgezochte **&#x200B;**&#x200B;om het API verzoek te verzenden en het rapport te produceren.

![](../images/dataset-overlap-report/postman-request.png)

**Reactie**

Een succesvol verzoek keert HTTP status 200 (OK) en de dataset overlappen rapport terug. Het rapport bevat een `data` -object, dat door komma&#39;s gescheiden lijsten met gegevenssets en hun respectievelijke aantal profielen bevat. Voor details op hoe te om het rapport te lezen, zie de sectie over [&#x200B; het interpreteren van de dataset overlappen rapportgegevens &#x200B;](#interpret-the-report).

![](../images/dataset-overlap-report/postman-response.png)

## Interpreteer de gegevens van het datasetoverlapping rapport {#interpret-the-report}

Het gegenereerde rapport voor de overlapping van gegevenssets bevat een tijdstempel met de datum en tijd van het rapport en een gegevensobject met unieke combinaties van id&#39;s voor gegevenssets als door komma&#39;s gescheiden lijsten. De volgende secties verstrekken extra informatie betreffende de componenten van het rapport.

### Tijdstempel rapporteren

De `reportTimestamp` komt overeen met de datum die is opgegeven in de API-aanvraag of, als er geen datum is opgegeven, met de tijdstempel van het meest recente rapport.

### Lijst met gegevensset-id&#39;s

Het `data` -object bevat unieke combinaties van id&#39;s van gegevenssets als door komma&#39;s gescheiden lijsten met het respectievelijke aantal profielen voor die combinatie van gegevenssets.

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

* Er zijn 123 profielen die bestaan uit gegevens die afkomstig zijn uit de volgende datasets: `5d92921872831c163452edc8`, `5da7292579975918a851db57`, `5eb2cdc6fa3f9a18a7592a98` .
* Er zijn 454.412 profielen die bestaan uit gegevens die afkomstig zijn uit deze twee gegevenssets: `5d92921872831c163452edc8` en `5eb2cdc6fa3f9a18a7592a98` .
* Er zijn 107 profielen die slechts van gegevens van dataset `5eeda0032af7bb19162172a7` worden samengesteld.
* Er zijn in totaal 454.642 profielen in de organisatie.

## Volgende stappen

Na het voltooien van deze zelfstudie kunt u nu het rapport voor de overlapping van gegevenssets genereren met behulp van de Real-Time Customer Profile API. Meer over het werken met de gegevens van het Profiel in zowel API als Experience Platform UI leren, gelieve te beginnen door de [&#x200B; het overzichtsdocumentatie van het Profiel &#x200B;](../home.md) te lezen.
