---
title: Doel van Auditieanalyse
description: Bekijk het publiek waarvoor klanten in Customer Journey Analytics in aanmerking komen.
badgeLimitedAvailability: label="Beperkte beschikbaarheid" type="Informative"
exl-id: 81437237-d746-4ce9-b938-7d2541f0ed32
hide: true
hidefromtoc: true
source-git-commit: 4bd94c292a13a80405a3d726295ebd6eaf86aaaa
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 0%

---

# Doel van Auditieanalyse

De [!UICONTROL Audience Analysis] bestemming staat u toe om het publieksgegevens van Adobe Experience Platform in [ Customer Journey Analytics ](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html) te verrijken. U kunt selecteren welk publiek u in de resulterende verrijkte gegevens wilt opnemen. De kwalificaties van het publiek zijn dan beschikbaar als afmetingen in [ Analysis Workspace ](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/home.html) rapporterend.

>[!AVAILABILITY]
>
>Deze bestemming bevindt zich in een beperkte testfase. Neem contact op met het Adobe-accountteam als u deze bestemming wilt gebruiken.

## Vereisten

Het volgende wordt vereist alvorens deze bestemming te gebruiken:

* U moet worden provisioned om de bestemming van de Analyse van de Publiek te gebruiken. Neem contact op met uw Adobe-accountteam als u nog geen provisioned bent voor het gebruik van deze bestemming.
* U moet zijn ingericht om Customer Journey Analytics te kunnen gebruiken.
* Er moet ten minste één publiek zijn gemaakt in Adobe Experience Platform.

## Ondersteunde identiteiten

De Analyse van het publiek steunt de activering van identiteiten die in de lijst hieronder worden beschreven. Leer meer over [ identiteiten ](/help/identity-service/features/namespaces.md). Experience Cloud-id (ECID) wordt doorgaans gebruikt.

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Selecteer de GAID doelidentiteit wanneer uw bronidentiteit een GAID-naamruimte is. |
| IDFA | Apple-id voor adverteerders | Selecteer de IDFA doelidentiteit wanneer uw bronidentiteit een IDFA namespace is. |
| ECID | Experience Cloud-id | Een naamruimte die ECID vertegenwoordigt. Deze naamruimte kan ook worden aangeduid met de volgende aliassen: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Zie het volgende document op [ ECID ](/help/identity-service/features/ecid.md) voor meer informatie. |
| phone_sha256 | Telefoonnummers die zijn hashed met het SHA256-algoritme | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-telefoonnummers. Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in om de gegevens automatisch te laten hashen bij activering door [!DNL Experience Platform] . |
| email_lc_sha256 | E-mailadressen die met het algoritme SHA256 worden gehasht | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-e-mailadressen met hashing. Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in om de gegevens automatisch te laten hashen bij activering door [!DNL Experience Platform] . |
| extern_id | Aangepaste gebruikers-id&#39;s | Selecteer deze doelidentiteit wanneer uw bronidentiteit een aangepaste naamruimte is. |

{style="table-layout:auto"}

## Ondersteunde doelgroepen

De volgende soorten doelgroepen worden ondersteund bij gebruik van dit doel:

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#128279;](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Het publiek [ ingevoerde ](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (naam, telefoonnummer of andere) die worden gebruikt in de bestemming Analyse van publiek. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Wanneer een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [ het stromen bestemmingen ](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Nieuwe bestemming configureren

>[!IMPORTANT]
> 
>Om bestemming tot stand te brengen, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om deze bestemming tot stand te brengen, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven.

### Doelgegevens

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: De doelnaam.
* **[!UICONTROL Description]**: De doelbeschrijving.
* **[!UICONTROL Datastream ID]**: De gegevensstroom-id die u wilt verrijken met gekwalificeerde doelgroepen. U kunt dit identiteitskaart in de [ manager van Datastreams ](/help/datastreams/overview.md) verkrijgen.
* **[!UICONTROL Integration alias]**: De alias voor integratie.

### Waarschuwingen

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Voor meer informatie over alarm, zie de gids bij [ het intekenen aan bestemmingsalarm gebruikend UI ](../../ui/alerts.md).

* **[!UICONTROL Activation Skipped Rate Exceed]**: een melding ontvangen wanneer de activeringsfrequentie een drempel overschrijdt.

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

### Beleid en handhavingsmaatregelen voor bestuur

Met deze optionele sectie kunt u uw beleid voor gegevensbeheer definiëren en ervoor zorgen dat de gebruikte gegevens voldoen wanneer het publiek wordt verstuurd en geactiveerd.

Wanneer u klaar bent met het selecteren van de gewenste marketingacties voor het doel, selecteert u **[!UICONTROL Create]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Nadat het doel is gemaakt, kunt u het gewenste publiek voor het doel activeren.

1. Als u zich nog niet in de gemaakte bestemming bevindt, kunt u deze opnieuw vinden door naar **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** te navigeren.
1. Selecteer **[!UICONTROL Activate audiences]**.
1. Selecteer het gewenste publiek waarvoor u kwalificaties wilt analyseren. Selecteer **[!UICONTROL Next]** als u klaar bent.
1. Controleer de doelconfiguratie en de publieksinstellingen en selecteer vervolgens **[!UICONTROL Finish]** .

U kunt meer soorten publiek toevoegen om in de toekomst te analyseren door terug te navigeren naar de pagina **[!UICONTROL Activate audiences]** . U kunt soorten publiek niet verwijderen als ze eenmaal zijn geactiveerd.
