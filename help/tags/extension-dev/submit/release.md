---
title: Een extensie opheffen
description: Leer hoe u een tagextensie privé of openbaar kunt maken in Adobe Experience Platform.
exl-id: a5eb6902-4b0f-4717-a431-a290c50fb5a6
source-git-commit: 8862a911f09d47c3a2260faba045f3c79826b52c
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# Een extensie opheffen

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Zodra het testen en het documenteren volledig zijn, is de uitbreiding klaar voor versie. Er zijn momenteel twee soorten versies die u kunt uitvoeren:

- **Persoonlijke release**: De voltooide extensie is beschikbaar voor alle eigendommen in uw bedrijf, maar is niet beschikbaar voor andere bedrijven in Adobe Experience Platform.
- **Openbare release**: De voltooide extensie is beschikbaar op de openbare markt voor alle Adobe Experience Platform-gebruikers.

>[!NOTE]
>
>Nadat u de extensie hebt losgelaten, kunt u er geen wijzigingen in aanbrengen en kunt u de release niet meer ongedaan maken.  Zodra vrijgegeven, worden de insectenmoeilijke situaties en eigenschaptoevoegingen verwezenlijkt door `POST`Een nieuwe versie van het extensiepakket maken en de bovenstaande test- en releasestappen voor die nieuwe versie uitvoeren.

U moet de extensie vrijgeven als een persoonlijke extensie voordat u deze openbaar kunt maken.

## Persoonlijke release

De eenvoudigste manier om uw extensie vrij te geven met persoonlijke beschikbaarheid is om de [tagextensie-releaseprogramma](https://www.npmjs.com/package/@adobe/reactor-releaser). Meer instructies vindt u in de documentatie.

Als u uw extensie rechtstreeks wilt vrijgeven met persoonlijke beschikbaarheid via de API, raadpleegt u de voorbeeldaanroep voor [een extensiepakket privé vrijgeven](https://developer.adobelaunch.com/api/reference/1.0/extension_packages/release_private/) in de API-documenten voor meer informatie.

## Openbare release

Nadat u de privérelease hebt voltooid, kunt u Adobe vragen deze openbaar te maken.  Hierdoor wordt uw extensie beschikbaar in de openbare catalogus. Om het even welke gebruiker van de gegevensinzameling kan uw uitbreiding aan om het even welk bezit installeren.

Voltooi de [aanvraagformulier voor openbare release](https://experiencecloudpanel.adobe.com/c/r/DCExtensionReleaseRequest) om het releaseproces te starten.
