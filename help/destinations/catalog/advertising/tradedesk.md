---
keywords: reclame; de handelsdienst; reclamebureau
title: De verbinding van de handelsbureau
description: De Trade Desk is een zelfbedieningsplatform waarmee adverteerders doelgerichte digitale campagnes kunnen voeren op het hele scherm, de video en mobiele inventarisatiebronnen.
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: b1945d42b82b549985d848071762fa6ee2451368
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# [!DNL The Trade Desk] verbinding

## Overzicht {#overview}

[!DNL The Trade Desk] doel helpt u profielgegevens te verzenden naar [!DNL The Trade Desk].

[!DNL The Trade Desk] is een zelfbedieningsplatform dat kopers van advertenties in staat stelt doelgerichte digitale campagnes uit te voeren op het hele scherm, de video en mobiele inventarisatiebronnen.

Profielgegevens verzenden naar [!DNL Trade Desk], moet u eerst verbinding maken met het doel.

## Gebruiksscenario’s {#use-cases}

Als telleraar, wil ik segmenten kunnen gebruiken die van worden gebouwd [!DNL Trade Desk IDs] of apparaat-id&#39;s om doelgerichte digitale campagnes te maken.

## Ondersteunde identiteiten {#supported-identities}

[!DNL The Trade Desk] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](/help/identity-service/namespaces.md).

| Doelidentiteit | Beschrijving |
|---|---|
| GAID | [!DNL Google Advertising ID] |
| IDFA | [!DNL Apple ID for Advertisers] |
| Handelsbureau-id | Advertiser-id in het Trade Desk-platform |

{style=&quot;table-layout:auto&quot;}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Segment export]** | U exporteert alle leden van een segment (publiek) naar de bestemming. |
| Uitvoerfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op segmentevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Vereisten {#prerequisites}

>[!IMPORTANT]
>
>Als u uw eerste bestemming wilt maken met [!DNL The Trade Desk] en hebben de [ID-synchronisatiefunctie](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) in Experience Cloud ID Service in het verleden (met Adobe Audience Manager of andere toepassingen), neemt u contact op met Adobe Consulting of Customer Care om ID-syncs in te schakelen. Als u al eerder was ingesteld [!DNL The Trade Desk] Als u integreert in Audience Manager, worden de id-syncs die u hebt ingesteld, overgedragen naar Platform.

## Verbinden met de bestemming {#connect}

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md).

### Verbindingsparameters {#parameters}

while [opzetten](../../ui/connect-destination.md) voor deze bestemming moet u de volgende informatie opgeven:

* **[!UICONTROL Name]**: Een naam waarmee u deze bestemming in de toekomst zult erkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Account ID]**: Uw [!DNL Trade Desk] [!UICONTROL Account ID].
* **[!UICONTROL Server Location]**: Vraag uw [!DNL Trade Desk] representatief voor welke regionale server u zou moeten gebruiken. Dit zijn de beschikbare regionale servers waaruit u kunt kiezen:
   * **[!UICONTROL Europe]**
   * **[!UICONTROL Singapore]**
   * **[!UICONTROL Tokyo]**
   * **[!UICONTROL North America East]**
   * **[!UICONTROL North America West]**
   * **[!UICONTROL Latin America]**

## Segmenten naar dit doel activeren {#activate}

Zie [De publieksgegevens van de activering aan het stromen segment de uitvoerbestemmingen](../../ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

In de [Segmentatieschema](../../ui/activate-segment-streaming-destinations.md#scheduling) stap, moet u uw segmenten aan hun overeenkomstige identiteitskaart of vriendschappelijke naam in het bestemmingsplatform manueel in kaart brengen.

Wanneer het in kaart brengen van segmenten, adviseren wij u de naam van het Platform of een kortere vorm van het, voor gebruiksgemak gebruiken. Nochtans, te hoeven segmentidentiteitskaart of de naam in uw bestemming niet om in uw rekening van het Platform aan te passen. Elke waarde die u in het toewijzingsveld invoegt, wordt weerspiegeld door het doel.

Als u meerdere apparaattoewijzingen gebruikt (cookie-id&#39;s, [!DNL IDFA], [!DNL GAID]), moet u dezelfde toewijzingswaarde gebruiken voor alle drie de toewijzingen. [!DNL The Trade Desk] zij zullen allen in één enkel segment, met een apparaat-vlakke onderbreking bijeenvoegen.

![Id voor segmenttoewijzing](../../assets/common/segment-mapping-id.png)

## Geëxporteerde gegevens {#exported-data}

Controleren of gegevens zijn geëxporteerd naar [!DNL The Trade Desk] doel, controleer uw [!DNL Trade Desk] account. Als de activering succesvol was, worden de soorten publiek in uw account ingevuld.
