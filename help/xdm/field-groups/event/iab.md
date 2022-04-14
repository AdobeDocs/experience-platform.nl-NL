---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;ExperienceEvent;fields;schema's;Schema's;Schema-ontwerp;veldgroep;field-groep;iab;tcf;permission;
solution: Experience Platform
title: IAB TCF 2.0 De Toegelaten Groep van het Gebied voor Gebeurtenisschema's
topic-legacy: overview
description: Dit document biedt een overzicht van de IAB TCF 2.0-groep met het schema voor instemming voor de XDM ExperienceEvent-klasse.
exl-id: c236d0d4-27bd-45d7-a912-d0e93a609254
source-git-commit: 046486d5e154b45fc2c2f5408eee235dddf46a4d
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---

# [!UICONTROL IAB TCF 2.0 Consent] veldgroep voor gebeurtenisschema&#39;s

>[!IMPORTANT]
>
>In dit document worden de [!UICONTROL IAB TCF 2.0 Consent] schemaveldgroep voor de klasse XDM ExperienceEvent. Deze veldgroep mag alleen worden gebruikt als u wijzigingen in de toestemming wilt bijhouden tijdens een tijdsverloop.
>
>Merk op dat toestemmingswaarden die in gebeurtenisgegevens worden geregistreerd niet in automatische handhavingswerkschema&#39;s worden nageleefd. Om automatische handhaving te kunnen plaatsvinden, moeten de toestemmingswaarden in de klasse van het Profiel van Individuele XDM worden opgenomen en voor het Profiel van de Klant in real time worden toegelaten.
>
>Raadpleeg het volgende voor de veldgroep die is bedoeld voor de klasse Individueel profiel XDM [document](../profile/iab.md) in plaats daarvan.

[!UICONTROL IAB TCF 2.0 Consent] is een standaardschemagebiedgroep voor [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md) gebruikt voor het vastleggen van reeksen IAB-toestemmingstekenreeksen met tijdstempels, om toestemmings-veranderingspatronen in de loop van de tijd bij te houden.

![](../../images/field-groups/iab-event.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `consentStrings` | Array van [Goedkeuringsstrings](../../data-types/consent-string.md) | Een array van waarden van de toestemmingstekenreeks die aan de gebeurtenis zijn gekoppeld. |

{style=&quot;table-layout:auto&quot;}

Zie de handleiding op [IAB TCF 2.0-ondersteuning in Platform](../../../landing/governance-privacy-security/consent/iab/overview.md) voor meer informatie over het gebruik van deze veldgroep. Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep zelf:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.schema.json)
