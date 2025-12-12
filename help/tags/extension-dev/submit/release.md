---
title: Een extensie opheffen
description: Leer hoe u een tagextensie privé of openbaar kunt maken in Adobe Experience Platform.
exl-id: a5eb6902-4b0f-4717-a431-a290c50fb5a6
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---

# Een extensie opheffen

Zodra het testen en het documenteren volledig zijn, is de uitbreiding klaar voor versie. Er zijn momenteel twee soorten versies die u kunt uitvoeren:

- **Privéversie**: De voltooide uitbreiding is beschikbaar aan alle eigenschappen binnen uw bedrijf, maar is niet beschikbaar aan andere bedrijven in Adobe Experience Platform.
- **Openbare versie**: De voltooide uitbreiding is beschikbaar in de openbare markt voor alle gebruikers van Adobe Experience Platform.

>[!NOTE]
>
>Nadat u de extensie hebt losgelaten, kunt u er geen wijzigingen in aanbrengen en kunt u de release niet meer ongedaan maken.  Zodra vrijgegeven, worden de insectenmoeilijke situaties en eigenschaptoevoegingen verwezenlijkt door `POST` een nieuwe versie van uw uitbreidingspakket en na de bovengenoemde het testen en versiestappen op die nieuwe versie te voeren.

U moet uw extensie eerst vrijgeven als een persoonlijke extensie voordat deze openbaar kan worden gemaakt.

## Persoonlijke release

De gemakkelijkste manier om uw uitbreiding met privé beschikbaarheid vrij te geven is de [ versie van de markeringsuitbreiding releaser ](https://www.npmjs.com/package/@adobe/reactor-releaser) te gebruiken.

```bash
npx @adobe/reactor-releaser
```

Met `npx` kunt u een npm-pakket downloaden en uitvoeren zonder het daadwerkelijk op uw computer te installeren. Dit is de eenvoudigste manier om het losser in werking te stellen.

>[!NOTE]
> Standaard verwacht de releaseprovider Adobe I/O-referenties voor een server-naar-server Oauth-flow. De oudere `jwt-auth` gebruikersgegevens
> kan worden gebruikt door `npx @adobe/reactor-releaser@v3.1.3` tot aan afschrijving uit te voeren op 1 januari 2025. De vereiste parameters
> om de `jwt-auth` versie in werking te stellen kan [ hier ](https://github.com/adobe/reactor-releaser/tree/9ea66aa2c683fe7da0cca50ff5c9b9372f183bb5) worden gevonden.

U hoeft slechts enkele gegevens in te voeren. De `clientId` en `clientSecret` kunnen worden opgehaald uit de Adobe I/O-console. Navigeer aan de [ pagina van Integraties ](https://console.adobe.io/integrations) in de I/O console. Selecteer de juiste organisatie in het vervolgkeuzemenu, zoek de juiste integratie en selecteer **[!UICONTROL View]** .

- Wat is uw `clientId`? Kopieer en plak deze vanuit de I/O-console.
- Wat is uw `clientSecret`? Kopieer en plak deze vanuit de I/O-console.

De releaser leest de `name` - en `platform` -velden van uw extensiemanifest en vraagt de API om een overeenkomend extensiepakket in de beschikbaarheid van Development.
De releasewerker zal u dan vragen om te bevestigen dat het juiste uitbreidingspakket vond dat u aan privé beschikbaarheid zou willen vrijgeven.

Als u uw uitbreiding met privé beschikbaarheid zou willen vrijgeven die API gebruiken direct, zie de voorbeeldvraag [ privé het vrijgeven van een uitbreidingspakket ](/help/tags/api/endpoints/extension-packages.md#private-release) in API voor meer detail.

## Openbare release

Nadat u de persoonlijke release hebt voltooid, kunt u Adobe vragen deze openbaar te maken.  Hierdoor wordt uw extensie beschikbaar in de openbare catalogus. Om het even welke gebruiker van de gegevensinzameling kan uw uitbreiding aan om het even welk bezit installeren.

Gelieve te voltooien de [ openbare versie aanvraagvorm ](https://www.feedbackprogram.adobe.com/c/r/DCExtensionReleaseRequest) om met het versieproces te beginnen.
