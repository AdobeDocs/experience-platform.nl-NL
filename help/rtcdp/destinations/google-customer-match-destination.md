---
keywords: google customer match;Google customer match;Google Customer Match
title: Google Customer Match Destination
seo-title: Google Customer Match Destination
description: Met Google Customer Match kunt u uw online- en offline gegevens gebruiken om uw klanten te bereiken en opnieuw contact op te nemen met andere eigendommen van Google, zoals Zoeken, Winkelen, Gmail en YouTube.
seo-description: Met Google Customer Match kunt u uw online- en offline gegevens gebruiken om uw klanten te bereiken en opnieuw contact op te nemen met andere eigendommen van Google, zoals Zoeken, Winkelen, Gmail en YouTube.
translation-type: tm+mt
source-git-commit: 0232acdc64019b9d93888e8137ef9bc8e114779b
workflow-type: tm+mt
source-wordcount: '1554'
ht-degree: 0%

---


# Google Customer Match Destination

## Overzicht {#overview}

[Met Google Customer Match](https://support.google.com/google-ads/answer/6379332?hl=en) kunt u uw online- en offline gegevens gebruiken om uw klanten te bereiken en opnieuw contact op te nemen met andere klanten over de eigendommen van Google, zoals: [!DNL Search], [!DNL Shopping], [!DNL Gmail]en [!DNL YouTube].

![Google Customer Match-bestemming in de CDP-gebruikersinterface in realtime](/help/rtcdp/destinations/assets/google-customer-match-catalog.png)

## Gevallen gebruiken

Om u beter te helpen begrijpen hoe en wanneer u de [!DNL Google Customer Match] bestemming zou moeten gebruiken, zijn hier de gevallen van het steekproefgebruik die de klanten in real time van de Gegevens van de Klant kunnen oplossen door deze eigenschap te gebruiken.


### Hoofdletters en kleine letters gebruiken 1

Een atletisch merkje wil bestaande klanten bereiken via [!DNL Google Search] [!DNL Google Shopping] en aanbiedingen en objecten aanpassen op basis van hun aankopen en browsergeschiedenis. Het merkteken kan e-mailadressen van hun eigen CRM aan Adobe in real time CDP opnemen, segmenten van hun eigen off-line gegevens bouwen, en deze segmenten verzenden om over [!DNL Google Customer Match] en [!DNL Search] [!DNL Shopping]te worden gebruikt, optimaliserend hun reclame uitgaven.

### Hoofdletters en kleine letters gebruiken 2

Een vooraanstaand technologiebedrijf heeft zojuist een nieuwe telefoon uitgebracht. In een inspanning om dit nieuwe telefoonmodel te bevorderen, kijken zij om bewustzijn van de nieuwe eigenschappen en de functionaliteit van de telefoon aan klanten te drijven die vorige modellen van hun telefoons bezitten.

Om de versie te bevorderen, uploaden zij e-mailadressen van hun gegevensbestand van CRM in Adobe in real time CDP, gebruikend de e-mailadressen als herkenningstekens. De segmenten worden gecreeerd gebaseerd op klanten die oudere telefoonmodellen bezitten en naar worden verzonden [!DNL Google Customer Match] zodat zij huidige klanten, klanten kunnen richten die oudere telefoonmodellen, evenals gelijkaardige klanten op [!DNL YouTube]. bezitten.

## Gegevensbeheer voor [!DNL Google Customer Match] bestemmingen {#data-governance}

De bestemmingen in Adobe real time CDP kunnen bepaalde regels en verplichtingen voor gegevens hebben die naar, of van, het bestemmingsplatform worden verzonden ontvangen. U bent verantwoordelijk voor het begrijpen van de beperkingen en verplichtingen van uw gegevens en hoe u die gegevens gebruikt in Adobe Experience Platform en het doelplatform. Adobe Experience Platform biedt tools voor gegevensbeheer om u te helpen bij het beheren van een aantal van deze gegevensgebruiksverplichtingen. [Meer](/help/data-governance/labels/overview.md) informatie over tools en beleid voor gegevensbeheer.

## Exporttype en -identiteiten {#export-type}

**Segmentexport** - u exporteert alle leden van een segment (publiek) met de id&#39;s (naam, telefoonnummer, enzovoort) gebruikt in de [!DNL Google Customer Match] bestemming.

**Identiteiten** - u kunt onbewerkte of gehashte e-mails gebruiken als klant-id&#39;s in Google

## [!DNL Google Customer Match] accountvereisten {#google-account-prerequisites}

Voordat u een [!DNL Google Customer Match] bestemming instelt in CDP in real-time Adobe, moet u ervoor zorgen dat u het beleid van Google voor het gebruik van [!DNL Customer Match], zoals beschreven in de documentatie [van de](https://support.google.com/google-ads/answer/6299717)Google-ondersteuning, leest en volgt.

### Lijst van gewenste personen {#allowlist}

>[!NOTE]
>
>Het is verplicht om aan de lijst van gewenste personen van Google vóór vestiging uw eerste [!DNL Google Customer Match] bestemming in Adobe in real time CDP te worden toegevoegd. Controleer of Google het hieronder beschreven lijst van gewenste personen-proces heeft voltooid voordat u een bestemming maakt.

Voordat u de [!DNL Google Customer Match] bestemming maakt in CDP in real-time Adobe, moet u contact opnemen met Google en de instructies van de lijst van gewenste personen volgen in [Customer Match-partners gebruiken om uw gegevens](https://support.google.com/google-ads/answer/7361372?hl=en&amp;ref_topic=6296507) te uploaden in de Google-documentatie.


### Vereisten voor e-mailhashing {#hashing-requirements}

<!--

>[!IMPORTANT]
>
> When using mobile device IDs as identifiers, an AppId must be provided in the activation flow. For more information, see step 6 in the [Activate segments](#activate-segments) section of this page.

-->

Google vereist dat er geen informatie met een persoonlijk identificeerbaar karakter (PII) duidelijk wordt verzonden. Daarom [!DNL Google Customer Match] moet het publiek dat wordt geactiveerd om *gehashte* e-mailadressen worden afgevinkt. U kunt ervoor kiezen e-mailadressen te hashen alvorens hen in Adobe Experience Platform op te nemen, of u kunt verkiezen om met e-mailadressen in duidelijk Experience Platform te werken en onze algoritme te hebben hen op activering hakt.

Raadpleeg de volgende secties in de documentatie van Google voor meer informatie over de hashing-vereisten van Google en andere activeringsbeperkingen:

* [[!DNL Customer Match] met e-mailadres, adres of gebruikersnaam](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] overwegingen](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_considerations)

<!--

Links to be added when activation based on phone number and device IDs becomes available.

* [Customer Match with phone number](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_phone_number)
* [Customer Match with mobile device IDs](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_mobile_device_ids)

-->

Als u meer wilt weten over het invoeren van e-mailadressen in Experience Platforms, raadpleegt u het [overzicht](/help/ingestion/batch-ingestion/overview.md) van het gebruik van batches en het [overzicht](/help/ingestion/streaming-ingestion/overview.md)van het opnemen van tags.

Als u ervoor kiest om de e-mailadressen zelf te hashen, moet u voldoen aan de vereisten van Google, zoals beschreven in de koppelingen hierboven.


>[!IMPORTANT]
>
>Als u ervoor kiest geen e-mailadressen te hacken, zal Adobe in real time CDP dat voor u doen wanneer u segmenten aan activeert. [!DNL Google Customer Match] Selecteer in de [activeringsworkflow](/help/rtcdp/destinations/google-customer-match-destination.md#activate-segments) (zie stap 5) de `Email` optie die hieronder wordt weergegeven voor e- *mailadressen* met onbewerkte tekst en `Email_LC_SHA256` voor *gehashte e-mailadressen*.


![Hashing bij activering](/help/rtcdp/destinations/assets/identity-mapping.png)

## Verbinden met doel {#connect-destination}

1. Blader in **[!UICONTROL Doelen]** > **[!UICONTROL Catalogus]** naar de categorie **[!UICONTROL Adverteren]** . Selecteer [!DNL Google Customer Match], dan uitgezocht **[!UICONTROL vormen]**.

   ![Verbinding maken met Google Customer Match-doel](/help/rtcdp/destinations/assets/connect-google-customer-match.png)

   >[!NOTE]
   >
   >Als er al een verbinding met dit doel bestaat, ziet u een knop **[!UICONTROL Activeren]** op de doelkaart. Voor meer informatie over het verschil tussen **[!UICONTROL Activate]** en **[!UICONTROL Configure]**, verwijs naar de sectie van de [Catalogus](/help/rtcdp/destinations/destinations-workspace.md#catalog) van de documentatie van de bestemmingswerkruimte.

2. Als u in de stap **Account** eerder een verbinding met uw [!DNL Google Customer Match] doel hebt ingesteld, selecteert u **[!UICONTROL Bestaande account]** en selecteert u de bestaande verbinding. U kunt ook **[!UICONTROL Nieuwe account]** selecteren om een nieuwe verbinding in te stellen met [!DNL Google Customer Match]. Selecteer **[!UICONTROL Verbinding maken met doel]** om u aan te melden en Adobe Experience Cloud te verbinden met uw [!DNL Google Ad] account.

   >[!NOTE]
   >
   >Adobe CDP in real time steunt geloofsbevestiging in het authentificatieproces en toont een foutenmelding als u onjuiste geloofsbrieven aan uw [!DNL Google Ad] rekening invoert. Dit zorgt ervoor dat u de werkstroom niet met onjuiste geloofsbrieven voltooit.

   ![Verbinden met Google Customer Match-bestemming - verificatiestap](/help/rtcdp/destinations/assets/google-customer-match-pre-connect-view.png)

3. Nadat uw referenties zijn bevestigd en Adobe Experience Cloud is verbonden met uw Google-account, kunt u **[!UICONTROL Volgende]** selecteren om door te gaan naar de stap **[!UICONTROL Setup]** .

   ![Credentials bevestigd](/help/rtcdp/destinations/assets/google-customer-match-connection-success.png)

4. Voer in de stap **[!UICONTROL Verificatie]** een [!UICONTROL naam] en een [!UICONTROL beschrijving] in voor de activeringsstroom en vul de Google- [!UICONTROL account-id]in. <br> Ook in deze stap kunt u elke **[!UICONTROL Gebruikszaak]** voor marketingdoeleinden selecteren die op deze bestemming moet worden toegepast. Gebruiksgevallen voor marketingdoeleinden geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door de Adobe gedefinieerde gebruiksgevallen voor marketingdoeleinden of u kunt uw eigen gebruiksscenario voor marketingdoeleinden maken. Voor meer informatie over het op de markt brengen van gebruiksgevallen, zie de [Governance van Gegevens in Echte tijd CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) pagina. Voor informatie over de individuele Adobe-bepaalde het in de handel brengen gebruiksgevallen, zie het overzicht [van het het gebruiksbeleid van](/help/data-governance/policies/overview.md#core-actions)Gegevens. <br> Selecteer Doel **** maken nadat u de bovenstaande velden hebt ingevuld.

   >[!IMPORTANT]
   >
   > * De **[!UICONTROL optie Combineren met PII]** -marketingtoepassing is standaard geselecteerd voor de [!DNL Google Customer Match] bestemming en kan niet worden verwijderd.
   > * Voor [!DNL Google Customer Match] bestemmingen. **[!UICONTROL De account-id]** is uw client-id met Google. De indeling van de id is xxx-xxx-xxxx.


   ![Google-klantovereenkomst aansluiten - verificatiestap](/help/rtcdp/destinations/assets/google-customer-match-authentication-step.png)

5. Uw doel is nu gemaakt. U kunt **[!UICONTROL Opslaan en afsluiten]** selecteren als u segmenten later wilt activeren of u kunt **[!UICONTROL Volgende]** selecteren om de workflow voort te zetten en segmenten te selecteren om te activeren. In beide gevallen raadpleegt u de volgende sectie Segmenten [activeren voor [!DNL Google Customer Match]](#activate-segments)de rest van de workflow.


## Segmenten activeren om [!DNL Google Customer Match] {#activate-segments}

Volg onderstaande stappen om segmenten te activeren [!DNL Google Customer Match]:

1. Kies in **[!UICONTROL Doelen > Bladeren]** de [!DNL Google Customer Match] bestemming waar u de segmenten wilt activeren.
2. Klik op de naam van het doel. Hiermee gaat u naar de flow Activeren.
   ![activate-flow](/help/rtcdp/destinations/assets/google-customer-match-activate-flow.png)Merk op dat als een activeringsstroom reeds voor een bestemming bestaat, u de segmenten kunt zien die momenteel naar de bestemming worden verzonden. Selecteer Activering **** bewerken in de rechtertrack en voer de onderstaande stappen uit om de activeringsdetails te wijzigen.
3. Selecteer **[!UICONTROL Activeren]**;
4. In het **[!UICONTROL Activate bestemmingswerkschema]** , op de **[!UICONTROL Uitgezochte pagina van Segmenten]** , selecteer welke segmenten naar [!DNL Google Customer Match].
   ![segmenten-naar-bestemming](/help/rtcdp/destinations/assets/activate-segments-google-customer-match.png)
5. Selecteer in de stap **[!UICONTROL Identiteitskaart]** welke kenmerken als identiteit in deze bestemming moeten worden opgenomen. Selecteer **[!UICONTROL Nieuwe toewijzing]** toevoegen en blader in uw schema, selecteer e-mail en/of gehakt e-mail, en wijs hen aan de overeenkomstige doelidentiteit toe
   ![startscherm voor identiteitstoewijzing](/help/rtcdp/destinations/assets/gcm-identity-mapping.png) <br> 
   *E-mailadres voor normale tekst als primaire identiteit*: Als u normale (niet-gehashte) e-mailadressen als primaire identiteit in uw schema hebt, selecteert u het e-mailveld in uw **[!UICONTROL bronkenmerken]** en wijst u de e-mailadressen toe aan het veld E-mail in de rechterkolom onder **[!UICONTROL Doelidentiteiten]**, zoals hieronder wordt weergegeven:
   ![e-mailidentiteit voor normale tekst selecteren](/help/rtcdp/destinations/assets/gcm-raw-email.gif) <br> 
   *Onderbroken e-mailadres als primaire identiteit*: Als u hashed e-mailadressen als primaire identiteit in uw schema hebt, selecteer het gehakte e-mailgebied in uw **[!UICONTROL BronAttributen]** en kaart aan het E-mail_LC_SHA256 gebied in de juiste kolom onder **[!UICONTROL Doelidentiteiten]**, zoals hieronder getoond:
   ![hashidentiteit voor e-mailberichten selecteren](/help/rtcdp/destinations/assets/gcm-hashed-emails.gif) <br> 
6. Op de het **[!UICONTROL programmapagina]** van het Segment, kunt u de begindatum voor het verzenden van gegevens naar de bestemming plaatsen.
7. Op de pagina **[!UICONTROL Revisie]** ziet u een overzicht van uw selectie. Selecteer **[!UICONTROL Annuleren]** om de stroom te verbreken, **[!UICONTROL Terug]** om uw instellingen te wijzigen of **[!UICONTROL Voltooien]** om uw selectie te bevestigen en gegevens naar de bestemming te verzenden.

>[!IMPORTANT]
>
>In deze stap, CDP in real time controleert op de schendingen van het beleid van het gegevensgebruik. Hieronder ziet u een voorbeeld waarin een beleid wordt overtreden. U kunt de workflow voor segmentactivering pas voltooien nadat u de schending hebt opgelost. Voor informatie over hoe te om beleidsschendingen op te lossen, zie [Beleidshandhaving](/help/rtcdp/privacy/data-governance-overview.md#enforcement) in de sectie van de documentatie van het gegevensbeheer.

![selectie bevestigen](/help/rtcdp/destinations/assets/data-policy-violation.png)

Als er geen beleidsovertredingen zijn vastgesteld, selecteert u **[!UICONTROL Voltooien]** om uw selectie te bevestigen en gegevens naar de bestemming te verzenden.

![selectie bevestigen](/help/rtcdp/destinations/assets/gcm-review.png)


<!--

Insert in Step 6 when mobile device ID activation is available

    >[!IMPORTANT]
    >
    >If you select mobile device IDs (GAID or IDFA) as primary identity in the Identity mapping step, you must also provide an Application Id in this step. If you selected GAID as identity, see [Set the Application ID](https://developer.android.com/studio/build/application-id) in the Android developer documentation. IF you selected IDFA as identity, see [App ID](https://developer.android.com/studio/build/application-id) in the Apple developer documentation.

    ![segment schedule page](/help/rtcdp/destinations/assets/gcm-segment-schedule.png) 

-->

## Controleren of segmentactivering is gelukt {#verify-activation}

Schakel na het voltooien van de activeringsstroom over naar uw **[!UICONTROL Google Ads]** -account. De geactiveerde segmenten worden nu in uw Google-account weergegeven als klantenlijsten. Houd er rekening mee dat sommige doelgroepen, afhankelijk van de grootte van uw segment, alleen vullen met meer dan 100 actieve gebruikers.

## Aanvullende bronnen {#additional-resources}

* [Google Customer Match integreren - videozelfstudie](https://docs.adobe.com/content/help/en/platform-learn/tutorials/rtcdp/integrate-with-google-customer-match.html)