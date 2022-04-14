---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;individueel profiel;gebieden;schema's;Schema's;Schema-ontwerp;veldgroep;veldgroep;iab;tcf;toestemming;
solution: Experience Platform
title: IAB TCF 2.0 de Groep van het Gebied van de Goedkeuring voor de Schema's van het Profiel
topic-legacy: overview
description: Dit document verstrekt een overzicht van de IAB TCF 2.0 het gebiedsgroep van het schema van de Toestemming voor de klasse van het Individuele Profiel XDM.
exl-id: 52a4fee8-d7f4-4f27-8e26-0c132985eb84
source-git-commit: 046486d5e154b45fc2c2f5408eee235dddf46a4d
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 0%

---

# [!UICONTROL IAB TCF 2.0 Consent] veldgroep voor profielschema&#39;s

>[!NOTE]
>
>In dit document worden de [!UICONTROL IAB TCF 2.0 Consent] schemaveldgroep voor de klasse van het Profiel Individual XDM. Raadpleeg het volgende voor de veldgroep die is bedoeld voor de klasse XDM ExperienceEvent: [document](../event/iab.md) in plaats daarvan.

[!UICONTROL IAB TCF 2.0 Consent] is een standaardschemagebiedgroep voor [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md) gebruikt voor het vastleggen van reeksen IAB-toestemmingstekenreeksen met tijdstempels, om toestemmings-veranderingspatronen in de loop van de tijd bij te houden.

![](../../images/field-groups/iab-profile.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `identityPrivacyInfo` | Kaart | Een map-type object dat de individuele identiteitswaarden van een klant koppelt aan verschillende TCF toestemmingstekenreeksen. Hieronder ziet u een voorbeeld van de structuur van dit object. |

{style=&quot;table-layout:auto&quot;}

Het volgende JSON demonstreert de structuur van de `identityPrivacyInfo` kaart.

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

Zoals in het voorbeeld wordt getoond, geldt voor elke key op hoofdniveau van `xdm:identityPrivacyInfo` komt overeen met een naamruimte voor identiteiten die wordt herkend door Identity Service. Elke naamruimte-eigenschap moet op zijn beurt ten minste één subeigenschap hebben waarvan de sleutel overeenkomt met de overeenkomstige identiteitswaarde van de klant voor die naamruimte. In dit voorbeeld wordt de klant aangeduid met een Experience Cloud-id (`ECID`) waarde van `13782522493631189`.

>[!NOTE]
>
>Terwijl het bovenstaande voorbeeld één enkele namespace/waardepaar gebruikt om de identiteit van de klant te vertegenwoordigen, kunt u extra sleutels voor andere namespaces toevoegen, en elke namespace kan veelvoudige identiteitswaarden hebben, elk met hun eigen reeks toestemmingsvoorkeur TCF.

Voor elke identiteitswaarde, en `identityIABConsent` moet eigenschap worden opgegeven, die de TCF-waarde voor de toestemming voor de identiteit biedt. De waarde voor deze eigenschap moet overeenkomen met de [[!UICONTROL Consent String] gegevenstype](../../data-types/consent-string.md).

Zie de handleiding op [IAB TCF 2.0-ondersteuning in Platform](../../../landing/governance-privacy-security/consent/iab/overview.md) voor meer informatie over het gebruik van deze veldgroep. Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep zelf:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.schema.json)
