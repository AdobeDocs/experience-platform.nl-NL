---
title: Doel van Auditieanalyse
description: Bekijk het publiek waarvoor klanten in Customer Journey Analytics in aanmerking komen.
badgeLimitedAvailability: label="Beperkte beschikbaarheid" type="Informative"
exl-id: 81437237-d746-4ce9-b938-7d2541f0ed32
hide: true
hidefromtoc: true
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 1%

---

# Doel van Auditieanalyse

Gebruik de [!UICONTROL Audience Analysis] bestemming om [!DNL Adobe Experience Platform] publieksgegevens in [&#x200B; Customer Journey Analytics &#x200B;](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=nl-NL) te verrijken. U kunt selecteren welk publiek u in de resulterende verrijkte gegevens wilt opnemen. De kwalificaties van het publiek zijn dan beschikbaar als afmetingen in [&#x200B; Analysis Workspace &#x200B;](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/home.html?lang=nl-NL) rapporterend.

>[!AVAILABILITY]
>
>Deze bestemming bevindt zich in een beperkte testfase. Neem contact op met het Adobe-accountteam als u deze bestemming wilt gebruiken.

## Vereisten {#prerequisites}

Het volgende wordt vereist alvorens deze bestemming te gebruiken:

* U moet worden provisioned om de bestemming van de Analyse van de Publiek te gebruiken. Neem contact op met uw Adobe-accountteam als u nog geen provisioned bent voor het gebruik van deze bestemming.
* U moet zijn ingericht om Customer Journey Analytics te kunnen gebruiken.
* Er moet ten minste één publiek worden gemaakt in [!DNL Adobe Experience Platform] .

## Ondersteunde identiteiten {#supported-identities}

De Analyse van het publiek steunt de activering van identiteiten die in de lijst hieronder worden beschreven. Leer meer over [&#x200B; identiteiten &#x200B;](/help/identity-service/features/namespaces.md). Experience Cloud-id (ECID) wordt doorgaans gebruikt.

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Selecteer de GAID doelidentiteit wanneer uw bronidentiteit een GAID-naamruimte is. |
| IDFA | Apple-id voor adverteerders | Selecteer de IDFA doelidentiteit wanneer uw bronidentiteit een IDFA namespace is. |
| ECID | Experience Cloud-id | Een naamruimte die ECID vertegenwoordigt. Deze namespace kan ook door de volgende aliassen worden bedoeld: &quot;identiteitskaart van Adobe Marketing Cloud&quot;, &quot;[!DNL Adobe Experience Cloud] identiteitskaart&quot;, &quot;[!DNL Adobe Experience Platform] identiteitskaart&quot;. Zie het volgende document op [&#x200B; ECID &#x200B;](/help/identity-service/features/ecid.md) voor meer informatie. |
| phone_sha256 | Telefoonnummers die zijn hashed met het SHA256-algoritme | Onbewerkte tekst en via SHA256 gehashte telefoonnummers worden ondersteund door [!DNL Adobe Experience Platform] . Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in om de gegevens automatisch te laten hashen bij activering door [!DNL Experience Platform] . |
| email_lc_sha256 | E-mailadressen die met het algoritme SHA256 worden gehasht | Zowel platte tekst als gehashte e-mailadressen van SHA256 worden ondersteund door [!DNL Adobe Experience Platform]. Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in om de gegevens automatisch te laten hashen bij activering door [!DNL Experience Platform] . |
| extern_id | Aangepaste gebruikers-id&#39;s | Selecteer deze doelidentiteit wanneer uw bronidentiteit een aangepaste naamruimte is. |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

De volgende soorten doelgroepen worden ondersteund bij gebruik van dit doel:

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | Ja | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#x200B; &#x200B;](../../../segmentation/home.md). |
| Alle andere doelgroepen | Nee | Deze categorie omvat alle oorsprong van het publiek buiten het publiek dat via [!DNL Segmentation Service] wordt gegenereerd. Lees over de [&#x200B; diverse publieksoorsprong &#x200B;](/help/segmentation/ui/audience-portal.md#customize). Voorbeelden zijn: <ul><li> de douane uploadt publiek [&#x200B; ingevoerde &#x200B;](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers,</li><li> gelijksoortige doelgroepen, </li><li> federaal publiek, </li><li> publiek dat wordt gegenereerd in andere Experience Platform-toepassingen, zoals [!DNL Adobe Journey Optimizer] , </li><li> en meer. </li></ul> |

{style="table-layout:auto"}



Ondersteund publiek per type publieksgegevens:

| Gegevenstype Publiek | Ondersteund | Beschrijving | Gebruiksscenario&#39;s |
|--------------------|-----------|-------------|-----------|
| [&#x200B; het publiek van Mensen &#x200B;](/help/segmentation/types/people-audiences.md) | Ja | Gebaseerd op klantenprofielen, die u toestaan om specifieke groepen mensen voor marketing campagnes te richten. | Frequente kopers, winkeliers |
| [&#x200B; publiek van de Rekening &#x200B;](/help/segmentation/types/account-audiences.md) | Nee | Doelpersonen binnen specifieke organisaties voor marketingstrategieën op basis van account. | B2B-marketing |
| [&#x200B; Het publiek van het Vooruitzicht &#x200B;](/help/segmentation/types/prospect-audiences.md) | Nee | De individuen van het doel die nog geen klanten zijn maar eigenschappen met uw doelpubliek delen. | Waarschuwing met gegevens van derden |
| [&#x200B; de uitvoer van de Dataset &#x200B;](/help/catalog/datasets/overview.md) | Nee | Verzamelingen gestructureerde gegevens die zijn opgeslagen in het [!DNL Adobe Experience Platform] Data Lake. | Rapportage, workflows voor gegevenswetenschap |

{style="table-layout:auto"}


## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (naam, telefoonnummer of andere) die worden gebruikt in de bestemming Analyse van publiek. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Wanneer een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [&#x200B; het stromen bestemmingen &#x200B;](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Nieuwe bestemming configureren {#configure-destination}

>[!IMPORTANT]
>
>Om bestemming tot stand te brengen, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om deze bestemming tot stand te brengen, volg de stappen die in het [&#x200B; leerprogramma van de bestemmingsconfiguratie &#x200B;](../../ui/connect-destination.md) worden beschreven.

### Doelgegevens {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: De doelnaam.
* **[!UICONTROL Description]**: De doelbeschrijving.
* **[!UICONTROL Datastream ID]**: De gegevensstroom-id die u wilt verrijken met gekwalificeerde doelgroepen. U kunt dit identiteitskaart in de [&#x200B; manager van Datastreams &#x200B;](/help/datastreams/overview.md) verkrijgen.
* **[!UICONTROL Integration alias]**: De alias voor integratie.

### Waarschuwingen {#alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Voor meer informatie over alarm, zie de gids bij [&#x200B; het intekenen aan bestemmingsalarm gebruikend UI &#x200B;](../../ui/alerts.md).

* **[!UICONTROL Activation Skipped Rate Exceed]**: een melding ontvangen wanneer de activeringsfrequentie een drempel overschrijdt.

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

### Beleid en handhavingsmaatregelen voor bestuur {#governance-policy}

Met deze optionele sectie kunt u uw beleid voor gegevensbeheer definiëren en ervoor zorgen dat de gebruikte gegevens voldoen wanneer het publiek wordt verstuurd en geactiveerd.

Wanneer u klaar bent met het selecteren van de gewenste marketingacties voor het doel, selecteert u **[!UICONTROL Create]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
>
>Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Nadat het doel is gemaakt, kunt u het gewenste publiek voor het doel activeren.

1. Als u zich nog niet in de gemaakte bestemming bevindt, kunt u deze opnieuw vinden door naar **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** te navigeren.
1. Selecteer **[!UICONTROL Activate audiences]**.
1. Selecteer het gewenste publiek waarvoor u kwalificaties wilt analyseren. Selecteer **[!UICONTROL Next]** als u klaar bent.
1. Controleer de doelconfiguratie en de publieksinstellingen en selecteer vervolgens **[!UICONTROL Finish]** .

U kunt meer soorten publiek toevoegen om in de toekomst te analyseren door terug te navigeren naar de pagina **[!UICONTROL Activate audiences]** . U kunt soorten publiek niet verwijderen als ze eenmaal zijn geactiveerd.
