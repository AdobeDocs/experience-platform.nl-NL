---
title: Mailchimp-rentecategorieën
description: Mailchimp (ook wel Intuit Mailchimp genoemd) is een populair marketingplatform voor automatisering en marketing via e-mail dat door bedrijven wordt gebruikt om contactpersonen (klanten, klanten of andere belanghebbenden) te beheren en met hen te spreken via mailinglijsten en marketingcampagnes via e-mail. Gebruik deze schakelaar om uw contacten te sorteren die op hun belangen en voorkeur worden gebaseerd.
last-substantial-update: 2023-05-24T00:00:00Z
exl-id: bdce8295-7305-4d54-81c1-7fa3e580ce70
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2218'
ht-degree: 0%

---

# [!DNL Mailchimp Interest Categories] verbinding

[[!DNL Mailchimp] ](https://mailchimp.com) is een populair platform van de marketing automatisering en e-mailmarketing de dienst die door ondernemingen wordt gebruikt om en met contacten te beheren *(cliënten, klanten, of andere geïnteresseerde partijen)* te spreken gebruikend mailing lijsten en e-mail marketing campagnes. Gebruik deze schakelaar om uw contacten te sorteren die op hun belangen en voorkeur worden gebaseerd.

[!DNL Mailchimp Interest Categories] gebruikt [ publiek ](https://mailchimp.com/help/getting-started-audience/), [ groepen ](https://mailchimp.com/help/getting-started-with-groups/), en interessecategorieën *(ook gekend als groepsnamen of groepstitels)*. Elke [!DNL Mailchimp] -groep is een lijst met belangencategorieën. Contactpersonen zijn gekoppeld aan een belangencategorie wanneer zij zich abonneren op een of meer belangencategorieën via een aanmeldingsformulier op uw website. Binnen een publiek, kunt u de contacten in groepen ook organiseren en hen associëren met rentecategorieën, en deze kunnen dan worden gebruikt om segmenten tot stand te brengen. U kunt dit publiek gebruiken om gerichte campagnee-mails naar de geabonneerde contacten uit te zenden.

<!--
Compared to [!DNL Mailchimp Tags] which you would use for internal classification, [!DNL Mailchimp Interest Categories] is meant to manage subscriptions to topics of interest that your contacts might be interested in. *Note, Experience Platform also has a connection for [!DNL Mailchimp Tags], you can check it out on the [[!DNL Mailchimp Tags]](/help/destinations/catalog/email-marketing/mailchimp-tags.md) page.*
-->

Dit [!DNL Adobe Experience Platform] [ bestemming ](/help/destinations/home.md) gebruikt [[!DNL Mailchimp batch subscribe or unsubscribe API] ](https://mailchimp.com/developer/marketing/api/lists/batch-subscribe-or-unsubscribe/) API om [ rentecategorieën ](https://mailchimp.com/developer/marketing/api/interest-categories/) tot stand te brengen en dan contacten van elk geselecteerd publiek van Experience Platform in een overeenkomstige rentecategorie toe te voegen. U kunt **nieuwe contacten** toevoegen of **de informatie van bestaande [!DNL Mailchimp] contacten** bijwerken, dan **toevoegen of verwijderen hen uit hun gewenste groepen** binnen een bestaand [!DNL Mailchimp] publiek na het activeren van hen binnen een nieuw segment. [!DNL Mailchimp Interest Groups] gebruikt de geselecteerde publieksnamen van Experience Platform als belangencategorieën binnen [!DNL Mailchimp] .

## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de [!DNL Mailchimp Interest Categories] bestemming zou moeten gebruiken, is hier een geval van het steekproefgebruik dat de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.

### E-mails verzenden naar contactpersonen voor marketingcampagnes {#use-case-send-emails}

De verkoopafdeling van een website over sportartikelen wil een marketingcampagne per e-mail uitzenden naar een lijst met contactpersonen die zichzelf hebben geïdentificeerd als geïnteresseerd in voetbal. De lijsten van contacten worden gescheiden als partijen in de gegevensuitvoer die van het ontwikkelingsteam van de website wordt ontvangen en moeten daarom worden gevolgd. Het team identificeert een bestaand [!DNL Mailchimp] publiek en begint het publiek van Experience Platform te bouwen waarin de contacten van elke lijst worden toegevoegd. Nadat u deze soorten publiek naar [!DNL Mailchimp Interest Categories] hebt verzonden, worden contactpersonen die niet aanwezig zijn in het geselecteerde [!DNL Mailchimp] -publiek, toegevoegd aan een groep met de publieksnaam waartoe de contactpersoon behoort. Als er al contactpersonen aanwezig zijn in het publiek of de groep van [!DNL Mailchimp] , wordt de informatie van deze contactpersonen bijgewerkt. Zodra de gegevens naar [!DNL Mailchimp Interest Categories] zijn verzonden, kan het verkoopteam de marketingcampagne selecteren en per e-mail verzenden naar de belangengroep van de voetbal in het [!DNL Mailchimp] -publiek.

## Vereisten {#prerequisites}

Raadpleeg de onderstaande secties voor alle voorwaarden die u in Experience Platform en [!DNL Mailchimp] moet instellen en voor informatie die u moet verzamelen voordat u met het [!DNL Mailchimp Interest Categories] -doel kunt werken.

### Vereisten in Experience Platform {#prerequisites-in-experience-platform}

Alvorens gegevens aan de [!DNL Mailchimp Interest Categories] bestemming te activeren, moet u a [ schema ](/help/xdm/schema/composition.md), a [ dataset ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=nl-NL) hebben, en [ segmenten ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=nl-NL) die in [!DNL Experience Platform] worden gecreeerd.

### Vereisten voor het doel [!DNL Mailchimp Interest Categories] {#prerequisites-destination}

Houd rekening met de volgende voorwaarden om gegevens van Experience Platform naar uw [!DNL Mailchimp] -account te exporteren:

#### U moet een [!DNL Mailchimp] -account hebben {#prerequisites-account}

Voordat u een [!DNL Mailchimp Interest Categories] -doel kunt maken, moet u eerst controleren of u een [!DNL Mailchimp] -account hebt. Als u niet reeds hebt, bezoek de [[!DNL Mailchimp]  aanmeldingspagina ](https://login.mailchimp.com/signup/) om uw rekening te registreren en te creëren.

#### API-sleutel van [!DNL Mailchimp] verzamelen {#gather-credentials}

U hebt uw [!DNL Mailchimp] **API sleutel** nodig om de [!DNL Mailchimp Interest Categories] bestemming tegen uw [!DNL Mailchimp] rekening voor authentiek te verklaren. De **API sleutel** dient als **Wachtwoord** wanneer u [ de bestemming ](#authenticate) voor authentiek verklaart.

Als u niet uw **API sleutel** hebt, het Teken binnen aan uw rekening en verwijs naar [[!DNL Mailchimp]  produceer uw API sleutel ](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key) documentatie om tot te leiden.

Een voorbeeld van een API-sleutel is `0123456789abcdef0123456789abcde-us14` .

>[!IMPORTANT]
>
>Als u de **API sleutel** produceert, schrijf het neer aangezien u niet tot het na generatie zult kunnen toegang hebben.

#### [!DNL Mailchimp] datacenter identificeren {#identify-data-center}

Vervolgens moet u het datacenter van [!DNL Mailchimp] identificeren. Dit doen, login aan uw [!DNL Mailchimp] rekening en navigeer aan de **API sleutelensectie** van uw rekening.

De waarde is het eerste deel van de URL die u in uw browser ziet. Als URL *https:// `us14` .mailchimp.com/account/api/* is, dan is het gegevenscentrum `us14`.

Het is ook toegevoegd aan uw API sleutel in de vorm *sleutel-dc*; als uw API sleutel `0123456789abcdef0123456789abcde-us14` is, dan is het gegevenscentrum `us14`.

Schrijf de waarde van het gegevenscentrum *(`us14` in dit voorbeeld)* neer, hebt u deze waarde nodig wanneer u [ bestemmingsdetails ](#destination-details) vult.

Als u verdere begeleiding vereist, verwijs naar de [[!DNL Mailchimp]  documentatie van Grondbeginselen ](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-structure).

### Guardrails {#guardrails}

Elk van uw [!DNL Mailchimp] publiek kan tot 60 groepnamen (of rentecategorieën) in één enkele groep of over verscheidene groepen binnen het zelfde publiek bevatten. Verwijs naar [!DNL Mailchimp] [ groepen ](https://mailchimp.com/help/getting-started-with-groups/) voor om het even welke vereiste verduidelijkingen. Wanneer u deze limiet bereikt, ontvangt u een `400 BAD_REQUEST Cannot have more than 60 interests per list (Across all categories)` -bericht als een foutreactie van de API van [!DNL Mailchimp] .

Bovendien, verwijs naar [!DNL Mailchimp] [ tariefgrenzen ](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-limits) voor gedetailleerde informatie over de grenzen die door [!DNL Mailchimp] API worden opgelegd.

## Ondersteunde identiteiten {#supported-identities}

[!DNL Mailchimp] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [ identiteiten ](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| Email | E-mailadres contactpersoon | Verplicht |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | <ul><li>U exporteert alle leden van een segment samen met de gewenste schemavelden *(bijvoorbeeld: e-mailadres, telefoonnummer, achternaam)* volgens uw veldtoewijzing.</li><li> Voor elk geselecteerd publiek in Experience Platform wordt de bijbehorende segmentstatus van [!DNL Mailchimp Interest Categories] bijgewerkt met de publieksstatus van Experience Platform.</li></ul> |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Wanneer een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [ het stromen bestemmingen ](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

Zoek in **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** naar [!DNL Mailchimp Interest Categories] . U kunt de locatie ook in de categorie **[!UICONTROL Email marketing]** vinden.

### Verifiëren voor bestemming {#authenticate}

Als u voor verificatie bij het doel wilt zorgen, vult u de vereiste velden hieronder in en selecteert u **[!UICONTROL Connect to destination]** .

| Veld | Beschrijving |
| --- | --- |
| **[!UICONTROL Username]** | Uw [!DNL Mailchimp Interest Categories] gebruikersnaam. |
| **[!UICONTROL Password]** | Uw [!DNL Mailchimp] **API sleutel**, die u neer in de [ Gather  [!DNL Mailchimp]  geloofsbrieven ](#gather-credentials) sectie had genoteerd.<br> Uw API sleutel neemt de vorm van `{KEY}-{DC}`, waar het `{KEY}` gedeelte naar de waarde verwijst neer in de [[!DNL Mailchimp]  API belangrijkste ](#gather-credentials) sectie en het `{DC}` gedeelte verwijst naar het [[!DNL Mailchimp]  gegevenscentrum ](#identify-data-center). <br> U kunt of het `{KEY}` gedeelte of het volledige vorm verstrekken.<br> Als uw API-sleutel bijvoorbeeld <br>*`0123456789abcdef0123456789abcde-us14`*is, <br> kunt u *`0123456789abcdef0123456789abcde`*of *`0123456789abcdef0123456789abcde-us14`*als waarde opgeven. |

{style="table-layout:auto"}

{het schermschot van 0} Experience Platform UI die toont hoe te voor authentiek te verklaren.![&#128279;](../../assets/catalog/email-marketing/mailchimp-interest-categories/authenticate-destination.png)

Als de opgegeven gegevens geldig zijn, geeft de gebruikersinterface de status **[!UICONTROL Connected]** weer met een groen vinkje. Vervolgens kunt u verdergaan met de volgende stap.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

{het schermschot van 0} Experience Platform UI die de bestemmingsdetails toont.![&#128279;](../../assets/catalog/email-marketing/mailchimp-interest-categories/destination-details.png)

| Veld | Beschrijving |
| --- | --- |
| **[!UICONTROL Name]** | Een naam waarmee u deze bestemming in de toekomst zult erkennen. |
| **[!UICONTROL Description]** | Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren. |
| **[!UICONTROL Data center]** | Uw [!DNL Mailchimp] account `data center` . Verwijs naar [ identificeer  [!DNL Mailchimp]  gegevenscentrum ](#identify-data-center) sectie voor om het even welke begeleiding. |
| **[!UICONTROL Audience Name (Please select Data center first)]** | Nadat u **[!UICONTROL Data center]** hebt geselecteerd, wordt deze vervolgkeuzelijst automatisch gevuld met de publieksnamen van uw [!DNL Mailchimp] -account. Selecteer het publiek dat u wilt bijwerken met gegevens uit Experience Platform. |
| **[!UICONTROL Interest Category (Please select Data center and Audience Name first)]** | Nadat u **[!UICONTROL Audience Name]** hebt geselecteerd, wordt deze vervolgkeuzelijst automatisch gevuld met de categorienamen van de belangengroep van uw [!DNL Mailchimp] -account. Selecteer de categorienaam die u wilt bijwerken met gegevens uit Experience Platform. |

{style="table-layout:auto"}

>[!TIP]
>
> Als de API-sleutel die u in het veld **[!UICONTROL Password]** of de waarde **[!UICONTROL Data center]** hebt opgegeven, onjuist is, geeft de interface een API-foutreactie [!DNL Mailchimp] weer: *`No options are available. Please verify the values selected for the following dependent fields: dataCenter`* zoals hieronder wordt weergegeven. In dit geval kunt u geen waarde selecteren in het veld **[!UICONTROL Audience Name (Please select Data center first)]** . Geef de juiste waarden op om deze fout te corrigeren.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [ het intekenen aan bestemmingsalarm gebruikend UI ](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [ activeer profielen en publiek aan het stromen publiek uitvoerbestemmingen ](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiek aan deze bestemming.

### Afbeeldingsoverwegingen en voorbeeld {#mapping-considerations-example}

Als u uw publieksgegevens correct vanuit Adobe Experience Platform naar de [!DNL Mailchimp Interest Categories] -bestemming wilt verzenden, moet u de stap voor veldtoewijzing doorlopen. Toewijzing bestaat uit het maken van een koppeling tussen de schemavelden van uw Experience Data Model (XDM) in uw Experience Platform-account en de overeenkomstige equivalenten van de doelbestemming.

Voer de onderstaande stappen uit om uw XDM-velden correct toe te wijzen aan de [!DNL Mailchimp Interest Categories] -doelvelden:

1. Selecteer **[!UICONTROL Add new mapping]** in de stap **[!UICONTROL Mapping]** . U ziet nu een nieuwe toewijzingsrij op het scherm.
1. Kies in het venster **[!UICONTROL Select source field]** de categorie **[!UICONTROL Select attributes]** en selecteer het XDM-kenmerk of kies de categorie **[!UICONTROL Select identity namespace]** en selecteer een identiteit.
1. Kies in het **[!UICONTROL Select target field]** -venster de **[!UICONTROL Select identity namespace]** en selecteer een identiteit of kies **[!UICONTROL Select attributes]** -categorie en selecteer een van de kenmerken die zijn ingevuld in de [!DNL Mailchimp] API. *om het even welke douanekenmerken die u aan het geselecteerde [!DNL Mailchimp] publiek hebt toegevoegd zullen ook voor selectie als doelgebieden beschikbaar zijn.*

   De toewijzingen tussen uw XDM-profielschema en [!DNL Mailchimp Interest Categories] zijn als volgt:

   | Source-veld | Doelveld | Notities |
   | --- | --- | --- |
   | `IdentityMap: Email` | `Identity: email` | Verplicht: Ja |
   | `xdm: person.name.firstName` | `Attribute: FNAME` | |
   | `xdm: person.name.lastName` | `Attribute: LNAME` | |
   | `xdm: person.birthDayAndMonth` | `Attribute: BIRTHDAY` | |

   Daarnaast is `ADDRESS` een speciaal doelveld dat `merge field` binnen uw publiek [!DNL Mailchimp] wordt genoemd. De [[!DNL Mailchimp]  documentatie ](https://mailchimp.com/developer/marketing/docs/merge-fields/) bepaalt de vereiste sleutels zoals `addr1`, `city`, `state`, en `zip`, en de facultatieve sleutels `addr2` en `country`. De waarden voor deze velden moeten tekenreeksen zijn. Als een van de `ADDRESS` -veldtoewijzingen aanwezig is, geeft de bestemming het `ADDRESS` -object door aan de [!DNL Mailchimp] API voor update. Voor alle `ADDRESS` -velden die niet worden toegewezen, wordt de standaardwaarde `NULL` gebruikt, behalve voor het land dat standaard op `US` is ingesteld.

   De volgende toewijzingen zijn beschikbaar voor het veld `ADDRESS` :

   | Source-veld | Doelveld |
   | --- | --- |
   | `xdm: workAddress.street1` | `Attribute: ADDRESS.addr1` |
   | `xdm: workAddress.street2` | `Attribute: ADDRESS.addr2` |
   | `xdm: workAddress.city` | `Attribute: ADDRESS.city` |
   | `xdm: workAddress.state` | `Attribute: ADDRESS.state` |
   | `xdm: workAddress.postalCode` | `Attribute: ADDRESS.zip` |
   | `xdm: workAddress.country` | `Attribute: ADDRESS.country` |

   U wilt bijvoorbeeld de waarde voor `country` bijwerken met de bestaande adresvelden `addr1` , `city` , `state` en `zip` van de contactpersoon als `132, My Street, Kingston` , `New York` , `New York` en `12401` . Om `country` bij te werken moet u de bestaande waarden met veranderingen *(als om het even welk)* en de nieuwe waarde voor land overgaan. De waarden in uw gegevensset moeten dus `132, My Street, Kingston`, `New York`, `New York`, `12401` en `US` zijn. Als u alleen `country` doorgeeft en geen waarden voor `addr1` , `city` , `state` en `zip` opgeeft, worden deze door `NULL` overschreven.

   Hieronder ziet u een voorbeeld met de voltooide toewijzingen:
   {het schermschot van 0} Experience Platform UI die gebiedsafbeeldingen toont.![&#128279;](../../assets/catalog/email-marketing/mailchimp-interest-categories/mappings.png)

Wanneer u klaar bent met het opgeven van de toewijzingen voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Gegevens exporteren valideren {#exported-data}

Volg onderstaande stappen om te controleren of u de bestemming correct hebt ingesteld:

* Meld u aan bij uw [[!DNL Mailchimp] ](https://login.mailchimp.com/) -account. Navigeer vervolgens naar de pagina **[!DNL Audience]** . Vouw vervolgens het menu **[!DNL Manage Contacts]** uit en selecteer **[!DNL Groups]** .

{het schermschot van 0} Mailchimp UI die de de groepspagina van het Publiek toont.![&#128279;](../../assets/catalog/email-marketing/mailchimp-interest-categories/audience-groups.png)

* Selecteer de groep en controleer of het geselecteerde publiek is gemaakt als categorieën met de publieksnaam uit Experience Platform, die kunnen worden gevolgd door een automatisch gegenereerd achtervoegsel.
   * Deze bestemming gebruikt de geselecteerde segmenten&#39; namen om de rentecategorie tot stand te brengen door [[!DNL Mailchimp]  te gebruiken voeg rentecategorie API ](https://mailchimp.com/developer/marketing/api/interest-categories/add-interest-category/) toe. Als u een nieuw doel maakt en hetzelfde publiek weer activeert, voegt [!DNL Mailchimp] een achtervoegsel toe om onderscheid te maken tussen de bestaande en de nieuwe segmenten.
* Contacten waarvan de e-mails niet in de groep bestonden, worden toegevoegd aan de nieuwe categorie.
* Voor contacten die reeds binnen de groep bestaan, worden de gegevens van het attributengebied bijgewerkt, en het contact toegevoegd aan de pas gecreëerde categorie.

{het schermschot van 0} Mailchimp UI die de de groepscategorieën van het Publiek toont.![&#128279;](../../assets/catalog/email-marketing/mailchimp-interest-categories/audience-groups-category.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, zie het [ overzicht van het Beleid van Gegevens ](/help/data-governance/home.md).

## Fouten en problemen oplossen {#errors-and-troubleshooting}

### Fout aangetroffen als de waarden van de [!DNL Mailchimp] API-sleutel of het datacenter onjuist zijn {#incorrect-credentials-error}

Als de API-sleutel die u in het veld **[!UICONTROL Password]** of de waarde **[!UICONTROL Data center]** hebt opgegeven, onjuist is, geeft de interface een API-foutreactie [!DNL Mailchimp] weer: *`No options are available. Please verify the values selected for the following dependent fields: dataCenter`* zoals hieronder wordt weergegeven. In dit geval kunt u geen waarde selecteren in het veld **[!UICONTROL Audience Name (Please select Data center first)]** .

![ het schermschot van Experience Platform UI die fout toont als uw sleutel van de Brievenchimp API of waarden van het gegevenscentrum onjuist zijn.](../../assets/catalog/email-marketing/mailchimp-interest-categories/error.png)

Als u deze fout wilt verhelpen en wilt doorgaan naar de volgende stap, moet u de juiste waarden opgeven. Verwijs naar [  [!DNL Mailchimp]  gegevenscentrum ](#identify-data-center) identificeren en
[ verzamel  [!DNL Mailchimp]  API zeer belangrijke ](#gather-credentials) secties als u begeleiding nodig hebt.

### Fout aangetroffen als de limiet voor [!DNL Mailchimp] groepsnaam is overschreden {#group-name-limits-error}

Wanneer u het doel maakt, ontvangt u mogelijk de volgende foutberichten: *`Cannot have more than 60 interests per list (Across all categories)`* of *`400 BAD_REQUEST`* . Dit gebeurt wanneer u de 60 groepsnamen (of rentecategorieën) in één enkele groep of over verscheidene groepen binnen de zelfde publieksgrens overschrijdt, zoals die in de [ wordt beschreven guardrails ](#guardrails) sectie. Als u deze fout wilt corrigeren, moet u ervoor zorgen dat de limiet voor de groepsnaam in [!DNL Mailchimp] niet wordt overschreden.

### [!DNL Mailchimp] Status- en foutcodes

Verwijs naar de [[!DNL Mailchimp]  pagina van fouten ](https://mailchimp.com/developer/marketing/docs/errors/) voor een uitvoerige lijst van status en foutencodes met verklaringen.

## Aanvullende bronnen {#additional-resources}

Hieronder vindt u aanvullende nuttige informatie uit de documentatie van [!DNL Mailchimp] :
* [ Begonnen het worden met  [!DNL Mailchimp] ](https://mailchimp.com/help/getting-started-with-mailchimp/)
* [ Begonnen het worden met Soorten publiek ](https://mailchimp.com/help/getting-started-audience/)
* [ creeer een Publiek ](https://mailchimp.com/help/create-audience/)
* [ Begonnen het worden met Groepen ](https://mailchimp.com/help/getting-started-with-groups/)
* [ creeer een nieuwe Groep van het Publiek ](https://mailchimp.com/help/create-new-audience-group/)
* [ Categorieën van de Rente ](https://mailchimp.com/developer/marketing/api/interest-categories/)
* [ Marketing API ](https://mailchimp.com/developer/marketing/api/)
