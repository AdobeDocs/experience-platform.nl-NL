---
keywords: advertising; the trade desk;
title: De bestemming van het handelsbureau
seo-title: De bestemming van het handelsbureau
description: 'De Trade Desk is een zelfbedieningsplatform waarmee adverteerders doelgerichte digitale campagnes kunnen voeren op het hele scherm, de video en de mobiele voorraad. '
seo-description: De Trade Desk is een zelfbedieningsplatform waarmee adverteerders doelgerichte digitale campagnes kunnen voeren op het hele scherm, de video en de mobiele voorraad.
translation-type: tm+mt
source-git-commit: a64f9f1f078d8380cc25c9760eac1699512a5870
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 0%

---


# [!DNL The Trade Desk] doel

## Overzicht {#overview}

[!DNL The Trade Desk] doel helpt u profielgegevens te verzenden naar [!DNL The Trade Desk].

[!DNL The Trade Desk] is een zelfbedieningsplatform dat kopers van advertenties in staat stelt doelgerichte digitale campagnes uit te voeren op het hele scherm, de video en mobiele inventarisatiebronnen.

Als u profielgegevens naar wilt verzenden, moet u eerst verbinding maken met het doel. [!DNL The Trade Desk]

## Doelspecificaties {#destination-specs}

Let op de volgende details die specifiek zijn voor het [!DNL The Trade Desk] doel:

* U kunt de volgende [identiteiten](../../identity-service/namespaces.md) naar [!DNL The Trade Desk] bestemmingen verzenden: [!DNL The Trade Desk ID], [!DNL IDFA], [!DNL GAID].

## Gebruiksscenario’s {#use-cases}

Als markator, wil ik segmenten kunnen gebruiken die van of apparaat IDs worden gebouwd om het opnieuw richten of publiek gerichte digitale campagnes tot stand te brengen. [!DNL Trade Desk IDs]

## Exporttype {#export-type}

**[!DNL Segment export]** - u exporteert alle leden van een segment (publiek) naar de bestemming.

## Verbinden met doel {#connect-destination}

1. Selecteer in **[!UICONTROL Verbindingen]** > **[!UICONTROL Doelen]** de optie [!DNL The Trade Desk]en selecteer **[!UICONTROL Configureren]**.

   ![Vorm de bestemming van de handelsbureau](assets/tradedesk-destination-configure.png)

   >[!NOTE]
   >
   >Als er al een verbinding met dit doel bestaat, ziet u een knop **[!UICONTROL Activeren]** op de doelkaart. Voor meer informatie over het verschil tussen **[!UICONTROL Activate]** en **[!UICONTROL Configure]**, verwijs naar de sectie van de [Catalogus](../destinations/destinations-workspace.md#catalog) van de documentatie van de bestemmingswerkruimte.
   >
   >![Activeer de bestemming van het handelsbureau](assets/tradedesk-destination-activate.png)

2. In de stap [!UICONTROL Verificatie] moet u [!DNL The Trade Desk] verbindingsgegevens invoeren:

   * **[!UICONTROL Naam]**: Een naam waarmee u deze bestemming in de toekomst zult erkennen.
   * **[!UICONTROL Omschrijving]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
   * **[!UICONTROL Account-id]**: Je [!DNL Trade Desk] account-id .
   * **[!UICONTROL Clientgeheim]**: De `clientSecret` parameter die in de [!DNL OAuth2] clientreferenties wordt gebruikt.
   * **[!UICONTROL Serverlocatie]**: Vraag uw [!DNL The Trade Desk] vertegenwoordiger welke regionale server u zou moeten gebruiken. Dit zijn de beschikbare regionale servers waaruit u kunt kiezen:

      * **[!UICONTROL Europa]**
      * **[!UICONTROL Singapore]**
      * **[!UICONTROL Tokyo]**
      * **[!UICONTROL Noord-Amerika Oost]**
      * **[!UICONTROL North America West]**
      * **[!UICONTROL Latijns-Amerika]**
   * **[!UICONTROL Geval]** voor gebruik bij het in de handel brengen: Gebruiksgevallen voor marketingdoeleinden geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door de Adobe gedefinieerde gebruiksgevallen voor marketingdoeleinden of u kunt uw eigen gebruiksscenario voor marketingdoeleinden maken. Raadpleeg de pagina [Data Governance in Adobe Experience Platform](../privacy/data-governance-overview.md#destinations) voor meer informatie over gevallen van marketinggebruik. Voor informatie over de individuele Adobe-bepaalde het in de handel brengen gebruiksgevallen, zie het overzicht [van het het gebruiksbeleid van](../../data-governance/policies/overview.md#core-actions)Gegevens.

   ![De Stap van de Authentificatie van het Handelsbureau](assets/tradedesk-destination-authentication.png)

3. Klik op **[!UICONTROL Doel]** maken. Uw doel is nu gemaakt. U kunt op [!UICONTROL Opslaan en afsluiten] klikken als u de segmenten later wilt activeren. U kunt ook [!UICONTROL Volgende] selecteren om door te gaan met de workflow en de gewenste segmenten te selecteren. In beide gevallen raadpleegt u de volgende sectie Segmenten [](#activate-segments)activeren voor de rest van de workflow.

## Segmenten activeren {#activate-segments}

Zie Profielen en segmenten [activeren naar een doel](activate-destinations.md#select-attributes) voor informatie over de workflow voor segmentactivering.

In de het programmastap [van het](activate-destinations.md#segment-schedule) Segment, moet u uw segmenten aan hun overeenkomstige identiteitskaart of vriendschappelijke naam in de bestemming manueel in kaart brengen.

Wanneer het in kaart brengen van segmenten, adviseren wij u de [!DNL Platform] segmentnaam of een kortere vorm van het, voor gebruiksgemak gebruiken. De segment-id of naam in uw bestemming hoeft echter niet overeen te komen met de id of naam in uw [!DNL Platform] account. Elke waarde die u in het toewijzingsveld invoegt, wordt weerspiegeld door het doel.

Als u meerdere apparaattoewijzingen gebruikt (cookie-id&#39;s, [!DNL IDFA], [!DNL GAID]), moet u dezelfde toewijzingswaarde gebruiken voor alle drie toewijzingen. [!DNL The Trade Desk] zij zullen allen in één enkel segment, met een apparaat-vlakke onderbreking bijeenvoegen.

![Id voor segmenttoewijzing](assets/segment-mapping-id.png)


## Geëxporteerde gegevens {#exported-data}

Controleer uw [!DNL The Trade Desk] account om te controleren of gegevens naar de [!DNL The Trade Desk] bestemming zijn geëxporteerd. Als de activering succesvol was, worden de soorten publiek in uw account ingevuld.
