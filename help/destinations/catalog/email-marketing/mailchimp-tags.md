---
title: Mailchimp-tags
description: De bestemming van de Markeringen van Mailchimp staat u toe om uw rekeningsgegevens uit te voeren en het binnen Mailchimp te activeren om met contacten in wisselwerking te staan.
last-substantial-update: 2024-02-20T00:00:00Z
exl-id: 0f278ca8-4fcf-4c47-b538-9cffa45a3d90
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1601'
ht-degree: 0%

---

# [!DNL Mailchimp Tags] verbinding

[[!DNL Mailchimp] &#x200B;](https://mailchimp.com) *(ook gekend als [!DNL Intuit Mailchimp])* is een populair platform van de marketingautomatisering en e-mailmarketing de dienst die door ondernemingen wordt gebruikt om met contacten *(cliënten, klanten, of andere geïnteresseerde partijen) te beheren* gebruikend het posteren lijsten en e-mailmarketing campagnes.

[!DNL Mailchimp Tags] gebruikt [&#x200B; publiek &#x200B;](https://mailchimp.com/help/getting-started-audience/) en [&#x200B; markeringen &#x200B;](https://mailchimp.com/help/getting-started-tags/) om uw contactinformatie te beheren. Tags zijn labels waarmee u uw contactpersonen kunt ordenen en labels kunt toewijzen aan uw interne categorisering binnen [!DNL Mailchimp] .

Vergeleken met [!DNL Mailchimp Interest Categories] waarmee u contactpersonen kunt sorteren op basis van hun interesses en voorkeuren, is [!DNL Mailchimp Tags] bedoeld voor het beheren van abonnementen op onderwerpen die u mogelijk interesseert. *Nota, heeft Experience Platform ook een verbinding voor [!DNL Mailchimp Interest Categories], kunt u het uit op de [[!DNL Mailchimp Interest Categories]](/help/destinations/catalog/email-marketing/mailchimp-interest-categories.md) pagina controleren.*

Dit [!DNL Adobe Experience Platform] [&#x200B; doel &#x200B;](/help/destinations/home.md) hefboomwerkingen het [[!DNL Mailchimp batch subscribe or unsubscribe API] &#x200B;](https://mailchimp.com/developer/marketing/api/lists/batch-subscribe-or-unsubscribe/) eindpunt. U kunt **nieuwe contacten** of **updatemarkeringen van bestaande [!DNL Mailchimp] contacten** binnen een bestaand [!DNL Mailchimp] publiek toevoegen na het activeren van hen binnen een nieuw publiek. [!DNL Mailchimp Tags] gebruikt de geselecteerde publieksnamen van Experience Platform als de tagnamen binnen [!DNL Mailchimp] .

## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de [!DNL Mailchimp Tags] bestemming zou moeten gebruiken, is hier een geval van het steekproefgebruik dat de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.

### E-mails verzenden naar contactpersonen voor marketingcampagnes {#use-case-send-emails}

De verkoopafdeling van een organisatie wil een op e-mail gebaseerde marketing campagne aan een gebogen lijst van contacten uitzenden. De contactlijsten worden ontvangen in partijen uit verschillende off-line bronnen en moeten daarom worden gevolgd. Het team identificeert een bestaand [!DNL Mailchimp] publiek en begint het publiek van Experience Platform te bouwen waarin de contacten van elke lijst worden toegevoegd. Nadat u deze soorten publiek naar [!DNL Mailchimp Tags] hebt verzonden en er geen contactpersonen aanwezig zijn in het geselecteerde [!DNL Mailchimp] -publiek, worden ze toegevoegd met een bijbehorende tag die de naam van het publiek bevat waartoe de contactpersoon behoort. Als er al contactpersonen aanwezig zijn in het publiek van [!DNL Mailchimp] , wordt een nieuwe tag met de naam van het publiek toegevoegd. Aangezien de labels zichtbaar zijn in [!DNL Mailchimp] , zijn de offlinebronnen gemakkelijk herkenbaar. Nadat de gegevens naar [!DNL Mailchimp] zijn verzonden, sturen ze de campagne voor marketing via e-mail naar het publiek.

## Vereisten {#prerequisites}

Raadpleeg de onderstaande secties voor alle voorwaarden die u in Experience Platform en [!DNL Mailchimp] moet instellen en voor informatie die u moet verzamelen voordat u met het [!DNL Mailchimp Tags] -doel kunt werken.

### Vereisten in Experience Platform {#prerequisites-in-experience-platform}

Alvorens gegevens aan de [!DNL Mailchimp Tags] bestemming te activeren, moet u a [&#x200B; schema &#x200B;](/help/xdm/schema/composition.md), a [&#x200B; dataset &#x200B;](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=nl-NL) hebben, en [&#x200B; publiek &#x200B;](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html?lang=nl-NL) dat in [!DNL Experience Platform] wordt gecreeerd.

### Vereisten voor het doel [!DNL Mailchimp Tags] {#prerequisites-destination}

Houd rekening met de volgende voorwaarden om gegevens van Experience Platform naar uw [!DNL Mailchimp Tags] -account te exporteren:

#### U moet een [!DNL Mailchimp] -account hebben {#prerequisites-account}

Voordat u een [!DNL Mailchimp Tags] -doel kunt maken, moet u eerst controleren of u een [!DNL Mailchimp] -account hebt. Als u niet één hebt reeds bezoek de [[!DNL Mailchimp]  aanmeldingspagina &#x200B;](https://login.mailchimp.com/signup/) om uw rekening te registreren en tot stand te brengen.

#### API-sleutel van [!DNL Mailchimp] verzamelen {#gather-credentials}

U hebt uw [!DNL Mailchimp] **API sleutel** nodig om de [!DNL Mailchimp Interest Categories] bestemming tegen uw [!DNL Mailchimp] rekening voor authentiek te verklaren. De **API sleutel** dient als **Wachtwoord** wanneer u [&#x200B; de bestemming &#x200B;](#authenticate) voor authentiek verklaart.

Als u uw **API sleutel** niet hebt, teken binnen aan uw [!DNL Mailchimp] rekening en verwijs naar de [!DNL Mailchimp] documentatie op [&#x200B; hoe te om uw API sleutel &#x200B;](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key) te produceren.

Een voorbeeld van een API-sleutel is `0123456789abcdef0123456789abcde-us14` .

>[!IMPORTANT]
>
>Als u de **API sleutel** produceert, schrijf het neer aangezien u niet tot het na generatie zult kunnen toegang hebben.

#### Uw [!DNL Mailchimp] datacenter identificeren {#identify-data-center}

Vervolgens moet u het datacenter van [!DNL Mailchimp] identificeren. Dit doen, login aan uw [!DNL Mailchimp] rekening en navigeer aan de **API sleutelensectie** van uw rekening.

De datacenter-id is de eerste sectie van de URL die u in uw browser ziet. Als URL *https:// `us14` .mailchimp.com/account/api/* is, dan is het gegevenscentrum `us14`.

Identiteitskaart van het gegevenscentrum wordt ook toegevoegd aan uw API sleutel in de vorm *key-dc*; bijvoorbeeld, als uw API sleutel `0123456789abcdef0123456789abcde-us14` is, dan is het gegevenscentrum `us14`.

Schrijf de waarde van het gegevenscentrum *(`us14` in dit voorbeeld) neer*. U zult deze waarde nodig hebben wanneer u [&#x200B; de bestemmingsdetails &#x200B;](#destination-details) vult.

Als u verdere begeleiding vereist, verwijs naar de [[!DNL Mailchimp]  documentatie van Grondbeginselen &#x200B;](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-structure).

### Guardrails {#guardrails}

Verwijs naar [!DNL Mailchimp] [&#x200B; tariefgrenzen &#x200B;](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-limits) voor gedetailleerde informatie over de grenzen die door [!DNL Mailchimp] API worden opgelegd.

## Ondersteunde identiteiten {#supported-identities}

[!DNL Mailchimp] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [&#x200B; identiteiten &#x200B;](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| Email | The email address of the contact. | Verplicht |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welk type publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#128279;](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Het publiek [&#x200B; ingevoerde &#x200B;](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | <ul><li>U exporteert alle leden van een publiek samen met de gewenste schemavelden *(bijvoorbeeld: e-mailadres, telefoonnummer, achternaam)* volgens uw veldtoewijzing.</li><li> Voor elk publiek dat is geselecteerd in Experience Platform, wordt de bijbehorende segmentstatus van [!DNL Mailchimp Tags] bijgewerkt met de publieksstatus van Experience Platform.</li></ul> |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [&#x200B; het stromen bestemmingen &#x200B;](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u de **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [&#x200B; leerprogramma van de bestemmingsconfiguratie &#x200B;](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

Zoek in **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** naar [!DNL Mailchimp Tags] . U kunt de locatie ook in de categorie **[!UICONTROL Email marketing]** vinden.

### Verifiëren voor bestemming {#authenticate}

Als u voor verificatie bij het doel wilt zorgen, vult u de vereiste velden hieronder in en selecteert u **[!UICONTROL Connect to destination]** .

| Veld | Beschrijving |
| --- | --- |
| **[!UICONTROL Username]** | Uw [!DNL Mailchimp] gebruikersnaam. |
| **[!UICONTROL Password]** | Uw [!DNL Mailchimp] **API sleutel**, die u neer in de [&#x200B; Gather  [!DNL Mailchimp]  geloofsbrieven &#x200B;](#gather-credentials) sectie had genoteerd.<br> Uw API sleutel neemt de vorm van `{KEY}-{DC}`, waar het `{KEY}` gedeelte naar de waarde verwijst neer in de [[!DNL Mailchimp]  API belangrijkste &#x200B;](#gather-credentials) sectie en het `{DC}` gedeelte verwijst naar het [[!DNL Mailchimp]  gegevenscentrum &#x200B;](#identify-data-center). <br> U kunt of het `{KEY}` gedeelte of het volledige vorm verstrekken.<br> Als uw API-sleutel bijvoorbeeld <br>*`0123456789abcdef0123456789abcde-us14`*is, <br> kunt u *`0123456789abcdef0123456789abcde`*of *`0123456789abcdef0123456789abcde-us14`*als waarde opgeven. |

{style="table-layout:auto"}

{het schermschot van 0} Experience Platform UI die toont hoe te voor authentiek te verklaren.![&#128279;](../../assets/catalog/email-marketing/mailchimp-tags/authenticate-destination.png)

Als de opgegeven gegevens geldig zijn, geeft de gebruikersinterface de status **[!UICONTROL Connected]** weer met een groen vinkje. Vervolgens kunt u verdergaan met de volgende stap.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

{het schermschot van 0} Experience Platform UI die de bestemmingsdetails toont.![&#128279;](../../assets/catalog/email-marketing/mailchimp-tags/destination-details.png)

| Veld | Beschrijving |
| --- | --- |
| **[!UICONTROL Name]** | Een naam waarmee u deze bestemming in de toekomst zult erkennen. |
| **[!UICONTROL Description]** | Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren. |
| **[!UICONTROL Data center]** | Uw [!DNL Mailchimp] account `data center` . Verwijs naar [&#x200B; identificeer  [!DNL Mailchimp]  gegevenscentrum &#x200B;](#identify-data-center) sectie voor om het even welke begeleiding. |
| **[!UICONTROL Audience Name (Please enter Data center first)]** | Nadat u uw **[!UICONTROL Data center]** hebt ingevoerd, wordt deze vervolgkeuzelijst automatisch gevuld met de publieksnamen van uw [!DNL Mailchimp] -account. Selecteer het publiek dat u wilt bijwerken met gegevens uit Experience Platform. |

{style="table-layout:auto"}

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [&#x200B; het intekenen aan bestemmingsalarm gebruikend UI &#x200B;](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. <br> ![&#x200B; Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [&#x200B; actief publiek aan het stromen bestemmingen &#x200B;](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiek aan deze bestemming.

### Afbeeldingsoverwegingen en voorbeeld {#mapping-considerations-example}

Als u uw publieksgegevens correct vanuit Adobe Experience Platform naar de [!DNL Mailchimp Tags] -bestemming wilt verzenden, moet u de stap voor veldtoewijzing doorlopen. Toewijzing bestaat uit het maken van een koppeling tussen de schemavelden van uw Experience Data Model (XDM) in uw Experience Platform-account en de overeenkomstige equivalenten van de doelbestemming.

Voer de onderstaande stappen uit om uw XDM-velden correct toe te wijzen aan de [!DNL Mailchimp Tags] -doelvelden:

1. Selecteer **[!UICONTROL Add new mapping]** in de stap **[!UICONTROL Mapping]** . Er verschijnt een nieuwe toewijzingsrij op het scherm.
1. Kies **[!UICONTROL Select identity namespace]** in het `Email` -venster en selecteer de naamruimte van de identiteit.**[!UICONTROL Select source field]**

   {het schermschot van 0} Experience Platform UI met het gebied van Source als E-mail van identiteitsnamespace.![&#128279;](../../assets/catalog/email-marketing/mailchimp-tags/source-field.png)

1. Kies **[!UICONTROL Select identity namespace]** in het `Email` -venster en selecteer de naamruimte van de identiteit.**[!UICONTROL Select target field]**

   {het schermschot van 0} Experience Platform UI met het gebied van het Doel als E-mail van identiteitsnamespace.![&#128279;](../../assets/catalog/email-marketing/mailchimp-tags/target-field.png)

   De toewijzingen tussen uw XDM-profielschema en [!DNL Mailchimp Tags] zijn als volgt:

   | Source-veld | Doelveld | Verplicht |
   | --- | --- | --- |
   | `IdentityMap: Email` | `Identity: Email` | Ja |

   Hieronder ziet u een voorbeeld met de voltooide toewijzingen:
   {het schermschot van 0} Experience Platform UI die gebiedsafbeeldingen toont.![&#128279;](../../assets/catalog/email-marketing/mailchimp-tags/mappings.png)

Wanneer u klaar bent met het opgeven van de toewijzingen voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Gegevens exporteren valideren {#exported-data}

Volg onderstaande stappen om te controleren of u de bestemming correct hebt ingesteld:

1. Meld u aan bij uw [[!DNL Mailchimp] &#x200B;](https://login.mailchimp.com/) -account. Navigeer vervolgens naar de pagina **[!DNL Audience]** > **[!DNL All Contacts]** en controleer of de contacten van het publiek zijn toegevoegd en of de contacten binnen het publiek zijn bijgewerkt met de naam van het publiek.
   {het schermschot van 0} Mailchimp UI die de pagina van het Publiek toont.![&#128279;](../../assets/catalog/email-marketing/mailchimp-tags/contacts.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, zie het [&#x200B; overzicht van het Beleid van Gegevens &#x200B;](/help/data-governance/home.md).

## Fouten en problemen oplossen {#errors-and-troubleshooting}

Verwijs naar de [[!DNL Mailchimp]  pagina van fouten &#x200B;](https://mailchimp.com/developer/marketing/docs/errors/) voor een uitvoerige lijst van status en foutencodes met verklaringen.

## Aanvullende bronnen {#additional-resources}

Hieronder vindt u aanvullende nuttige informatie uit de documentatie van [!DNL Mailchimp] :
* [&#x200B; Begonnen het worden met  [!DNL Mailchimp] &#x200B;](https://mailchimp.com/help/getting-started-with-mailchimp/)
* [&#x200B; Begonnen het worden met Soorten publiek &#x200B;](https://mailchimp.com/help/getting-started-audience/)
* [&#x200B; creeer een Publiek &#x200B;](https://mailchimp.com/help/create-audience/)
* [&#x200B; Begonnen het worden met Markeringen &#x200B;](https://mailchimp.com/help/getting-started-tags/)
* [&#x200B; Marketing API &#x200B;](https://mailchimp.com/developer/marketing/api/)
