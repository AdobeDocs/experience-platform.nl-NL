---
keywords: luchtschepen, codes;bestemming van het luchtschip
title: Koppeling met vliegtuigcodes
description: Geef naadloos Adobe-geluidsgegevens van het publiek door aan het luchtschip als Publiek-tags voor doelwit binnen het luchtschip.
translation-type: tm+mt
source-git-commit: 7d579d85d427c45f39d000288ed883c7ffd003bf
workflow-type: tm+mt
source-wordcount: '1134'
ht-degree: 0%

---


# (Bèta) [!DNL Airship Tags] verbinding {#airship-tags-destination}

>[!IMPORTANT]
>
>De bestemming [!DNL Airship Tags] in Adobe Experience Platform is momenteel in bèta. De documentatie en de functionaliteit kunnen worden gewijzigd.

## Overzicht

[!DNL Airship] is het toonaangevende Platform voor betrokkenheid van klanten, waarmee u in elke fase van de levenscyclus van de klant betekenisvolle, gepersonaliseerde omnichanale berichten aan uw gebruikers kunt leveren.

Deze integratie gaat Adobe Experience Platform segmentgegevens in [!DNL Airship] als [Codes](https://docs.airship.com/guides/audience/tags/) voor het richten of het teweegbrengen over.

Zie [Airship Docs](https://docs.airship.com) voor meer informatie over [!DNL Airship].


>[!TIP]
>
>Deze documentatiepagina is gemaakt door het team van [!DNL Airship]. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen via [support.airship.com](https://support.airship.com/).

## Vereisten

Voordat u uw Adobe Experience Platform-segmenten kunt verzenden naar [!DNL Airship], moet u:

* Creeer een markeringsgroep in uw [!DNL Airship] project.
* Een token voor toonder genereren voor verificatie.

>[!TIP]
> 
>Maak een [!DNL Airship]-account via [deze aanmeldlink](https://go.airship.eu/accounts/register/plan/starter/) als u dat nog niet hebt gedaan.

## Taggroepen

Het concept van segmenten in het platform van de Ervaring van Adobe is gelijkaardig aan [Markeringen](https://docs.airship.com/guides/audience/tags/) in Airship, met lichte verschillen in implementatie. Door deze integratie wordt de status van een [lidmaatschap van een gebruiker in een Experience Platform segment](https://experienceleague.adobe.com/docs/experience-platform/xdm/mixins/profile/segmentation.html?lang=en#mixins) toegewezen aan de aanwezigheid of niet-aanwezigheid van een [!DNL Airship]-tag. Bijvoorbeeld, in een segment van het Platform waar `xdm:status` in `realized` verandert, wordt de markering toegevoegd aan [!DNL Airship] kanaal of genoemde gebruiker wordt dit profiel in kaart gebracht aan. Als `xdm:status` in `exited` verandert, wordt de markering verwijderd.

Om deze integratie toe te laten, creeer een *markeringsgroep* in [!DNL Airship] genoemd `adobe-segments`.

>[!IMPORTANT]
>
>Wanneer het creëren van uw nieuwe markeringsgroep **controleer** niet het radioknoop dat &quot;[!DNL Allow these tags to be set only from your server]&quot;zegt. Als u dit doet, mislukt de integratie van de Adobe-tags.

Zie [Taggroepen beheren](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) voor instructies over het maken van de taggroep.

## Dragertoken genereren

Ga naar **[!UICONTROL Settings]**&quot; **[!UICONTROL APIs & Integrations]** in [Luchtvaartdashboard](https://go.airship.com) en selecteer **[!UICONTROL Tokens]** in het linkermenu.

Klik op **[!UICONTROL Create Token]**.

Geef uw token een gebruikersvriendelijke naam, bijvoorbeeld &quot;Doel van Adobe-tags&quot;, en selecteer &quot;Alle toegang&quot; voor de rol.

Klik op **[!UICONTROL Create Token]** en sla de details op als vertrouwelijk.

## Gebruiksscenario’s

Om u beter te helpen begrijpen hoe en wanneer u [!DNL Airship Tags] bestemming zou moeten gebruiken, zijn hier voorbeelden van gebruiksgevallen die de klanten van Adobe Experience Platform door deze bestemming kunnen oplossen.

### Hoofdletters gebruiken #1

Detailhandelaars of entertainmentplatforms kunnen gebruikersprofielen maken voor hun klanten die loyaal zijn en die segmenten doorgeven aan [!DNL Airship] voor berichten die bestemd zijn voor mobiele campagnes.

### Hoofdletters gebruiken #2

U kunt een-op-een berichten in real-time activeren wanneer gebruikers binnen of buiten specifieke segmenten in Adobe Experience Platform vallen.

Een detailhandelaar stelt bijvoorbeeld een merkspecifiek segment voor jeans in Platform in. Deze detailhandelaar kan nu een mobiel bericht activeren zodra iemand zijn jeans-voorkeur op een bepaald merk instelt.

## Verbinden met [!DNL Airship Tags] {#connect-airship-tags}

Blader in **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** naar de categorie **[!UICONTROL Mobile Engagement]**. Selecteer **[!DNL Airship Tags]** en selecteer **[!UICONTROL Configure]**.

>[!NOTE]
>
>Als er al een verbinding met dit doel bestaat, kunt u een **[!UICONTROL Activate]** knop op de doelkaart zien. Raadpleeg voor meer informatie over het verschil tussen **[!UICONTROL Activate]** en **[!UICONTROL Configure]** de sectie [Catalog](../../ui/destinations-workspace.md#catalog) van de documentatie van de doelwerkruimte.

![Verbinden met luchtvaartcodes](../../assets/catalog/mobile-engagement/airship-tags/catalog.png)

Als u in de stap **Account** eerder een verbinding met uw [!DNL Airship Tags]-doel hebt ingesteld, selecteert u **[!UICONTROL Existing Account]** en selecteert u de bestaande verbinding. U kunt ook **[!UICONTROL New Account]** selecteren om een nieuwe verbinding in te stellen met [!DNL Airship Tags]. Selecteer **[!UICONTROL Connect to destination]** om Adobe Experience Platform met uw [!DNL Airship] project te verbinden gebruikend het dragerteken dat u van het [!DNL Airship] dashboard produceerde.

>[!NOTE]
>
>Adobe Experience Platform ondersteunt validatie van referenties in het verificatieproces en geeft een foutbericht weer als u onjuiste gegevens hebt ingevoerd voor uw [!DNL Airship]-account. Dit zorgt ervoor dat u de werkstroom niet met onjuiste geloofsbrieven voltooit.

![Verbinden met luchtvaartcodes](../../assets/catalog/mobile-engagement/airship-tags/connect-account.png)

Nadat uw referenties zijn bevestigd en Adobe Experience Platform is verbonden met uw [!DNL Airship]-project, kunt u **[!UICONTROL Next]** selecteren om door te gaan naar de stap **[!UICONTROL Setup]**.

Voer in de stap **[!UICONTROL Authentication]** een **[!UICONTROL Name]** en een **[!UICONTROL Description]** in voor de activeringsstroom.

In deze stap kunt u ook Amerikaans of EU-datacenter selecteren, afhankelijk van welk [!DNL Airship] datacenter op dit doel van toepassing is. Tot slot selecteer één of meerdere **[!UICONTROL Marketing Actions]** waarvoor de gegevens naar de bestemming zullen worden uitgevoerd. U kunt kiezen uit door Adobe gedefinieerde marketingacties of u kunt uw eigen acties maken. Voor meer informatie over marketing acties, zie [Overzicht van het beleid van het gebruik van Gegevens](../../../data-governance/policies/overview.md).

Selecteer **[!UICONTROL Create Destination]** nadat u de bovenstaande velden hebt ingevuld.

![Verbinden met luchtvaartcodes](../../assets/catalog/mobile-engagement/airship-tags/select-domain.png)

Uw doel is nu gemaakt. U kunt **[!UICONTROL Save & Exit]** selecteren als u segmenten later wilt activeren of u kunt **[!UICONTROL Next]** selecteren om de workflow voort te zetten en segmenten te selecteren om te activeren. In beide gevallen raadpleegt u de volgende sectie [Segmenten activeren](#activate-segments) voor de rest van de workflow.

## Segmenten {#activate-segments} activeren

Volg onderstaande stappen om segmenten te activeren op [!DNL Airship Tags]:

Selecteer in **[!UICONTROL Destinations > Browse]** de bestemming [!DNL Airship Tags] waar u de segmenten wilt activeren.

![activeren-flow](../../assets/catalog/mobile-engagement/airship-tags/browse.png)

Klik op de naam van het doel. Hiermee gaat u naar de flow Activeren.

Merk op dat als een activeringsstroom reeds voor een bestemming bestaat, u de segmenten kunt zien die momenteel naar de bestemming worden verzonden. Selecteer **[!UICONTROL Edit activation]** in het rechterspoor en volg de onderstaande stappen om de activeringsdetails te wijzigen.

![activeren-flow](../../assets/catalog/mobile-engagement/airship-tags/activate.png)

Selecteer **[!UICONTROL Activate]**. Selecteer in de **[!UICONTROL Activate destination]**-workflow op de **[!UICONTROL Select Segments]**-pagina welke segmenten naar [!DNL Airship Tags] moeten worden verzonden.

![segmenten-naar-bestemming](../../assets/catalog/mobile-engagement/airship-tags/select-segments.png)

In de **[!UICONTROL Mapping]** stap, selecteer welke attributen en identiteiten van [XDM](../../../xdm/home.md) schema aan kaart aan het bestemmingsschema. Selecteer **[!UICONTROL Add new mapping]** om uw schema te doorbladeren en hen in kaart te brengen aan de overeenkomstige doelidentiteit.

![startscherm voor identiteitstoewijzing](../../assets/catalog/mobile-engagement/airship-tags/identity-mapping.png)

[!DNL Airship] tags kunnen worden ingesteld op een kanaal dat apparaatinstantie vertegenwoordigt, bijvoorbeeld iPhone, of een benoemde gebruiker, die alle apparaten van een gebruiker toewijst aan een gemeenschappelijke id, zoals een klant-id. Als u gewone (niet-gehakte) e-mailadressen als primaire identiteit in uw schema hebt, selecteer het e-mailgebied in uw **[!UICONTROL Source Attributes]** en kaart aan [!DNL Airship] genoemde gebruiker in de juiste kolom onder **[!UICONTROL Target Identities]**, zoals hieronder getoond.

![Toewijzing van benoemde gebruikers](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

Voor herkenningstekens die aan een kanaal, d.w.z., een apparaat moeten worden in kaart gebracht, kaart aan het aangewezen kanaal dat op de bron wordt gebaseerd. In de volgende afbeeldingen ziet u hoe u een Google Advertising-id toewijst aan een Android-kanaal [!DNL Airship].

![Verbinden met ](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![Airship TagsVerbinden met ](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![Airship TagsChannel-toewijzing](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

Op de pagina **[!UICONTROL Segment schedule]** is planning momenteel uitgeschakeld. Klik op **[!UICONTROL Next]** om door te gaan naar de revisiestap.

Op de **[!UICONTROL Review]** pagina, kunt u een samenvatting van uw selectie zien. Selecteer **[!UICONTROL Cancel]** om de stroom te verbreken, **[!UICONTROL Back]** om uw montages te wijzigen, of **[!UICONTROL Finish]** om uw selectie te bevestigen en te beginnen gegevens naar de bestemming te verzenden.

>[!IMPORTANT]
>
>In deze stap controleert Adobe Experience Platform op overtredingen van het gegevensgebruiksbeleid. Hieronder ziet u een voorbeeld waarin een beleid wordt overtreden. U kunt de workflow voor segmentactivering pas voltooien nadat u de schending hebt opgelost. Voor informatie over hoe te om beleidsschendingen op te lossen, zie [Beleidshandhaving](../../../data-governance/enforcement/auto-enforcement.md) in de sectie van de documentatie van het gegevensbeheer.

![selectie bevestigen](../../assets/common/data-policy-violation.png)

Als er geen beleidsovertredingen zijn vastgesteld, selecteert u **[!UICONTROL Finish]** om uw selectie te bevestigen en gegevens naar de bestemming te verzenden.

![selectie bevestigen](../../assets/catalog/mobile-engagement/airship-tags/review.png)


## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Zie [Overzicht gegevensbeheer](../../../data-governance/home.md) voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt.

