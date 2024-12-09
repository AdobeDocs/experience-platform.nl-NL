---
title: Medicatieaanvraag schema veldgroep
description: Meer informatie over de veldgroep Geneesmiddelenaanvragen.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 0%

---

# [!UICONTROL Medication Request] schemaveldgroep

[!UICONTROL Medication Request] is een standaardgroep van het schemagebied voor de [[!DNL Medication]  klasse ](../../classes/location.md), de [[!DNL XDM Individual Profile]  Klasse ](../../classes/individual-profile.md), en [[!DNL Provider class]](../../classes/provider.md). Het biedt één objecttype veld `healthcareMedicationDispense` waarin een bestelling of aanvraag voor zowel de verstrekking van de medicatie als de instructies voor de toediening van de medicatie aan een patiënt wordt vastgelegd.

![ de groepsstructuur van het Gebied ](../../images/field-groups/healthcare-medication-request/medication-request.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Based On] | `basedOn` | Array van [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | Het plan of de aanvraag waaraan deze aanvraag voor medicatie voldoet. |
| [!UICONTROL Category] | `category` | Array van [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | De indeling of groepering van het verzoek om medicatie. |
| [!UICONTROL Course Of Therapy Type] | `courseOfTherapyType` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | De beschrijving van het algehele patroon voor de toediening van het geneesmiddel aan de patiënt. |
| [!UICONTROL Device] | `device` | Array van [[!UICONTROL Codeable Reference]](../../data-types/healthcare/codeable-reference.md) | Het type hulpmiddel dat gebruikt moet worden voor de toediening van het geneesmiddel. |
| [!UICONTROL Dispense Request] | `dispenseRequest` | Object | Hiermee worden de specifieke details van het verzoek aangegeven, die vaak een medicatievolgorde worden genoemd. Zie de [ sectie hieronder ](#dispense-request) voor meer informatie. |
| [!UICONTROL Dosage Instruction] | `dosageInstructions` | Array van [[!UICONTROL Dosage]](../../data-types/healthcare/dosage.md) | Specifieke instructies voor het gebruik van het geneesmiddel door de patiënt. |
| [!UICONTROL Effective Dose Period] | `effectiveDosePeriod` | [[!UICONTROL Period]](../../data-types/healthcare/period.md) | De periode waarin het geneesmiddel moet worden ingenomen. Wanneer er meerdere `dosageInstruction` regels zijn (bijvoorbeeld bij het afbouwen van doses), is dit de vroegste datum en de laatste datum van de doseringsinstructies. |
| [!UICONTROL Encounter] | `encounter` | [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | De gebeurtenis tijdens welke het verzoek werd gecreeerd. |
| [!UICONTROL Event History] | `eventHistory` | Array van [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | Koppeling naar gebeurtenissen die verband houden met het verzoek om medicatie, zoals het voldoen aan het verzoek, momenten van belangrijke statusovergangen of relevante updates. |
| [!UICONTROL Group Identifier] | `groupIdentifier` | [[!UICONTROL Identifier]](../../data-types/healthcare/identifier.md) | Een gedeelde id voor meerdere onafhankelijke aanvraaginstanties die door één auteur zijn geactiveerd. |
| [!UICONTROL Identifier] | `identifier` | Array van [[!UICONTROL Identifier]](../../data-types/healthcare/identifier.md) | Identificatiecodes die aan het medicatieverzoek zijn gekoppeld en die door bedrijfsprocessen worden gedefinieerd en/of worden gebruikt om ernaar te verwijzen wanneer een directe URL-verwijzing naar de bron zelf niet geschikt is. |
| [!UICONTROL Information Source] | `informationSource` | Array van [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | De persoon of organisatie die de informatie voor het verzoek heeft verstrekt als de bron een andere persoon dan `requester` is. |
| [!UICONTROL Insurance] | `insurance` | Array van [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | Verzekeringsplannen, uitbreidingen van de dekking, voorafgaande vergunningen en/of voorafgaande bepalingen die nodig kunnen zijn voor het verlenen van de gevraagde dienst. |
| [!UICONTROL Medication] | `medication` | [[!UICONTROL Codeable Reference]](../../data-types/healthcare/codeable-reference.md) | Identificeert de gewenste medicatie. Dit moet een link zijn naar een bron die details van de medicatie vertegenwoordigt, of een code die de medicatie identificeert. |
| [!UICONTROL Note] | `note` | Array van [[!UICONTROL Annotation]](../../data-types/healthcare/annotation.md) | Extra informatie over het recept die niet door de andere kenmerken kon worden verstrekt. |
| [!UICONTROL Performer] | `performer` | Array van [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | De gespecificeerde uitvoerder van de medicatiebehandeling/toediening. Voor hulpmiddelen is dit het hulpmiddel dat bedoeld is om de toediening van de medicatie uit te voeren. |
| [!UICONTROL Performer Type] | `performerType` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Geeft het type uitvoerder aan voor de toediening van de medicatie. |
| [!UICONTROL Prior Prescription] | `priorPrescription` | [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | De verwijzing naar een bevel of recept dat door dit verzoek wordt vervangen. |
| [!UICONTROL Reason] | `reason` | Array van [[!UICONTROL Codeable Reference]](../../data-types/healthcare/reference.md) | De reden of indicatie voor het al dan niet bestellen van de medicatie. |
| [!UICONTROL Recorder] | `recorder` | [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | De persoon die namens een andere persoon het bevel heeft uitgevaardigd. |
| [!UICONTROL Requester] | `requester` | [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | De persoon, organisatie of apparaat die het verzoek heeft geïnitieerd en die verantwoordelijk is voor de activering ervan. |
| [!UICONTROL Status Reason] | `statusReason` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | De reden voor de huidige status van het verzoek. |
| [!UICONTROL Subject] | `subject` | [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | De persoon of de groep waarvoor het geneesmiddel is aangevraagd. |
| [!UICONTROL Substitution] | `substitution` | Object | Geeft aan of een vervanging al dan niet deel kan of moet uitmaken van de vrijstelling. Bevat drie eigenschappen: <li>`allowedBoolean`: Een Booleaanse waarde die waar is als de voorschrijver een vervanging toestaat.</li> <li>`allowedCodeableConcept`: Een [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) -waarde die een code bevat als de voorschrijver een vervanging toestaat.</li> <li>`reason`: Een [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) -waarde die een reden voor de vervanging aangeeft.</li> |
| [!UICONTROL Supporting Information] | `supportingInformation` | Array van [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | Informatie ter ondersteuning van het voldoen aan de medicatie, zoals de lengte en het gewicht van de patiënt. |
| [!UICONTROL Authored On] | `authoredOn` | DateTime | De datum (en eventueel het tijdstip) waarop het recept is opgesteld. |
| [!UICONTROL Do Not Perform] | `doNotPerform` | Boolean | Een booleaanse indicator die waar is, is dat de patiënt moet stoppen (of niet beginnen) met het innemen van de medicatie. |
| [!UICONTROL Intent] | `intent` | String | De intentie van het verzoek. De waarde van deze eigenschap moet gelijk zijn aan een van de volgende bekende opsommingswaarden. <li> `proposal` </li> <li> `plan` </li> <li> `order` </li> <li> `original-order` </li> <li> `reflex-order` </li> <li> `filler-order` </li> <li> `instance-order` </li> <li> `option` </li> |
| [!UICONTROL Priority] | `priority` | String | De prioriteit van het verzoek. De waarde van deze eigenschap moet gelijk zijn aan een van de volgende bekende opsommingswaarden. <li> `routine` </li> <li> `urgent` </li> <li> `asap` </li> <li> `stat` </li> |
| [!UICONTROL Rendered Dosage Instruction] | `renderedDosageInstruction` | String | De volledige weergave van de dosis die in alle doseringsinstructies is opgenomen. Te gebruiken wanneer meerdere doseringsinstructies worden meegeleverd om complexe doseringen te vertegenwoordigen, zoals verhoging of vermindering van de dosering. |
| [!UICONTROL Reported] | `reported` | Boolean | Geeft aan of deze record is vastgelegd als een secundaire gerapporteerde record in plaats van als een oorspronkelijke primaire bron-van-waarheidsrecord. |
| [!UICONTROL Status] | `status` | String | De status van de verstrekking. De waarde van deze eigenschap moet gelijk zijn aan een van de volgende bekende opsommingswaarden. <li> `preperation` </li> <li> `in-progress` </li> <li> `cancelled` </li> <li> `on-hold` </li> <li> `completed` </li> <li> `entered-in-error` </li> <li> `stopped` </li> <li> `declined` </li> <li> `unknown` </li> |
| [!UICONTROL Status Changed] | `statusChanged` | DateTime | De datum (en optioneel de tijd) waarop de status is gewijzigd. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationrequest.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationrequest.schema.json)

## `dispenseRequest` {#dispense-request}

`dispenseRequest` wordt opgegeven als een array van objecten. De structuur van elk object wordt hieronder beschreven.

![ de structuur van het Verzoek van de Aflossing ](../../images/field-groups/healthcare-medication-request/dispense-request.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Dispense Interval] | `dispenseInterval` | [[!UICONTROL Duration]](../../data-types/healthcare/duration.md) | De minimale tijdsduur die moet optreden tussen het toedienen van het geneesmiddel. |
| [!UICONTROL Dispenser] | `dispenser` | [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | De beoogde organisatie die de medicatie zal afgeven zoals gespecificeerd door de voorschrijver. |
| [!UICONTROL Dispenser Instruction] | `dispenserInstruction` | Array van [[!UICONTROL Annotation]](../../data-types/healthcare/annotation.md) | Aanvullende informatie voor de dispenser, zoals advies aan de patiënt |
| [!UICONTROL Dose Administration Aid] | `doseAdministrationAid` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Informatie over het type aanhangende verpakking dat voor de medicatie moet worden geleverd. |
| [!UICONTROL Expected Supply Duration] | `expectedSupplyDuration` | [[!UICONTROL Duration]](../../data-types/healthcare/duration.md) | De periode waarin het geleverde product naar verwachting zal worden gebruikt of de duur van de afwijking. |
| [!UICONTROL Initial Fill] | `initialFill` | Object | Informatie voor de eerste vulling. Bevat twee eigenschappen: <li>`quantity`: Een [[!UICONTROL Simple Quantity]](../../data-types/healthcare/simple-quantity.md) -waarde die het bedrag bevat dat tijdens de eerste verzending moet worden opgegeven.</li> <li>`duration`: Een [[!UICONTROL Duration]](../../data-types/healthcare/duration.md) -waarde die de tijdsduur opgeeft waarin de eerste verzending naar verwachting zal duren.</li> |
| [!UICONTROL Quantity] | `quantity` | [[!UICONTROL Simple Quantity]](../../data-types/healthcare/simple-quantity.md) | De hoeveelheid die voor een vulling moet worden weggelaten. |
| [!UICONTROL Validity Period] | `validityPeriod` | [[!UICONTROL Period]](../../data-types/healthcare/period.md) | De geldigheidsduur van het recept. |
| [!UICONTROL Number Of Repeats Allowed] | `numberOfRepeatsAllowed` | Geheel | Het aantal toegestane vullingen met een minimumwaarde van 0. |
