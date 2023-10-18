---
title: Voorbeeldscenario's voor het configureren van identiteitsinstellingen
description: Leer over voorbeeldscenario's voor het vormen van de Montages van de Identiteit.
hide: true
hidefromtoc: true
badge: Alfa
source-git-commit: 03e4cd440f8627ad837a31e1c017d0b824cafb04
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---

# Voorbeeldscenario&#39;s voor het configureren van identiteitsgrafiek-koppelingsregels

>[!IMPORTANT]
>
>Identiteitsgrafiekkoppelingsregels zijn momenteel in Alpha. De functie en documentatie kunnen worden gewijzigd.

Dit document schetst voorbeeldscenario&#39;s die u kunt overwegen wanneer het vormen van identiteitsgrafiek die regels verbindt.

## Gedeeld apparaat

Er zijn gevallen waarin meerdere aanmeldingen op één apparaat kunnen plaatsvinden:

| Gedeeld apparaat | Beschrijving |
| --- | --- |
| Familiecomputers en -tablets | Echtgenoot en echtgenote melden zich beide aan bij hun bankrekening. |
| Openbare kiosk | Reizigers op een luchthaven melden zich aan met hun loyaliteitsidentiteitskaart om zakken in te checken en instapkaarten af te drukken. |
| Bellen | Het personeel van het centrum van de vraag login op één enkel apparaat namens klanten die klantensteun roepen om kwesties op te lossen. |

![gezamenlijke apparaten](../images/identity-settings/shared-devices.png)

In deze gevallen, vanuit een grafiekstandpunt, zonder toegelaten grenzen, zal één enkele ECID met veelvoudige CRM IDs worden verbonden.

Met de regels voor identiteitsgrafieken kunt u:

* Vorm identiteitskaart die voor login als uniek herkenningsteken wordt gebruikt. Bijvoorbeeld, kunt u een grafiek beperken om enkel één identiteit met een identiteitskaart van CRM op te slaan namespace, en zo die identiteitskaart van CRM als unieke herkenningsteken van een gedeeld apparaat te bepalen.
   * Op deze manier kunt u ervoor zorgen dat CRM-id&#39;s niet worden samengevoegd met de ECID.

## Ongeldige scenario&#39;s voor e-mail/telefoon

Er zijn ook instanties van gebruikers die valse waarden als telefoonaantallen en/of e-mailadressen verstrekken wanneer het registreren. In deze gevallen, als de grenzen niet worden toegelaten, dan zal telefoon/e-mail verwante identiteiten uiteindelijk worden verbonden met veelvoudige verschillende CRM IDs.

![invalid-email-phone](../images/identity-settings/invalid-email-phone.png)

Met de regels voor identiteitsgrafieken kunt u:

* Vorm of identiteitskaart van CRM, telefoonaantal, of e-mailadres als unieke herkenningsteken en beperkt zo één persoon tot enkel identiteitskaart van CRM, telefoonaantal, en/of e-mailadres verbonden aan hun rekening.

## Onjuiste of onjuiste identiteitswaarden

Er zijn gevallen waarin niet-unieke, onjuiste identiteitswaarden in het systeem worden opgenomen, ongeacht de naamruimte. Voorbeelden zijn:

* IDFA-naamruimte met de identiteitswaarde &quot;user_null&quot;.
   * IDFA-identiteitswaarden moeten uit 36 tekens bestaan: 32 alfanumerieke tekens en vier afbreekstreepjes.
* Naamruimte voor telefoonnummers met de identiteitswaarde &quot;not-specified&quot;.
   * Telefoonnummers mogen geen alfabet bevatten.

Deze identiteiten kunnen resulteren in de volgende grafieken, waarbij meerdere CRM-id&#39;s samen met de &#39;slechte&#39; identiteit worden samengevoegd:

![ongeldige gegevens](../images/identity-settings/bad-data.png)

Met de verbindingsregels van de identiteitsgrafiek kunt u identiteitskaart van CRM als unieke herkenningsteken vormen om ongewenste profiel te verhinderen die als gevolg van dit type van gegevens ineenstorten.

## Volgende stappen

Lees de volgende documentatie voor meer informatie over koppelingsregels voor identiteitsgrafieken:

* [Overzicht van regels voor identiteitsgrafiek](./overview.md)
* [Identiteitsservice en realtime klantprofiel](identity-and-profile.md)
* [Logica voor identiteitskoppeling](./identity-linking-logic.md)