---
keywords: luchtschepen, codes;bestemming van het luchtschip
title: Koppeling met vliegtuigcodes
description: Geef naadloos Adobe-geluidsgegevens van het publiek door aan het luchtschip als Publiek-tags voor doelwit binnen het luchtschip.
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
source-git-commit: e413933920028e3239f6044111d9cf215c865eba
workflow-type: tm+mt
source-wordcount: '688'
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

Het concept van segmenten in het platform van de Ervaring van Adobe is gelijkaardig aan [Markeringen](https://docs.airship.com/guides/audience/tags/) in Airship, met lichte verschillen in implementatie. Door deze integratie wordt de status van een [lidmaatschap van een gebruiker in een Experience Platform segment](../../../xdm/field-groups/profile/segmentation.md) toegewezen aan de aanwezigheid of niet-aanwezigheid van een [!DNL Airship]-tag. Bijvoorbeeld, in een segment van het Platform waar `xdm:status` in `realized` verandert, wordt de markering toegevoegd aan [!DNL Airship] kanaal of genoemde gebruiker wordt dit profiel in kaart gebracht aan. Als `xdm:status` in `exited` verandert, wordt de markering verwijderd.

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

## Verbinden met de bestemming {#connect}

Om met deze bestemming te verbinden, volg de stappen in [het leerprogramma van de bestemmingsconfiguratie](../../ui/connect-destination.md) worden beschreven.

### Verbindingsparameters {#parameters}

Terwijl [vestiging](../../ui/connect-destination.md) deze bestemming, u de volgende informatie moet verstrekken:

* **[!UICONTROL Bearer token]**: De token die u hebt gegenereerd van het  [!DNL Airship] dashboard.
* **[!UICONTROL Name]**: Voer een naam in die u helpt deze bestemming te identificeren.
* **[!UICONTROL Description]**: Voer een beschrijving in voor deze bestemming.
* **[!UICONTROL Domain]**: Selecteer een Amerikaans of EU-datacenter, afhankelijk van het  [!DNL Airship] datacenter dat op dit doel van toepassing is.


## Segmenten naar dit doel activeren {#activate}

Zie [De publieksgegevens van Activate aan het stromen segment de uitvoerbestemmingen ](../../ui/activate-segment-streaming-destinations.md) voor instructies op het activeren van publiekssegmenten aan deze bestemming.

## Toewijzingsoverwegingen {#mapping-considerations}

[!DNL Airship] tags kunnen worden ingesteld op een kanaal dat apparaatinstantie vertegenwoordigt, bijvoorbeeld iPhone, of een benoemde gebruiker, die alle apparaten van een gebruiker toewijst aan een gemeenschappelijke id, zoals een klant-id. Als u gewone (niet-gehakte) e-mailadressen als primaire identiteit in uw schema hebt, selecteer het e-mailgebied in uw **[!UICONTROL Source Attributes]** en kaart aan [!DNL Airship] genoemde gebruiker in de juiste kolom onder **[!UICONTROL Target Identities]**, zoals hieronder getoond.

![Toewijzing van benoemde gebruikers](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

Voor herkenningstekens die aan een kanaal, d.w.z., een apparaat moeten worden in kaart gebracht, kaart aan het aangewezen kanaal dat op de bron wordt gebaseerd. In de volgende afbeeldingen ziet u hoe u een Google Advertising-id toewijst aan een Android-kanaal [!DNL Airship].

![Verbinden met ](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![Airship TagsVerbinden met ](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![Airship TagsChannel-toewijzing](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Zie [Overzicht gegevensbeheer](../../../data-governance/home.md) voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt.
