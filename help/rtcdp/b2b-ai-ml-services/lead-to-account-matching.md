---
title: Lood-aan-rekening matching in Real-Time CDP B2B
type: Documentation
description: Een overzicht en meer informatie over de lead to account matching feature in Experience Platform CDP B2B.
feature: Get Started, Profiles, B2B
badgeB2B: label="B2B Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 2f853599-6bca-4ba6-bbba-131a49d8854e
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 0%

---

# Lood-aan-rekening matching in Real-Time CDP B2B

## Overzicht {#overview}

Op account gebaseerde marketing is een steeds belangrijker strategie voor B2B marketing. Op account gebaseerde marketing biedt de volgende belangrijke voordelen om specifieke klanten met een hoge waarde aan te schaffen:

- ROI wissen
- Afstemming van verkoop en marketing
- Een gepersonaliseerde aanpak
- Minder verspilde bronnen
- Een kortere verkoopcyclus

Op accounts gebaseerde marketing biedt de mogelijkheid om bekende personen en anonieme webbezoekers te koppelen aan verkoopaccounts. Dit staat marketing teams toe om met potentiële leiders van de doelrekeningen vroeg in de klantenreis in dienst te nemen om hun kansen op omzetting te verhogen. Een bekende persoonrecord bevat doorgaans de volgende informatie of een deel ervan:

- Naam persoon
- E-mailadres
- Contactnummer
- Bedrijfsnaam
- Website van bedrijf
- Functie
- Locatie

Met Aanpassen aan account kunt u profielen van bekende personen toevoegen aan accountprofielen. U kunt gegevens dan segmenteren en richten in een context B2B zoals rekeningen, kansen, etc. De profielen van personen kunnen in de volgende drie categorieën worden ingedeeld:

- **het profiel van de persoon van de Rekening:** het persoonsprofiel wordt reeds geassocieerd aan minstens één rekeningsprofiel door de verhouding van een gegevensbron. Dit betekent dat er ten minste één contactfragment is.

>[!NOTE]
>
> Profielen van accountpersonen komen niet overeen wanneer het uitvoeren leidt tot overeenkomstige taken.

- **Bekend persoonprofiel:** het personenprofiel wordt NIET geassocieerd aan om het even welk rekeningsprofiel, en minstens één van de volgende attributen van het persoonprofiel heeft een waarde:

   - E-mailadres
   - Bedrijfsnaam
   - Website van bedrijf

- **Anoniem persoonsprofiel:** het personenprofiel wordt NIET geassocieerd aan om het even welk rekeningsprofiel, en geen van de volgende attributen van het persoonprofiel heeft een waarde:

   - E-mailadres
   - Bedrijfsnaam
   - Website van bedrijf

>[!NOTE]
>
> Een persoonsprofiel kan gerelateerd zijn aan meerdere accountprofielen. De procedure voor het afleiden naar account komt echter alleen overeen met de beste overeenkomst. Als een bredere reeks overeenkomsten vereist is, koppelt u de leiding aan account die overeenkomt met de bijbehorende accountfunctie.

## Werking {#how-it-works}

Dagelijkse banen gebruiken zowel deterministische als probabilistische factoren om bekende hoofdprofielen zonder bestaande accountverenigingen met elkaar in overeenstemming te brengen. Bekende lead-profielen beschikken over een van de volgende kenmerken:

- b2b.companyName
- b2b.companyWebsite
- workEmail

>[!NOTE]
>
> Het kenmerk b2b.personKey.sourceKey moet bestaan.

De attributen b2b.companyName, b2b.companyWebsite en b2b.personKey.sourceKey kunnen in de b2b gebiedsgroep in het B2B persoonschema worden gevestigd.

![ B2B persoonschema dat attributen ](/help/rtcdp/accounts/images/b2b-person-schema.png) toont

Het kenmerk workEmail kan worden gevonden als veldgroep op hoofdniveau in het B2B-personenschema.

![ B2B persoonschema dat workEmail ](/help/rtcdp/accounts/images/b2b-person-workemail.png) toont

Profielen kunnen alleen het beste worden gevonden als de overeenkomende score een interne betrouwbaarheidsdrempel overschrijdt. De resultaten worden bewaard in een nieuwe systeemdataset van de bestaande relatie XDM van de rekeningspersoon.

De lead to account matching service run when a new person profile snapshot which is once om de 24 uur. Zie de documentatie voor meer informatie over de [ configuratie van lood aan rekening aanpassing ](/help/rtcdp/accounts/account-profile-ui-guide.md).

## Hoe kan ik leiden tot een overeenkomende uitvoer van een account {#how-to-view}

Nadat de baan in werking wordt gesteld, worden de resultaten bewaard in een nieuwe dataset van de bestaande relatie XDM van de rekeningspersoon.

Selecteer **[!UICONTROL Preview dataset]** in de rechterbovenhoek om een voorvertoning van de gegevensset weer te geven.

![ Nieuwe dataset ](/help/rtcdp/accounts/images/b2b-dataset-output.png)

De dataset omvat de aangepaste rekeningsinformatie evenals de overeenkomende score voor uw gekozen dataset. In het veld **[!UICONTROL Relationship Source]** wordt aangegeven of het afkomstig is van het proces voor afstemmen van accounts.

![ de vertrouwensscores en output van de dataset van de Voorproef ](/help/rtcdp/accounts/images/b2b-dataset-preview.png)

## Monitoring leidt tot het afstemmen van accounts {#monitoring-jobs}

U kunt de taakstatus en de bijbehorende metriek controleren voor elke lead in taken die overeenkomen met een account via het dashboard.

Zie de documentatie voor meer informatie over [ controletaken voor lood aan rekening aanpassing ](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).
