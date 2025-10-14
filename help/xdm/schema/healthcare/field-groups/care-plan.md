---
title: Zorgplanschema-veldgroep
description: Leer over de het schemagebiedgroep van het Plan van de Zorg.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: e6cbf44f-6c39-42bd-b083-a975860a64db
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# [!UICONTROL Care Plan] schemaveldgroep

[!UICONTROL Care Plan] is een standaardgroep van het schemagebied voor de [[!DNL XDM Individual Profile]  klasse &#x200B;](../../../classes/individual-profile.md). Het biedt één objecttype veld `healthcareCarePlan` waarin een gezondheidszorgplan voor een patiënt of groep wordt vastgelegd.

![&#x200B; de groepsstructuur van het Gebied &#x200B;](../../../images/healthcare/field-groups/care-plan/care-plan.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Activity] | `activity` | Array van objecten | Identificeert een actie die is voorgekomen of gepland om als deel van het plan voor te komen. Zie de [&#x200B; sectie hieronder &#x200B;](#activity) voor meer informatie. |
| [!UICONTROL Addresses] | `addresses` | Array van [[!UICONTROL Codeable Reference]](../data-types/codeable-reference.md) | Identificeert de voorwaarden of betreffen de handvatten van het zorgplan. |
| [!UICONTROL Based On] | `basedOn` | Array van [[!UICONTROL Reference]](../data-types/reference.md) | Een aanvraagbron op een hoger niveau die geheel of gedeeltelijk door dit zorgplan wordt vervuld. |
| [!UICONTROL Care Team] | `careTeam` | Array van [[!UICONTROL Reference]](../data-types/reference.md) | Identificeert alle mensen en organisaties die naar verwachting betrokken zullen zijn bij de zorg die door dit plan wordt voorzien. |
| [!UICONTROL Category] | `category` | Array van [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Identificeert welk soort plan dit is onderscheid tussen veelvoudige coëxistente plannen te steunen. |
| [!UICONTROL Contributor] | `contributor` | Array van [[!UICONTROL Reference]](../data-types/reference.md) | Identificeert de individu(n), organisatie of apparaat die de inhoud van het zorgplan heeft geleverd. |
| [!UICONTROL Custodian] | `custodian` | [[!UICONTROL Reference]](../data-types/reference.md) | Wanneer de bewaarder wordt gevuld, is hij verantwoordelijk voor en wordt hij toegerekend aan het zorgplan. |
| [!UICONTROL Encounter] | `encounter` | [[!UICONTROL Reference]](../data-types/reference.md) | De ontmoeting tijdens welke het zorgplan werd opgesteld. |
| [!UICONTROL Goal] | `goal` | Array van [[!UICONTROL Reference]](../data-types/reference.md) | de beoogde doelstelling(en) voor de uitvoering van het plan. |
| [!UICONTROL Identifier] | `identifier` | Array van [[!UICONTROL Identifier]](../data-types/identifier.md) | De bedrijfs-id&#39;s die aan dit zorgplan zijn toegewezen door de uitvoerder of andere systemen die constant blijven terwijl de bron wordt bijgewerkt en van server aan server wordt doorgegeven. |
| [!UICONTROL Note] | `note` | Array van [[!UICONTROL Annotation]](../data-types/annotation.md) | Algemene opmerkingen over het zorgplan die niet onder andere kenmerken vallen. |
| [!UICONTROL Part Of] | `partOf` | Array van [[!UICONTROL Reference]](../data-types/reference.md) | Het grotere zorgplan waarin dit specifieke zorgplan een onderdeel of stap is. |
| [!UICONTROL Period] | `period` | [[!UICONTROL Period]](../data-types/period.md) | Geeft aan wanneer het plan in werking is getreden (of bedoeld is te worden) en wanneer het eindigt. |
| [!UICONTROL Replaces] | `replaces` | Array van [[!UICONTROL Reference]](../data-types/reference.md) | Het voltooide of beëindigde zorgplan waarvan de functie wordt overgenomen door dit zorgplan. |
| [!UICONTROL Subject] | `subject` | [[!UICONTROL Reference]](../data-types/reference.md) | Identificeert de patiënt of groep waarvan de beoogde zorg in het plan wordt beschreven. |
| [!UICONTROL Supporting Info] | `supportingInfo` | Array van [[!UICONTROL Reference]](../data-types/reference.md) | Identificeert delen van het dossier van de patiënt die de vorming van het plan beïnvloedden. Dit kunnen comorbiditeiten, recente procedures, beperkingen of recente beoordelingen zijn. |
| [!UICONTROL Created] | `created` | DateTime | Vertegenwoordigt wanneer dit zorgplan in het systeem werd gecreeerd, dat vaak een systeem-geproduceerde datum is. |
| [!UICONTROL Description] | `description` | String | Een beschrijving van het toepassingsgebied en de aard van de regeling. |
| [!UICONTROL Instantiates Canonical] | `instantiatesCanonical` | Array van tekenreeksen | De URL die verwijst naar een door FHIR gedefinieerd protocol, richtsnoer, vragenlijst of andere definitie die geheel of gedeeltelijk door dit plan wordt nageleefd. |
| [!UICONTROL Instantiates Uri] | `instantiatesUri` | Array van tekenreeksen | De URL die verwijst naar een extern onderhouden protocol, richtsnoer, vragenlijst of andere definitie die geheel of gedeeltelijk door dit plan wordt nageleefd, wordt vertegenwoordigd als URI. |
| [!UICONTROL Intent] | `intent` | String | De intentie van het zorgplan. De waarde van deze eigenschap moet gelijk zijn aan een van de volgende bekende opsommingswaarden. <li> `proposal` </li> <li> `plan` </li> <li> `order` </li> <li> `option` </li> <li> `directive` </li> |
| [!UICONTROL Status] | `status` | String | De status van het zorgplan. De waarde van deze eigenschap moet gelijk zijn aan een van de volgende bekende opsommingswaarden. <li> `draft` </li> <li> `active` </li> <li> `on-hold` </li> <li> `revoked` </li> <li> `completed` </li> <li> `entered-in-error` </li> <li> `unknown` </li> |
| [!UICONTROL Title] | `title` | String | De naam van het zorgplan. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/careplan.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/careplan.schema.json)

## `activity` {#activity}

`activity` wordt opgegeven als een array van objecten. De structuur van elk object wordt hieronder beschreven.

![&#x200B; activiteitenstructuur &#x200B;](../../../images/healthcare/field-groups/care-plan/activity.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Performed Activity] | `performedActivity` | Array van [[!UICONTROL Codeable Reference]](../data-types/codeable-reference.md) | De resultaten van de activiteit, zoals een aanstelling of een procedure. |
| [!UICONTROL Planned Activity Reference] | `plannedActivityReference` | [[!UICONTROL Reference]](../data-types/reference.md) | De details van de voorgestelde activiteit. |
| [!UICONTROL Progress] | `progress` | Array van [[!UICONTROL Annotation]](../data-types/annotation.md) | Nota&#39;s over de aanhangen, de status, of de vooruitgang van de activiteit. |
