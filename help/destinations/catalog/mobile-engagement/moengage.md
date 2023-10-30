---
title: Verbinding maken
description: Moconnect is een platform voor klantbetrokkenheid dat klantgerichte interacties tussen consumenten en merken in real time mogelijk maakt.
last-substantial-update: 2023-10-11T00:00:00Z
exl-id: 051f1a10-3c41-4c0a-b187-bf80de0565f0
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 0%

---

# [!DNL Moengage] verbinding

## Overzicht {#overview}

Gebruik de [!DNL Moengage] bestemming om uw gegevens van de Adobe (gebruikersattributen, segmenten en gebeurtenissen) aan MoEngage in real time te verbinden en in kaart te brengen. Klanten kunnen vervolgens op deze gegevens reageren en persoonlijke, doelgerichte ervaringen bieden.

Met Adobe is de integratie heel eenvoudig en intuïtief. Neem eenvoudig om het even welk gebruikersprofiel van de Adobe, en wijs het aan een MoEngage gebruikersattribuut in kaart.

>[!IMPORTANT]
>
>Deze bestemmingsschakelaar en documentatiepagina worden gecreeerd en gehandhaafd door *Moskou* team. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen via *`https://help.moengage.com/hc/en-us`.*

## Gebruiksscenario’s {#use-cases}

Een markeerteken wil een gebruikerssegment (ingebouwd in Adobe Experience Platform) activeren via [!DNL Moengage] campagnes. Bovendien willen ze de inhoud van de campagne aanpassen op basis van kenmerken uit Adobe Experience Platform-profielen. Met deze integratie worden gebruikers en kenmerken in MoEngage bijgewerkt zodra segmenten en profielen in Adobe Experience Platform worden bijgewerkt.

## Vereisten {#prerequisites}

Voordat je Adobe Experience Platform-gegevens kunt verzenden naar [!DNL Moengage], let op de volgende voorwaarden:

* Om de bestemming MoEngage met Adobe Experience Platform te gebruiken, moeten de gebruikers eerst toegang tot hun hebben [!DNL Moengage] Account. Ga naar de volgende pagina om u aan te melden bij of aan te melden bij uw MoEngage-account: https://app.moengage.com


## Ondersteunde identiteiten {#supported-identities}

[!DNL Moengage] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven.

| Doelidentiteit | Beschrijving | Overwegingen |
|---|------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| user_id | Unieke id die een gebruikersprofiel in de [!DNL Moengage] systeem. | Deze id ondersteunt het type tekenreeks. Een van de volgende waarden is vereist: user_id of anoniem_id |
| anoniem_id | Een andere id voor een onbekend gebruikersprofiel: een profiel dat niet in het systeem bestaat. | Deze id ondersteunt het type tekenreeks. Een van de volgende waarden is vereist: user_id of anoniem_id |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment (publiek) met de id&#39;s (user_id, anonieme_id) samen met de aangepaste kenmerken die door u zijn geëxporteerd naar [!DNL Moengage]. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op segmentevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u zich wilt verifiëren bij de bestemming, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]**.

![Verificatie bestemming activeren](../../assets/catalog/mobile-engagement/moengage/authentication.png)

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.
![Verificatie bestemming activeren](../../assets/catalog/mobile-engagement/moengage/settings.png)
* **[!UICONTROL USERNAME]**: APP ID DATA van instellingen pagina met instellingen [!DNL Moengage] dashboard.
* **[!UICONTROL PASSWORD]**: DATA APP KEY van instellingenpagina van [!DNL Moengage] dashboard.

