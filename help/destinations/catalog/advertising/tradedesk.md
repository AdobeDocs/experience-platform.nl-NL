---
keywords: reclame; de handelsdienst; reclamebureau
title: De verbinding van de handelsbureau
description: De Trade Desk is een zelfbedieningsplatform waarmee adverteerders doelgerichte digitale campagnes kunnen voeren op het hele scherm, de video en mobiele inventarisatiebronnen.
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: 802b1844bec1e577e978da5d5a69de87278c04b9
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 1%

---

# [!DNL The Trade Desk] verbinding

## Overzicht {#overview}

[!DNL The Trade Desk] doel helpt u profielgegevens te verzenden naar  [!DNL The Trade Desk].

[!DNL The Trade Desk] is een zelfbedieningsplatform dat kopers van advertenties in staat stelt doelgerichte digitale campagnes uit te voeren op het hele scherm, de video en mobiele inventarisatiebronnen.

Als u profielgegevens naar [!DNL Trade Desk] wilt verzenden, moet u eerst verbinding maken met het doel.

## Gebruiksscenario’s {#use-cases}

Als markeerteken, wil ik segmenten kunnen gebruiken die van [!DNL Trade Desk IDs] of apparaat IDs worden gebouwd om het opnieuw richten of publiek gerichte digitale campagnes tot stand te brengen.

## Ondersteunde identiteiten {#supported-identities}

[!DNL The Trade Desk] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](/help/identity-service/namespaces.md).

| Doelidentiteit | Beschrijving |
|---|---|
| GAID | [!DNL Google Advertising ID] |
| IDFA | [!DNL Apple ID for Advertisers] |
| Handelsbureau-id | Advertiser-id in het Trade Desk-platform |

## Exporttype {#export-type}

**[!DNL Segment export]** - u exporteert alle leden van een segment (publiek) naar de bestemming.

## Vereisten {#prerequisites}

Als u uw eerste bestemming met [!DNL The Trade Desk] wilt maken en in het verleden (met Adobe Audience Manager of andere toepassingen) de [ID-synchronisatiefunctionaliteit](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) niet hebt ingeschakeld in de Experience Cloud ID-service, neemt u contact op met Adobe Consulting of de klantenservice om id-syncs in te schakelen. Als u eerder [!DNL The Trade Desk] integraties in Audience Manager had opgezet, de syncs van identiteitskaart u opstelling dragen over aan Platform.

## Verbinden met de bestemming {#connect}

Om met deze bestemming te verbinden, volg de stappen in [het leerprogramma van de bestemmingsconfiguratie](../../ui/connect-destination.md) worden beschreven.

### Verbindingsparameters {#parameters}

Terwijl [vestiging](../../ui/connect-destination.md) deze bestemming, u de volgende informatie moet verstrekken:

* **[!UICONTROL Name]**: Een naam waarmee u deze bestemming in de toekomst zult erkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Account ID]**: Uw [!DNL Trade Desk] [!UICONTROL Account ID].
* **[!UICONTROL Server Location]**: Vraag uw  [!DNL Trade Desk] vertegenwoordiger welke regionale server u zou moeten gebruiken. Dit zijn de beschikbare regionale servers waaruit u kunt kiezen:
   * **[!UICONTROL Europe]**
   * **[!UICONTROL Singapore]**
   * **[!UICONTROL Tokyo]**
   * **[!UICONTROL North America East]**
   * **[!UICONTROL North America West]**
   * **[!UICONTROL Latin America]**

## Segmenten naar dit doel activeren {#activate}

Zie [Profielen en segmenten activeren aan een doel](../../ui/activate-destinations.md) voor instructies bij het activeren van publiekssegmenten aan bestemmingen.

In [Segmentprogramma](../../ui/activate-destinations.md#segment-schedule) stap, moet u uw segmenten aan hun overeenkomstige identiteitskaart of vriendschappelijke naam in het bestemmingsplatform manueel in kaart brengen.

Wanneer het in kaart brengen van segmenten, adviseren wij u de naam van het Platform of een kortere vorm van het, voor gebruiksgemak gebruiken. Nochtans, te hoeven segmentidentiteitskaart of de naam in uw bestemming niet om in uw rekening van het Platform aan te passen. Elke waarde die u in het toewijzingsveld invoegt, wordt weerspiegeld door het doel.

Als u veelvoudige apparatenafbeeldingen (koekje IDs, [!DNL IDFA], [!DNL GAID]) gebruikt, zorg ervoor om de zelfde toewijzingswaarde voor alle drie afbeeldingen te gebruiken. [!DNL The Trade Desk] zij zullen allen in één enkel segment, met een apparaat-vlakke onderbreking bijeenvoegen.

![Id voor segmenttoewijzing](../../assets/common/segment-mapping-id.png)

## Geëxporteerde gegevens {#exported-data}

Controleer uw [!DNL Trade Desk]-account om te controleren of gegevens zijn geëxporteerd naar de [!DNL The Trade Desk]-bestemming. Als de activering succesvol was, worden de soorten publiek in uw account ingevuld.
