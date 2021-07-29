---
title: Een extensie opheffen
description: Leer hoe u een tagextensie privé of openbaar kunt maken in Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '321'
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
>Nadat u de extensie hebt losgelaten, kunt u er geen wijzigingen in aanbrengen en kunt u de release niet meer ongedaan maken.  Zodra vrijgegeven, worden de insectenmoeilijke situaties en eigenschaptoevoegingen verwezenlijkt door `POST`een nieuwe versie van uw uitbreidingspakket en na de bovengenoemde test en versiestappen op die nieuwe versie te volgen.

U moet de extensie vrijgeven als een persoonlijke extensie voordat u deze openbaar kunt maken.

## Persoonlijke release

De gemakkelijkste manier om uw extensie vrij te geven met persoonlijke beschikbaarheid is om [tag extension releaser](https://www.npmjs.com/package/@adobe/reactor-releaser) te gebruiken. Meer instructies vindt u in de documentatie.

Als u uw uitbreiding met privé beschikbaarheid wilt vrijgeven direct gebruikend API, zie de voorbeeldvraag voor [privé het vrijgeven van een uitbreidingspakket](https://developer.adobelaunch.com/api/reference/1.0/extension_packages/release_private/) in de API documenten voor meer detail.

## Openbare release

Nadat u de privérelease hebt voltooid, kunt u Adobe vragen deze openbaar te maken.  Hierdoor wordt uw extensie beschikbaar in de openbare catalogus. Om het even welke gebruiker van de gegevensinzameling kan uw uitbreiding aan om het even welk bezit installeren.

Vul het [aanvraagformulier voor openbare release](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=7DRB5U) in om het releaseproces te starten.