![Verificatie bestemming activeren](../../assets/catalog/mobile-engagement/moengage/destination_details.png)

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst wilt herkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Region]**: Uw app *datacenter*.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Segmenten naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Zie [De publieksgegevens van de activering aan het stromen segment de uitvoerbestemmingen](../../ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

### Kenmerken en identiteiten toewijzen {#map}

Om uw publieksgegevens correct te verzenden van [!DNL Adobe Experience Platform] aan de [!DNL Moengage] doel, moet u door de stap van de gebiedstoewijzing gaan.

Toewijzing bestaat uit het maken van een koppeling tussen uw [!DNL Experience Data Model] (XDM) schemavelden in uw [!DNL Platform] en de overeenkomstige equivalenten van de doelbestemming.

Uw XDM-velden op de juiste wijze toewijzen aan de [!DNL Moengage] doelvelden, voer de volgende stappen uit:

In de [!UICONTROL Mapping] stap, selecteren **[!UICONTROL Checkbox]**.

![Toewijzing bestemming toevoegen verplaatsen](../../assets/catalog/mobile-engagement/moengage/segments.png)

In de [!UICONTROL Mapping] stap, selecteren **[!UICONTROL Add new mapping]**.

![Toewijzing bestemming toevoegen verplaatsen](../../assets/catalog/mobile-engagement/moengage/mapping.png)

In de [!UICONTROL Source Field] selecteert u de pijlknop naast het lege veld.

![Toewijzing doelbron verplaatsen](../../assets/catalog/mobile-engagement/moengage/mapping-source.png)

In de [!UICONTROL Select source field] kunt u kiezen uit twee categorieën XDM-velden:
* [!UICONTROL Select attributes]: gebruik deze optie om een specifiek veld van uw XDM-schema toe te wijzen aan [!DNL Moengage] kenmerk.

![Bronkenmerk voor doeltoewijzing verplaatsen](../../assets/catalog/mobile-engagement/moengage/mapping-attributes.png)

Kies uw bronveld en selecteer **[!UICONTROL Select]**.

In de [!UICONTROL Target Field] selecteert u het toewijzingspictogram rechts van het veld.

![Doeltoewijzing verplaatsen](../../assets/catalog/mobile-engagement/moengage/mapping-target.png)

In de [!UICONTROL Select target field] kunt u kiezen uit twee categorieën doelvelden:
* [!UICONTROL Select identity namespace]: Gebruik deze optie om toe te wijzen [!DNL Platform] naamruimten naar [!DNL Moengage] naamruimten.
* [!UICONTROL Select custom attributes]: Gebruik deze optie om XDM-kenmerken toe te wijzen aan aangepaste kenmerken [!DNL Moengage] kenmerken die u in uw [!DNL Moengage] account. <br> U kunt deze optie ook gebruiken om bestaande XDM-kenmerken te hernoemen in [!DNL Moengage]. Bijvoorbeeld het toewijzen van een `lastName` XDM-kenmerk aan een aangepast element `Last_Name` kenmerk in [!DNL Moengage], worden de `Last_Name` kenmerk in [!DNL Moengage], als het nog niet bestaat, en kaart de `lastName` XDM-kenmerk eraan gekoppeld.

![Doeltoewijzingsvelden activeren](../../assets/catalog/mobile-engagement/moengage/mapping-target-fields.png)

Kies uw doelveld en selecteer **[!UICONTROL Select]**.

Nu wordt de veldtoewijzing weergegeven in de lijst.

![Toewijzing bestemming verplaatsen voltooid](../../assets/catalog/mobile-engagement/moengage/mapping-complete.png)

Herhaal de vorige stappen om meer toewijzingen toe te voegen.

## Geëxporteerde gegevens/Gegevens valideren bij exporteren {#exported-data}

Controleren of gegevens zijn geëxporteerd naar de [!DNL Moengage] doel, ga naar het gebruikersprofiel op uw [!DNL Moengage] account. Er wordt een gebruikerskenmerk met de naam AEP Segment weergegeven.

![Toewijzing bestemming verplaatsen voltooid](../../assets/catalog/mobile-engagement/moengage/validation.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] dwingt gegevensbeheer af, lees de [Overzicht van gegevensbeheer](/help/data-governance/home.md).
