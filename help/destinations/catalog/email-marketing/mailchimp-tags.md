---
title: Mailchimp-tags
description: De bestemming van de Markeringen van Mailchimp staat u toe om uw rekeningsgegevens uit te voeren en het binnen Mailchimp te activeren om met contacten in wisselwerking te staan.
last-substantial-update: 2024-02-20T00:00:00Z
source-git-commit: dff460f0b0d365d3d643744544642d9f9488e18a
workflow-type: tm+mt
source-wordcount: '1590'
ht-degree: 0%

---

# [!DNL Mailchimp Tags] verbinding

[[!DNL Mailchimp]](https://mailchimp.com) *(ook bekend als [!DNL Intuit Mailchimp])* is een populair platform voor marketingautomatisering en e-mailmarketingservice dat door bedrijven wordt gebruikt om contacten te beheren en te onderhouden *(klanten, klanten of andere belanghebbenden)* het gebruiken van mailing lijsten en e-mailmarketing campagnes.

[!DNL Mailchimp Tags] gebruik [publiek](https://mailchimp.com/help/getting-started-audience/) en [tags](https://mailchimp.com/help/getting-started-tags/) om uw contactgegevens te beheren. De markeringen zijn etiketten gebruiken waarmee u uw contacten kunt organiseren en hen voor uw interne categorisering binnen etiketteren [!DNL Mailchimp].

Vergeleken met [!DNL Mailchimp Interest Categories] die u zou gebruiken om uw contacten te sorteren op hun belangen en voorkeur, [!DNL Mailchimp Tags] is bedoeld om abonnementen aan onderwerpen van belang te beheren die uw contacten zouden kunnen geinteresseerd zijn. *Opmerking: Experience Platform heeft ook een verbinding voor [!DNL Mailchimp Interest Categories], kunt u het uitchecken op het tabblad [[!DNL Mailchimp Interest Categories]](/help/destinations/catalog/email-marketing/mailchimp-interest-categories.md) pagina.*

Dit [!DNL Adobe Experience Platform] [doel](/help/destinations/home.md) gebruikt de [[!DNL Mailchimp batch subscribe or unsubscribe API]](https://mailchimp.com/developer/marketing/api/lists/batch-subscribe-or-unsubscribe/) eindpunt. U kunt **nieuwe contactpersonen toevoegen** of **bijwerken, tags van bestaande [!DNL Mailchimp] contactpersonen** binnen een bestaande [!DNL Mailchimp] het publiek na het activeren in een nieuw publiek. [!DNL Mailchimp Tags] gebruikt de geselecteerde publieksnamen van Platform als tagnamen binnen [!DNL Mailchimp].

## Gebruiksscenario’s {#use-cases}

Om u te helpen beter begrijpen hoe en wanneer u het [!DNL Mailchimp Tags] doel, hier is een geval van steekproefgebruik dat de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.

### E-mails verzenden naar contactpersonen voor marketingcampagnes {#use-case-send-emails}

De verkoopafdeling van een organisatie wil een op e-mail gebaseerde marketing campagne aan een gebogen lijst van contacten uitzenden. De contactlijsten worden ontvangen in partijen uit verschillende off-line bronnen en moeten daarom worden gevolgd. Het team identificeert een bestaand [!DNL Mailchimp] publiek en begint het publiek van het Experience Platform te bouwen waarin de contacten van elke lijst worden toegevoegd. Na verzending van deze soorten publiek naar [!DNL Mailchimp Tags], als er geen contactpersonen aanwezig zijn in de geselecteerde [!DNL Mailchimp] voor het publiek worden ze toegevoegd met een bijbehorende tag, die de naam van het publiek bevat waartoe de contactpersoon behoort. Als om het even welke contacten reeds in [!DNL Mailchimp] publiek wordt een nieuwe tag met de naam van het publiek toegevoegd. Als de labels zichtbaar zijn in [!DNL Mailchimp] de offlinebronnen gemakkelijk kunnen worden geïdentificeerd. Nadat de gegevens zijn verzonden naar [!DNL Mailchimp] zij sturen de campagne voor marketing e - mail naar het publiek .

## Vereisten {#prerequisites}

Raadpleeg de onderstaande secties voor alle voorwaarden die u in Experience Platform moet instellen en [!DNL Mailchimp] en voor informatie die u moet verzamelen voordat u met de [!DNL Mailchimp Tags] bestemming.

### Vereisten in Experience Platform {#prerequisites-in-experience-platform}

Voordat u gegevens activeert naar de [!DNL Mailchimp Tags] doel, u moet een [schema](/help/xdm/schema/composition.md), [gegevensset](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), en [publiek](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html) gemaakt in [!DNL Experience Platform].

### Vereisten voor de [!DNL Mailchimp Tags] doel {#prerequisites-destination}

Houd rekening met de volgende voorwaarden om gegevens van Platform naar uw [!DNL Mailchimp Tags] account:

#### U hebt een [!DNL Mailchimp] account {#prerequisites-account}

Voordat u een [!DNL Mailchimp Tags] doel, moet u eerst ervoor zorgen dat u een [!DNL Mailchimp] account. Als u er nog geen hebt, gaat u naar [[!DNL Mailchimp] aanmeldpagina](https://login.mailchimp.com/signup/) om uw account te registreren en te maken.

#### Gather [!DNL Mailchimp] API-sleutel {#gather-credentials}

U hebt uw [!DNL Mailchimp] **API-sleutel** om de [!DNL Mailchimp Interest Categories] bestemming tegen uw [!DNL Mailchimp] account. De **API-sleutel** dient als **Wachtwoord** wanneer u [authenticeer de bestemming](#authenticate).

Als u geen **API-sleutel**, meld u aan bij uw [!DNL Mailchimp] en verwijst naar de [!DNL Mailchimp] documentatie over [hoe te om uw API sleutel te produceren](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key).

Een voorbeeld van een API-sleutel is `0123456789abcdef0123456789abcde-us14`.

>[!IMPORTANT]
>
>Als u de **API-sleutel**, noteer het omdat u het na generatie niet meer kunt openen.

#### Identificeer uw [!DNL Mailchimp] datacenter {#identify-data-center}

Vervolgens moet u uw [!DNL Mailchimp] datacenter. Meld u hiertoe aan bij uw [!DNL Mailchimp] en navigeer naar de **Sectie API-sleutels** van uw account.

De datacenter-id is de eerste sectie van de URL die u in uw browser ziet. Als de URL *https://`us14`.mailchimp.com/account/api/*, dan is het datacenter `us14`.

De datacenter-id wordt ook toegevoegd aan de API-sleutel in het formulier *key-dc*; bijvoorbeeld als uw API-sleutel `0123456789abcdef0123456789abcde-us14`, dan is het datacenter `us14`.

De waarde van het datacenter noteren *(`us14` in dit voorbeeld)*. U hebt deze waarde nodig wanneer u [de bestemmingsdetails invullen](#destination-details).

Raadpleeg voor meer informatie de bijsluiter. [[!DNL Mailchimp] Grondbeginselen van documentatie](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-structure).

### Guardrails {#guardrails}

Zie de [!DNL Mailchimp] [tarieflimieten](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-limits) voor nadere informatie over de door de [!DNL Mailchimp] API.

## Ondersteunde identiteiten {#supported-identities}

[!DNL Mailchimp] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| Email | The email address of the contact. | Verplicht |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welk type publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Door het Experience Platform gegenereerde soorten publiek [Segmenteringsservice](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Soorten publiek [geïmporteerd](../../../segmentation/ui/overview.md#import-audience) in Experience Platform van CSV-bestanden. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | <ul><li>U exporteert alle leden van een publiek samen met de gewenste schemavelden *(bijvoorbeeld: e-mailadres, telefoonnummer, achternaam)*, op basis van uw veldtoewijzing.</li><li> Voor elk publiek dat is geselecteerd in Platform, wordt de bijbehorende [!DNL Mailchimp Tags] de segmentstatus wordt bijgewerkt met de publieksstatus van Platform.</li></ul> |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

Within **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**, zoeken naar [!DNL Mailchimp Tags]. U kunt de locatie ook onder de **[!UICONTROL Email marketing]** categorie.

### Verifiëren voor bestemming {#authenticate}

Als u zich wilt verifiëren bij de bestemming, vult u de vereiste velden hieronder in en selecteert u **[!UICONTROL Connect to destination]**.

| Veld | Beschrijving |
| --- | --- |
| **[!UICONTROL Username]** | Uw [!DNL Mailchimp] gebruikersnaam. |
| **[!UICONTROL Password]** | Uw [!DNL Mailchimp] **API-sleutel**, die u in het [Gather [!DNL Mailchimp] geloofsbrieven](#gather-credentials) sectie.<br> Uw API-sleutel bestaat uit `{KEY}-{DC}`, waarbij de `{KEY}` gedeelte verwijst naar de waarde die in de [[!DNL Mailchimp] API-sleutel](#gather-credentials) en de `{DC}` portie verwijst naar de [[!DNL Mailchimp] datacenter](#identify-data-center). <br>U kunt de `{KEY}` of het hele formulier.<br> Als uw API-sleutel bijvoorbeeld <br>*`0123456789abcdef0123456789abcde-us14`*,<br> u kunt *`0123456789abcdef0123456789abcde`*of *`0123456789abcdef0123456789abcde-us14`*als de waarde. |

{style="table-layout:auto"}

![Schermopname van de gebruikersinterface van het platform waarin wordt getoond hoe te voor authentiek te verklaren.](../../assets/catalog/email-marketing/mailchimp-tags/authenticate-destination.png)

Als de verstrekte gegevens geldig zijn, geeft de interface een **[!UICONTROL Connected]** status met een groen vinkje. Vervolgens kunt u verdergaan met de volgende stap.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![Platform UI het schermschot die de bestemmingsdetails tonen.](../../assets/catalog/email-marketing/mailchimp-tags/destination-details.png)

| Veld | Beschrijving |
| --- | --- |
| **[!UICONTROL Name]** | Een naam waarmee u deze bestemming in de toekomst zult erkennen. |
| **[!UICONTROL Description]** | Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren. |
| **[!UICONTROL Data center]** | Uw [!DNL Mailchimp] account `data center`. Zie de [Identificeren [!DNL Mailchimp] datacenter](#identify-data-center) voor eventuele richtsnoeren. |
| **[!UICONTROL Audience Name (Please enter Data center first)]** | Nadat u uw **[!UICONTROL Data center]**, wordt deze vervolgkeuzelijst automatisch gevuld met de publieksnamen van uw [!DNL Mailchimp] account. Selecteer het publiek dat u wilt bijwerken met gegevens van Platform. |

{style="table-layout:auto"}

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.
>* Om te exporteren *identiteiten*, hebt u de **[!UICONTROL View Identity Graph]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). <br> ![Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren."){width="100" zoomable="yes"}

Lezen [Stimulansen voor het publiek naar streamingdoelen activeren](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies voor het activeren van het publiek naar deze bestemming.

### Afbeeldingsoverwegingen en voorbeeld {#mapping-considerations-example}

Als u uw publieksgegevens correct vanuit Adobe Experience Platform naar de [!DNL Mailchimp Tags] doel, moet u door de stap van de gebiedstoewijzing gaan. Toewijzing bestaat uit het maken van een koppeling tussen de schemavelden van uw Experience Data Model (XDM) in uw Platform-account en de bijbehorende equivalenten van de doelbestemming.

Uw XDM-velden op de juiste wijze toewijzen aan de [!DNL Mailchimp Tags] doelvelden, voert u de volgende stappen uit:

1. In de **[!UICONTROL Mapping]** stap, selecteren **[!UICONTROL Add new mapping]**. Er verschijnt een nieuwe toewijzingsrij op het scherm.
1. In de **[!UICONTROL Select source field]** venster, kiest u **[!UICONTROL Select identity namespace]** en selecteert u de `Email` naamruimte identiteit.

   ![Schermopname van platformgebruikersinterface met bronveld als e-mail vanuit naamruimte van identiteit.](../../assets/catalog/email-marketing/mailchimp-tags/source-field.png)

1. In de **[!UICONTROL Select target field]** venster, kiest u **[!UICONTROL Select identity namespace]** en selecteert u de `Email` naamruimte identiteit.

   ![Schermopname van platformgebruikersinterface met doelveld als e-mail vanuit naamruimte Identiteit.](../../assets/catalog/email-marketing/mailchimp-tags/target-field.png)

   De toewijzingen tussen uw XDM-profielschema en [!DNL Mailchimp Tags] is als volgt: | Bronveld | Doelveld | Verplicht | | — | — | — | |`IdentityMap: Email`|`Identity: Email`| Ja |

   Hieronder ziet u een voorbeeld met de voltooide toewijzingen:
   ![Voorbeeld van platformgebruikersinterface met schermafbeeldingen die veldtoewijzingen weergeven.](../../assets/catalog/email-marketing/mailchimp-tags/mappings.png)

Wanneer u klaar bent met het opgeven van de toewijzingen voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Gegevens exporteren valideren {#exported-data}

Volg onderstaande stappen om te controleren of u de bestemming correct hebt ingesteld:

1. Aanmelden bij uw [[!DNL Mailchimp]](https://login.mailchimp.com/) account. Navigeer vervolgens naar de **[!DNL Audience]** > **[!DNL All Contacts]** pagina en controleer of de contacten van het publiek zijn toegevoegd en de contacten binnen het publiek zijn bijgewerkt met de publieksnaam.
   ![Brievenchimp UI het schermschot die de pagina van het Publiek toont.](../../assets/catalog/email-marketing/mailchimp-tags/contacts.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] handhaaft gegevensbeheer, zie [Overzicht van gegevensbeheer](/help/data-governance/home.md).

## Fouten en problemen oplossen {#errors-and-troubleshooting}

Zie de [[!DNL Mailchimp] foutpagina](https://mailchimp.com/developer/marketing/docs/errors/) voor een uitgebreide lijst van status- en foutcodes met uitleg.

## Aanvullende bronnen {#additional-resources}

Aanvullende nuttige informatie uit de [!DNL Mailchimp] de documentatie is hieronder:
* [Aan de slag met [!DNL Mailchimp]](https://mailchimp.com/help/getting-started-with-mailchimp/)
* [Aan de slag met Soorten publiek](https://mailchimp.com/help/getting-started-audience/)
* [Een publiek maken](https://mailchimp.com/help/create-audience/)
* [Aan de slag met tags](https://mailchimp.com/help/getting-started-tags/)
* [Marketing-API](https://mailchimp.com/developer/marketing/api/)
