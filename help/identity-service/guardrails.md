---
keywords: Experience Platform;identiteit;identiteitsdienst;het oplossen van problemen;gidsen;richtlijnen;grens;
title: Guardrails voor identiteitsservice
description: Dit document bevat informatie over het gebruik en de tarieflimieten voor identiteitsservicegegevens, zodat u de identiteitsgrafiek optimaal kunt gebruiken.
exl-id: bd86d8bf-53fd-4d76-ad01-da473a1999ab
source-git-commit: b07a45e5bb9cae6e147ea790ebb77cb63f8790c1
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 2%

---

# Guardrails voor [!DNL Identity Service] data

Dit document bevat informatie over het gebruik en de tarieflimieten voor [!DNL Identity Service] gegevens die u helpen het gebruik van de identiteitsgrafiek te optimaliseren. Bij het bekijken van de volgende instructies wordt aangenomen dat u de gegevens correct hebt gemodelleerd. Als u vragen hebt over het modelleren van uw gegevens, neemt u contact op met uw medewerker van de klantenservice.

## Aan de slag

De volgende diensten van het Experience Platform zijn betrokken bij het modelleren van de Gegevens van de Identiteit:

* [Identiteiten](home.md): De identiteiten van de brug van ongelijksoortige gegevensbronnen aangezien zij in Platform worden opgenomen.
* [[!DNL Real-time Customer Profile]](../profile/home.md): Uniforme consumentenprofielen maken met gegevens uit meerdere bronnen.

## Gegevensmodellimieten

In de onderstaande tabellen vindt u richtlijnen voor het gebruik van statische limieten en validatieregels voor naamruimten.

### Statische grenswaarden

In de volgende tabel worden de statische limieten weergegeven die worden toegepast op identiteitsgegevens.

| Guardrail | Limiet | Notities |
| --- | --- | --- |
| Aantal identiteiten in een grafiek | 150 | De limiet wordt toegepast op sandboxniveau. De identiteitsgrafiek wordt niet bijgewerkt wanneer de limiet is bereikt. |
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

## Volgende stappen

Zie de volgende documentatie voor meer informatie over [!DNL Identity Service]:

* [[!DNL Identity Service] - overzicht](home.md)
* [Identiteitsgrafiekviewer](ui/identity-graph-viewer.md)
