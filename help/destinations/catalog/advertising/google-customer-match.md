---
keywords: Google-klantovereenkomst;Google-klantovereenkomst;Google-klantovereenkomst
title: Google Customer Match-verbinding
description: Met Google Customer Match kunt u uw online- en offline gegevens gebruiken om uw klanten te bereiken en opnieuw contact op te nemen met andere eigendommen van Google, zoals Zoeken, Winkelen, Gmail en YouTube.
exl-id: 8209b5eb-b05c-4ef7-9fdc-22a528d5f020
translation-type: tm+mt
source-git-commit: 95ca7112d1f2655bf33e8a1c549e886ced244a5d
workflow-type: tm+mt
source-wordcount: '1574'
ht-degree: 0%

---

# [!DNL Google Customer Match] verbinding

## Overzicht {#overview}

[Met Google Customer ](https://support.google.com/google-ads/answer/6379332?hl=en) Matchlets kunt u uw online- en offline-gegevens gebruiken om uw klanten te bereiken en opnieuw contact op te nemen met andere klanten over de eigendommen en gebruiksmogelijkheden van Google, zoals:  [!DNL Search],  [!DNL Shopping],  [!DNL Gmail]en  [!DNL YouTube].

![Google Customer Match-bestemming in Adobe Experience Platform-gebruikersinterface](../../assets/catalog/advertising/google-customer-match/catalog.png)

## Gebruiksscenario’s

Om u beter te helpen begrijpen hoe en wanneer om de [!DNL Google Customer Match] bestemming te gebruiken, zijn hier voorbeelden van gebruiksgevallen die de klanten van Adobe Experience Platform door deze eigenschap kunnen oplossen.

### Hoofdletters gebruiken #1

Een atletisch merkje wil bestaande klanten bereiken via [!DNL Google Search] en [!DNL Google Shopping] om aanbiedingen en objecten aan te passen op basis van hun eerdere aankopen en browsergeschiedenis. Het merk apparel kan e-mailadressen van hun eigen CRM aan Experience Platform opnemen, en segmenten van hun eigen off-line gegevens bouwen. Vervolgens kunnen ze deze segmenten naar [!DNL Google Customer Match] sturen om te worden gebruikt tussen [!DNL Search] en [!DNL Shopping], zodat hun advertentiepatroon wordt geoptimaliseerd.

### Hoofdletters gebruiken #2

Een vooraanstaande technologiebedrijf lanceerde een nieuwe telefoon. Om dit nieuwe telefoonmodel te bevorderen, kijken zij om bewustzijn van de nieuwe eigenschappen en de functionaliteit van de telefoon aan klanten te drijven die vorige modellen van hun telefoons bezitten.

Om de versie te promoten, uploaden zij e-mailadressen van hun gegevensbestand van CRM in Experience Platform, gebruikend de e-mailadressen als herkenningstekens. De segmenten worden gecreeerd gebaseerd op klanten die oudere telefoonmodellen bezitten. Vervolgens worden segmenten verzonden naar [!DNL Google Customer Match], zodat het bedrijf zich kan richten op huidige klanten, klanten die eigenaar zijn van oudere telefoonmodellen en vergelijkbare klanten op [!DNL YouTube].

## Gegevensbeheer voor [!DNL Google Customer Match] doelen {#data-governance}

Sommige bestemmingen in Experience Platform hebben bepaalde regels en verplichtingen voor gegevens die worden verzonden naar of ontvangen van het bestemmingsplatform. U bent verantwoordelijk voor het begrijpen van de beperkingen en verplichtingen van uw gegevens en hoe u die gegevens gebruikt in Adobe Experience Platform en het doelplatform. Adobe Experience Platform biedt tools voor gegevensbeheer om u te helpen bij het beheren van een aantal van deze gegevensgebruiksverplichtingen. [Meer informatie ](../../..//data-governance/labels/overview.md) over tools en beleid voor gegevensbeheer.

## Ondersteunde identiteiten {#supported-identities}

[!DNL Google Customer Match] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](/help/identity-service/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| GAID | Google-advertentie-id | Selecteer deze doelidentiteit wanneer uw bronidentiteit een GAID-naamruimte is. |
| IDFA | Apple ID for Advertisers | Selecteer deze doelidentiteit wanneer uw bronidentiteit een IDFA-naamruimte is. |
| phone_sha256_e.164 | Telefoonnummers in E164-indeling, gehasht met het SHA256-algoritme | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-telefoonnummers. Volg de instructies in de [ID passende vereisten](#id-matching-requirements-id-matching-requirements) sectie en gebruik aangewezen namespaces voor gewone teksten en haktige telefoonaantallen, respectievelijk. Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in om [!DNL Platform] de gegevens automatisch te laten hashen bij activering. |
| email_lc_sha256 | E-mailadressen die met het algoritme SHA256 worden gehasht | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-e-mailadressen met hashing. Volg de instructies in de [sectie Identiteitsaanpassing ](#id-matching-requirements-id-matching-requirements) en gebruik aangewezen namespaces voor gewone teksten en gehakt e-mailadressen, respectievelijk. Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in om [!DNL Platform] de gegevens automatisch te laten hashen bij activering. |
| user_id | Aangepaste gebruikers-id&#39;s | Selecteer deze doelidentiteit wanneer uw bronidentiteit een aangepaste naamruimte is. |

## Type exporteren {#export-type}

**De Uitvoer**  van het segment - u exporteert alle leden van een segment (publiek) met de herkenningstekens (naam, telefoonaantal, en anderen) die in de  [!DNL Google Customer Match] bestemming worden gebruikt.

## [!DNL Google Customer Match] accountvereisten  {#google-account-prerequisites}

Voordat u een [!DNL Google Customer Match]-bestemming in Experience Platform instelt, moet u het Google-beleid voor het gebruik van [!DNL Customer Match] lezen en volgen. Dit wordt beschreven in de [Google-ondersteuningsdocumentatie](https://support.google.com/google-ads/answer/6299717).

### Lijst van gewenste personen {#allowlist}

>[!NOTE]
>
>U moet de eerste [!DNL Google Customer Match]-bestemming in het Experience Platform eerst aan de lijst van gewenste personen van Google toevoegen. Controleer of Google het hieronder beschreven lijst van gewenste personen-proces heeft voltooid voordat u een bestemming maakt.

Voordat u de [!DNL Google Customer Match]-bestemming in Experience Platform maakt, moet u contact opnemen met Google en de instructies voor de lijst van gewenste personen volgen in [Customer Match partners gebruiken om uw gegevens te uploaden](https://support.google.com/google-ads/answer/7361372?hl=en&amp;ref_topic=6296507) in de Google-documentatie.

Er is ook een tweede Google-lijst van gewenste personen waaraan u uw account moet toevoegen als u gegevens wilt uploaden met de [Gebruikersnaam](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id) van Google. Neem contact op met uw Google-accountmanager om uw account aan de lijst van gewenste personen toe te voegen.

## Overeenkomende vereisten {#id-matching-requirements}

[!DNL Google] vereist dat er geen duidelijk identificeerbare informatie (PII) wordt verstrekt. Daarom kan het publiek dat aan [!DNL Google Customer Match] wordt geactiveerd *hashed* herkenningstekens, zoals e-mailadressen of telefoonaantallen worden afgevinkt.

Afhankelijk van het type id&#39;s dat u in Adobe Experience Platform invoert, moet u aan de desbetreffende vereisten voldoen.

## Vereisten voor hashing voor telefoonnummers {#phone-number-hashing-requirements}

Er zijn twee methodes om telefoonaantallen in [!DNL Google Customer Match] te activeren:

* **Onbewerkte telefoonnummers** worden geïnstalleerd: u kunt onbewerkte telefoonnummers in de  [!DNL E.164] notatie invoeren in  [!DNL Platform]en deze worden automatisch gehasht bij activering. Als u deze optie kiest, zorg ervoor om uw ruwe telefoonaantallen in `Phone_E.164` namespace altijd in te nemen.
* **Hashed-telefoonnummers** invoegen: U kunt uw telefoonaantallen pre-hash alvorens in te gaan  [!DNL Platform]. Als u deze optie kiest, zorg ervoor om uw gehakt telefoonaantallen in `PHONE_SHA256_E.164` namespace altijd in te nemen.

>[!NOTE]
>
>Telefoonnummers die worden ingevoerd in de naamruimte `Phone` kunnen niet worden geactiveerd in [!DNL Google Customer Match].

## Vereisten voor e-mailhashing {#hashing-requirements}

U kunt e-mailadressen hashen alvorens hen in Adobe Experience Platform op te nemen, of e-mailadressen gebruiken duidelijk in Experience Platform, en hebben [!DNL Platform] hen op activering hakt.

Raadpleeg de volgende secties in de documentatie van Google voor meer informatie over de hashing-vereisten van Google en andere activeringsbeperkingen:

* [[!DNL Customer Match] met e-mailadres, adres of gebruikersnaam](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] overwegingen](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_considerations)
* [Klanten komen overeen met telefoonnummer](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_phone_number)
* [Klanten komen overeen met mobiele apparaat-id&#39;s](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_mobile_device_ids)


Als u meer wilt weten over het invoeren van e-mailadressen in Experience Platform, raadpleegt u het [batchoverzicht](../../../ingestion/batch-ingestion/overview.md) en het [streamingoverzicht](../../../ingestion/streaming-ingestion/overview.md).

Als u ervoor kiest om de e-mailadressen zelf te hashen, moet u voldoen aan de vereisten van Google, zoals beschreven in de koppelingen hierboven.

## Aangepaste naamruimten gebruiken {#custom-namespaces}

Voordat u de naamruimte `User_ID` kunt gebruiken om gegevens naar Google te verzenden, moet u uw eigen id&#39;s eerst synchroniseren met [!DNL gTag]. Raadpleeg de [officiële documentatie van Google](https://support.google.com/google-ads/answer/9199250) voor meer informatie.

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

## Vorm bestemming - videoanalyse {#video}

In de onderstaande video ziet u de stappen voor het configureren van een [!DNL Google Customer Match]-bestemming en het activeren van segmenten. De stappen worden ook achtereenvolgens beschreven in de volgende secties.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

## Verbinden met doel {#connect-destination}

Blader in **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** naar de categorie **[!UICONTROL Advertising]**. Selecteer [!DNL Google Customer Match] en selecteer **[!UICONTROL Configure]**.

![Verbinding maken met Google Customer Match-doel](../../assets/catalog/advertising/google-customer-match/connect.png)

>[!NOTE]
>
>Als een verbinding met deze bestemming bestaat, kunt u een **[!UICONTROL Activate]** knoop op de bestemmingskaart zien. Raadpleeg voor meer informatie over het verschil tussen **[!UICONTROL Activate]** en **[!UICONTROL Configure]** de sectie [Catalog](../../ui/destinations-workspace.md#catalog) van de documentatie van de doelwerkruimte.

Als u in de stap **Account** eerder een verbinding met uw [!DNL Google Customer Match]-doel hebt ingesteld, selecteert u **[!UICONTROL Existing Account]** en selecteert u de bestaande verbinding. U kunt ook **[!UICONTROL New Account]** selecteren om een nieuwe verbinding in te stellen met [!DNL Google Customer Match]. Als u zich wilt aanmelden en Adobe Experience Cloud wilt verbinden met uw [!DNL Google Ad]-account, selecteert u **[!UICONTROL Connect to destination]**.

>[!NOTE]
>
>Experience Platform ondersteunt validatie van referenties in het verificatieproces. Er wordt een foutbericht weergegeven als u onjuiste gegevens hebt ingevoerd voor uw [!DNL Google Ad]-account, om ervoor te zorgen dat u de workflow niet met onjuiste gegevens voltooit.

![Verbinden met Google Customer Match-bestemming - verificatiestap](../../assets/catalog/advertising/google-customer-match/connection.png)

Nadat uw referenties zijn bevestigd en Adobe Experience Cloud is verbonden met uw Google-account, kunt u **[!UICONTROL Next]** selecteren om door te gaan naar de stap **[!UICONTROL Authentication]**.

![Credentials bevestigd](../../assets/catalog/advertising/google-customer-match/connection-success.png)

Voer in de stap **[!UICONTROL Authentication]** een **[!UICONTROL Name]** en een **[!UICONTROL Description]** in voor uw activeringsstroom en vul uw Google **[!UICONTROL Account ID]** in.

In deze stap, kunt u om het even welke **[!UICONTROL Marketing actions]** selecteren die op deze bestemming van toepassing zijn. Marketingsacties geven de intentie aan waarvoor de gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door Adobe gedefinieerde marketingacties of u kunt uw eigen marketingactie maken. Voor meer informatie over marketing acties, zie [Overzicht van het beleid van het gebruik van Gegevens](../../../data-governance/policies/overview.md).

Selecteer **[!UICONTROL Create Destination]** nadat u de bovenstaande velden hebt ingevuld.

>[!IMPORTANT]
>
> * De marketingactie **[!UICONTROL Combine with PII]** is standaard geselecteerd voor het doel [!DNL Google Customer Match] en kan niet worden verwijderd.
> * Voor [!DNL Google Customer Match] doelen. **[!UICONTROL Account ID]** is uw klant-id met Google. De indeling van de id is xxx-xxx-xxxx.


![Google-klantovereenkomst aansluiten - verificatiestap](../../assets/catalog/advertising/google-customer-match/authentication.png)

Uw doel is nu gemaakt. U kunt **[!UICONTROL Save & Exit]** selecteren als u segmenten later wilt activeren of u kunt **[!UICONTROL Next]** selecteren om de workflow voort te zetten en segmenten te selecteren om te activeren. In beide gevallen, zie de volgende sectie, [Activate segmenten aan  [!DNL Google Customer Match]](#activate-segments), voor de rest van het werkschema.

## Segmenten activeren naar [!DNL Google Customer Match] {#activate-segments}

Zie [Gegevens naar doelen activeren](../../ui/activate-destinations.md) voor instructies over het activeren van segmenten naar [!DNL Google Customer Match].


In de stap **[!UICONTROL Segment schedule]** moet u [!UICONTROL App ID] verstrekken wanneer het verzenden van [!DNL IDFA] of [!DNL GAID] segmenten naar [!DNL Google Customer Match].

![Google Customer Match App ID](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

Raadpleeg de [officiële documentatie van Google](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid) voor meer informatie over het zoeken naar de [!DNL App ID].

## Controleren of segmentactivering is gelukt {#verify-activation}

Nadat u de activeringsstroom hebt voltooid, schakelt u over naar uw **[!UICONTROL Google Ads]**-account. De geactiveerde segmenten worden in uw Google-account weergegeven als klantenlijsten. Houd er rekening mee dat sommige doelgroepen, afhankelijk van de grootte van het segment, alleen vullen met meer dan 100 actieve gebruikers.

Wanneer u een segment toewijst aan zowel [!DNL IDFA] als [!DNL GAID] mobiele id&#39;s, maakt [!DNL Google Customer Match] een afzonderlijk segment voor elke id-toewijzing. Uw [!DNL Google Ads]-account toont twee verschillende segmenten, een voor de [!DNL IDFA] en een voor de [!DNL GAID]-toewijzing.

## Extra bronnen {#additional-resources}

* [Google Customer Match integreren - videozelfstudie](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/integrate-with-google-customer-match.html)
