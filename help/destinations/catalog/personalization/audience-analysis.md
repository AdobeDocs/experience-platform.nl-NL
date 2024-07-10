---
title: Doel van Auditieanalyse
description: Bekijk het publiek waarvoor klanten in Customer Journey Analytics in aanmerking komen.
badgeLimitedAvailability: label="Beperkte beschikbaarheid" type="Informative"
exl-id: 81437237-d746-4ce9-b938-7d2541f0ed32
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 0%

---

# Doel van Auditieanalyse

De [!UICONTROL Audience Analysis] doel: hiermee verrijkt u Adobe Experience Platform-publieksgegevens [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html). U kunt selecteren welk publiek u in de resulterende verrijkte gegevens wilt opnemen. De kwalificaties van het publiek zijn dan beschikbaar als afmetingen in [Analysis Workspace](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/home.html) rapportage.

>[!AVAILABILITY]
>
>Deze bestemming bevindt zich in een beperkte testfase. Als u in het gebruiken van deze bestemming geinteresseerd bent, contacteer uw Team van de Rekening van de Adobe.

## Vereisten

Het volgende wordt vereist alvorens deze bestemming te gebruiken:

* U moet worden provisioned om de bestemming van de Analyse van de Publiek te gebruiken. Neem contact op met het accountteam van de Adobe als u nog geen provisioned bent voor het gebruik van deze bestemming.
* U moet zijn provisioned om Customer Journey Analytics te gebruiken.
* Er moet ten minste één publiek zijn gemaakt in Adobe Experience Platform.

## Ondersteunde identiteiten

De Analyse van het publiek steunt de activering van identiteiten die in de lijst hieronder worden beschreven. Meer informatie over [identiteiten](/help/identity-service/features/namespaces.md). Experience Cloud-id (ECID) wordt doorgaans gebruikt.

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Selecteer de GAID doelidentiteit wanneer uw bronidentiteit een GAID-naamruimte is. |
| IDFA | Apple-id voor adverteerders | Selecteer de IDFA doelidentiteit wanneer uw bronidentiteit een IDFA namespace is. |
| ECID | Experience Cloud-id | Een naamruimte die ECID vertegenwoordigt. Deze naamruimte kan ook worden aangeduid met de volgende aliassen: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Zie het volgende document op [ECID](/help/identity-service/features/ecid.md) voor meer informatie . |
| phone_sha256 | Telefoonnummers die zijn hashed met het SHA256-algoritme | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-telefoonnummers. Wanneer het bronveld hashkenmerken bevat, controleert u de **[!UICONTROL Apply transformation]** optie, om [!DNL Platform] de gegevens bij activering automatisch hashen. |
| email_lc_sha256 | E-mailadressen die met het algoritme SHA256 worden gehasht | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-e-mailadressen met hashing. Wanneer het bronveld hashkenmerken bevat, controleert u de **[!UICONTROL Apply transformation]** optie, om [!DNL Platform] de gegevens bij activering automatisch hashen. |
| extern_id | Aangepaste gebruikers-id&#39;s | Selecteer deze doelidentiteit wanneer uw bronidentiteit een aangepaste naamruimte is. |

{style="table-layout:auto"}

## Ondersteunde doelgroepen

De volgende soorten doelgroepen worden ondersteund bij gebruik van dit doel:

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Door het Experience Platform gegenereerde soorten publiek [Segmenteringsservice](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Soorten publiek [geïmporteerd](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van CSV-bestanden. |

{style="table-layout:auto"}

## Type en frequentie exporteren

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (naam, telefoonnummer of andere) die worden gebruikt in de bestemming Analyse van publiek. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Wanneer een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Nieuwe bestemming configureren

>[!IMPORTANT]
> 
>Als u een doel wilt maken, hebt u de opdracht **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Voer de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md).

### Doelgegevens

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: De doelnaam.
* **[!UICONTROL Description]**: De beschrijving van de bestemming.
* **[!UICONTROL Datastream ID]**: De gegevensstroom-id die u wilt verrijken met gekwalificeerde doelgroepen. U kunt deze id verkrijgen in het dialoogvenster [DataStreams-beheer](/help/datastreams/overview.md).
* **[!UICONTROL Integration alias]**: De alias voor integratie.

### Waarschuwingen

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

* **[!UICONTROL Activation Skipped Rate Exceed]**: Wordt op de hoogte gesteld wanneer de activeringsfrequentie een drempel overschrijdt.

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

### Beleid en handhavingsmaatregelen voor bestuur

Met deze optionele sectie kunt u uw beleid voor gegevensbeheer definiëren en ervoor zorgen dat de gebruikte gegevens voldoen wanneer het publiek wordt verstuurd en geactiveerd.

Wanneer u klaar bent met het selecteren van de gewenste marketingacties voor de bestemming, selecteert u **[!UICONTROL Create]**.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Nadat het doel is gemaakt, kunt u het gewenste publiek voor het doel activeren.

1. Als u zich nog niet in de gemaakte bestemming bevindt, kunt u deze opnieuw vinden door naar **[!UICONTROL Destinations]** > **[!UICONTROL Browse]**.
1. Selecteer **[!UICONTROL Activate audiences]**.
1. Selecteer het gewenste publiek waarvoor u kwalificaties wilt analyseren. Selecteer **[!UICONTROL Next]**.
1. Herzie de bestemmingsconfiguratie en publieksmontages, dan uitgezocht **[!UICONTROL Finish]**.

U kunt meer publiek toevoegen om in de toekomst te analyseren door terug naar **[!UICONTROL Activate audiences]** pagina. U kunt soorten publiek niet verwijderen als ze eenmaal zijn geactiveerd.
