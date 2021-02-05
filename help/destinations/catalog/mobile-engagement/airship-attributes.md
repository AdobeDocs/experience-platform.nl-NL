---
keywords: kenmerken van het luchtschip;bestemming van het luchtschip
title: Luchtvaartkenmerken verbindingsbestemming
description: Geef naadloos Adobe-geluidsgegevens van het publiek door aan het luchtschip als publiekskenmerken voor het aansturen van vluchten binnen het luchtschip.
translation-type: tm+mt
source-git-commit: f4095a90ff70e8d054bae4f3b0f884552ffd30df
workflow-type: tm+mt
source-wordcount: '1205'
ht-degree: 0%

---


# (Bèta) [!DNL Airship Attributes] verbinding {#airship-attributes-destination}

>[!IMPORTANT]
>
>De bestemming [!DNL Airship Attributes] in Adobe Experience Platform is momenteel in bèta. De documentatie en de functionaliteit kunnen worden gewijzigd.

[!DNL Airship] is het toonaangevende Platform voor betrokkenheid van klanten, waarmee u in elke fase van de levenscyclus van de klant betekenisvolle, gepersonaliseerde omnichanale berichten aan uw gebruikers kunt leveren.

Deze integratie geeft Adobe-profielgegevens door in [!DNL Airship] als [Attributen](https://docs.airship.com/guides/audience/attributes/) voor activering of activering.

Zie [Airship Docs](https://docs.airship.com) voor meer informatie over [!DNL Airship].


>[!TIP]
>
>Deze documentatiepagina is gemaakt door het team van [!DNL Airship]. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen via [support.airship.com](https://support.airship.com/).

## Vereisten {#prerequisites}

Voordat u publiekssegmenten naar [!DNL Airship] kunt verzenden, moet u:

* Laat attributen in uw [!DNL Airship] project toe.
* Een token voor toonder genereren voor verificatie.

>[!TIP]
>
>Maak een [!DNL Airship]-account via [deze aanmeldlink](https://go.airship.eu/accounts/register/plan/starter/) als u dat nog niet hebt gedaan.

### Kenmerken {#enable-attributes} inschakelen

Adobe Experience Platform-profielkenmerken lijken op [!DNL Airship]-kenmerken en kunnen gemakkelijk aan elkaar worden toegewezen in het Platform met behulp van het toewijzingsgereedschap dat verderop op op deze pagina wordt getoond.

[!DNL Airship] de projecten hebben verscheidene vooraf bepaalde en standaardattributen. Als u een douanekenmerk hebt, moet u het in [!DNL Airship] eerst bepalen. Zie [Kenmerken instellen en beheren](https://docs.airship.com/tutorials/audience/attributes/) voor meer informatie.

### Dragertoken {#bearer-token}

Ga naar **[!UICONTROL Instellingen]**&quot; **[!UICONTROL API&#39;s &amp; integraties]** in het [Airship dashboard](https://go.airship.com) en selecteer **[!UICONTROL Tokens]** in het linkermenu.

Klik **[!UICONTROL Token maken]**.

Geef een gebruikersvriendelijke naam voor uw token op, bijvoorbeeld &quot;Doel Adobe-kenmerken&quot;, en selecteer &quot;Alle toegang&quot; voor de rol.

Klik **[!UICONTROL Token maken]** en sla de details op als vertrouwelijk.

## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u [!DNL Airship Attributes] bestemming zou moeten gebruiken, zijn hier voorbeelden van gebruiksgevallen die de klanten van Adobe Experience Platform door deze bestemming kunnen oplossen.

### Hoofdletters gebruiken #1

Gebruik profielgegevens die in Adobe Experience Platform zijn verzameld voor personalisatie van het bericht en rijke inhoud binnen de kanalen van [!DNL Airship]. Gebruik bijvoorbeeld [!DNL Experience Platform]-profielgegevens om locatiekenmerken in te stellen binnen [!DNL Airship]. Hierdoor kan een hotelmerk voor elke gebruiker een afbeelding weergeven voor de dichtstbijzijnde hotellocatie.

### Hoofdletters gebruiken #2

Gebruik kenmerken van Adobe Experience Platform om [!DNL Airship]-profielen verder te verrijken en combineer deze met SDK of [!DNL Airship] voorspellende gegevens. Bijvoorbeeld, kan een detailhandelaar een segment met loyaliteitsstatus en plaatsgegevens (eigenschappen van Platform) tot stand brengen en [!DNL Airship] voorspeld om gegevens te koelen om hoogst gerichte berichten naar gebruikers in de gouden loyaliteitsstatus te verzenden die in Las Vegas, NV wonen, en een hoge waarschijnlijkheid van het kuren hebben.

## Verbinden met [!DNL Airship Attributes] {#connect-airship-attributes}

Blader in **[!UICONTROL Doelen]** > **[!UICONTROL Catalogus]** naar de categorie **[!UICONTROL Mobiele betrokkenheid]**. Selecteer **[!DNL Airship Attributes]**, dan uitgezocht **[!UICONTROL vorm]**.

>[!NOTE]
>
>Als er al een verbinding met dit doel bestaat, kunt u een **[!UICONTROL knop Activeer]** op de doelkaart zien. Voor meer informatie over het verschil tussen **[!UICONTROL Activate]** en **[!UICONTROL Configure]**, verwijs naar [Catalog](../../ui/destinations-workspace.md#catalog) sectie van de documentatie van de bestemmingswerkruimte.

![Verbinden met kenmerken van het luchtschip](../../assets/catalog/mobile-engagement/airship/catalog.png)

Als u in de stap **Account** eerder een verbinding met uw [!DNL Airship Attributes]-doel hebt ingesteld, selecteert u **[!UICONTROL Bestaande account]** en selecteert u de bestaande verbinding. U kunt ook **[!UICONTROL Nieuwe account]** selecteren om een nieuwe verbinding in te stellen met [!DNL Airship Attributes]. Selecteer **[!UICONTROL Verbinding maken met doel]** om Adobe Experience Platform te verbinden met uw [!DNL Airship]-project met behulp van het towertoken dat u hebt gegenereerd op het dashboard [!DNL Airship].

>[!NOTE]
>
>Adobe Experience Platform ondersteunt validatie van referenties in het verificatieproces en geeft een foutbericht weer als u onjuiste gegevens hebt ingevoerd voor uw [!DNL Airship]-account. Dit zorgt ervoor dat u de werkstroom niet met onjuiste geloofsbrieven voltooit.

![Verbinden met kenmerken van het luchtschip](../../assets/catalog/mobile-engagement/airship/connect.png)

Zodra uw geloofsbrieven worden bevestigd en Adobe Experience Platform wordt aangesloten aan uw [!DNL Airship] project, kunt u **[!UICONTROL Volgende]** selecteren om aan de **[!UICONTROL Opstelling]** stap te werk te gaan.

Voer in de stap **[!UICONTROL Verificatie]** een **[!UICONTROL Naam]** en een **[!UICONTROL Beschrijving]** voor uw activeringsstroom in.

In deze stap kunt u ook Amerikaans of EU-datacenter selecteren, afhankelijk van welk [!DNL Airship] datacenter op dit doel van toepassing is. Selecteer ten slotte een of meer gevallen waarin gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door de Adobe gedefinieerde gebruiksgevallen voor marketingdoeleinden of u kunt uw eigen gebruiksscenario&#39;s maken. Zie [Overzicht van beleidsregels voor gegevensgebruik](../../../data-governance/policies/overview.md) voor meer informatie over gevallen van marketinggebruik.

Selecteer **[!UICONTROL Doel maken]** nadat u de bovenstaande velden hebt ingevuld.

![Verbinden met kenmerken van het luchtschip](../../assets/catalog/mobile-engagement/airship/select-domain.png)

Uw doel is nu gemaakt. U kunt **[!UICONTROL Opslaan en afsluiten]** selecteren als u segmenten later wilt activeren of u kunt **[!UICONTROL Volgende]** selecteren om door te gaan met de workflow en segmenten te selecteren om te activeren. In beide gevallen raadpleegt u de volgende sectie [Segmenten activeren](#activate-segments) voor de rest van de workflow.

## Segmenten {#activate-segments} activeren

Volg onderstaande stappen om segmenten te activeren op [!DNL Airship Attributes]:

Selecteer in **[!UICONTROL Doelen > Bladeren]** de [!DNL Airship Attributes] bestemming waar u de segmenten wilt activeren.

![activeren-flow](../../assets/catalog/mobile-engagement/airship/browse.png)

Klik op de naam van het doel. Hiermee gaat u naar de flow Activeren.

Merk op dat als een activeringsstroom reeds voor een bestemming bestaat, u de segmenten kunt zien die momenteel naar de bestemming worden verzonden. Selecteer **[!UICONTROL Activering bewerken]** in de rechtertrack en voer de onderstaande stappen uit om de activeringsdetails te wijzigen.

![activeren-flow](../../assets/catalog/mobile-engagement/airship/activate.png)

Selecteer **[!UICONTROL Activeren]**. In **[!UICONTROL Activeer bestemming]** werkschema, op **[!UICONTROL Selecteer Segmenten]** pagina, selecteer welke segmenten om naar [!DNL Airship Attributes] te verzenden.

![segmenten-naar-bestemming](../../assets/catalog/mobile-engagement/airship/select-segments.png)

Selecteer in de stap **[!UICONTROL Toewijzing]** welke kenmerken en identiteiten in het schema [XDM](../../../xdm/home.md) om toe te wijzen aan het doelschema. Selecteer **[!UICONTROL Nieuwe toewijzing toevoegen]** om uw schema te doorbladeren en hen in kaart te brengen aan de overeenkomstige doelidentiteit.

![startscherm voor identiteitstoewijzing](../../assets/catalog/mobile-engagement/airship/identity-mapping.png)

[!DNL Airship] attributen kunnen op of een kanaal worden geplaatst, dat apparateninstantie, b.v., iPhone, of een genoemde gebruiker vertegenwoordigt, die alle apparaten van een gebruiker aan een gemeenschappelijk herkenningsteken zoals een klantenidentiteitskaart in kaart brengt. Als u gewone (unhashed) e-mailadressen als primaire identiteit in uw schema hebt, selecteer het e-mailgebied in uw **[!UICONTROL BronAttributen]** en kaart aan [!DNL Airship] genoemd gebruiker in de juiste kolom onder **[!UICONTROL Doelidentiteiten]**, zoals hieronder getoond.

![Toewijzing van benoemde gebruikers](../../assets/catalog/mobile-engagement/airship/mapping.png)

Voor herkenningstekens die aan een kanaal, d.w.z., een apparaat moeten worden in kaart gebracht, kaart aan het aangewezen kanaal dat op de bron wordt gebaseerd. De volgende afbeeldingen laten zien hoe twee toewijzingen worden gemaakt:

* IDFA iOS Advertising ID to an [!DNL Airship] iOS channel
* Adobe `fullName`-kenmerk naar [!DNL Airship]-kenmerk &quot;Volledige naam&quot;

>[!NOTE]
>
>Gebruik de gebruikersvriendelijke naam die op het dashboard [!DNL Airship] verschijnt wanneer het selecteren van het doelgebied voor uw attributenafbeelding.

**Identiteit kaart**

Bronveld selecteren:

![Verbinden met kenmerken van het luchtschip](../../assets/catalog/mobile-engagement/airship/select-source-identity.png)

Doelveld selecteren:

![Verbinden met kenmerken van het luchtschip](../../assets/catalog/mobile-engagement/airship/select-target-identity.png)

**Kenmerk Kaart**

Bronkenmerk selecteren:

![Bronveld selecteren](../../assets/catalog/mobile-engagement/airship/select-source-attributes.png)

Doelkenmerk selecteren:

![Doelveld selecteren](../../assets/catalog/mobile-engagement/airship/select-target-attribute.png)

Toewijzing verifiëren:

![Kanaaltoewijzing](../../assets/catalog/mobile-engagement/airship/mapping.png)

Op **[!UICONTROL Segmentprogramma]** pagina, is het plannen momenteel gehandicapt. Klik **[!UICONTROL Volgende]** om door te gaan aan de overzichtsstap.

![Momenteel uitgeschakeld plannen](../../assets/catalog/mobile-engagement/airship/scheduling.png)

Op de **[!UICONTROL pagina van het Overzicht]**, kunt u een samenvatting van uw selectie zien. Selecteer **[!UICONTROL Annuleren]** om de stroom te verbreken, **[!UICONTROL Terug]** om uw instellingen te wijzigen of **[!UICONTROL Voltooien]** om uw selectie te bevestigen en gegevens naar de bestemming te verzenden.

>[!IMPORTANT]
>
>In deze stap controleert Adobe Experience Platform op overtredingen van het gegevensgebruiksbeleid. Hieronder ziet u een voorbeeld waarin een beleid wordt overtreden. U kunt de workflow voor segmentactivering pas voltooien nadat u de schending hebt opgelost. Voor informatie over hoe te om beleidsschendingen op te lossen, zie [Beleidshandhaving](../../../data-governance/enforcement/auto-enforcement.md) in de sectie van de documentatie van het gegevensbeheer.

![selectie bevestigen](../../assets/common/data-policy-violation.png)

Als er geen beleidsovertredingen zijn vastgesteld, selecteert u **[!UICONTROL Voltooien]** om uw selectie te bevestigen en gegevens naar de bestemming te verzenden.

![revisie](../../assets/catalog/mobile-engagement/airship/review.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Zie [Overzicht gegevensbeheer](../../../data-governance/home.md) voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt.
