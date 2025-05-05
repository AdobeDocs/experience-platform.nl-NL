---
title: (V1) Pega CDH Realtime Audience-verbinding
description: Gebruik de bestemming van het publiek van de Hub van het Beslissingshub Realtime van de Hub van de Klant van Pega bestemming in Adobe Experience Platform om profielattributen en gegevens van het publiekslidmaatschap naar de Hub van het Besluit van de Klant van Pega voor volgende-best-actie beslissing te verzenden.
exl-id: 0546da5d-d50d-43ec-bbc2-9468a7db4d90
source-git-commit: 71de5b0d3e9c4413caa911fbe174e74c0e409d89
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 0%

---

# Pega CDH Realtime Audience-verbinding

>[!IMPORTANT]
>
>Deze versie van de bestemming van het publiek van de Hub van het Besluit van de Klant Realtime van de Hub steunt slechts één enkele toepassing van het Besluit van de Klant Pega. Als u de veelvoudige gevormde toepassingen van de Hub van het Besluit van de Klant van Pega hebt, moet u [ gebruiken (V2) de bestemmingsschakelaar van het Publiek van Pega CDH Realtime ](./pega-v2.md).

## Overzicht {#overview}

Gebruik de [!DNL Pega Customer Decision Hub] bestemming van het publiek Realtime in Adobe Experience Platform om profielattributen en gegevens van het publiekslidmaatschap naar [!DNL Pega Customer Decision Hub] voor volgende-best-actie beslissing te verzenden.

Wanneer u het lidmaatschap van het publiek van Adobe Experience Platform in [!DNL Pega Customer Decision Hub] laadt, kunt u het profiel gebruiken als voorspeller in adaptieve modellen en de juiste contextafhankelijke gegevens en gedragsgegevens leveren voor de volgende beste actie-beslissingsdoeleinden.

>[!IMPORTANT]
>
>Deze bestemmings schakelaar en documentatiepagina worden gecreeerd en door Pegasystems gehandhaafd. Voor om het even welke onderzoeken of updateverzoeken, gelieve te contacteren direct [ hier ](mailto:support@pega.com).

## Gebruiksscenario’s

Om u beter te helpen begrijpen hoe en wanneer u de [!DNL Customer Decision Hub] bestemming zou moeten gebruiken, zijn hier voorbeelden van gebruiksgevallen die de klanten van Adobe Experience Platform door deze bestemming kunnen oplossen.

### Telecommunicatie

Een marketeter wil inzichten van de op het gegevenswetenschapsmodel gebaseerde next-best-action zoals geleverd door [!DNL Pega Customer Decision Hub] voor de betrokkenheid van de klant benutten. [!DNL Pega Customer Decision Hub] is sterk afhankelijk van de intentie van de klant, bijvoorbeeld &quot;Interested_In_5G&quot;, &quot;Interested_in_Unlimited_Dataplan&quot; of &quot;Interest_in_iPhone_accessoires&quot;.

### Financiële diensten

Een markator wil de aanbiedingen optimaliseren voor klanten die zich hebben geabonneerd op of zich niet hebben geabonneerd op nieuwsbrieven van het pensioenplan of het pensioenplan. Bedrijven met financiële services kunnen meerdere CustomerID&#39;s van hun eigen CRM&#39;s opnemen in Adobe Experience Platform, een publiek opbouwen van hun eigen offline gegevens en profielen verzenden die het publiek binnenkomen en verlaten naar [!DNL Pega Customer Decision Hub] voor NBA-beslissingen (next-best-action) in uitgaande kanalen.

## Vereisten {#prerequisites}

Voordat u deze bestemming kunt gebruiken om gegevens uit Adobe Experience Platform te exporteren, moet u controleren of aan de volgende voorwaarden is voldaan in [!DNL Pega Customer Decision Hub] :

