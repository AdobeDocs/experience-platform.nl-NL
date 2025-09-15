---
title: (V2) Salesforce Marketing Cloud Account Engagement
description: Leer hoe u de (V2) Salesforce Marketing Cloud-accountservice (voorheen Pardot genoemd) bestemming kunt gebruiken om uw profielgegevens te exporteren en deze te activeren in Salesforce Marketing Cloud Account Engagement met behulp van batchverwerking voor uw zakelijke behoeften.
badge: label="Alpha" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: d1405237698271607fa672ccae1ac731d66df263
workflow-type: tm+mt
source-wordcount: '1742'
ht-degree: 1%

---

# [!DNL (V2) Salesforce Marketing Cloud Account Engagement]-verbinding

Met het doel [[!DNL Salesforce Marketing Cloud Account Engagement] ](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) (voorheen bekend als [!DNL Pardot] ) kunt u uw Adobe Experience Platform-profielgegevens exporteren naar het Salesforce B2B-marketingautomatiseringsplatform.

Dankzij deze integratie kunt u uw klantprofielen in Adobe Experience Platform naadloos synchroniseren met uw marketingcampagnes in [!DNL Salesforce Marketing Cloud Account Engagement] .

Deze bestemming gebruikt [[!DNL Salesforce Import API v5] ](https://developer.salesforce.com/docs/marketing/pardot/guide/import-v5.html) om de uitvoer van partijgegevens efficiënt te verwerken.


>[!IMPORTANT]
> 
> Dit is de V2 versie van de [ 1} bestemming van het Betrokkenheid van de Rekening van Marketing Cloud van Salesforce {. ](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md) Deze versie vervangt de vorige bestemming en is momenteel in Alpha-versie.
> > <br>
> > Als u momenteel de vorige versie van de [ bestemming van de Rekening van Salesforce Marketing Cloud van ](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md) gebruikt, moet u aan deze V2 versie vóór **Januari 2026** migreren. Na januari 2026 zal Adobe de vorige versie uit bedrijf nemen en is deze niet meer beschikbaar.


## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de [!DNL (V2) Marketing Cloud Account Engagement] bestemming zou moeten gebruiken, zijn hier voorbeelden van gebruiksgevallen die de klanten van Adobe Experience Platform door deze bestemming kunnen oplossen.

### B2B Leadbeheer {#use-case-lead-management}

Synchroniseer de loodgegevens van Adobe Experience Platform tot [!DNL Salesforce Marketing Cloud Account Engagement] voor uitgebreide zorg en scoring van leads. Uw marketingteam kan profielen voor rijke doelgroepen maken in Experience Platform en deze exporteren naar [!DNL Salesforce Marketing Cloud Account Engagement] voor geautomatiseerde B2B-marketingcampagnes.

### Automatisering van Campaign {#use-case-campaign-automation}

U kunt marketingcampagnes activeren in [!DNL Salesforce Marketing Cloud Account Engagement] door gebruik te maken van publiek dat u in Adobe Experience Platform definieert. Nadat u uw doelpubliek naar [!DNL Salesforce] hebt geëxporteerd, kunt u deze gebruikers gebruiken om e-mailcampagnes uit te voeren en uw leads te beheren via het opvoeden, scoren en segmenteren van de campagne.

### Profielverrijking {#use-case-profile-enrichment}

Verbeter uw [!DNL Salesforce Marketing Cloud Account Engagement] perspectiefprofielen met rijke klantgegevens van Adobe Experience Platform. Exporteer uitgebreide profielkenmerken om gedetailleerdere perspectiefrecords in [!DNL Salesforce Marketing Cloud Account Engagement] te maken voor een betere doelgerichtheid en personalisatie.

## Vereisten {#prerequisites}

Raadpleeg de onderstaande secties voor alle voorwaarden die u in Experience Platform en [!DNL Salesforce] moet instellen en voor informatie die u moet verzamelen voordat u met het [!DNL (V2) Marketing Cloud Account Engagement] -doel kunt werken.

### Experience Platform-voorwaarden {#prerequisites-in-experience-platform}

Alvorens gegevens aan de [!DNL (V2) Marketing Cloud Account Engagement] bestemming te activeren, moet u a [ schema ](/help/xdm/schema/composition.md), a [ dataset ](../../../catalog/datasets/overview.md) hebben, en [ publiek ](../../../segmentation/types/overview.md) dat in [!DNL Experience Platform] wordt gecreeerd.

### [!DNL Salesforce Marketing Cloud Account Engagement] voorwaarden {#prerequisites-destination}

Houd rekening met de volgende voorwaarden om gegevens van Experience Platform naar uw [!DNL Marketing Cloud Account Engagement] -account te exporteren:

#### U moet een [!DNL Marketing Cloud Account Engagement] -account hebben {#prerequisites-account}

Een [!DNL Marketing Cloud Account Engagement] rekening met een abonnement op het [ product van de Betrokkenheid van de Rekening van Marketing Cloud ](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) is verplicht te werk te gaan.

#### [!DNL Marketing Cloud Account Engagement] gebruikersgegevens verzamelen {#gather-credentials}

Schrijf de onderstaande items naar beneden voordat u deze verifieert voor de bestemming [!DNL (V2) Marketing Cloud Account Engagement] .

| Credentials | Beschrijving |
| --- | --- |
| **[!UICONTROL Account Engagement Business Unit ID]** | Uw [!DNL Salesforce] ID van de Business Unit voor accountbetrokkenheid. Verwijs naar de Salesforce [ documentatie ](https://help.salesforce.com/s/articleView?id=000381973&type=1) om te leren hoe te om identiteitskaart te vinden. |

{style="table-layout:auto"}

## Ondersteunde identiteiten {#supported-identities}

[!DNL (V2) Marketing Cloud Account Engagement] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [ identiteiten ](/help/identity-service/features/namespaces.md).

Als er een overeenkomst wordt gevonden met een van deze id&#39;s, wordt het perspectiefrecord voor Betrokkenheid van account bijgewerkt met de gegevens van Adobe Experience Platform. Als er geen overeenkomst wordt gevonden, wordt een nieuw perspectiefrecord gemaakt in Account Engagement.

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| `matchId` | Prospectie-id in accountservice | Ten minste een van deze drie identiteiten is vereist |
| `matchSalesforceId` | Salesforce-lead/contact-id van het vooruitzicht | Ten minste een van deze drie identiteiten is vereist |
| `matchEmail` | E-mailadres van het vooruitzicht | Ten minste een van deze drie identiteiten is vereist |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | <ul><li>U exporteert alle leden van een publiek samen met de gewenste schemavelden *(bijvoorbeeld: e-mailadres, telefoonnummer, achternaam)* volgens uw veldtoewijzing.</li><li>Dit doel ondersteunt batchexport van profielgegevens met de Salesforce Import API v5.</li></ul> |
| Exportfrequentie | **[!UICONTROL Batch]** | <ul><li>**Aanvankelijke Uitvoer**: Volledige uitvoer onmiddellijk na afbeelding</li><li>**Volgende Uitvoer**: De stijgende uitvoer om de 3 uren</li><li>Dit schema is vast en kan niet worden aangepast in Alpha</li></ul> |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Selecteer **[!UICONTROL Connect to destination]** als u wilt verifiëren bij het doel.

![ het werkschema van de de bestemmingsverbinding van de Rekening van Salesforce van Marketing Cloud van de Rekening van Salesforce Marketing Cloud van het Betrokkenheid V2 het werkschema van de bestemmingsverbinding ](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/connect-to-destination.png "")

U wordt omgeleid naar de aanmeldingspagina van [!DNL Salesforce] . Voer uw [!DNL Marketing Cloud Account Engagement] -accountgegevens in en selecteer **[!UICONTROL Log In]** .

![ Salesforce login pagina ](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/salesforce-auth.png " Salesforce login pagina.")

Daarna, uitgezochte **[!UICONTROL Allow]** om toestemmingen aan **Adobe Experience Platform** app te geven om tot uw [!DNL Salesforce Marketing Cloud Account Engagement] rekening toegang te hebben. *u moet dit slechts eenmaal doen*.

![ het screenshot van Salesforce App pop-up om toestemmingen aan Experience Platform te geven app toegang tot de Betrokkenheid van de Rekening van Marketing Cloud.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/allow-app.png)

Als de verstrekte details geldig zijn, toont UI een bericht: *u met succes verbonden met (V2) de rekening van de Betrokkenheid van de Rekening van Salesforce Marketing Cloud* en a **[!UICONTROL Connected]** status met een groen vinkje.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Account Engagement Business Unit ID]**: Uw [!DNL Salesforce] `Account Engagement Business Unit ID` .
* **[!UICONTROL Account Engagement API]**: selecteer of u de productie (`https://pi.pardot.com`) of demo (`https://pi.demo.pardot.com`) eindpunten van de RekeningBetrokkenheid API wilt gebruiken.
* **[!UICONTROL Account Engagement Campaign ID]**: elk [!DNL Account Engagement] perspectief moet aan een campagne worden gekoppeld. Als u geen campagne-id instelt, probeert Account Engagement automatisch een dergelijke id toe te wijzen als er een standaard bestaat in uw Salesforce-account.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [ het intekenen aan bestemmingsalarm gebruikend UI ](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [ activeer publieksgegevens aan de uitvoerbestemmingen van het partijprofiel ](/help/destinations/ui/activate-batch-profile-destinations.md) voor instructies bij het activeren van publiek aan deze bestemming.

### Afbeeldingsoverwegingen en voorbeeld {#mapping-considerations-example}

Als u publieksgegevens van Adobe Experience Platform naar de [!DNL (V2) Marketing Cloud Account Engagement] -bestemming wilt verzenden, moet u de XDM-schemavelden (Experience Data Model) toewijzen aan de corresponderende velden in de bestemming.

Verwijs naar de [ Verwijzing API v5 documentatie van het Vooruitzicht van Salesforce ](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html) voor een volledige lijst van gesteunde gebieden. Merk op dat [ douanegebieden ](https://developer.salesforce.com/docs/marketing/pardot/guide/custom-field-v5.html) niet in de versie van Alpha worden gesteund.

#### Ondersteunde kenmerken {#supported-attributes}

De Salesforce Marketing Cloud Account Engagement-bestemming ondersteunt de doelkenmerken die in de onderstaande tabel worden beschreven.

| Kenmerk | Type | Beschrijving |
|---------|----------|----------|
| `salesforceId` | String | De Salesforce-id van het vooruitzicht |
| `salesforceOwnerId` | Geheel | De Salesforce-gebruikersnaam van de toekomstige eigenaar |
| `salutation` | String | De aanhef van het vooruitzicht (bv. meneer, mevrouw, dr.) |
| `score` | Geheel | De score van het vooruitzicht in Betrokkenheid bij account |
| `source` | String | De bron van het perspectiefrecord |
| `state` | String | De staat/provincie van het vooruitzicht |
| `territory` | String | Het aan het vooruitzicht toegewezen gebied |
| `userId` | Geheel | De gebruiker - identiteitskaart verbonden aan het vooruitzicht |
| `website` | String | De URL van de website van het vooruitzicht |
| `yearsInBusiness` | String | Het aantal jaren dat het vooruitzicht in zaken is geweest |
| `zip` | String | De postcode van het vooruitzicht |

#### Vereiste toewijzingen {#required-mappings}

Voordat u uw gegevens gaat toewijzen, bekijkt u de vereiste veldtoewijzingen hieronder.

| Doelveld | Type | Vereist | Wanneer gebruiken |
|---|---|---|---|
| `email` | Kenmerk | Altijd vereist | Het e-mailadres van het vooruitzicht. Dit is de primaire id voor het zoeken naar en zoeken naar overeenkomende perspectiefrecords in Account Engagement wanneer u geen `matchId` of `matchSalesforceId` hebt. <br> **Nota:** met de &quot;Toestaan Veelvoudige Vooruitzichten van de Betrokkenheid van de Rekening met de Zelfde eigenschap E-mail van het Adres&quot;, die alleen op e-mail baseert kan tot dubbelzinnigheid leiden als er veelvoudige vooruitzichten met zelfde e-mail zijn. De Betrokkenheid van de rekening zal gewoonlijk aan het bijwerken van het vooruitzicht met de meest recente activiteit in dergelijke gevallen in gebreke blijven. |
| `matchId` | Identiteit | Ten minste een van deze drie identiteiten is vereist | Een unieke id die wordt gegenereerd door Account Engagement voor elk afzonderlijk perspectiefrecord. Gebruik dit wanneer u reeds identiteitskaart van het Vooruitzicht van de Betrokkenheid van de Rekening hebt en wilt ervoor zorgen de updates op het correcte vooruitzicht worden toegepast, vooral wanneer de veelvoudige vooruitzichten het zelfde e-mailadres delen. |
| `matchSalesforceId` | Identiteit | Ten minste een van deze drie identiteiten is vereist | De Salesforce-id van een lead of contactpersoon in Salesforce. Gebruik deze optie als er al een vooruitzicht is gesynchroniseerd met Salesforce om de consistentie van gegevens tussen Account Engagement en Salesforce te behouden. |
| `matchEmail` | Identiteit | Ten minste een van deze drie identiteiten is vereist | Het e-mailadres van het vooruitzicht dat voor aanpassing wordt gebruikt. Gebruik dit als een alternatieve id wanneer u niet beschikt over de specifieke Uitzicht-id voor Betrokkenheid van account of de Salesforce-id. Opmerking: als meerdere vooruitzichten hetzelfde e-mailadres delen, wordt het perspectief standaard bijgewerkt met de meest recente activiteit. |

Voer de onderstaande stappen uit om de juiste velden toe te wijzen.

1. Selecteer **[!UICONTROL Mapping]** in de stap **[!UICONTROL Add new mapping]** . Er verschijnt een nieuwe toewijzingsrij op het scherm.
1. Kies in het venster **[!UICONTROL Select source field]** de categorie **[!UICONTROL Select attributes]** en selecteer het XDM-kenmerk of kies de categorie **[!UICONTROL Select identity namespace]** en selecteer een identiteit.
1. Kies in het **[!UICONTROL Select target field]** -venster de **[!UICONTROL Select identity namespace]** en selecteer een identiteit of kies **[!UICONTROL Select custom attributes]** -categorie en geef een waarde op in de lijst met standaardvelden voor het vooruitzicht van accountbetrokkenheid.

![ Voorbeeld van het in kaart brengen van XDM gebieden en identiteiten XDM aan de gebieden van het Betrokkenheid van de Rekening van Salesforce Marketing Cloud V2 van de Rekening ](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/mapping.png " van de Verhouding van ") van XDM gebieden en identiteiten aan de gebieden van de Rekening van Salesforce Marketing Cloud

## Gegevens exporteren valideren {#exported-data}

Volg onderstaande stappen om te controleren of u de bestemming correct hebt ingesteld:

1. Navigeer naar een geselecteerd publiek. Selecteer het tabblad **[!DNL Activation data]**. In de kolom **[!UICONTROL Mapping ID]** wordt de naam weergegeven van het aangepaste veld dat op de pagina [!DNL Marketing Cloud Account Engagement Prospects] wordt gegenereerd.
   ![ het het schermschot van Experience Platform UI die identiteitskaart van de Toewijzing voor een geselecteerd segment tonen.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/selected-segment-mapping-id.png)

1. Meld u aan bij de [[!DNL Salesforce] ](https://login.salesforce.com/) -website. Navigeer vervolgens naar de pagina **[!DNL Account Engagement]** > **[!DNL Prospects]** > **[!DNL Pardot Prospects]** en controleer of de perspectieven van het publiek zijn toegevoegd of bijgewerkt. U kunt ook toegang krijgen tot [[!DNL Account Engagement] ](https://pi.pardot.com/) en tot de pagina **[!DNL Prospects]** .
   {het schermschot van 0} Salesforce UI die de pagina van Vooruitzichten toont.![](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/prospects.png)

1. Om te controleren of de vooruitzichten zijn bijgewerkt, selecteer een vooruitzicht en verifieer of is het gebied van het douanevooruitzicht bijgewerkt met de het publieksstatus van Experience Platform.
   {het schermschot van 0} Salesforce UI die de geselecteerde pagina van het Vooruitzicht toont, wordt het gebied van het douanevooruitzicht bijgewerkt met de publieksstatus.![](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/prospect.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, zie het [ overzicht van het Beleid van Gegevens ](/help/data-governance/home.md).

## Aanvullende bronnen {#additional-resources}

* [!DNL Marketing Cloud Account Engagement] [ API documentatie ](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html)
* [ de Import API van Salesforce v5 Documentatie ](https://developer.salesforce.com/docs/marketing/pardot/guide/import-v5.html)
* [ de Verhouding API van Salesforce v5 Documentatie ](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html)