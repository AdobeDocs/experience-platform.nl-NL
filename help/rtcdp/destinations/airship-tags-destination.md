---
keywords: airship tags;airship destination
title: Doel van airship-tags
seo-title: Doel van airship-tags
description: Geef naadloos Adobe-geluidsgegevens van het publiek door aan het luchtschip als Publiek-tags voor doelwit binnen het luchtschip.
seo-description: Geef naadloos Adobe-geluidsgegevens van het publiek door aan het luchtschip als Publiek-tags voor doelwit binnen het luchtschip.
translation-type: tm+mt
source-git-commit: 4b1bf5bbce57a22529c5d025c5bae10557400d54
workflow-type: tm+mt
source-wordcount: '1236'
ht-degree: 0%

---


# (Beta) [!DNL Airship Tags] bestemming {#airship-tags-destination}

>[!IMPORTANT]
>
>De [!DNL Airship Tags] bestemming in Adobe Experience Platform is momenteel in bèta. De documentatie en de functionaliteit kunnen worden gewijzigd.

## Overzicht

[!DNL Airship] is het toonaangevende Platform voor betrokkenheid van klanten, waarmee u in elke fase van de levenscyclus van de klant betekenisvolle, gepersonaliseerde omnichanale berichten aan uw gebruikers kunt leveren.

