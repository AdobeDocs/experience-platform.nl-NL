---
title: Voorbeeld van scenario's voor klanten die zijn opgelost door regels voor identiteitsgrafiekkoppeling
description: Leer over de scenario's van de voorbeeldklant die door identiteitsgrafiek die regels verbinden worden opgelost.
badge: Beta
exl-id: bccd5b7a-3836-47d8-b976-51747b9c1803
source-git-commit: be6fdb7e23ed4769ab4ee7ef72532296f020f4a4
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# Voorbeeld van klantscenario&#39;s die worden opgelost door regels voor identiteitsgrafiek koppelen

>[!AVAILABILITY]
>
>Deze functie is nog niet beschikbaar. Het bètaprogramma voor koppelingsregels voor identiteitsgrafieken zal naar verwachting in juli van start gaan voor ontwikkelingssandboxen. Neem contact op met het accountteam van de Adobe voor meer informatie over de deelnemingscriteria.

Dit document schetst voorbeeldscenario&#39;s die u kunt overwegen wanneer het vormen van identiteitsgrafiek die regels verbindt.

## Gedeeld apparaat

Er zijn gevallen waarin meerdere aanmeldingen op één apparaat kunnen plaatsvinden:

| Gedeeld apparaat | Beschrijving |
| --- | --- |
| Familiecomputers en -tablets | Echtgenoot en echtgenote melden zich beide aan bij hun bankrekening. |
| Openbare kiosk | Reizigers op een luchthaven melden zich aan met hun loyaliteitsidentiteitskaart om zakken in te checken en instapkaarten af te drukken. |
| Bellen | Het personeel van het centrum van de vraag login op één enkel apparaat namens klanten die klantensteun roepen om kwesties op te lossen. |

![ delen-apparaten ](../images/identity-settings/shared-devices.png)

In deze gevallen, vanuit grafiekstandpunt, zonder toegelaten grenzen, zal één enkele ECID met veelvoudige CRMIDs worden verbonden.

Met de regels voor identiteitsgrafieken kunt u:

* Vorm identiteitskaart die voor login als uniek herkenningsteken wordt gebruikt. U kunt bijvoorbeeld een grafiek beperken tot het opslaan van slechts één identiteit met een CRMID-naamruimte en zo die CRMID definiëren als de unieke id van een gedeeld apparaat.
   * Op deze manier kunt u ervoor zorgen dat CRMID&#39;s niet worden samengevoegd met de ECID.

## Ongeldige scenario&#39;s voor e-mail/telefoon

Er zijn ook instanties van gebruikers die valse waarden als telefoonaantallen en/of e-mailadressen verstrekken wanneer het registreren. In deze gevallen, als de grenzen niet worden toegelaten, dan zal telefoon/e-mail verwante identiteiten uiteindelijk worden verbonden met veelvoudige verschillende CRMIDs.

![ ongeldig-e-mail-telefoon ](../images/identity-settings/invalid-email-phone.png)

Met de regels voor identiteitsgrafieken kunt u:

* Configureer de CRMID, het telefoonnummer of het e-mailadres als de unieke id en beperkt zo één persoon tot slechts één CRMID, telefoonnummer en/of e-mailadres dat aan zijn account is gekoppeld.

## Onjuiste of onjuiste identiteitswaarden

Er zijn gevallen waarin niet-unieke, onjuiste identiteitswaarden in het systeem worden opgenomen, ongeacht de naamruimte. Voorbeelden zijn:

* IDFA-naamruimte met de identiteitswaarde &quot;user_null&quot;.
   * IDFA-identiteitswaarden moeten uit 36 tekens bestaan: 32 alfanumerieke tekens en vier afbreekstreepjes.
* Naamruimte voor telefoonnummers met de identiteitswaarde &quot;not-specified&quot;.
   * Telefoonnummers mogen geen alfabet bevatten.

Deze identiteiten zouden in de volgende grafieken kunnen resulteren, waar veelvoudige CRMIDs samen met de &quot;slechte&quot;identiteit worden samengevoegd:

![ slecht-gegevens ](../images/identity-settings/bad-data.png)

Met identiteitsgrafiek die regels verbindt kunt u CRMID als unieke herkenningsteken vormen om ongewenste profiel te verhinderen die als gevolg van dit type gegevens ineenstorten.

## Volgende stappen

Lees de volgende documentatie voor meer informatie over koppelingsregels voor identiteitsgrafieken:

* [Overzicht van regels voor identiteitsgrafiek](./overview.md)
* [Algoritme voor identiteitsoptimalisatie](./identity-optimization-algorithm.md)
* [Identiteitsservice en realtime klantprofiel](../identity-and-profile.md)
* [Logica voor identiteitskoppeling](../features/identity-linking-logic.md)
