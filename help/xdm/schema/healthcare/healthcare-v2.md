---
title: Gegevensmodel gezondheidszorg V2
description: Meer informatie over enkele gangbare gevallen van gebruik in de gezondheidszorg en de beste klassen, verwante veldgroepen en te gebruiken datatypen.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: a796b58b-b36f-4277-870b-0d3939af8061
source-git-commit: 36f1a443eda47917d5b6bd84d4765ff044b5093a
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 1%

---

# [!UICONTROL Healthcare] Gegevensmodel V2

## Veldgroepen en -klassen {#field-groups}

De volgende lijst schetst de geadviseerde klassen en de groepen van het schemagebied voor verscheidene gemeenschappelijke gevallen van het gezondheidszorggebruik.

<table>
  <thead>
    <tr>
      <th>Gebruiksscenario’s</th>
      <th>Veldgroepen</th>
      <th>Compatibele klassen</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong> creeer/werk patiënt </strong> bij: Wanneer een patiënt bij de ziekenhuisvoordesk aankomt, wordt een patiëntenverslag gevestigd, met inbegrip van demografische details zoals (facultatief) herkenningsteken, de patiëntennaam, hun geboortedatum, hun geslacht, en hun adres. Dit is een essentieel onderdeel van IT in de gezondheidszorg.</td>
      <td><a href="./field-groups/patient.md">Patiënt</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Afzonderlijk XDM-profiel</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="6"><strong> Vaccinatie </strong>: Faciliterend het vaccinatieproces, het beheren van de dossiers van de patiëntenimmunisatie, en het integreren van EMRs met de Systemen van het Beheer van Vaccins.</td>
      <td><a href="./field-groups/immunization.md">Immunisatie</a></td>
      <td>
        <li><a href="../../classes/experienceevent.md">XDM Experience Event</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/patient.md">Patiënt</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Afzonderlijk XDM-profiel</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/location.md">Locatie</a></td>
      <td>
        <li><a href="./classes/location.md">Locatie</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/medication.md">Geneesmiddelen</a></td>
      <td>
        <li><a href="../../classes/medication.md">Geneesmiddelen</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/medication-dispense.md">Geneesmiddelenverlies</a></td>
      <td>
        <li><a href="../../classes/medication.md">Geneesmiddelen</a></li>
        <li><a href="../../classes/individual-profile.md">Afzonderlijk XDM-profiel</a></li>
        <li><a href="../../classes/provider.md">Provider</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/medication-request.md">Aanvraag voor geneesmiddelen</a></td>
      <td>
        <li><a href="../../classes/medication.md">Geneesmiddelen</a></li>
        <li><a href="../../classes/individual-profile.md">Afzonderlijk XDM-profiel</a></li>
        <li><a href="../../classes/provider.md">Provider</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="4"><strong> Aanhandiging na de zorg </strong>: Motivering van patiënten en verzorgers om hun behandelingsplannen te voltooien en de overmakingspercentages te verminderen.</td>
      <td><a href="./field-groups/patient.md">Patiënt</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Afzonderlijk XDM-profiel</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/location.md">Locatie</a></td>
      <td>
        <li><a href="./classes/location.md">Locatie</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/care-plan.md">Zorgplan</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Afzonderlijk XDM-profiel</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/goal.md">Goal</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Afzonderlijk XDM-profiel</a></li>
        <li><a href="../../classes/provider.md">Provider</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="7"><strong> de ervaring van de consument voor verzekering </strong>: Verbeter digitale verwerving en ervaringen onder consumenten die voor verzekering winkelen. Voorbeelden zijn: 
        <li> Werken met consumentengedrag om speciale e-mails of doeladvertenties van derden te verzenden naar mensen die pagina's met algemene informatie openen (zoals plannen, plannamen/lagen, medicaid- of welzijnsprogramma's)
        </li> 
        <li> Het verzenden van vaccingerelateerde informatie over hartgezondheid om merkbekendheid te creëren of verzoeken om vaccins te plannen aan mensen die op zoek zijn naar hartgezondheid en vaccininformatie.
        </li>
      </td>
      <td><a href="./field-groups/patient.md">Patiënt</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Afzonderlijk XDM-profiel</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/coverage.md">Dekking</a></td>
      <td>
        <li><a href="../../classes/plan.md">Plan</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/account.md">Account</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Afzonderlijk XDM-profiel</a></li>
        <li><a href="../../classes/provider.md">Provider</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/location.md">Locatie</a></td>
      <td>
        <li><a href="./classes/location.md">Locatie</a></li>
      </td>
    </tr>
      <tr>
      <td><a href="./field-groups/medication.md">Geneesmiddelen</a></td>
      <td>
        <li><a href="../../classes/medication.md">Geneesmiddelen</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/medication-dispense.md">Geneesmiddelenverlies</a></td>
      <td>
        <li><a href="../../classes/medication.md">Geneesmiddelen</a></li>
        <li><a href="../../classes/individual-profile.md">Afzonderlijk XDM-profiel</a></li>
        <li><a href="../../classes/provider.md">Provider</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/medication-request.md">Aanvraag voor geneesmiddelen</a></td>
      <td>
        <li><a href="../../classes/medication.md">Geneesmiddelen</a></li>
        <li><a href="../../classes/individual-profile.md">Afzonderlijk XDM-profiel</a></li>
        <li><a href="../../classes/provider.md">Provider</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="5"><strong> Verbeterde leverancierservaring </strong>: Het gebruiken van leveranciersgegevens van het systeem EMR om alternatieve leveranciers voor te stellen die op benoemingsbeschikbaarheid, plaats, en specialiteit worden gebaseerd. <br> <br> het verbeteren van leveranciersonderzoeken om resultaten met gewenste beschikbaarheid te tonen, controlerend dat de geselecteerde leverancier deel van het loonnetwerk uitmaakt, en het verstrekken van kostenramingen.
      </td>
      <td><a href="./field-groups/patient.md">Patiënt</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Afzonderlijk XDM-profiel</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/location.md">Locatie</a></td>
      <td>
        <li><a href="./classes/location.md">Locatie</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/organization.md">Organisatie</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Afzonderlijk XDM-profiel</a></li>
        <li><a href="../../classes/provider.md">Provider</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/practioner.md">Praktijkster</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Afzonderlijk XDM-profiel</a></li>
        <li><a href="../../classes/provider.md">Provider</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/schedule.md">Schema</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Afzonderlijk XDM-profiel</a></li>
        <li><a href="../../classes/provider.md">Provider</a></li>
      </td>
    </tr>
  </tbody>
