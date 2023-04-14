---
title: Salesforce-accountbetrokkenheid Marketing Cloud
description: Leer hoe u de Salesforce Marketing Cloud Account Engagement (voorheen Pardot genoemd)-bestemming kunt gebruiken om uw accountgegevens te exporteren en deze te activeren in Salesforce Marketing Cloud Account Engagement voor uw zakelijke behoeften.
last-substantial-update: 2023-04-14T00:00:00Z
source-git-commit: 65feb905bfa7d663d1d463d94af428a04dc55b01
workflow-type: tm+mt
source-wordcount: '1536'
ht-degree: 1%

---

# [!DNL Salesforce Marketing Cloud Account Engagement] verbinding

Gebruik de [[!DNL Salesforce Marketing Cloud Account Engagement]](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) *(voorheen bekend als [!DNL Pardot])* bestemming voor het vastleggen, bijhouden, scoren en beoordelen van leads. U kunt lood sporen voor alle stadia van de pijpleiding voor gerichte marktsegmenten en klantengroepen door e-maildruppelcampagnes en loodbeheer met het koesteren, het scoren en campagnesegmentatie ook ontwerpen.

Vergeleken met [!DNL Salesforce Marketing Cloud Engagement] dat meer gericht is op **B2C** afzet, [!DNL Marketing Cloud Account Engagement] is ideaal voor **B2B** gebruik van zaken waarbij meerdere afdelingen en besluitvormers betrokken zijn en die langere verkoop- en besluitvormingscycli vereisen. Bovendien houdt u ook nauwere nabijheid en integratie met uw CRM aan om aangewezen verkoop en marketing besluiten te nemen. *Opmerking: Experience Platform heeft ook verbindingen voor [!DNL Salesforce Marketing Cloud Engagement], kunt u deze controleren op de [[!DNL Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) en [[!DNL (API) Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md) pagina&#39;s.*

Dit [!DNL Adobe Experience Platform] [doel](/help/destinations/home.md) gebruikt de [[!DNL Salesforce Account Engagement API > Prospect Upsert by Email]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#prospect-upsert-by-email) eindpunt, naar **voeg of werk uw leads bij** nadat ze in een nieuwe [!DNL Marketing Cloud Account Engagement] segment.

[!DNL Marketing Cloud Account Engagement] gebruikt OAuth 2 met het protocol van de Code van de Vergunning om aan te verklaren [!DNL Account Engagement] API. Instructies voor verificatie aan uw [!DNL Marketing Cloud Account Engagement] de instantie is verder onderaan, in de [Verifiëren voor bestemming](#authenticate) sectie.

## Gebruiksscenario’s {#use-cases}

Om u te helpen beter begrijpen hoe en wanneer u het [!DNL Marketing Cloud Account Engagement] doel, hier is een geval van steekproefgebruik dat de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.

### E-mails verzenden naar contactpersonen voor marketingcampagnes {#use-case-send-emails}

De marketingafdeling van een onlineplatform wil een e-mailcampagne uitzenden naar een nieuwsberichten van B2B-leads. Het marketingteam van het platform kan nieuwe leads toevoegen of bestaande lead-informatie bijwerken via Adobe Experience Platform, segmenten van hun eigen offline-gegevens maken en deze segmenten verzenden naar [!DNL Marketing Cloud Account Engagement], die vervolgens kan worden gebruikt om de marketingcampagne per e-mail te verzenden.

## Vereisten {#prerequisites}

Raadpleeg de onderstaande secties voor alle voorwaarden die u in Experience Platform moet instellen en [!DNL Salesforce] en voor informatie die u moet verzamelen voordat u met de [!DNL Marketing Cloud Account Engagement] bestemming.

### Vereisten in Experience Platform {#prerequisites-in-experience-platform}

Voordat u gegevens activeert naar de [!DNL Marketing Cloud Account Engagement] doel, u moet een [schema](/help/xdm/schema/composition.md), [gegevensset](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), en [segmenten](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) gemaakt in [!DNL Experience Platform].

### Vereisten in [!DNL Marketing Cloud Account Engagement] {#prerequisites-destination}

Houd rekening met de volgende voorwaarden om gegevens van Platform naar uw [!DNL Marketing Cloud Account Engagement] account:

#### U hebt een [!DNL Marketing Cloud Account Engagement] account {#prerequisites-account}

A [!DNL Marketing Cloud Account Engagement] account met een abonnement op de [Betrokkenheid Marketing Cloud account](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) Het product is verplicht verder te gaan.

Uw [!DNL Salesforce] de rekening moet [!DNL Salesforce] `Account Engagement Administrator role`. Dit is vereist voor [aangepaste perspectiefvelden maken](https://help.salesforce.com/s/articleView?id=sf.pardot_fields_create_custom_field.htm&amp;type=5).

Tot slot moet uw account ook toegang hebben tot de [[!DNL Account Engagement Lightning App]](https://help.salesforce.com/s/articleView?id=sf.pardot_lightning_enable.htm&amp;type=5).

Uitstrekken tot [[!DNL Salesforce] Ondersteuning](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10) of uw [!DNL Salesforce] accountbeheerder als u geen account hebt of als het account een [!DNL Marketing Cloud Account Engagement] abonnement of [!DNL Account Engagement Administrator role].

#### Gather [!DNL Marketing Cloud Account Engagement] geloofsbrieven {#gather-credentials}

Noteer de onderstaande items voordat u deze verifieert voor de [!DNL Marketing Cloud Account Engagement] bestemming.

| Credentials | Beschrijving |
| --- | --- |
| `Username` | Uw [!DNL Marketing Cloud Account Engagement] gebruikersnaam account. |
| `Password` | Uw [!DNL Marketing Cloud Account Engagement] accountwachtwoord. |
| `Account Engagement Business Unit ID` | Als u de bedrijfs-eenheid-id van Account Engagement wilt vinden, gebruikt u Setup in [!DNL Salesforce]. Van Opstelling, ga binnen *Instellen bedrijfseenheid* in het vak Snel zoeken. De bedrijfs-eenheid voor accountbetrokkenheid begint met `0Uv` en is 18 tekens lang. Als u niet tot de informatie van de Opstelling van de BedrijfsEenheid kunt toegang hebben, vraag uw [!DNL Salesforce] Accountbeheerder om u `Account Engagement Business Unit ID`. Als u aanvullende richtlijnen nodig hebt, raadpleegt u de [[!DNL Salesforce] Verificatie](https://developer.salesforce.com/docs/marketing/pardot/guide/authentication) pagina met hulplijnen. |

{style="table-layout:auto"}

### Guardrails {#guardrails}

Zie de [!DNL Marketing Cloud Account Engagement] [tarieflimieten](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html#rate-limits) die de grenzen van uw plan aangeeft en ook van toepassing is op de executies van het Experience Platform.

>[!IMPORTANT]
>
>Als uw [!DNL Salesforce] de accountbeheerder heeft toegang tot vertrouwde op IP waaiers beperkt, moet u hen contacteren om te krijgen [IP&#39;s van Experience Platform](/help/destinations/catalog/streaming/ip-address-allow-list.md) gevoegd op lijst van gewenste personen. Zie de [!DNL Salesforce] [Toegang tot vertrouwde IP-bereiken beperken voor een verbonden app](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) documentatie als u extra begeleiding nodig hebt.

## Ondersteunde identiteiten {#supported-identities}

[!DNL Marketing Cloud Account Engagement] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](/help/identity-service/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| Email | E-mailadres vooruitzichten | Verplicht |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | <ul><li>U exporteert alle leden van een segment samen met de gewenste schemavelden *(bijvoorbeeld: e-mailadres, telefoonnummer, achternaam)*, op basis van uw veldtoewijzing.</li><li> Voor elk geselecteerd segment in Platform, het overeenkomstige [!DNL Salesforce Marketing Cloud Account Engagement] de segmentstatus wordt bijgewerkt met zijn segmentstatus van Platform.</li></ul> |
| Uitvoerfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op segmentevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

Within **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**, zoeken naar [!DNL Salesforce Marketing Cloud Account Engagement]. U kunt de locatie ook onder de **[!UICONTROL Email marketing]** categorie.

### Verifiëren voor bestemming {#authenticate}

Om voor authentiek te verklaren aan de bestemming, selecteer **[!UICONTROL Connect to destination]**. U gaat naar de [!DNL Salesforce] aanmeldingspagina. Voer uw [!DNL Marketing Cloud Account Engagement] accountgegevens en selecteer [!DNL Log In].

![Het schermschot van UI van het Platform dat toont hoe te om aan de Betrokkenheid van de Rekening van de Marketing Cloud voor authentiek te verklaren.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/authenticate-destination.png)

Volgende, selecteren [!UICONTROL Allow] in het volgende venster om machtigingen te verlenen aan de **Adobe Experience Platform** app voor toegang tot uw [!DNL Salesforce Marketing Cloud Account Engagement] account. *U hoeft dit slechts eenmaal te doen*.

![Het pop-upvenster met de bevestiging van het screenshot van de Salesforce-app geeft toestemming aan de Experience Platform-app voor toegang tot de Marketing Cloud Account Engagement.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/allow-app.png)

Als de verstrekte details geldig zijn, toont UI een bericht: *U hebt verbinding gemaakt met de account voor accountbeheer voor Salesforce Marketing Cloud* bericht en **[!UICONTROL Connected]** Als u een groene markering hebt, kunt u verdergaan met de volgende stap.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is. Zie de [Gather [!DNL Marketing Cloud Account Engagement] geloofsbrieven](#gather-credentials) voor eventuele richtsnoeren.

![Het schermschot van het Platform UI die de bestemmingsdetails toont.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/destination-details.png)

| Veld | Beschrijving |
| --- | --- |
| **[!UICONTROL Name]** | Een naam waarmee u deze bestemming in de toekomst zult erkennen. |
| **[!UICONTROL Description]** | Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren. |
| **[!UICONTROL Account Engagement Business Unit ID]** | Uw [!DNL Salesforce] `Account Engagement Business Unit ID`. |

{style="table-layout:auto"}

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over waarschuwingen raadpleegt u de handleiding over [het abonneren aan bestemmingen alarm gebruikend UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Segmenten naar dit doel activeren {#activate}

>[!IMPORTANT]
>
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Lezen [Profielen en segmenten activeren voor streaming segmentexportdoelen](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

### Afbeeldingsoverwegingen en voorbeeld {#mapping-considerations-example}

Als u uw publieksgegevens correct vanuit Adobe Experience Platform naar de [!DNL Marketing Cloud Account Engagement] doel, moet u door de stap van de gebiedstoewijzing gaan. Toewijzing bestaat uit het maken van een koppeling tussen de schemavelden van uw Experience Data Model (XDM) in uw Platform-account en de bijbehorende equivalenten van de doelbestemming.

Uw XDM-velden op de juiste wijze toewijzen aan de [!DNL Marketing Cloud Account Engagement] de bestemmingsgebieden, volg de hieronder stappen.

1. In de **[!UICONTROL Mapping]** stap, selecteren **[!UICONTROL Add new mapping]**. Er verschijnt een nieuwe toewijzingsrij op het scherm.
1. In de **[!UICONTROL Select source field]** venster, kiest u de **[!UICONTROL Select attributes]** en selecteer het XDM-kenmerk of kies de **[!UICONTROL Select identity namespace]** en selecteer een identiteit.
1. In de **[!UICONTROL Select target field]** venster, kiest u de **[!UICONTROL Select identity namespace]** en selecteer een identiteit of kies **[!UICONTROL Select custom attributes]** categorie en specificeren in de lijst van [[!DNL Prospect API fields]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#fields) in het beschikbare schema.

   * Herhaal deze stappen om toewijzingen toe te voegen tussen uw XDM-profielschema en [!DNL Marketing Cloud Account Engagement]: | Bronveld | Doelveld | Verplicht | | — | — | — | |`IdentityMap: Email`|`Identity: email`| Ja | |`xdm: MailingAddress.city`|`xdm: city`| | |`xdm: person.name.firstName`|`Attribute: firstName`| |

   * Hieronder ziet u een voorbeeld met de bovenstaande toewijzingen:
      ![Voorbeeld van schermafbeelding van gebruikersinterface van Platform met doeltoewijzingen.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/mappings.png)

Wanneer u klaar bent met het opgeven van de toewijzingen voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Gegevens exporteren valideren {#exported-data}

Volg onderstaande stappen om te controleren of u de bestemming correct hebt ingesteld:

1. Navigeer naar een van de segmenten die u hebt geselecteerd. Selecteer het tabblad **[!DNL Activation data]**. De **[!UICONTROL Mapping ID]** de kolom toont de naam van het douaneveld dat binnen wordt geproduceerd [!DNL Marketing Cloud Account Engagement Prospects] pagina.
   ![Het het schermschot van het Platform UI die identiteitskaart van de Toewijzing voor een geselecteerd segment toont.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/selected-segment-mapping-id.png)

1. Aanmelden bij de [[!DNL Salesforce]](https://login.salesforce.com/) website. Navigeer vervolgens naar de **[!DNL Account Engagement]** > **[!DNL Prospects]** > **[!DNL Pardot Prospects]** pagina en controleer of de perspectieven van het segment zijn toegevoegd/bijgewerkt. U kunt ook toegang krijgen tot [[!DNL Salesforce Pardot]](https://pi.pardot.com/) en toegang tot **[!DNL Prospects]** pagina.
   ![Schermopname van de Salesforce-gebruikersinterface met de pagina Prospects.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospects.png)

1. Om te controleren of de vooruitzichten zijn bijgewerkt, selecteer een vooruitzicht en verifieer of is het gebied van het douanevooruitzicht bijgewerkt met de status van het Experience Platform segment.
   ![De het schermschot van Salesforce UI die de geselecteerde pagina van het Vooruitzicht toont, wordt het gebied van het douanevooruitzicht bijgewerkt met de segmentstatus.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospect.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] handhaaft gegevensbeheer, zie [Overzicht van gegevensbeheer](/help/data-governance/home.md).

## Aanvullende bronnen {#additional-resources}

* [!DNL Marketing Cloud Account Engagement] [API-documentatie](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html).