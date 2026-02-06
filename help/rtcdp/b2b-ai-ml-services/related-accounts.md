---
title: Verwante accounts in Real-Time CDP B2B edition
type: Documentation
description: Een overzicht en meer informatie over de bijbehorende accounts vindt u in Experience Platform Real-Time CDP B2B.
feature: Get Started, Profiles, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html#rtcdp-editions" newtab=true
exl-id: 37fd2cdb-87c0-4e5e-9599-ad4f397f7c28
source-git-commit: 5998adf98aa7250864983d7e4e629921633e1a1c
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 2%

---

# Verwante accounts in Real-Time CDP B2B edition

## Overzicht {#overview}

B2B-ondernemingen hebben vaak hun klantgegevens opgeslagen in meerdere systemen, elk met inbegrip van slechts gedeeltelijke of zelfs conflicterende gegevens voor dezelfde reële bedrijfsentiteit. Dit zorgt voor een enorme uitdaging om tot een accuraat beeld van hun klanten te komen, waardoor de efficiëntie en effectiviteit van hun B2B-marketing- en -verkoopinspanningen afnemen.

| ID | Naam | Website | Industrie | Staat | Telefoon | Heeft open mogelijkheid met bedrag > `$1 million` |
|---|---|---|---|---|---|---|
| 1 | Acme | acme.com | Software | CA | (408)536-6000 |   |
| 2 | Acme | acm.com | Software | CA | 4085366000 | x |
| 3 | Acme Inc |   |   | CA | (408)5366000 |   |
| 4 | Accme Consulting Service | `http://www.acme.com/consulting` | Technologisch advies | NY | (212)471-0904 | x |
| 5 | IT benaderen |   |   | CA |   |   |

{style="table-layout:auto"}

Met verwante accounts geeft [!DNL Real-Time CDP B2B] nu een lijst weer met accounts die lijken op de account waarin u bladert.

![ het Scherm dat Verwante rekeningen in Experience Platform UI toont.](/help/rtcdp/b2b-ai-ml-services/assets/related-accounts-in-ui.png)

Met deze functie kunt u verwante accountprofielen voor een accountprofiel bekijken in de gebruikersinterface van Experience Platform. Vervolgens neemt u de verwante accounts op in uw segmentdefinities om uw bereik te vergroten of bredere criteria toe te passen bij uw publiek.

## De verwante accountservice inschakelen {#enable}

Als u de service wilt inschakelen, selecteert u **[!UICONTROL Profiles]** in het zijpaneel gevolgd door **[!UICONTROL Settings]** .

![ Experience Platform UI die profielen en montages benadrukt.](../assets/../b2b-ai-ml-services/assets/related-account-settings.png)

Selecteer de schakeloptie naast [!UICONTROL Enable related accounts] om de service in te schakelen en selecteer vervolgens **[!UICONTROL Save]** .

![ het scherm van de montages van de Rekening het benadrukken van knevel en sparen.](../assets/../b2b-ai-ml-services/assets/related-account-toggle.png)

## Werking {#how-it-works}

Taken voor het dagelijks leren van machines gebruiken een hiërarchisch algoritme om vergelijkbare accountprofielen in groepen te groeperen op basis van drie factoren:

* Koppeling bovenliggende account
* Webdomein
* Accountnaam

Na een geslaagde verwerkingstaak wordt elk lid van de accountprofielgroep gelabeld met de lijst Verwante accounts. U kunt de lijst in de **Verwante Rekeningen** tabel van de pagina van het Profiel van de Rekening bekijken, en de verwante rekeningen in segmentdefinities gebruiken.

Zie de documentatie voor meer informatie over de [ profielverrijking verwante rekeningenbanen ](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).

## Verwante accounts bekijken {#how-to-view}

U kunt verwante accounts bekijken voor een account waarin u bladert in de gebruikersinterface van Experience Platform.

Zie de documentatie voor meer informatie over [ hoe te om verwante rekeningen in UI ](/help/rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab) te vinden.

## Hoe u verwante accounts kunt gebruiken {#how-to-use}

U kunt accounts en verwante accounts segmenteren. Het besluit om verwante rekeningen in uw segmentdefinities te gebruiken hangt van uw marketing gebruiksgeval af. U kunt bijvoorbeeld verwante accounts gebruiken voor marketing- of advertentiecampagnes waarin u een lagere nauwkeurigheid accepteert in ruil voor een groter bereik.

Zie a [ segmentatievoorbeeld ](/help/rtcdp/segmentation/b2b.md#related-accounts) dat verwante rekeningen gebruikt.
