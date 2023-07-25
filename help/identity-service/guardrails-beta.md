---
title: Guardrails voor Identity Service (met verwijderingslogica)
description: Meer informatie over hulplijnen voor identiteitsservice.
hide: true
hidefromtoc: true
source-git-commit: db8edbbc3ea5d8fcec3de95b9a37387bea493693
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 1%

---

# Guardrails voor [!DNL Identity Service] gegevens (met verwijderingslogica)

Dit document bevat informatie over het gebruik en de tarieflimieten voor [!DNL Identity Service] gegevens die u helpen het gebruik van de identiteitsgrafiek te optimaliseren. Bij het bekijken van de volgende instructies wordt aangenomen dat u de gegevens correct hebt gemodelleerd. Als u vragen hebt over het modelleren van uw gegevens, neemt u contact op met uw medewerker van de klantenservice.

## Aan de slag

De volgende diensten van het Experience Platform zijn betrokken bij het modelleren van de Gegevens van de Identiteit:

* [Identiteiten](home.md): Bridge-id&#39;s van verschillende gegevensbronnen die in het Platform worden opgenomen.
* [[!DNL Real-Time Customer Profile]](../profile/home.md): Maak geharmoniseerde consumentenprofielen met behulp van gegevens uit meerdere bronnen.

## Gegevensmodellimieten

In de onderstaande tabellen vindt u richtlijnen voor het gebruik van statische limieten en validatieregels voor naamruimten.

### Statische grenswaarden

In de volgende tabel worden de statische limieten weergegeven die worden toegepast op identiteitsgegevens.

| Guardrail | Limiet | Notities |
| --- | --- | --- |
| Aantal identiteiten in een grafiek [!BADGE Beta]{type=Informative} | 50 | Wanneer een grafiek met 50 verbonden identiteiten wordt bijgewerkt, zal de Dienst van de Identiteit een &quot;eerste-binnen, eerste-uit&quot;mechanisme toepassen en de oudste identiteit schrapt om ruimte voor de nieuwste identiteit te maken. Verwijderen is gebaseerd op het type identiteit en het tijdstempel. De limiet wordt toegepast op sandboxniveau. Lees de [aanhangsel](#appendix) voor meer informatie over hoe de Identiteitsdienst identiteiten schrapt zodra de grens wordt bereikt. |
| Aantal identiteiten in een XDM-record | 20 | Het minimum aantal vereiste XDM-records is twee. |
| Aantal aangepaste naamruimten | Geen | Het aantal aangepaste naamruimten dat u kunt maken, is niet beperkt. |
| Aantal grafieken | Geen | Het aantal identiteitsgrafieken dat u kunt maken, is niet beperkt. |
| Aantal tekens voor een naamruimte, weergavenaam of identiteitssymbool | Geen | Er zijn geen limieten aan het aantal tekens van een naamruimte, weergavenaam of identiteitssymbool. |

### Validatie van identiteitswaarden

In de volgende tabel worden de bestaande regels beschreven die u moet volgen om ervoor te zorgen dat uw identiteitswaarde correct wordt gevalideerd.

| Naamruimte | Validatieregel | Systeemgedrag wanneer regel wordt overtreden |
| --- | --- | --- |
| ECID | <ul><li>De identiteitswaarde van een ECID moet precies 38 tekens zijn.</li><li>De identiteitswaarde van een ECID mag alleen uit getallen bestaan.</li></ul> | <ul><li>Als de identiteitswaarde van ECID niet precies 38 tekens is, wordt de record overgeslagen.</li><li>Als de identiteitswaarde van ECID niet-numerieke tekens bevat, wordt de record overgeslagen.</li></ul> |
| Niet-ECID | De identiteitswaarde mag niet langer zijn dan 1024 tekens. | Als de identiteitswaarde meer dan 1024 tekens bevat, wordt de record overgeslagen. |

### Naamnaamruimte-opname

Vanaf 31 maart 2023 blokkeert Identity Service de inname van Adobe Analytics ID (AID) voor nieuwe klanten. Deze identiteit wordt doorgaans opgenomen via het dialoogvenster [Adobe Analytics-bron](../sources/connectors/adobe-applications/analytics.md) en de [Adobe Audience Manager-bron](../sources//connectors/adobe-applications/audience-manager.md) en is overbodig omdat de ECID dezelfde webbrowser vertegenwoordigt. Neem contact op met het Adobe-accountteam als u deze standaardconfiguratie wilt wijzigen.

## Volgende stappen

Zie de volgende documentatie voor meer informatie over [!DNL Identity Service]:

* [[!DNL Identity Service]-overzicht](home.md)
* [Naamgrafiekviewer](ui/identity-graph-viewer.md)

## Bijlage {#appendix}

Het volgende gedeelte bevat aanvullende informatie over instructies voor identiteitsdienst.

### [!BADGE Beta]{type=Informative} Begrijpen met de verwijderingslogica wanneer een identiteitsgrafiek met capaciteit wordt bijgewerkt {#deletion-logic}

Wanneer een volledige identiteitsgrafiek wordt bijgewerkt, schrapt de Dienst van de Identiteit de oudste identiteit in de grafiek alvorens de recentste identiteit toe te voegen. Dit is om de juistheid en relevantie van identiteitsgegevens te behouden. Dit proces van schrapping volgt twee primaire regels:

#### Regel 1 schrapping wordt geprioriteerd gebaseerd op het identiteitstype van een namespace

De schrappingsprioriteit is als volgt:

1. Cookie-id
2. Apparaat-id
3. Apparaatoverschrijdende id, e-mail en telefoon

#### Regel nr. 2 schrapping is gebaseerd op timestamp die op de identiteit wordt opgeslagen

Elke identiteit die in een grafiek is gekoppeld, heeft een eigen corresponderende tijdstempel. Wanneer een volledige grafiek wordt bijgewerkt, verwijdert Identiteitsservice de identiteit met de oudste tijdstempel.

Wanneer een volledige grafiek met een nieuwe identiteit wordt bijgewerkt, werken deze twee regels samen om aan te geven welke oudere identiteit wordt verwijderd. De Dienst van de identiteit schrapt eerst de oudste identiteitskaart van het Koekje, dan de oudste identiteitskaart van het Apparaat, en tenslotte de oudste identiteitskaart van het dwars-Apparaat/E-mail/Telefoon.

>[!NOTE]
>
>Als de identiteit die u wilt verwijderen aan meerdere andere identiteiten in de grafiek is gekoppeld, worden de koppelingen die deze identiteit verbinden ook verwijderd.

In het onderstaande voorbeeld moet Identity Service, voordat de grafiek aan de linkerkant kan worden bijgewerkt met een nieuwe identiteit, eerst de bestaande identiteit verwijderen met de oudste tijdstempel. Nochtans, omdat de oudste identiteit een apparatenidentiteitskaart is, slaat de Dienst van de Identiteit die identiteit over tot het aan namespace met een type krijgt dat hoger op de schrappingspriorlijst is, die in dit geval is `ecid-3`. Zodra de oudste identiteit met een hoger type van schrappingsprioriteit wordt verwijderd, wordt de grafiek dan bijgewerkt met een nieuwe verbinding, `ecid-51`.

>[!NOTE]
>
>In het zeldzame geval dat er twee identiteiten met het zelfde timestamp en identiteitstype zijn, zal de Dienst van de Identiteit de IDs sorteren die op XID en gedragsschrapping wordt gebaseerd.

![Een voorbeeld van de oudste identiteit die wordt geschrapt om de recentste identiteit aan te passen](./images/graph-limits-v3.png)