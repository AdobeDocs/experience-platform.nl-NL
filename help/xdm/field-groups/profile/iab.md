---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;individueel profiel;gebieden;schema's;Schema's;Schema-ontwerp;veldgroep;veldgroep;iab;tcf;toestemming;
solution: Experience Platform
title: IAB TCF 2.0 de Groep van het Gebied van het Schema van de toestemming
topic-legacy: overview
description: Dit document verstrekt een overzicht van de IAB TCF 2.0 het gebiedsgroep van het schema van de Toestemming voor de klasse van het Individuele Profiel XDM.
source-git-commit: 9b75a69cc6e31ea0ad77048a6ec1541df2026f27
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# [!UICONTROL IAB TCF 2.0 Consent] schemaveldgroep

>[!NOTE]
>
>Dit document behandelt de [!UICONTROL IAB TCF 2.0 Consent] schemagebiedgroep voor de klasse van het Profiel Individual XDM. Voor de gebiedsgroep voorgenomen voor de klasse XDM ExperienceEvent, verwijs in plaats daarvan naar [document](../event/iab.md).

[!UICONTROL IAB TCF 2.0 Consent] is een standaardschemagebiedgroep voor de  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) klasse die wordt gebruikt om een timestamped reeksIAB toestemmingskoorden te vangen, om toestemming-verandering patronen in tijd te volgen.

![](../../images/field-groups/iab-profile.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `identityPrivacyInfo` | Kaart | Een map-type object dat de individuele identiteitswaarden van een klant koppelt aan verschillende TCF toestemmingstekenreeksen. Hieronder ziet u een voorbeeld van de structuur van dit object. |

{style=&quot;table-layout:auto&quot;}

De volgende JSON demonstreert de structuur van de `identityPrivacyInfo`-kaart.

```json
{
  "identityPrivacyInfo": {
    "ECID": {
      "13782522493631189": {
        "identityIABConsent": {
          "consentTimestamp": "2020-04-11T05:05:05Z",
          "consentString": {
            "consentStandard": "IAB TCF",
            "consentStandardVersion": "2.0",
            "consentStringValue": "BObdrPUOevsguAfDqFENCNAAAAAmeAAA.PVAfDObdrA.DqFENCAmeAENCDA",
            "gdprApplies": true,
            "containsPersonalData": false
          }
        }
      }
    }
  }
}
```

Zoals in het voorbeeld wordt getoond, komt elke sleutel op hoofdniveau van `xdm:identityPrivacyInfo` overeen met een naamruimte voor identiteiten die door Identity Service wordt herkend. Elke naamruimte-eigenschap moet op zijn beurt ten minste één subeigenschap hebben waarvan de sleutel overeenkomt met de overeenkomstige identiteitswaarde van de klant voor die naamruimte. In dit voorbeeld wordt de klant aangeduid met een Experience Cloud-id (`ECID`)-waarde van `13782522493631189`.

>[!NOTE]
>
>Terwijl het bovenstaande voorbeeld één enkele namespace/waardepaar gebruikt om de identiteit van de klant te vertegenwoordigen, kunt u extra sleutels voor andere namespaces toevoegen, en elke namespace kan veelvoudige identiteitswaarden hebben, elk met hun eigen reeks toestemmingsvoorkeur TCF.

Voor elke identiteitswaarde, moet een `identityIABConsent` bezit worden verstrekt, die de TCF toestemmingswaarde voor de identiteit verstrekt. De waarde voor deze eigenschap moet overeenkomen met het gegevenstype [[!UICONTROL Consent String]](../../data-types/consent-string.md).

Zie de gids op [IAB TCF 2.0 steun in Platform](../../../landing/governance-privacy-security/consent/iab/overview.md) voor meer informatie over het gebruiksgeval van deze gebiedsgroep. Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep zelf:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.schema.json)