</table>

## Datatypen {#data-types}

In de volgende tabel worden de gegevenstypen weergegeven die volgens de [!DNL HL7 FHIR Release 5] -specificaties zijn gemaakt.

| Naam | Beschrijving |
| --- | --- |
| [[!UICONTROL Address]](./data-types/address.md) | Beschrijft een adres dat wordt uitgedrukt gebruikend postovereenkomsten (in tegenstelling tot GPS of andere formaten van de plaatsdefinitie). |
| [[!UICONTROL Annotation]](./data-types/annotation.md) | Een tekstknooppunt met kenmerk aan de auteur. |
| [[!UICONTROL Availability]](./data-types/availability.md) | Beschikbaarheidsgegevens voor een item. |
| [[!UICONTROL Codeable Concept]](./data-types/codeable-concept.md) | Een verwijzing van de ene bron naar de andere. |
| [[!UICONTROL Codeable Reference]](./data-types/codeable-reference.md) | Een verwijzing naar een bron of concept. |
| [[!UICONTROL Coding]](./data-types/coding.md) | Een verwijzing naar een code die wordt gedefinieerd door een terminologiesysteem. |
| [[!UICONTROL Contact Point]](./data-types/contact-point.md) | Contactgegevens van een persoon. |
| [[!UICONTROL Dosage]](./data-types/dosage.md) | Hoe wordt het geneesmiddel ingenomen of moet het worden gebruikt? |
| [[!UICONTROL Duration]](./data-types/duration.md) | Een tijdsduur. |
| [[!UICONTROL Extended Contact Details]](./data-types/extended-contact-detail.md) | Uitgebreide contactgegevens. |
| [[!UICONTROL Human Name]](./data-types/human-name.md) | Informatie over de naam van een menselijke of andere levende entiteit. |
| [[!UICONTROL Identifier]](./data-types/identifier.md) | Een id die is bedoeld voor berekeningen. |
| [[!UICONTROL Money]](./data-types/money.md) | Een bedrag aan economisch nut in een erkende valuta. |
| [[!UICONTROL Period]](./data-types/period.md) | Een tijdsperiode die wordt gedefinieerd door een begin- en einddatum/-tijd. |
| [[!UICONTROL Person]](./data-types/person.md) | Informatie over een generieke persoonrecord. |
| [[!UICONTROL Quantity]](./data-types/quantity.md) | Een gemeten of meetbare hoeveelheid. |
| [[!UICONTROL Range]](./data-types/range.md) | Een set waarden die worden gebonden door lage en hoge waarden. |
| [[!UICONTROL Ratio]](./data-types/ratio.md) | Een verhouding van twee [[!UICONTROL Quantity]](./data-types/quantity.md) -waarden via een teller en een noemer. |
| [[!UICONTROL Reference]](./data-types/reference.md) | Een verwijzing van de ene bron naar de andere. |
| [[!UICONTROL Repeat]](./data-types/repeat.md) | Een set regels die beschrijven wanneer een gebeurtenis gepland is. |
| [[!UICONTROL Simple Quantity]](./data-types/simple-quantity.md) | Een gemeten of meetbare hoeveelheid. |
| [[!UICONTROL Timing]](./data-types/timing.md) | Informatie over een gebeurtenis die meerdere keren kan plaatsvinden. |
| [[!UICONTROL Virtual Service Detail]](./data-types/virtual-service-detail.md) | Contactgegevens van de virtuele service. |
