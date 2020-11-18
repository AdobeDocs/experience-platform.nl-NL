---
keywords: airship attributes;airship destination
title: Airship Attributes destination
seo-title: Airship Attributes destination
description: Geef naadloos Adobe-geluidsgegevens van het publiek door aan het luchtschip als publiekskenmerken voor het aansturen van vluchten binnen het luchtschip.
seo-description: Geef naadloos Adobe-geluidsgegevens van het publiek door aan het luchtschip als publiekskenmerken voor het aansturen van vluchten binnen het luchtschip.
translation-type: tm+mt
source-git-commit: 4b1bf5bbce57a22529c5d025c5bae10557400d54
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 0%

---


# (Beta) [!DNL Airship Attributes] bestemming {#airship-attributes-destination}

>[!IMPORTANT]
>
>De [!DNL Airship Attributes] bestemming in Adobe Experience Platform is momenteel in bèta. De documentatie en de functionaliteit kunnen worden gewijzigd.

## Overzicht {#overview}

[!DNL Airship] is het toonaangevende Platform voor betrokkenheid van klanten, waarmee u in elke fase van de levenscyclus van de klant betekenisvolle, gepersonaliseerde omnichanale berichten aan uw gebruikers kunt leveren.

Deze integratie geeft Adobe-profielgegevens door [!DNL Airship] als [kenmerken](https://docs.airship.com/guides/audience/attributes/) voor activering of activering.

Raadpleeg de [!DNL Airship]Airship Docs voor meer informatie [over deze documenten](https://docs.airship.com).


>[!TIP]
>
>Deze documentatiepagina is gemaakt door het [!DNL Airship] team. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen via [support.airship.com](https://support.airship.com/).

## Vereisten {#prerequisites}

Voordat u publiekssegmenten kunt verzenden naar [!DNL Airship], moet u:

* Kenmerken in uw [!DNL Airship] project inschakelen.
* Een token voor toonder genereren voor verificatie.

>[!TIP]
>
>Maak een [!DNL Airship] account via [deze aanmeldkoppeling](https://go.airship.eu/accounts/register/plan/starter/) als u dat nog niet hebt gedaan.

### Kenmerken inschakelen {#enable-attributes}

Adobe Experience Platform-profielkenmerken lijken op [!DNL Airship] kenmerken en kunnen gemakkelijk aan elkaar worden toegewezen in Platform met het toewijzingsgereedschap dat hieronder op deze pagina wordt getoond.

[!DNL Airship] de projecten hebben verscheidene vooraf bepaalde en standaardattributen. Als u een aangepast kenmerk hebt, moet u het [!DNL Airship] eerst definiëren. Zie Kenmerken [instellen en beheren](https://docs.airship.com/tutorials/audience/attributes/) voor meer informatie.

### Token aan toonder {#bearer-token}

1. Ga naar **[!UICONTROL Instellingen]** &quot;-API&#39; **[!UICONTROL s en -integratie]** in het [Airship-dashboard](https://go.airship.com) en selecteer **[!UICONTROL Tokens]** in het linkermenu.
1. Klik op **[!UICONTROL Token]** maken.
1. Geef een gebruikersvriendelijke naam voor uw token op, bijvoorbeeld &quot;Doel Adobe-kenmerken&quot;, en selecteer &quot;Alle toegang&quot; voor de rol.
1. Klik op **[!UICONTROL Token]** maken en sla de details op als vertrouwelijk.


## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de [!DNL Airship Attributes] bestemming zou moeten gebruiken, zijn hier de gevallen van het steekproefgebruik die de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.

### Hoofdletters gebruiken #1

Gebruik profielgegevens die in Adobe Experience Platform zijn verzameld voor personalisatie van het bericht en rijke inhoud binnen [!DNL Airship]de kanalen van een van de kanalen. U kunt bijvoorbeeld [!DNL Experience Platform] profielgegevens gebruiken om locatiekenmerken in te stellen binnen [!DNL Airship]. Hierdoor kan een hotelmerk voor elke gebruiker een afbeelding weergeven voor de dichtstbijzijnde hotellocatie.

### Hoofdletters gebruiken #2

Benut kenmerken van Adobe Experience Platform om profielen verder te verrijken en te combineren met SDK of [!DNL Airship] [!DNL Airship] voorspellende gegevens. Bijvoorbeeld, kan een detailhandelaar een segment met loyaliteitsstatus en plaatsgegevens (eigenschappen van Platform) tot stand brengen en [!DNL Airship] voorspeld aan koordgegevens om hoogst gerichte berichten naar gebruikers in de gouden loyaliteitsstatus te verzenden die in Las Vegas, NV wonen, en een hoge waarschijnlijkheid van het kuren hebben.

## Verbinden met [!DNL Airship Attributes] {#connect-airship-attributes}

1. Blader in **[!UICONTROL Doelen]** > **[!UICONTROL Catalogus]** naar de categorie **[!UICONTROL Mobiele betrokkenheid]** . Selecteer **[!DNL Airship Attributes]**, dan uitgezocht **[!UICONTROL vormen]**.

   >[!NOTE]
   >
   >Als er al een verbinding met dit doel bestaat, ziet u een knop **[!UICONTROL Activeren]** op de doelkaart. Voor meer informatie over het verschil tussen **[!UICONTROL Activate]** en **[!UICONTROL Configure]**, verwijs naar de sectie van de [Catalogus](/help/rtcdp/destinations/destinations-workspace.md#catalog) van de documentatie van de bestemmingswerkruimte.

   ![Verbinden met kenmerken van het luchtschip](/help/rtcdp/destinations/assets/airship-attributes-in-catalog.png)

2. Als u in de stap **Account** eerder een verbinding met uw [!DNL Airship Attributes] doel hebt ingesteld, selecteert u **[!UICONTROL Bestaande account]** en selecteert u de bestaande verbinding. U kunt ook **[!UICONTROL Nieuwe account]** selecteren om een nieuwe verbinding in te stellen met [!DNL Airship Attributes]. Selecteer **[!UICONTROL Verbinden met bestemming]** om Adobe Experience Platform met uw [!DNL Airship] project te verbinden gebruikend het dragertoken dat u van het [!DNL Airship] dashboard produceerde.

   >[!NOTE]
   >
   >Adobe Experience Platform ondersteunt validatie van referenties tijdens het verificatieproces en geeft een foutbericht weer als u onjuiste gegevens hebt ingevoerd voor uw [!DNL Airship] account. Dit zorgt ervoor dat u de werkstroom niet met onjuiste geloofsbrieven voltooit.

   ![Verbinden met kenmerken van het luchtschip](/help/rtcdp/destinations/assets/airship1-connect-to-airship.png)

3. Zodra uw geloofsbrieven worden bevestigd en Adobe Experience Platform met uw [!DNL Airship] project wordt verbonden, kunt u **[!UICONTROL Volgende]** selecteren om aan de stap van de **[!UICONTROL Opstelling]** te werk te gaan.

4. Voer in de stap **[!UICONTROL Verificatie]** een **[!UICONTROL naam]** en een **[!UICONTROL beschrijving]** in voor de activeringsstroom. <br> In deze stap kunt u ook Amerikaans of EU-datacenter selecteren, afhankelijk van het [!DNL Airship] datacenter dat op dit doel van toepassing is. Selecteer ten slotte een of meer gevallen waarin gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door de Adobe gedefinieerde gebruiksgevallen voor marketingdoeleinden of u kunt uw eigen gebruiksscenario&#39;s maken. Voor meer informatie over het op de markt brengen van gebruiksgevallen, zie de [Governance van Gegevens in Echte tijd CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) pagina. Voor informatie over de individuele Adobe-bepaalde het in de handel brengen gebruiksgevallen, zie het overzicht [van het het gebruiksbeleid van](/help/data-governance/policies/overview.md#core-actions)Gegevens. <br> Selecteer **[!UICONTROL Doel]** maken nadat u de bovenstaande velden hebt ingevuld.

   ![Verbinden met kenmerken van het luchtschip](/help/rtcdp/destinations/assets/airship2-select-airship-domain.png)

5. Uw doel is nu gemaakt. U kunt **[!UICONTROL Opslaan en afsluiten]** selecteren als u segmenten later wilt activeren of u kunt **[!UICONTROL Volgende]** selecteren om de workflow voort te zetten en segmenten te selecteren om te activeren. In beide gevallen raadpleegt u de volgende sectie Segmenten [](#activate-segments)activeren voor de rest van de workflow.

## Segmenten activeren {#activate-segments}

Volg onderstaande stappen om segmenten te activeren [!DNL Airship Attributes]:

1. Kies in **[!UICONTROL Doelen > Bladeren]** de [!DNL Airship Attributes] bestemming waar u de segmenten wilt activeren.
   ![activeren-flow](/help/rtcdp/destinations/assets/airship-attributes-activate1.png)
1. Klik op de naam van het doel. Hiermee gaat u naar de flow Activeren.
Merk op dat als een activeringsstroom reeds voor een bestemming bestaat, u de segmenten kunt zien die momenteel naar de bestemming worden verzonden. Selecteer Activering **** bewerken in de rechtertrack en voer de onderstaande stappen uit om de activeringsdetails te wijzigen. ![activeren-flow](/help/rtcdp/destinations/assets/airship-attributes-activate2.png)
1. Selecteer **[!UICONTROL Activeren]**;
1. In het **[!UICONTROL Activate bestemmingswerkschema]** , op de **[!UICONTROL Uitgezochte pagina van Segmenten]** , selecteer welke segmenten naar [!DNL Airship Attributes].
   ![segmenten-naar-bestemming](/help/rtcdp/destinations/assets/airship3-select-segments-to-export.png)
1. Selecteer in de stap **[!UICONTROL Toewijzing]** welke kenmerken en identiteiten in het [XDM](https://docs.adobe.com/content/help/nl-NL/experience-platform/xdm/home.html) -schema moeten worden toegewezen aan het doelschema. Selecteer **[!UICONTROL Nieuwe toewijzing]** toevoegen om uw schema te doorbladeren en hen in kaart te brengen aan de overeenkomstige doelidentiteit.
   ![startscherm voor identiteitstoewijzing](/help/rtcdp/destinations/assets/gcm-identity-mapping.png)
   [!DNL Airship] attributen kunnen op of een kanaal worden geplaatst, dat apparateninstantie, b.v., iPhone, of een genoemde gebruiker vertegenwoordigt, die alle apparaten van een gebruiker aan een gemeenschappelijk herkenningsteken zoals een klantenidentiteitskaart in kaart brengt. Als u normale tekst (unhashed) e-mailadressen als primaire identiteit in uw schema hebt, selecteer het e-mailgebied in uw **[!UICONTROL BronAttributen]** en kaart aan de [!DNL Airship] genoemde gebruiker in de juiste kolom onder **[!UICONTROL Doelidentiteiten]**, zoals hieronder getoond.
   ![Toewijzing](/help/rtcdp/destinations/assets/airshiptags7-mappingoption2.png)van benoemde gebruiker voor id&#39;s die moeten worden toegewezen aan een kanaal, d.w.z. een apparaat, toewijzen aan het juiste kanaal op basis van de bron. De volgende afbeeldingen laten zien hoe twee toewijzingen worden gemaakt:

   * IDFA iOS-advertentie-id naar een [!DNL Airship] iOS-kanaal
   * Adobe- `fullName` kenmerk naar kenmerk [!DNL Airship] &quot;Volledige naam&quot;

   >[!NOTE]
   >
   >Gebruik de gebruikersvriendelijke naam die in het [!DNL Airship] dashboard verschijnt wanneer het selecteren van het doelgebied voor uw attributenafbeelding.

   **Bronveld Identiteit**toewijzen:
   ![Verbinden met Airship Attributes](/help/rtcdp/destinations/assets/airship5-select-source-identity.png)Selecteer doelveld:
   ![Verbinden met kenmerken van het luchtschip](/help/rtcdp/destinations/assets/airship6-select-target-identity.png)

   **Kenmerk Kaart**

   Bronkenmerk selecteren:
   ![Selecteer bronveld](/help/rtcdp/destinations/assets/airship7-select-source-attributes.png)Doelkenmerk selecteren:
   ![Doelveld](/help/rtcdp/destinations/assets/airship8-select-target-attribute.png)selecteren controletoewijzing:
   ![Kanaaltoewijzing](/help/rtcdp/destinations/assets/airship9-mapping-final.png)

1. Op de pagina van het **[!UICONTROL Segmentprogramma]** , is het plannen momenteel gehandicapt. Klik op **[!UICONTROL Volgende]** om door te gaan naar de revisiestap. ![Momenteel uitgeschakeld plannen](/help/rtcdp/destinations/assets/airship10-scheduling-step-is-disabled-for-now.png)

1. Op de pagina **[!UICONTROL Revisie]** ziet u een overzicht van uw selectie. Selecteer **[!UICONTROL Annuleren]** om de stroom te verbreken, **[!UICONTROL Terug]** om uw instellingen te wijzigen of **[!UICONTROL Voltooien]** om uw selectie te bevestigen en gegevens naar de bestemming te verzenden.

>[!IMPORTANT]
>
>In deze stap controleert Adobe Experience Platform op overtredingen van het gegevensgebruiksbeleid. Hieronder ziet u een voorbeeld waarin een beleid wordt overtreden. U kunt de workflow voor segmentactivering pas voltooien nadat u de schending hebt opgelost. Voor informatie over hoe te om beleidsschendingen op te lossen, zie [Beleidshandhaving](/help/rtcdp/privacy/data-governance-overview.md#enforcement) in de sectie van de documentatie van het gegevensbeheer.

![selectie bevestigen](/help/rtcdp/destinations/assets/data-policy-violation.png)

Als er geen beleidsovertredingen zijn vastgesteld, selecteert u **[!UICONTROL Voltooien]** om uw selectie te bevestigen en gegevens naar de bestemming te verzenden.

![revisie](/help/rtcdp/destinations/assets/airship11-review-step.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] afdwingt gegevensbeheer, zie [Gegevensbeheer in real time CDP](/help/rtcdp/privacy/data-governance-overview.md).
