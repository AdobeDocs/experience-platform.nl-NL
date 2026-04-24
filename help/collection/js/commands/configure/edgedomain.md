---
title: edgeDomain
description: Bepaal het domein waarnaar u gegevens wilt verzenden.
exl-id: 6beb5116-cd23-42fd-934c-5cf84d1d7153
source-git-commit: 2d3c31e399989652a0472bbe2174ca8d8554ba30
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 1%

---

# `edgeDomain`

Met de eigenschap `edgeDomain` kunt u het domein wijzigen waar de Web SDK gegevens verzendt. Het gebruik van een aangepast domein kan de impact van adverteerders helpen verminderen.

>[!NOTE]
>
>Deze eigenschap wijzigt niet waar cookies worden ingesteld. SDK van het Web plaatst altijd [&#x200B; eerste-partijkoekjes &#x200B;](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html), ongeacht waar het uiteindelijk gegevens verzendt.

De waarde die u voor `edgeDomain` gebruikt hangt van uw participatie in het [&#x200B; Adobe-Beheerde certificaatprogramma &#x200B;](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/adobe-managed-cert) af:

**als uw organisatie aan het Adobe-Beheerde certificaatprogramma** deelneemt, plaats de waarde aan het eerste partijdomein dat toen vestiging het certificaat werd geselecteerd. Deze waarde is doorgaans een subdomein dat eigendom is van uw organisatie. Bijvoorbeeld `data.example.com` . CNAME-records in uw organisatie sturen die gegevens door naar Adobe.

**als uw organisatie niet aan het certificaatprogramma** deelneemt, plaats de waarde aan subdomain van `data.adobedc.net`. Adobe raadt u aan de door Adobe toegewezen IMS-bedrijfsidentiteitskaart van uw organisatie te gebruiken voor consistentie. Bijvoorbeeld `example.data.adobedc.net` . Gebruik de volgende stappen om uw IMS-bedrijfs-id te bepalen:

1. Login aan [&#x200B; experience.adobe.com &#x200B;](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Druk overal in de Experience Cloud-interface op `[Cmd]` + `[I]` (macOS) of `[Ctrl]` + `[I]` (Windows).
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

Het equivalent van de markeringsuitbreiding aan dit bezit is het **[!UICONTROL Edge domain]** gebied onder [&#x200B; de montages van de instantieconfiguratie van SDK &#x200B;](/help/tags/extensions/client/web-sdk/configure/general.md) wanneer het vormen van de uitbreiding.
