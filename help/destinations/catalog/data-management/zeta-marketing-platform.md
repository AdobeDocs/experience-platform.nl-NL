---
title: Zeta Marketing Platform
description: Het Zeta Marketing Platform (ZMP) is een cloudgebaseerd systeem dat u helpt klanten op efficiëntere wijze aan te schaffen, uit te breiden en te behouden, aangedreven door intelligentie (bedrijfseigen gegevens en AI).
hide: true
hidefromtoc: true
source-git-commit: bf553371316d9d9cb368fc4d1be14196201ef680
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 0%

---


# Zeta Marketing Platform {#zeta-marketing-platform}

## Overzicht {#overview}

Het Zeta Marketing Platform (ZMP) is een cloudgebaseerd systeem dat u helpt klanten op efficiëntere wijze aan te schaffen, uit te breiden en te behouden, aangedreven door intelligentie (bedrijfseigen gegevens en AI). Raadpleeg voor meer informatie [Zeta Global](https://zetaglobal.com/).

Met de Zeta Marketing Platform-aansluiting beschikbaar in Adobe Experience Platform kunt u uw publiek naadloos synchroniseren van Experience Platform naar ZMP.

>[!IMPORTANT]
>
>De bestemmingsschakelaar en documentatiepagina worden gecreeerd en door *Zeta Global* team. Voor vragen of verzoeken om updates kunt u contact opnemen met het team op [Contact opnemen](https://zetaglobal.com/about/contact-us/).

## Gebruiksscenario’s {#use-cases}

### publiekssegmenten samenstellen {#use-case-build-audiences}

Een markeerder wil unieke publieksprofielen bouwen, hun meest waardevolle segmenten identificeren, en hen over om het even welke digitale kanalen gebruiken die het Platform van de Marketing Zeta steunt. Ze willen een echte 360-weergave van een consumentenprofiel maken, een zinvol publiek opbouwen en activeren. Meer informatie over de kanalen die het Zeta Marketing Platform ondersteunt, is te vinden [hier](https://zetaglobal.com/platform/integrations/).

### Doelgebruikers met advertenties {#use-case-target-users}

Een adverteerder richt zich op gebruikers binnen een specifiek publiek via het Zeta-Demand Side Platform (DSP), aangezien deze gebruikers met hun merken communiceren. Voor meer informatie over de DSP Zeta klikt u op [hier](https://knowledgebase.zetaglobal.com/programmatic-user-guide/).

## Vereisten {#prerequisites}

### Voorwaarden voor het Zeta-marketingplatform

* Voordat u een nieuwe verbinding instelt met de bestemming van het Zeta-marketingplatform, moet u een lege lijst met klanten maken in uw account van het Zeta-marketingplatform. U moet één van deze klantenlijsten als aangewezen doel kiezen om het publiek van Adobe Experience Platform te ontvangen dat u van plan bent te verzenden. U kunt een lege klantlijst in ZMP tot stand brengen door de instructies te volgen [hier](https://knowledgebase.zetaglobal.com/zmp/creating-audiences#CreatingAudiences-CreatingaCustomerList).
* Hoewel de Adobe Experience Platform de activering van meerdere soorten publiek naar een bepaalde ZMP-doelinstantie toestaat, is het verplicht dat elke ZMP-doelinstantie slechts één Experience Platform publiek ontvangt. Als u meerdere soorten publiek van het Experience Platform wilt afhandelen, maakt u aanvullende ZMP-doelinstanties voor elk publiek en selecteert u een andere lijst met klanten in het vervolgkeuzemenu. Deze benadering zorgt ervoor dat het doelZMP publiek niet wordt beschreven. Zie [Doelgegevens invullen](#destination-details) voor meer informatie .
* Gebruik de volgende geloofsbrieven om de bestemming te vormen:
   * Gebruikersnaam: **api**
   * Wachtwoord: uw ZMP REST API-sleutel. U kunt de REST API-sleutel vinden door u aan te melden bij uw ZMP-account en naar **Instellingen** > **Integraties** > **Toetsen en toepassingen** sectie. Zie de [ZMP-documentatie](https://knowledgebase.zetaglobal.com/zmp/integrations) voor meer informatie .

## Ondersteunde identiteiten {#supported-identities}

[!DNL Zeta Marketing Platform] biedt ondersteuning voor de activering van aangepaste gebruikers-id&#39;s die in de onderstaande tabel worden beschreven. Zie voor meer informatie [identiteiten](/help/identity-service/features/namespaces.md).

>[!IMPORTANT]
> De bestemming van het Platform van de Marketing van Zeta vereist u een naamruimte van de bronidentiteit aan ZMP in kaart te brengen `uid` doelidentiteit. Hierdoor kan het Zeta-marketingplatform elk profiel op unieke wijze onderscheiden.

| Doelidentiteit | Beschrijving | Overwegingen | Notities |
---------|----------|----------|----------|
| uid | Unieke id die ZMP gebruikt om klantprofielen te onderscheiden | Verplicht | Kies de optie `Email` Standaard naamruimte voor identiteiten als u unieke profielen wilt identificeren aan de hand van hun e-mailadressen. U kunt er ook voor kiezen om uw aangepaste naamruimte toe te wijzen aan `uid` als de profielen van de klant geen e-mail hebben. |
| email_md5_id | E-mail MD5 die elk klantprofiel vertegenwoordigt | Optioneel | Kies deze doelidentiteit als u klantprofielen op unieke wijze wilt identificeren aan de hand van MD5-waarden per e-mail. Het is van essentieel belang dat e-mailadressen al in de MD5-indeling van het Experience Platform zijn, aangezien het Platform normale tekst niet omzet in MD5. In dit scenario stelt u `uid` (verplicht) aan of de zelfde e-mail MD5 waarden of een andere aangewezen identiteitsnaamruimte. |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welk type publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Door het Experience Platform gegenereerde soorten publiek [Segmenteringsservice](../../../segmentation/home.md). |
| Aangepaste uploads | X | Soorten publiek [geïmporteerd](../../../segmentation/ui/overview.md#import-audience) in Experience Platform van CSV-bestanden. |

{style="table-layout:auto"}

>[!NOTE]
> Aangezien de individuele leden worden toegevoegd of uit het publiek van het Platform verwijderd, zullen de updates naar ZMP worden verzonden om ervoor te zorgen dat de lijst van de bestemmingsklant dienovereenkomstig wordt gesynchroniseerd.

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op segmentevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u zich wilt verifiëren bij de bestemming, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]**.

* **[!UICONTROL Username]**: `api`
* **[!UICONTROL Password]**: Uw ZMP REST API-sleutel. U kunt de REST API-sleutel vinden door u aan te melden bij uw ZMP-account en naar **Instellingen** > **Integraties** > **Toetsen en toepassingen** sectie. Zie de [ZMP-documentatie](https://knowledgebase.zetaglobal.com/zmp/integrations) voor meer informatie .

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![Afbeelding met ZMP-configuratie](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-configure-new-destination.png)
* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst wilt herkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL ZMP Account Site Id]**: Uw ZMP **Site-id** waar u uw publiek naartoe wilt sturen. U kunt uw site-id weergeven door naar **Instellingen** > **Integraties** > **Toetsen en toepassingen** sectie. Meer informatie is beschikbaar op [hier](https://knowledgebase.zetaglobal.com/zmp/integrations).
* **[!UICONTROL ZMP Segment]**: Het segment met de klantenlijst in uw ZMP-site-id-account dat u wilt bijwerken met het publiek van het platform.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Segmenten naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.
>* Om te exporteren *identiteiten*, hebt u de **[!UICONTROL View Identity Graph]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). <br> ![Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren."){width="100" zoomable="yes"}

Lezen [Profielen en segmenten activeren voor streaming segmentexportdoelen](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

### Kenmerken en identiteiten toewijzen {#map}

Hieronder ziet u een voorbeeld van correcte identiteitstoewijzing bij het exporteren van profielen naar [!DNL Zeta Marketing Platform].

Bronvelden selecteren:
* Een naamruimte voor de bronidentiteit selecteren (aangepast of standaard, zoals `Email`) die een profiel in Adobe Experience Platform uniek identificeert en [!DNL Zeta Marketing Platform].
* Selecteer de kenmerken van het XDM-bronprofiel die u wilt exporteren naar en bijwerken in het dialoogvenster [!DNL Zeta Marketing Platform].

Doelvelden selecteren:
* (Verplicht) Selecteer `uid` als de doelidentiteit waaraan u een naamruimte voor de bronidentiteit toewijst.
* (Optioneel) Selecteer `email_md5_id` als de doelidentiteit waaraan u de naamruimte voor de bronidentiteit hebt toegewezen die de md5-e-mailwaarden vertegenwoordigt. Het is van essentieel belang dat e-mailadressen in het Experience Platform al in de MD5-indeling staan, aangezien het Platform normale tekst niet omzet in MD5
* Selecteer zo nodig aanvullende doeltoewijzingen.

![Identiteitskaart](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-mapping-example.png)

## Geëxporteerde gegevens/Gegevens valideren bij exporteren {#exported-data}

Een geslaagde activering van het publiek van Experience Platform tot het Zeta Marketing Platform werkt de lijst met doelklanten in het ZMP bij. De telling en de steekproefprofielen in de lijst van de doelklant zullen gelijk zijn aan het aantal identiteiten die met succes werden geactiveerd.

![Klantenlijst in ZMP](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-customer-list-in-zmp.png)

Elk publiekslid dat is geactiveerd vanuit een Experience Platform, wordt ook onder **Soorten publiek** > **Mensen** in het ZMP. U kunt ook de **Klantenlijst** deel een profiel uit in de weergave Eén klant, zoals hieronder wordt weergegeven.

![SingleCustomerViewInZMP](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-single-customer-view-in-zmp.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] dwingt gegevensbeheer af, lees de [Overzicht van gegevensbeheer](/help/data-governance/home.md).

## Aanvullende bronnen {#additional-resources}

* [Zeta Knowledge Base](https://knowledgebase.zetaglobal.com/zmp/)