Deze integratie geeft Adobe Experience Platform-segmentgegevens door [!DNL Airship] als [tags](https://docs.airship.com/guides/audience/tags/) voor het opgeven van doelen of het activeren.

Raadpleeg de [!DNL Airship]Airship Docs voor meer informatie [over deze documenten](https://docs.airship.com).


>[!TIP]
>
>Deze documentatiepagina is gemaakt door het [!DNL Airship] team. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen via [support.airship.com](https://support.airship.com/).

## Vereisten

Voordat je Adobe Experience Platform-segmenten kunt verzenden naar, moet je: [!DNL Airship]

* Maak een taggroep in uw [!DNL Airship] project.
* Een token voor toonder genereren voor verificatie.

>[!TIP]
> 
>Maak een [!DNL Airship] account via [deze aanmeldkoppeling](https://go.airship.eu/accounts/register/plan/starter/) als u dat nog niet hebt gedaan.

### Taggroepen

Het concept van segmenten in het Adobe Experience Platform lijkt op [Tags](https://docs.airship.com/guides/audience/tags/) in het vliegtuig, met kleine verschillen in implementatie. Deze integratie wijst de status van het [lidmaatschap van een gebruiker in een segment](https://experienceleague.adobe.com/docs/experience-platform/xdm/mixins/profile/segmentation.html?lang=en#mixins) van het Experience Platform aan de aanwezigheid of het niet-voorkomen van een [!DNL Airship] markering toe. Bijvoorbeeld in een segment van het Platform waar de `xdm:status` veranderingen in `realized`, wordt de markering toegevoegd aan het [!DNL Airship] kanaal of genoemde gebruiker wordt dit profiel in kaart gebracht aan. Als de code `xdm:status` verandert in `exited`, wordt de tag verwijderd.

Om deze integratie in te schakelen, maakt u een *taggroep* in de [!DNL Airship] naam `adobe-segments`.

>[!IMPORTANT]
>
>Wanneer u een nieuwe taggroep maakt, moet u **niet het keuzerondje &quot;** &quot; controleren[!DNL Allow these tags to be set only from your server]. Als u dit doet, mislukt de integratie van de Adobe-tags.

Zie Taggroepen [](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) beheren voor instructies over het maken van de taggroep.

### Token aan toonder

1. Ga naar **[!UICONTROL Instellingen]** &quot;-API&#39; **[!UICONTROL s en -integratie]** in het [Airship-dashboard](https://go.airship.com) en selecteer **[!UICONTROL Tokens]** in het linkermenu.
1. Klik op **[!UICONTROL Token]** maken.
1. Geef uw token een gebruikersvriendelijke naam, bijvoorbeeld &quot;Doel van Adobe-tags&quot;, en selecteer &quot;Alle toegang&quot; voor de rol.
1. Klik op **[!UICONTROL Token]** maken en sla de details op als vertrouwelijk.


## Gebruiksscenario’s

Om u beter te helpen begrijpen hoe en wanneer u de [!DNL Airship Tags] bestemming zou moeten gebruiken, zijn hier de gevallen van het steekproefgebruik die de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.

### Hoofdletters gebruiken #1

De detailhandelaars of de entertainmentplatforms kunnen gebruikersprofielen op hun loyaliteitklanten tot stand brengen, en die segmenten overgaan in [!DNL Airship] voor bericht richtend op mobiele campagnes.

### Hoofdletters gebruiken #2

U kunt een-op-een berichten in real-time activeren wanneer gebruikers binnen of buiten specifieke segmenten in Adobe Experience Platform vallen.

Een detailhandelaar stelt bijvoorbeeld een merkspecifiek segment voor jeans in Platform in. Deze detailhandelaar kan nu een mobiel bericht activeren zodra iemand zijn jeans-voorkeur op een bepaald merk instelt.

## Verbinden met [!DNL Airship Tags] {#connect-airship-tags}

1. Blader in **[!UICONTROL Doelen]** > **[!UICONTROL Catalogus]** naar de categorie **[!UICONTROL Mobiele betrokkenheid]** . Selecteer **[!DNL Airship Tags]**, dan uitgezocht **[!UICONTROL vormen]**.

   >[!NOTE]
   >
   >Als er al een verbinding met dit doel bestaat, ziet u een knop **[!UICONTROL Activeren]** op de doelkaart. Voor meer informatie over het verschil tussen **[!UICONTROL Activate]** en **[!UICONTROL Configure]**, verwijs naar de sectie van de [Catalogus](/help/rtcdp/destinations/destinations-workspace.md#catalog) van de documentatie van de bestemmingswerkruimte.

   ![Verbinden met luchtvaartcodes](/help/rtcdp/destinations/assets/airship-tags-in-catalog.png)

2. Als u in de stap **Account** eerder een verbinding met uw [!DNL Airship Tags] doel hebt ingesteld, selecteert u **[!UICONTROL Bestaande account]** en selecteert u de bestaande verbinding. U kunt ook **[!UICONTROL Nieuwe account]** selecteren om een nieuwe verbinding in te stellen met [!DNL Airship Tags]. Selecteer **[!UICONTROL Verbinden met bestemming]** om Adobe Experience Platform met uw [!DNL Airship] project te verbinden gebruikend het dragertoken dat u van het [!DNL Airship] dashboard produceerde.

   >[!NOTE]
   >
   >Adobe Experience Platform ondersteunt validatie van referenties tijdens het verificatieproces en geeft een foutbericht weer als u onjuiste gegevens hebt ingevoerd voor uw [!DNL Airship] account. Dit zorgt ervoor dat u de werkstroom niet met onjuiste geloofsbrieven voltooit.

   ![Verbinden met luchtvaartcodes](/help/rtcdp/destinations/assets/airshiptags1-connect-account.png)

3. Zodra uw geloofsbrieven worden bevestigd en Adobe Experience Platform met uw [!DNL Airship] project wordt verbonden, kunt u **[!UICONTROL Volgende]** selecteren om aan de stap van de **[!UICONTROL Opstelling]** te werk te gaan.

4. Voer in de stap **[!UICONTROL Verificatie]** een **[!UICONTROL naam]** en een **[!UICONTROL beschrijving]** in voor de activeringsstroom. <br> In deze stap kunt u ook Amerikaans of EU-datacenter selecteren, afhankelijk van het [!DNL Airship] datacenter dat op dit doel van toepassing is. Selecteer ten slotte een of meer gevallen waarin gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door de Adobe gedefinieerde gebruiksgevallen voor marketingdoeleinden of u kunt uw eigen gebruiksscenario&#39;s maken. Voor meer informatie over het op de markt brengen van gebruiksgevallen, zie de [Governance van Gegevens in Echte tijd CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) pagina. Voor informatie over de individuele Adobe-bepaalde het in de handel brengen gebruiksgevallen, zie het overzicht [van het het gebruiksbeleid van](/help/data-governance/policies/overview.md#core-actions)Gegevens. <br> Selecteer **[!UICONTROL Doel]** maken nadat u de bovenstaande velden hebt ingevuld.

   ![Verbinden met luchtvaartcodes](/help/rtcdp/destinations/assets/airshiptags2-select-domain.png)

5. Uw doel is nu gemaakt. U kunt **[!UICONTROL Opslaan en afsluiten]** selecteren als u segmenten later wilt activeren of u kunt **[!UICONTROL Volgende]** selecteren om de workflow voort te zetten en segmenten te selecteren om te activeren. In beide gevallen raadpleegt u de volgende sectie Segmenten [](#activate-segments)activeren voor de rest van de workflow.

## Segmenten activeren {#activate-segments}

Volg onderstaande stappen om segmenten te activeren [!DNL Airship Tags]:

1. Kies in **[!UICONTROL Doelen > Bladeren]** de [!DNL Airship Tags] bestemming waar u de segmenten wilt activeren. ![activeren-flow](/help/rtcdp/destinations/assets/airship-tags-activate1.png)
2. Klik op de naam van het doel. Hiermee gaat u naar de flow Activeren.
Merk op dat als een activeringsstroom reeds voor een bestemming bestaat, u de segmenten kunt zien die momenteel naar de bestemming worden verzonden. Selecteer Activering **** bewerken in de rechtertrack en voer de onderstaande stappen uit om de activeringsdetails te wijzigen.  ![activeren-flow](/help/rtcdp/destinations/assets/airship-tags-activate2.png)
3. Selecteer **[!UICONTROL Activeren]**;
4. In het **[!UICONTROL Activate bestemmingswerkschema]** , op de **[!UICONTROL Uitgezochte pagina van Segmenten]** , selecteer welke segmenten naar [!DNL Airship Tags].
   ![segmenten-naar-bestemming](/help/rtcdp/destinations/assets/airshiptags3-select-segments.png)
5. Selecteer in de stap **[!UICONTROL Toewijzing]** welke kenmerken en identiteiten in het [XDM](https://docs.adobe.com/content/help/nl-NL/experience-platform/xdm/home.html) -schema moeten worden toegewezen aan het doelschema. Selecteer **[!UICONTROL Nieuwe toewijzing]** toevoegen om uw schema te doorbladeren en hen in kaart te brengen aan de overeenkomstige doelidentiteit.
   ![startscherm voor identiteitstoewijzing](/help/rtcdp/destinations/assets/gcm-identity-mapping.png)
   [!DNL Airship] tags kunnen worden ingesteld op een kanaal dat apparaatinstantie vertegenwoordigt, bijvoorbeeld iPhone, of een benoemde gebruiker, die alle apparaten van een gebruiker toewijst aan een gemeenschappelijke id, zoals een klant-id. Als u normale tekst (unhashed) e-mailadressen als primaire identiteit in uw schema hebt, selecteer het e-mailgebied in uw **[!UICONTROL BronAttributen]** en kaart aan de [!DNL Airship] genoemde gebruiker in de juiste kolom onder **[!UICONTROL Doelidentiteiten]**, zoals hieronder getoond.
   ![Toewijzing](/help/rtcdp/destinations/assets/airshiptags7-mappingoption2.png)van benoemde gebruiker voor id&#39;s die moeten worden toegewezen aan een kanaal, d.w.z. een apparaat, toewijzen aan het juiste kanaal op basis van de bron. In de volgende afbeeldingen ziet u hoe u een Google Advertising-id toewijst aan een [!DNL Airship] Android-kanaal.
   ![Verbinden met luchtvaartcodes](/help/rtcdp/destinations/assets/airshiptags4-select-source-identity.png)
   ![Verbinden met luchtvaartcodes](/help/rtcdp/destinations/assets/airshiptags5-select-target-identity.png)
   ![Kanaaltoewijzing](/help/rtcdp/destinations/assets/airshiptags6-mappingoption1.png)

6. Op de pagina van het **[!UICONTROL Segmentprogramma]** , is het plannen momenteel gehandicapt. Klik op **[!UICONTROL Volgende]** om door te gaan naar de revisiestap.
7. Op de pagina **[!UICONTROL Revisie]** ziet u een overzicht van uw selectie. Selecteer **[!UICONTROL Annuleren]** om de stroom te verbreken, **[!UICONTROL Terug]** om uw instellingen te wijzigen of **[!UICONTROL Voltooien]** om uw selectie te bevestigen en gegevens naar de bestemming te verzenden.

>[!IMPORTANT]
>
>In deze stap controleert Adobe Experience Platform op overtredingen van het gegevensgebruiksbeleid. Hieronder ziet u een voorbeeld waarin een beleid wordt overtreden. U kunt de workflow voor segmentactivering pas voltooien nadat u de schending hebt opgelost. Voor informatie over hoe te om beleidsschendingen op te lossen, zie [Beleidshandhaving](/help/rtcdp/privacy/data-governance-overview.md#enforcement) in de sectie van de documentatie van het gegevensbeheer.

![selectie bevestigen](/help/rtcdp/destinations/assets/data-policy-violation.png)

Als er geen beleidsovertredingen zijn vastgesteld, selecteert u **[!UICONTROL Voltooien]** om uw selectie te bevestigen en gegevens naar de bestemming te verzenden.

![selectie bevestigen](/help/rtcdp/destinations/assets/Airship-tags-review.png)


## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] afdwingt gegevensbeheer, zie [Gegevensbeheer in real time CDP](/help/rtcdp/privacy/data-governance-overview.md).

