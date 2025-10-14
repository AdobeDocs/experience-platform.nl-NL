---
title: Veld groep accountschema
description: Meer informatie over de veldgroep Account Schema.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 376716bd-f79f-421d-b163-0f0e50876b48
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 0%

---

# [!UICONTROL Account] schemaveldgroep

[!UICONTROL Account] is een standaardgroep van het schemagebied voor de [[!DNL XDM Individual Profile]  klasse &#x200B;](../../../classes/individual-profile.md) en [[!DNL Provider class]](../../../classes/provider.md). Het verstrekt één enkel voorwerp-type gebied `healthcareAccount` dat wordt gebruikt om transacties, de diensten, en andere financiële informatie te registreren met betrekking tot gezondheidsdiensten die aan een patiënt of een groep individuen worden verleend (zoals voor een verzekeringspolis of factureringsdoeleinden).

![&#x200B; de groepsstructuur van het Gebied &#x200B;](../../../images/healthcare/field-groups/account/account.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Balance] | `balance` | Array van objecten | De door het financiële stelsel berekende en verwerkte rekeningsaldi. Zie [&#x200B; sectie-hieronder &#x200B;](#balances) voor meer informatie. |
| [!UICONTROL Billing Status] | `billingStatus` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Dit volgt de levenscyclus van de rekening door het factureringsproces. Het geeft aan hoe transacties worden verwerkt wanneer ze aan de rekening worden toegerekend. |
| [!UICONTROL Coverage] | `coverage` | Array van objecten | De partij(en) die verantwoordelijk is (zijn) voor de dekking van de kosten van deze rekening en in welke volgorde moeten deze worden toegepast. Zie de [&#x200B; sectie hieronder &#x200B;](#coverage) voor meer informatie. |
| [!UICONTROL Currency] | `currency` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | De standaardvaluta voor de account. |
| [!UICONTROL Diagnosis] | `diagnosis` | Array van objecten | De reeks diagnoses die relevant zijn voor de facturering worden hier opgeslagen op de rekening waar zij voorafgaand aan de verwerking naar behoren kunnen worden gerangschikt om claim(en) te produceren. Zie de [&#x200B; sectie hieronder &#x200B;](#diagnosis) voor meer informatie. |
| [!UICONTROL Guarantor] | `guarantor` | Array van objecten | De partijen die verantwoordelijk zijn voor het in evenwicht brengen van de rekening indien andere betalingsopties tekortschieten. Zie de [&#x200B; sectie hieronder &#x200B;](#guarantor) voor meer informatie. |
| [!UICONTROL Identifier] | `identifier` | Array van [[!UICONTROL Identifier]](../data-types/identifier.md) | Een unieke id die wordt gebruikt om naar de account te verwijzen. Het kan al dan niet voor menselijk gebruik zijn bestemd (bv. creditcardnummer). |
| [!UICONTROL Owner] | `owner` | [[!UICONTROL Reference]](../data-types/reference.md) | Geeft het servicegebied, het ziekenhuis, de afdeling enz. aan. verantwoordelijk is voor het beheer van de account. |
| [!UICONTROL Procedure] | `procedure` | Array van objecten | De voor facturering relevante reeks procedures wordt hier opgeslagen op de rekening waar zij voorafgaand aan de verwerking naar behoren kunnen worden gesequenceerd om de vordering(en) te produceren. Zie de [&#x200B; sectie hieronder &#x200B;](#procedure) voor meer informatie. |
| [!UICONTROL Related Account] | `relatedAccount` | Array van objecten | Overige met deze rekening verband houdende rekeningen. Zie de [&#x200B; sectie hieronder &#x200B;](#related-account) voor meer informatie. |
| [!UICONTROL Service Period] | `servicePeriod` | [[!UICONTROL Period]](../data-types/period.md) | Het datumbereik van services die aan dit account zijn gekoppeld. |
| [!UICONTROL Subject] | `subject` | Array van [[!UICONTROL Reference]](../data-types/reference.md) | Identificeert de entiteit die de kosten maakt. Hoewel de directe afnemers van diensten of goederen entiteiten zouden kunnen zijn die met het onderwerp van de rekening verband houden, werden de kosten uiteindelijk gedragen door het onderwerp van de rekening. |
| [!UICONTROL Type] | `type` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Hiermee categoriseert u de account voor rapportage- en zoekdoeleinden. |
| [!UICONTROL Calculated At] | `calculatedAt` | DateTime | Het tijdstip waarop het saldo werd berekend. |
| [!UICONTROL Description] | `description` | String | Biedt aanvullende informatie over wat de account bijhoudt en hoe deze wordt gebruikt. |
| [!UICONTROL Name] | `name` | String | De naam van de account. |
| [!UICONTROL Status] | `status` | String | De status van de rekening. De waarde van deze eigenschap moet gelijk zijn aan een van de volgende bekende opsommingswaarden. <li> `active` </li> <li> `inactive` </li> <li> `entered-in-error` </li> <li> `on-hold` </li> <li> `unknown`</li> |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/account.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/account.schema.json)

## `balances` {#balances}

`balances` wordt opgegeven als een array van objecten. De structuur van elk object wordt hieronder beschreven.

![&#x200B; evenwichtsstructuur &#x200B;](../../../images/healthcare/field-groups/account/balance.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Aggregate] | `aggregate` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Wie moet dit deel van het saldo betalen? |
| [!UICONTROL Amount] | `amount` | [[!UICONTROL Money]](../data-types/money.md) | Het feitelijke saldo berekend voor de leeftijd gedefinieerd in de term eigendom. |
| [!UICONTROL Term] | `term` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | De rekeningperiode. |
| [!UICONTROL Estimate] | `estimate` | Boolean | Indien het bedrag een geschatte waarde is. |

## `coverage` {#coverage}

`coverage` wordt opgegeven als een array van objecten. De structuur van elk object wordt hieronder beschreven.

![&#x200B; dekkingsstructuur &#x200B;](../../../images/healthcare/field-groups/account/coverage.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Coverage] | `coverage` | [[!UICONTROL Reference]](../data-types/reference.md) | De partij(en) die verantwoordelijk is (zijn) voor de dekking van de kosten van deze rekening en in welke volgorde moeten deze worden toegepast. |
| [!UICONTROL Priority] | `priority` | Geheel | De prioriteit van de dekking in de context van deze account, met een minimumwaarde van `0`. |

## `diagnosis` {#diagnosis}

`diagnosis` wordt opgegeven als een array van objecten. De structuur van elk object wordt hieronder beschreven.

![&#x200B; diagnosefunctie &#x200B;](../../../images/healthcare/field-groups/account/diagnosis.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Condition] | `condition` | [[!UICONTROL Codeable Reference]](../data-types/codeable-reference.md) | De diagnose die relevant is voor de account. |
| [!UICONTROL Package Code] | `packageCode` | Array van [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | De verpakkingscode kan worden gebruikt om diagnoses te groeperen die als één product kunnen worden geprijsd of geleverd (zoals DRG&#39;s). |
| [!UICONTROL Type] | `type` | Array van [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Type dat deze diagnose relevant is voor de rekening (bijv. toelating, facturering, afvoer ...). |
| [!UICONTROL Date Of Diagnosis] | `dateOfDiagnosis` | DateTime | Datum van de diagnose (wanneer gecodeerde diagnose). |
| [!UICONTROL On Admission] | `onAdmission` | Boolean | Of de diagnose aanwezig was bij toelating. |
| [!UICONTROL Squence] | `sequence` | Geheel | Rangschikking van de diagnose (voor elk type), met een minimumwaarde van `0`. |

## `guarantor` {#guarantor}

`guarantor` wordt opgegeven als een array van objecten. De structuur van elk object wordt hieronder beschreven.

![&#x200B; garantieersstructuur &#x200B;](../../../images/healthcare/field-groups/account/guarantor.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Party] | `party` | [[!UICONTROL Reference]](../data-types/reference.md) | De verantwoordelijke entiteit. |
| [!UICONTROL Period] | `period` | [[!UICONTROL Period]](../data-types/period.md) | Het tijdsbestek waarin de garant de verantwoordelijkheid voor de rekening op zich neemt. |
| [!UICONTROL On Hold] | `onHold` | Boolean | Een garant kan op krediet worden geplaatst of op een andere wijze tijdelijk worden geschorst. |

## `procedure` {#procedure}

`procedure` wordt opgegeven als een array van objecten. De structuur van elk object wordt hieronder beschreven.

![&#x200B; procedurestructuur &#x200B;](../../../images/healthcare/field-groups/account/procedure.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Code] | `code` | [[!UICONTROL Codeable Reference]](../data-types/codeable-reference.md) | De voor de rekening relevante procedure. |
| [!UICONTROL Device] | `device` | Array van [[!UICONTROL Reference]](../data-types/reference.md) | Alle apparaten die zijn gekoppeld aan de procedure die relevant is voor de account. |
| [!UICONTROL Type] | `type` | Array van [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Hoe de procedurewaarde moet worden gebruikt voor het aanrekenen van de rekening. |
| [!UICONTROL Package Code] | `packageCode` | Array van [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | De pakketcode kan worden gebruikt om procedures te groeperen die als één product (zoals DRGs) kunnen worden geprijsd of geleverd. |
| [!UICONTROL Date Of Service] | `dateOfService` | DateTime | De datum waarop een gecodeerde procedure wordt gebruikt. Als een verwijzing naar een procedure wordt gebruikt, moet de datum van de procedure worden gebruikt. |
| [!UICONTROL Sequence] | `sequence` | Geheel | Rangschikking van de procedure (voor elk type), met een minimumwaarde van `0`. |

## `relatedAccount` {#related-account}

`relatedAccount` wordt opgegeven als een array van objecten. De structuur van elk object wordt hieronder beschreven.

![&#x200B; relatedAccount structure &#x200B;](../../../images/healthcare/field-groups/account/related-account.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Account] | `account` | [[!UICONTROL Reference]](../data-types/reference.md) | Verwijzing naar een gekoppelde account. |
| [!UICONTROL Relationship] | `relationship` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Relatie van de bijbehorende account. |
