---
title: Een extensie opheffen
description: Leer hoe u een tagextensie privé of openbaar kunt maken in Adobe Experience Platform.
exl-id: a5eb6902-4b0f-4717-a431-a290c50fb5a6
source-git-commit: 60d88be5d710314cdc6900f4b63643c740b91fa6
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# Een extensie opheffen

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Gelieve te verwijzen naar het volgende [ document ](../../term-updates.md) voor een geconsolideerde verwijzing van de terminologieveranderingen.

Zodra het testen en het documenteren volledig zijn, is de uitbreiding klaar voor versie. Er zijn momenteel twee soorten versies die u kunt uitvoeren:

- **Privéversie**: De voltooide uitbreiding is beschikbaar aan alle eigenschappen binnen uw bedrijf, maar is niet beschikbaar aan andere bedrijven in Adobe Experience Platform.
- **Openbare versie**: De voltooide uitbreiding is beschikbaar in de openbare markt voor alle gebruikers van Adobe Experience Platform.

>[!NOTE]
>
>Nadat u de extensie hebt losgelaten, kunt u er geen wijzigingen in aanbrengen en kunt u de release niet meer ongedaan maken.  Zodra vrijgegeven, worden de insectenmoeilijke situaties en eigenschaptoevoegingen verwezenlijkt door `POST` een nieuwe versie van uw uitbreidingspakket en na de bovengenoemde het testen en versiestappen op die nieuwe versie te voeren.

U moet de extensie vrijgeven als een persoonlijke extensie voordat u deze openbaar kunt maken.

## Persoonlijke release

De gemakkelijkste manier om uw uitbreiding met privé beschikbaarheid vrij te geven is de [ versie van de markeringsuitbreiding releaser ](https://www.npmjs.com/package/@adobe/reactor-releaser) te gebruiken. Meer instructies vindt u in de documentatie.

Als u uw uitbreiding met privé beschikbaarheid zou willen vrijgeven die API gebruiken direct, zie de voorbeeldvraag [ privé het vrijgeven van een uitbreidingspakket ](../../api/endpoints/extension-packages.md/#private-release) in API voor meer detail.

## Openbare release

Nadat u de privérelease hebt voltooid, kunt u de Adobe vragen deze openbaar te maken.  Hierdoor wordt uw extensie beschikbaar in de openbare catalogus. Om het even welke gebruiker van de gegevensinzameling kan uw uitbreiding aan om het even welk bezit installeren.

Gelieve te voltooien de [ openbare versie aanvraagvorm ](https://www.feedbackprogram.adobe.com/c/r/DCExtensionReleaseRequest) om met het versieproces te beginnen.