* Vorm de [ de integratiecomponent van het Profiel van Adobe Experience Platform en van het Volwassenlidmaatschap ](https://docs.pega.com/bundle/components/page/customer-decision-hub/components/adobe-membership-component.html) in uw [!DNL Pega Customer Decision Hub] instantie.
* Vorm OAuth 2.0 [ Registratie van de Cliënt gebruikend het 1&rbrace; giftetype van de Credentials van de Cliënt in uw [!DNL Pega Customer Decision Hub] instantie.](https://docs.pega.com/bundle/platform/page/platform/security/configure-oauth-2-client-registration.html)
* Vorm [ in real time de gegevensstroom van looppas ](https://docs.pega.com/bundle/platform/page/platform/decision-management/data-flow-run-real-time-create.html) voor de gegevensstroom van het Lidmaatschap van de Audience van Adobe in uw [!DNL Pega Customer Decision Hub] instantie.

## Ondersteunde identiteiten {#supported-identities}

[!DNL Pega Customer Decision Hub] ondersteunt de activering van aangepaste gebruikers-id&#39;s die in de onderstaande tabel worden beschreven. Voor meer details, zie [ identiteiten ](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving |
|---|---|
| *CustomerID* | Algemene gebruikersnaam die een profiel in [!DNL Pega Customer Decision Hub] en Adobe Experience Platform op unieke wijze identificeert |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | Exporteer alle leden van een publiek met herkenningsteken (*CustomerID*), attributen (achternaam, voornaam, plaats, enz.) en de gegevens van het publiekslidmaatschap. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn altijd op API gebaseerde verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt, dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Voor meer informatie, zie [ het stromen bestemmingen ](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

#### OAuth 2 de authentificatie van de cliëntgeloofsbrieven {#oauth-2-client-credentials-authentication}

![ Beeld van het scherm UI waar u met de bestemming van Pega CDH kunt verbinden, gebruikend OAuth 2 met de authentificatie van cliëntgeloofsbrieven ](../../assets/catalog/personalization/pega/pega-api-authentication-oauth2-client-credentials.png)

Vul de onderstaande velden in en selecteer **[!UICONTROL Connect to destination]** :

* **[!UICONTROL Access Token URL]**: De URL van het toegangstoken OAuth 2 op uw [!DNL Pega Customer Decision Hub] -instantie.
* **[!UICONTROL Client ID]**: De OAuth 2 [!DNL client ID] die u in de [!DNL Pega Customer Decision Hub] -instantie hebt gegenereerd.
* **[!UICONTROL Client Secret]**: De OAuth 2 [!DNL client secret] die u in de [!DNL Pega Customer Decision Hub] -instantie hebt gegenereerd.

### Doelgegevens invullen {#destination-details}

Na het vestigen van de authentificatieverbinding aan [!DNL Pega Customer Decision Hub], verstrek de volgende informatie voor de bestemming:

![ Beeld van het scherm UI die voltooide gebieden voor de Peg CDH bestemmingsdetails tonen ](../../assets/catalog/personalization/pega/pega-connect-destination.png)

Als u details voor het doel wilt configureren, vult u de vereiste velden in en selecteert u **[!UICONTROL Next]** .

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Pega CDH Host Name]**: De hostnaam van de PEGA-client voor beslissingen van klanten waarnaar het profiel wordt geëxporteerd als JSON-gegevens.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Zie [ publieksgegevens aan het stromen van profieluitvoer bestemmingen ](../../ui/activate-streaming-profile-destinations.md) voor instructies op het activeren van publiek aan deze bestemming activeren.

### Doelkenmerken {#attributes}

In de [[!UICONTROL Select attributes]](../../ui/activate-streaming-profile-destinations.md#select-attributes) stap, adviseert Adobe dat u een uniek herkenningsteken van uw [ verenigingsschema ](../../../profile/home.md#profile-fragments-and-union-schemas) selecteert. Selecteer de unieke id en andere XDM-velden die u naar het doel wilt exporteren.

### Voorbeeld van toewijzing: profielupdates activeren in [!DNL Pega Customer Decision Hub] {#mapping-example}

Hieronder ziet u een voorbeeld van correcte identiteitstoewijzing bij het exporteren van profielen naar [!DNL Pega Customer Decision Hub] .

Bronvelden selecteren:

* Selecteer een id (bijvoorbeeld: CustomerID) als bronidentiteit die een profiel in Adobe Experience Platform en [!DNL Pega Customer Decision Hub] op unieke wijze identificeert.
* Selecteer wijzigingen in XDM-bronprofielkenmerken die u wilt exporteren en bijwerken in [!DNL Pega Customer Decision Hub] .

Doelvelden selecteren:

* Selecteer de naamruimte `CustomerID` als doelidentiteit.
* Selecteer namen van bestemmingsprofielkenmerken die moeten worden toegewezen aan de overeenkomende XDM-bronprofielkenmerken.

![ de afbeelding van de Identiteit ](../../assets/catalog/personalization/pega/pega-source-destination-mapping.png)

## Geëxporteerde gegevens/Gegevens valideren bij exporteren {#exported-data}

Een geslaagde update voor een profiel voor publiekslidmaatschap zou de publieksidentificatie, de naam en de status in de PEGA-datastore invoegen voor het publicatiepubliek. De lidmaatschapsgegevens zijn gekoppeld aan een klant die gebruikmaakt van Customer Profile Designer in [!DNL Pega Customer Decision Hub], zoals hieronder wordt weergegeven.
![ Beeld van het scherm UI waar u de gegevens van het Lidmaatschap van het publiek van Adobe aan Klant kunt associëren, gebruikend het Profiel van de Klant Designer ](../../assets/catalog/personalization/pega/pega-profile-designer-associate.png)

De gegevens van het publiekslidmaatschap worden gebruikt in het volgende-Beste beleid van de Aanwezigheid van de Designer van Pega voor volgende-best-actie besluit, zoals hieronder getoond.
![ Beeld van het scherm UI waar u de gebieden van het het lidmaatschapsaandeel van het Publiek als voorwaarden in het Beleid van de Betrokkenheid van volgende-Beste-Actie Designer ](../../assets/catalog/personalization/pega/pega-profile-designer-engagement.png) kunt toevoegen

De gegevensvelden voor het gebruikerslidmaatschap van de klant worden toegevoegd als voorspellers in Adaptieve modellen, zoals hieronder wordt weergegeven.
![ Beeld van het scherm UI waar u de gebieden van het lidmaatschapsaandeel van het Publiek als predikers in Aanpassings modellen kunt toevoegen, gebruikend de Studio van de Voorspelling ](../../assets/catalog/personalization/pega/pega-profile-designer-adaptivemodel.png)

## Aanvullende bronnen {#additional-resources}

Raadpleeg de volgende [!DNL Pega] documentatiebronnen voor meer informatie:

* [ Vestiging een OAuth 2.0 cliëntregistratie ](https://docs.pega.com/bundle/platform/page/platform/security/configure-oauth-2-client-registration.html)
* [ Creërend een runtime in real time voor gegevensstromen ](https://docs.pega.com/bundle/platform/page/platform/decision-management/data-flow-run-real-time-create.html)
* [ beheer klantenverslagen in Designer van het Profiel van de Klant ](https://docs.pega.com/bundle/customer-decision-hub/page/customer-decision-hub/implement/profile-designer-data-management.html)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, zie het [ overzicht van het Beleid van Gegevens ](/help/data-governance/home.md).
