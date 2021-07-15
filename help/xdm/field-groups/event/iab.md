---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;ExperienceEvent;fields;schema's;Schema's;Schema-ontwerp;field-groep;field-groep;iab;tcf;permission;
solution: Experience Platform
title: IAB TCF 2.0 de Groep van het Gebied van het Schema van de toestemming
topic-legacy: overview
description: Dit document biedt een overzicht van de IAB TCF 2.0-groep met het schema voor instemming voor de XDM ExperienceEvent-klasse.
source-git-commit: 7a0ac3970713e95438c6f0fdbd6175545ea7fdd0
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 0%

---


# [!UICONTROL IAB TCF 2.0 Consent] schemaveldgroep

>[!IMPORTANT]
>
>Dit document behandelt de [!UICONTROL IAB TCF 2.0 Consent] schemagebiedgroep voor de klasse XDM ExperienceEvent. Deze veldgroep mag alleen worden gebruikt als u wijzigingen in de toestemming wilt bijhouden tijdens een tijdsverloop.
>
>Merk op dat toestemmingswaarden die in gebeurtenisgegevens worden geregistreerd niet in automatische handhavingswerkschema&#39;s worden nageleefd. Voor automatische handhaving moet de toestemmingswaarden in de klasse van het Profiel van de Individuele XDM worden opgenomen en voor het Profiel van de Klant in real time worden toegelaten.
>
>Raadpleeg in plaats daarvan [document](../profile/iab.md) voor de veldgroep die is bedoeld voor de klasse XDM Individual Profile.

[!UICONTROL IAB TCF 2.0 Consent] is een standaardschemagebiedgroep voor de  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) klasse die wordt gebruikt om een timestamped reeksIAB toestemmingskoorden te vangen, om toestemming-verandering patronen in tijd te volgen.

![](../../images/field-groups/iab-event.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `consentStrings` | Array van [Goedgekeurde tekenreeksen](../../data-types/consent-string.md) | Een array van waarden van de toestemmingstekenreeks die aan de gebeurtenis zijn gekoppeld. |

{style=&quot;table-layout:auto&quot;}

Zie de gids op [IAB TCF 2.0 steun in Platform](../../../landing/governance-privacy-security/consent/iab/overview.md) voor meer informatie over het gebruiksgeval van deze gebiedsgroep. Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep zelf:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.schema.json)
