---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;individueel profiel;gebieden;schema's;Schema's;Schemaontwerp;veldgroep;veldgroep;iab;tcf;toestemming;
solution: Experience Platform
title: IAB TCF 2.0 de Groep van het Gebied van de Goedkeuring voor de Schema's van het Profiel
description: Leer over IAB TCF 2.0 de gebiedsgroep van het schema van de Toestemming voor de klasse van het Profiel Individual XDM.
exl-id: 52a4fee8-d7f4-4f27-8e26-0c132985eb84
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# [!UICONTROL IAB TCF 2.0 Consent] veldgroep voor profielschema&#39;s

>[!NOTE]
>
>Dit document behandelt de [!UICONTROL IAB TCF 2.0 Consent] schemagebiedgroep voor de klasse van het Profiel Individual XDM. Voor de gebiedsgroep voorgenomen voor de klasse XDM ExperienceEvent, verwijs in plaats daarvan naar het volgende [&#x200B; document &#x200B;](../event/iab.md).

[!UICONTROL IAB TCF 2.0 Consent] is een standaardgroep van het schemagebied voor de [[!DNL XDM Individual Profile]  klasse &#x200B;](../../classes/individual-profile.md) wordt gebruikt om een timestamped reeksenIAB toestemmingskoorden te vangen, om toestemming-verandering patronen in tijd te volgen die.

![](../../images/field-groups/iab-profile.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `identityPrivacyInfo` | Kaart | Een map-type object dat de individuele identiteitswaarden van een klant koppelt aan verschillende TCF toestemmingstekenreeksen. Hieronder ziet u een voorbeeld van de structuur van dit object. |

{style="table-layout:auto"}

In de volgende JSON ziet u de structuur van de `identityPrivacyInfo` -kaart.

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

Zoals in het voorbeeld wordt getoond, komt elke key op hoofdniveau van `xdm:identityPrivacyInfo` overeen met een naamruimte voor identiteit die wordt herkend door Identity Service. Elke naamruimte-eigenschap moet op zijn beurt ten minste één subeigenschap hebben waarvan de sleutel overeenkomt met de overeenkomstige identiteitswaarde van de klant voor die naamruimte. In dit voorbeeld wordt de klant aangeduid met de Experience Cloud-id (`ECID`)-waarde `13782522493631189` .

>[!NOTE]
>
>Terwijl het bovenstaande voorbeeld één enkele namespace/waardepaar gebruikt om de identiteit van de klant te vertegenwoordigen, kunt u extra sleutels voor andere namespaces toevoegen, en elke namespace kan veelvoudige identiteitswaarden hebben, elk met hun eigen reeks toestemmingsvoorkeur TCF.

Voor elke identiteitswaarde moet een eigenschap `identityIABConsent` worden opgegeven die de TCF-toestemmingswaarde voor de identiteit biedt. De waarde voor dit bezit moet met het [[!UICONTROL Consent String] gegevenstype &#x200B;](../../data-types/consent-string.md) in overeenstemming zijn.

Zie de gids op [&#x200B; IAB TCF 2.0 steun in Experience Platform &#x200B;](../../../landing/governance-privacy-security/consent/iab/overview.md) voor meer informatie over het gebruiksgeval van deze gebiedsgroep. Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep zelf:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.schema.json)
