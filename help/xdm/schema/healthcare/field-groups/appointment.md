---
title: Veld groep benoemingsschema
description: Leer meer over de het gebiedsgroep van het Schema van de Benoeming.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 8224a2ee-51ac-4512-b0e4-5f1ab6bfddc4
source-git-commit: cb39966de77846758c16153f78fcf521f6a421e3
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 0%

---

# [!UICONTROL Appointment] schemaveldgroep

[!UICONTROL Appointment] is een standaardgroep van het schemagebied voor de [[!DNL XDM Individual Profile]  klasse ](../../../classes/individual-profile.md) en [[!DNL Provider class]](../../../classes/provider.md). Het biedt één objecttype veld `healthcareAppointment` dat informatie bevat over het boeken van een gezondheidszorggebeurtenis onder patiënten, artsen, verwante personen en/of apparaten voor een bepaalde datum en tijd.

![ het schemadiagram van A van de structuur van de groep van het benoemingsgebied.](../../../images/healthcare/field-groups/appointment/appointment.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Account] | `account` | Array van [[!UICONTROL Reference]](../data-types/reference.md) | The set of accounts that are expected to be used for facilling. |
| [!UICONTROL Appointment Type] | `appointmentType` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | De soort afspraak of patiënt die in de sleuf is geboekt (geen servicetype). |
| [!UICONTROL Based On] | `basedOn` | Array van [[!UICONTROL Reference]](../data-types/reference.md) | Het verzoek om benoeming wordt toegewezen aan een beoordeling, zoals een procedureverzoek. |
| [!UICONTROL Cancellation Reason] | `cancellationReason` | Array van [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | De gecodeerde reden voor de annulering van de afspraak. Dit wordt vaak gebruikt in rapportering, facturering, of verwerking om te bepalen of verdere acties worden vereist, of als specifieke kosten van toepassing zijn. |
| [!UICONTROL Class] | `class` | Array van [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Concepten die de classificatie van een patiënt weergeven, zoals ambulant, polipatiënt, patiënt of noodgeval. |
| [!UICONTROL Identifier] | `identifier` | Array van [[!UICONTROL Identifier]](../data-types/identifier.md) | Een lijst met unieke id&#39;s die aan de afspraak zijn gekoppeld. Deze herkenningstekens worden toegewezen gebaseerd op bedrijfsregels of wanneer een directe verbinding URL aan de benoeming niet geschikt is. |
| [!UICONTROL Note] | `note` | Array van [[!UICONTROL Annotation]](../data-types/annotation.md) | Aanvullende opmerkingen of opmerkingen over de afspraak. |
| [!UICONTROL Originating Appointment] | `originatingAppointment` | [[!UICONTROL Reference]](../data-types/reference.md) | De oorspronkelijke afspraak in een terugkerende reeks van verwante benoemingen. |
| [!UICONTROL Participant] | `participant` | Array van objecten | Een lijst van deelnemers die betrokken zijn bij de benoeming. Zie de [ sectie hieronder ](#participant) voor meer informatie. |
| [!UICONTROL Patient Instruction] | `patientInstruction` | Array van [[!UICONTROL Codeable Reference]](../data-types/reference.md) | De diagnose die relevant is voor de aanstelling. |
| [!UICONTROL Previous Appointment] | `previousAppointment` | [[!UICONTROL Reference]](../data-types/reference.md) | De vorige aanstelling in een reeks van daarmee verband houdende benoemingen. |
| [!UICONTROL Priority] | `priority` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | De prioriteit van de benoeming die kan worden gebruikt om geïnformeerde beslissingen te nemen indien benoemingen opnieuw prioriteit moeten krijgen. De iCal-standaard geeft `0` aan als ongedefinieerd, `1` als hoogste prioriteit en `9` als laagste prioriteit. |
| [!UICONTROL Reason] | `reason` | Array van [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | De reden waarom de afspraak gepland is, wat doorgaans een voorwaarde of procedure is. |
| [!UICONTROL Reccurence Template] | `recurrenceTemplate` | Array van objecten | Bevat de details van het terugkeringspatroon of het malplaatje dat worden gebruikt om terugkomende benoemingen tot stand te brengen.  Zie de [ sectie hieronder ](#recurrence) voor meer informatie. |
| [!UICONTROL Replaces] | `replaces` | Array van [[!UICONTROL Reference]](../data-types/reference.md) | De benoeming wordt vervangen door deze benoeming. In gevallen waarin er sprake is van annulering, vindt u de details van de annulering in de eigenschap `cancellationReason` op de resource waarnaar wordt verwezen. |
| [!UICONTROL Requested Period] | `requestedPeriod` | Array van [[!UICONTROL Period]](../data-types/period.md) | Een reeks datumwaaiers (eventueel met inbegrip van tijden) waarin de benoeming verkiest te worden gepland. |
| [!UICONTROL Service Category] | `serviceCategory` | Array van [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Een brede categorisering van de dienst die tijdens de benoeming moet worden verricht. |
| [!UICONTROL Service Type] | `serviceType` | Array van [[!UICONTROL Codeable Reference]](../data-types/codeable-reference.md) | De specifieke dienst die tijdens de benoeming moet worden uitgevoerd. |
| [!UICONTROL Slot] | `slot` | Array van [[!UICONTROL Reference]](../data-types/reference.md) | De tijdsperiodes van de schema&#39;s van de deelnemers die door de benoeming zullen worden ingevuld. |
| [!UICONTROL Speciality] | `speciality` | Array van [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | De specialiteit van een arts die de in deze afspraak gevraagde dienst moet verrichten. |
| [!UICONTROL Subject] | `subject` | Array van [[!UICONTROL Reference]](../data-types/reference.md) | De patiënt of groep die bij de afspraak hoort. |
| [!UICONTROL Supporting Information] | `supportingInformation` | Array van [[!UICONTROL Reference]](../data-types/reference.md) | Aanvullende informatie bij de benoeming ter ondersteuning van de benoeming. |
| [!UICONTROL Virtual Service] | `virtualService` | Array van [[!UICONTROL Virtual Service Detail]](../data-types/virtual-service-detail.md) | Verbindingsdetails van een virtuele service, zoals een conferentiegesprek. |
| [!UICONTROL Cancellation Date] | `cancellationDate` | DateTime | De datum en het tijdstip waarop de afspraak werd geannuleerd. |
| [!UICONTROL Created] | `created` | DateTime | De datum en het tijdstip waarop de afspraak is gemaakt. |
| [!UICONTROL Description] | `description` | String | Een korte beschrijving van de aanstelling. Gedetailleerde of uitgebreide informatie moet in het veld `note` worden geplaatst. |
| [!UICONTROL End] | `end` | DateTime | De datum en het tijdstip waarop de afspraak afloopt. |
| [!UICONTROL Minutes Duration] | `minutesDuration` | Geheel | Het aantal minuten dat de afspraak zal duren. Dit kan minder zijn dan de duur tussen de begin- en eindtijd. De minimaal toegestane waarde is `0` . |
| [!UICONTROL Occurence Changed] | `occurenceChanged` | Boolean | Een vlag die aangeeft of deze afspraak afwijkt van het terugkerende patroon. |
| [!UICONTROL RecurrenceId] | `RecurrenceId` | Geheel | Het volgnummer dat een specifieke afspraak in een terugkerend patroon aangeeft. De minimumwaarde is `0` . |
| [!UICONTROL Start] | `start` | DateTime | De datum en het tijdstip waarop de benoeming plaatsvindt. |
| [!UICONTROL Status] | `status` | String | De status van de aanstelling. De waarde van deze eigenschap moet gelijk zijn aan een van de volgende bekende opsommingswaarden: <li> `proposed` </li> <li> `pending` </li> <li> `booked` </li> <li> `arrived` </li> <li> `fulfilled` </li> <li> `cancelled` </li> <li> `noshow` </li> <li> `entered-in-error` </li> <li> `checked-in` </li> <li> `waitlist` </li> |


Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/appointment.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/appointment.schema.json)

## `participant` {#participant}

`participant` wordt opgegeven als een array van objecten. De structuur van elk object wordt hieronder beschreven.

![ het schemadiagram van A van de structuur van het deelnemervoorwerp.](../../../images/healthcare/field-groups/appointment/participant.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Actor] | `actor` | [[!UICONTROL Reference]](../data-types/reference.md) | De persoon, het apparaat, de plaats, of de dienst die aan de benoeming deelnemen. |
| [!UICONTROL Period] | `period` | [[!UICONTROL Period]](../data-types/period.md) | De periode waarin de deelnemer (actor) bij de benoeming is betrokken. |
| [!UICONTROL Type] | `type` | Array van [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | De rol van de deelnemer (actor) bij de benoeming. |
| [!UICONTROL Required] | `required` | Boolean | Of deze deelnemer aanwezig moet zijn. |
| [!UICONTROL status] | `status` | String | De acceptatiestatus van de deelnemer. De waarde van deze eigenschap moet gelijk zijn aan een van de volgende bekende opsommingswaarden: <li> `accepted` </li> <li> `declined` </li> <li> `tentative` </li> <li> `needs-action` </li> |

## `recurrenceTemplate` {#recurrence}

`recurrenceTemplate` wordt opgegeven als een array van objecten. De structuur van elk object wordt hieronder beschreven.

![ het schemadiagram van A van de de objecten van het reccurence malplaatje structuur.](../../../images/healthcare/field-groups/appointment/recurrence-template.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Monthly Template] | `monthlyTemplate` | Array van objecten | Informatie over maandelijkse terugkerende benoemingen. Zie de [ sectie hieronder ](#monthly-template) voor meer informatie. |
| [!UICONTROL Recurrence Type] | `recurrenceType` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Hoe vaak de aanstellingsreeksen, zoals wekelijks, maandelijks, of jaarlijks moeten terugkeren. |
| [!UICONTROL Timezone] | `timezone` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | De tijdzone van de terugkerende benoeming. |
| [!UICONTROL Weekly Template] | `weeklyTemplate` | Array van objecten | Informatie over wekelijkse terugkerende afspraken. Zie de [ sectie hieronder ](#weekly-template) voor meer informatie. |
| [!UICONTROL Yearly Template] | `yearlyTemplate` | Object | Informatie over jaarlijkse periodieke benoemingen. Bevat één eigenschap, `yearInterval` , die een geheel-getalwaarde bevat die elk jaar aangeeft dat de afspraak opnieuw wordt uitgevoerd. |
| [!UICONTROL Excluding Date] | `excludingDate` | Array met datums | Datums, zoals feestdagen, die van de herhaling moeten worden uitgesloten. |
| [!UICONTROL Excluding Recurrence Id] | `excludingRecurrenceId` | Array van gehele getallen | Herhalings-id&#39;s die van de herhaling moeten worden uitgesloten. Dit is een alternatief voor `excludingDate` , waarin u de `reccurenceID` van de afspraak aangeeft die moet worden uitgesloten. |
| [!UICONTROL Last Occurence Date] | `lastOccurenceDate` | Datum | De datum waarna geen terugkerende benoemingen meer zullen worden gepland. |
| [!UICONTROL Occurence Count] | `occurenceCount` | Geheel | Hoeveel benoemingen zijn gepland bij herhaling? De minimumwaarde is `0` . |
| [!UICONTROL Occurence Date] | `occurenceDate` | Array met datums | Een lijst van specifieke data waarop benoemingen gepland zijn. |

## `weeklyTemplate` {#weekly-template}

`weeklyTemplate` wordt opgegeven als een array van objecten. De structuur van elk object wordt hieronder beschreven.

![ het schemadiagram van A van de wekelijkse malplaatjeobjecten structuur.](../../../images/healthcare/field-groups/appointment/weekly-template.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Friday] | `friday` | Boolean | Geeft aan dat terugkerende afspraken op vrijdag moeten worden gemaakt. |
| [!UICONTROL Monday] | `monday` | Boolean | Geeft aan dat terugkerende benoemingen moeten plaatsvinden op maandag. |
| [!UICONTROL Saturday] | `saturday` | Boolean | Geeft aan dat terugkerende afspraken op zaterdagen moeten plaatsvinden. |
| [!UICONTROL Sunday] | `sunday` | Boolean | Geeft aan dat terugkerende benoemingen op zondag moeten plaatsvinden. |
| [!UICONTROL Thursday] | `thursday` | Boolean | Geeft aan dat terugkerende benoemingen op donderdag moeten plaatsvinden. |
| [!UICONTROL Tuesday] | `tuesday` | Boolean | Geeft aan dat terugkerende benoemingen op dinsdagen moeten plaatsvinden. |
| [!UICONTROL Wednesday] | `wednesday` | Boolean | Geeft aan dat terugkerende benoemingen op woensdag moeten plaatsvinden. |
| [!UICONTROL Week Interval] | `weekInterval` | Geheel | Hiermee wordt aangegeven hoe vaak de benoemingen opnieuw plaatsvinden, in termen van elke negende week. De standaardwaarde is elke week, dus de typische waarde is 2 of hoger. |

## `monthlyTemplate` {#monthly-template}

`monthlyTemplate` wordt opgegeven als een array van objecten. De structuur van elk object wordt hieronder beschreven.

![ het schemadiagram van A van de maandelijkse malplaatjeobjecten structuur.](../../../images/healthcare/field-groups/appointment/monthly-template.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Day Of Week] | `dayOfWeek` | [[!UICONTROL Coding]] | Geeft aan dat benoemingen moeten plaatsvinden op deze specifieke dag van de week. |
| [!UICONTROL nth Week Of Month] | `nthWeekOfMonth` | [[!UICONTROL Coding]](../data-types/coding.md) | Geeft de nde week van de maand aan waarin de afspraak opnieuw moet plaatsvinden. |
| [!UICONTROL Day Of Month] | `dayOfMonth` | Geheel | Geeft aan dat benoemingen moeten plaatsvinden op deze specifieke dag van de maand. |
| [!UICONTROL Month Interval] | `monthInterval` | Geheel | Geeft aan dat terugkerende benoemingen elke maand moeten plaatsvinden. |

