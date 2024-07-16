---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;ExperienceEvent;fields;schema's;Schema's;Schema-ontwerp;field-groep;field-groep;iab;tcf;permission;
solution: Experience Platform
title: IAB TCF 2.0 De Toegelaten Groep van het Gebied voor Gebeurtenisschema's
description: Leer over IAB TCF 2.0 het gebiedsgroep van het Goedkeuring schema voor de klasse XDM ExperienceEvent.
exl-id: c236d0d4-27bd-45d7-a912-d0e93a609254
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---

# [!UICONTROL IAB TCF 2.0 Consent] veldgroep voor gebeurtenisschema&#39;s

>[!IMPORTANT]
>
>In dit document wordt de schemaveldgroep [!UICONTROL IAB TCF 2.0 Consent] voor de klasse XDM ExperienceEvent besproken. Deze veldgroep mag alleen worden gebruikt als u wijzigingen in de toestemming wilt bijhouden tijdens een tijdsverloop.
>
>Merk op dat toestemmingswaarden die in gebeurtenisgegevens worden geregistreerd niet in automatische handhavingswerkschema&#39;s worden nageleefd. Om automatische handhaving te kunnen plaatsvinden, moeten de toestemmingswaarden in de klasse van het Profiel van Individuele XDM worden opgenomen en voor het Profiel van de Klant in real time worden toegelaten.
>
>Voor de gebiedsgroep voorgenomen voor de individuele klasse van het Profiel XDM, verwijs in plaats daarvan naar het volgende [ document ](../profile/iab.md).

[!UICONTROL IAB TCF 2.0 Consent] is een standaardgroep van het schemagebied voor de [[!DNL XDM ExperienceEvent]  klasse ](../../classes/experienceevent.md) wordt gebruikt om een timestamped reeksenIAB toestemmingskoorden te vangen, om toestemming-verandering patronen in tijd te volgen die.

![](../../images/field-groups/iab-event.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `consentStrings` | Serie van [ Goedgekeurde Koorden ](../../data-types/consent-string.md) | Een array van waarden van de toestemmingstekenreeks die aan de gebeurtenis zijn gekoppeld. |

{style="table-layout:auto"}

Zie de gids op [ IAB TCF 2.0 steun in Platform ](../../../landing/governance-privacy-security/consent/iab/overview.md) voor meer informatie over het gebruiksgeval van deze gebiedsgroep. Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep zelf:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.schema.json)
