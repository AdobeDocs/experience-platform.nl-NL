---
title: edgeDomain
description: Bepaal het basisdomein waarnaar u gegevens wilt verzenden.
exl-id: 6beb5116-cd23-42fd-934c-5cf84d1d7153
source-git-commit: 09799847c61d82ed5b7cd372d92aa436697d54f3
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 1%

---

# `edgeDomain`

Met de eigenschap `edgeDomain` kunt u het domein wijzigen waar de Web SDK gegevens verzendt. Dit bezit wordt vaak gebruikt door organisaties die [ eerste partijkoekjes ](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html) gebruiken. De gegevens worden verzonden naar het eigen domein van de organisatie, dan een verslag CNAME door:sturen die gegevens naar Adobe.

De waarde die u voor `edgeDomain` gebruikt hangt van uw participatie in het [ Adobe-Beheerde certificaatprogramma ](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/adobe-managed-cert) af:

**als uw organisatie aan het Adobe-Beheerde certificaatprogramma** deelneemt, plaats de waarde aan het eerste partijdomein dat toen vestiging het certificaat werd geselecteerd. Deze waarde is doorgaans een subdomein dat eigendom is van uw organisatie. Bijvoorbeeld `data.example.com` . CNAME-records in uw organisatie leiden die gegevens om naar Adobe.

**als het niet deelnemen aan het certificaatprogramma**, plaats de waarde aan subdomain van `data.adobedc.net`. Adobe raadt u aan de bedrijfs-id van uw organisatie te gebruiken voor consistentie. Bijvoorbeeld `example.data.adobedc.net` . Gebruik de volgende stappen om uw bedrijfs-id te bepalen:

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Druk overal in de Experience Cloud-interface op `[Cmd]` + `[I]` (iOS) of `[Ctrl]` + `[I]` (Windows).
1. Er verschijnt een **[!UICONTROL User data debugger]** . Selecteer het tabblad **[!UICONTROL Assigned orgs]**. 
1. Breid de gewenste organisatie IMS uit.
1. Zoek het veld **[!UICONTROL Tenant]** . Deze waarde is het aanbevolen subdomein van `data.adobedc.net` om te gebruiken.

Stel de tekenreeks `edgeDomain` in wanneer u de opdracht `configure` uitvoert. Als u deze eigenschap weglaat bij het configureren van de SDK, wordt standaard ingesteld op `edge.adobedc.net` . Hoewel de standaardwaarde acceptabel is, vindt Adobe het een goede praktijk om een organisatiespecifieke waarde in te stellen.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  edgeDomain: "data.example.com"
});
```

## Edge-domein dat de Web SDK-tagextensie gebruikt

Het equivalent van de markeringsuitbreiding aan dit bezit is het **[!UICONTROL Edge domain]** gebied onder [ de montages van de instantieconfiguratie van SDK ](/help/tags/extensions/client/web-sdk/configure/general.md) wanneer het vormen van de uitbreiding.
