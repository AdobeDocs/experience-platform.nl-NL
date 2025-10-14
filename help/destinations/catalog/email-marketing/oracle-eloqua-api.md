---
title: (API) Oracle Eloqua-verbinding
description: Met de (API) Oracle Eloqua-bestemming kunt u uw accountgegevens exporteren en activeren binnen Oracle Eloqua voor uw zakelijke behoeften.
last-substantial-update: 2023-03-14T00:00:00Z
exl-id: 97ff41a2-2edd-4608-9557-6b28e74c4480
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1967'
ht-degree: 0%

---


# [!DNL (API) Oracle Eloqua] verbinding

[[!DNL Oracle Eloqua] &#x200B;](https://www.oracle.com/cx/marketing/automation/) laat marketers toe om campagnes te plannen en uit te voeren terwijl het leveren van een gepersonaliseerde klantenervaring voor hun vooruitzichten. Dankzij geïntegreerd beheer van leads en het eenvoudig maken van campagnes, kunnen marketers op het juiste moment het juiste publiek betrekken bij de reis van hun koper en schalen ze elegant om het publiek te bereiken via verschillende kanalen, zoals e-mail, display, search, video en mobile. Verkoopteams kunnen meer transacties sneller sluiten, waardoor het marketingrendement in real-time insight toeneemt.

Dit [!DNL Adobe Experience Platform] [&#x200B; doel &#x200B;](/help/destinations/home.md) hefboomwerkingen [&#x200B; werkt een contact &#x200B;](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-id-put.html) verrichting van [!DNL Oracle Eloqua] REST API bij, die u toestaat om **identiteiten** binnen een publiek in [!DNL Oracle Eloqua] bij te werken.

[!DNL Oracle Eloqua] gebruikt [&#x200B; Basisauthentificatie &#x200B;](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html) om met [!DNL Oracle Eloqua] REST API te communiceren. De instructies om aan uw [!DNL Oracle Eloqua] instantie voor authentiek te verklaren zijn verder hieronder, in [&#x200B; voor authentiek verklaren aan bestemmings &#x200B;](#authenticate) sectie.

## Gebruiksscenario’s {#use-cases}

De marketingafdeling van een onlineplatform wil een marketingcampagne op basis van e-mail uitzenden naar een publiek met nieuwsberichten. Het marketingteam van het platform kan bestaande informatie over leads bijwerken via Adobe Experience Platform, een publiek opbouwen op basis van hun eigen offline gegevens en deze soorten publiek doorsturen naar [!DNL Oracle Eloqua] , die vervolgens kan worden gebruikt om de marketingcampagne per e-mail te verzenden.

## Vereisten {#prerequisites}

### Experience Platform-voorwaarden {#prerequisites-in-experience-platform}

Alvorens gegevens aan de [!DNL Oracle Eloqua] bestemming te activeren, moet u a [&#x200B; schema &#x200B;](/help/xdm/schema/composition.md), a [&#x200B; dataset &#x200B;](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=nl-NL) hebben, en [&#x200B; segmenten &#x200B;](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=nl-NL) die in [!DNL Experience Platform] worden gecreeerd.

Verwijs naar de documentatie van Experience Platform voor [&#x200B; het schemagroep van de Details van het Lidmaatschap van de Publiek &#x200B;](/help/xdm/field-groups/profile/segmentation.md) als u begeleiding op publieksstatus nodig hebt.

### [!DNL Oracle Eloqua] voorwaarden {#prerequisites-destination}

Als u gegevens van Experience Platform naar uw [!DNL Oracle Eloqua] -account wilt exporteren, hebt u een [!DNL Oracle Eloqua] -account nodig.

Bovendien, moet u, bij een minimum, *&quot;Geavanceerde Gebruikers - de toestemmingen van de Marketing&quot;* voor uw [!DNL Oracle Eloqua] instantie. Verwijs naar de *&quot;Groepen van de Veiligheid&quot;* sectie op de [&#x200B; Beveiligde gebruikerstoegang &#x200B;](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/SecurityOverview/SecuredUserAccess.htm) pagina voor begeleiding. De toegang wordt vereist door de bestemming programmatically [&#x200B; uw basis URL &#x200B;](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/DeterminingBaseURL.html) bepalen wanneer het aanhalen van [!DNL Oracle Eloqua] API.

#### [!DNL Oracle Eloqua] gebruikersgegevens verzamelen {#gather-credentials}

Noteer de onderstaande items voordat u de verificatie uitvoert naar het doel van [!DNL Oracle Eloqua] :

| Credentials | Beschrijving |
| --- | --- |
| `Company Name` | De bedrijfsnaam die aan uw [!DNL Oracle Eloqua] account is gekoppeld. <br> u zult later `Company Name` en [!DNL Oracle Eloqua] `Username` als samengevoegde koord gebruiken dat als **[!UICONTROL Username]** moet worden gebruikt wanneer [&#x200B; voor authentiek verklaren aan de bestemming &#x200B;](#authenticate). |
| `Username` | De gebruikersnaam van uw [!DNL Oracle Eloqua] -account. |
| `Password` | Het wachtwoord van uw [!DNL Oracle Eloqua] -account. |
| `Pod` | [!DNL Oracle Eloqua] ondersteunt meerdere datacenters, elk met een unieke domeinnaam. [!DNL Oracle Eloqua] noemt deze als &quot;pods&quot;, er zijn momenteel zeven in totaal - p01, p02, p03, p04, p06, p07 en p08. Als u wilt weten welke POD u hebt ingeschakeld, meldt u zich aan bij [!DNL Oracle Eloqua] en noteert u de URL in uw browser nadat u zich met succes hebt aangemeld. Als de URL van uw browser bijvoorbeeld `secure.p01.eloqua.com` is, `pod` is `p01` . Verwijs naar [&#x200B; bepalend uw POD &#x200B;](https://community.oracle.com/topliners/discussion/4470225/determining-your-pod-number-for-oracle-eloqua) pagina voor extra begeleiding. |

Verwijs naar [&#x200B; het Ondertekenen binnen aan  [!DNL Oracle Eloqua] &#x200B;](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/Administration/Tasks/SigningInToEloqua.htm#Signing) voor begeleiding.

## Guardrails {#guardrails}

>[!NOTE]
>
>* [!DNL Oracle Eloqua] aangepaste contactvelden worden automatisch gemaakt met de namen van het publiek dat tijdens de stap **[!UICONTROL Select segments]** is geselecteerd.

* [!DNL Oracle Eloqua] heeft een maximale limiet van 250 aangepaste contactvelden.
* Voordat u nieuwe doelgroepen exporteert, moet u ervoor zorgen dat het aantal Experience Platform-doelgroepen en het aantal bestaande doelgroepen binnen [!DNL Oracle Eloqua] deze limiet niet overschrijden.
* Als deze limiet wordt overschreden, treedt er een fout op in Experience Platform. Dit is omdat [!DNL Oracle Eloqua] API er niet in slaagt om het verzoek te bevestigen, en met a - *400 antwoordt: Er was een bevestigingsfout* - foutenmelding beschrijvend de kwestie.
* Als u de hierboven opgegeven limiet hebt bereikt, moet u bestaande toewijzingen verwijderen van uw bestemming en de bijbehorende aangepaste contactvelden in uw [!DNL Oracle Eloqua] -account verwijderen voordat u meer segmenten kunt exporteren.

* Verwijs naar [[!DNL Oracle Eloqua]  Creërend de pagina van de Gebieden van het Contact &#x200B;](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/ContactFields/Tasks/CreatingContactFields.htm) voor informatie over extra grenzen.

## Ondersteunde identiteiten {#supported-identities}

[!DNL Oracle Eloqua] ondersteunt het bijwerken van de identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [&#x200B; identiteiten &#x200B;](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving | Verplicht |
|---|---|---|
| `EloquaId` | Unieke id van het contact. | Ja |

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | <ul><li>U exporteert alle leden van een segment samen met de gewenste schemavelden *(bijvoorbeeld: e-mailadres, telefoonnummer, achternaam)* volgens uw veldtoewijzing.</li><li> Voor elk geselecteerd publiek in Experience Platform wordt de bijbehorende segmentstatus van [!DNL Oracle Eloqua] bijgewerkt met de publieksstatus van Experience Platform.</li></ul> |
| Exportfrequentie | **[!UICONTROL Streaming]** | <ul><li>Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [&#x200B; het stromen bestemmingen &#x200B;](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [&#x200B; leerprogramma van de bestemmingsconfiguratie &#x200B;](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

Kies in **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** Zoeken naar [!DNL (API) Oracle Eloqua] . U kunt de locatie ook in de categorie **[!UICONTROL Email Marketing]** vinden.

### Verifiëren voor bestemming {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_apioracleeloqua_companyname_username"
>title="Bedrijfsnaam\Gebruikersnaam"
>abstract="Vul dit veld in met uw bedrijfsnaam en gebruikersnaam in de vorm Oracle Eloqua `{COMPANY_NAME}\{USERNAME}`"

Vul de vereiste velden hieronder in. Verwijs naar de [&#x200B; Gather  [!DNL Oracle Eloqua]  geloofsbrieven &#x200B;](#gather-credentials) sectie voor om het even welke begeleiding.
* **[!UICONTROL Password]**: Het wachtwoord van uw [!DNL Oracle Eloqua] -account.
* **[!UICONTROL Username]**: Een samengevoegde tekenreeks die bestaat uit uw [!DNL Oracle Eloqua] bedrijfsnaam en de [!DNL Oracle Eloqua] gebruikersnaam.<br> de samengevoegde waarde neemt de vorm van `{COMPANY_NAME}\{USERNAME}`.<br> Opmerking: gebruik geen accolades of spaties en zorg dat de `\` behouden blijft. <br> Bijvoorbeeld als uw [!DNL Oracle Eloqua] Bedrijfsnaam `MyCompany` is en [!DNL Oracle Eloqua] Gebruikersnaam `Username` is, is de samengevoegde waarde u in het **[!UICONTROL Username]** gebied zult gebruiken `MyCompany\Username`.

Selecteer **[!UICONTROL Connect to destination]** als u wilt verifiëren bij het doel.
{het schermschot van 0} Experience Platform UI die toont hoe te voor authentiek te verklaren.![&#128279;](../../assets/catalog/email-marketing/oracle-eloqua-api/authenticate-destination.png)

Als de opgegeven gegevens geldig zijn, geeft de gebruikersinterface de status **[!UICONTROL Connected]** weer met een groen vinkje. Vervolgens kunt u verdergaan met de volgende stap.

### Doelgegevens invullen {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_apioracleeloqua_pod"
>title="Pod"
>abstract="Meld u aan bij Oracle Eloqua om uw podnummer te vinden. Noteer de URL in uw browser nadat u zich hebt aangemeld. "

<!-- >additional-url="https://support.oracle.com/knowledge/Oracle%20Cloud/2307176_1.html" text="Oracle Knowledge base - find out your Pod number" -->

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.
{het schermschot van 0} Experience Platform UI die de bestemmingsdetails toont.![&#128279;](../../assets/catalog/email-marketing/oracle-eloqua-api/destination-details.png)

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Pod]**: Als u wilt weten welke `pod` u bent ingeschakeld, meldt u zich aan bij [!DNL Oracle Eloqua] en noteert u de URL in uw browser nadat u zich hebt aangemeld. Als de URL van uw browser bijvoorbeeld `secure.p01.eloqua.com` is, moet u de waarde `pod` selecteren `p01` . Verwijs naar de [&#x200B; Gather  [!DNL Oracle Eloqua]  geloofsbrieven &#x200B;](#gather-credentials) sectie voor extra begeleiding.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [&#x200B; het intekenen aan bestemmingsalarm gebruikend UI &#x200B;](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. <br> ![&#x200B; Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [&#x200B; activeer profielen en publiek aan het stromen publiek uitvoerbestemmingen &#x200B;](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiek aan deze bestemming.

### Afbeeldingsoverwegingen en voorbeeld {#mapping-considerations-example}

Als u uw publieksgegevens correct vanuit Adobe Experience Platform naar de [!DNL Oracle Eloqua] -bestemming wilt verzenden, moet u de stap voor veldtoewijzing doorlopen. Toewijzing bestaat uit het maken van een koppeling tussen de schemavelden van uw Experience Data Model (XDM) in uw Experience Platform-account en de overeenkomstige equivalenten van de doelbestemming.

Voer de volgende stappen uit om uw XDM-velden toe te wijzen aan de [!DNL Oracle Eloqua] -doelvelden:

1. Selecteer **[!UICONTROL Add new mapping]** in de stap **[!UICONTROL Mapping]** . Er verschijnt een nieuwe toewijzingsrij op het scherm.
1. Kies in het venster **[!UICONTROL Select source field]** de categorie **[!UICONTROL Select attributes]** en selecteer het XDM-kenmerk of kies de categorie **[!UICONTROL Select identity namespace]** en selecteer een identiteit.
1. Kies in het venster **[!UICONTROL Select target field]** de optie **[!UICONTROL Select identity namespace]** en selecteer een identiteit of kies **[!UICONTROL Select custom attributes]** en typ in het veld **[!UICONTROL Attribute name]** de gewenste kenmerknaam. De kenmerknaam die u opgeeft, moet overeenkomen met een bestaand contactkenmerk in [!DNL Oracle Eloqua] . Zie [[!DNL create a contact] &#x200B;](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html) voor de nauwkeurige attributennamen die u in [!DNL Oracle Eloqua] kunt gebruiken.

   * Herhaal deze stappen om de vereiste en gewenste kenmerktoewijzingen toe te voegen tussen uw XDM-profielschema en [!DNL Oracle Eloqua] :

     | Source-veld | Doelveld | Verplicht |
     |---|---|---|
     | `IdentityMap: Eid` | `Identity: EloquaId` | Ja |
     | `xdm: personalEmail.address` | `Attribute: emailAddress` | Ja |
     | `xdm: personName.firstName` | `Attribute: firstName` | |
     | `xdm: personName.lastName` | `Attribute: lastName` | |
     | `xdm: workAddress.street1` | `Attribute: address1` | |
     | `xdm: workAddress.street2` | `Attribute: address2` | |
     | `xdm: workAddress.street3` | `Attribute: address3` | |
     | `xdm: workAddress.postalCode` | `Attribute: postalCode` | |
     | `xdm: workAddress.country` | `Attribute: country` | |
     | `xdm: workAddress.city` | `Attribute: city` | |

   * Hieronder ziet u een voorbeeld met de bovenstaande toewijzingen:

     ![&#x200B; het schermschot van Experience Platform UI met attributenafbeeldingen.](../../assets/catalog/email-marketing/oracle-eloqua-api/mappings.png)

>[!IMPORTANT]
>
>* Attributen die in **[!UICONTROL Target field]** worden gespecificeerd zouden precies zoals die in [[!DNL Create a contact] worden gespecificeerd &#x200B;](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html) moeten worden genoemd aangezien deze attributen verzoeklichaam zullen vormen.
>* Kenmerken die in **[!UICONTROL Source field]** worden opgegeven, volgen een dergelijke beperking niet. U kunt deze toewijzen op basis van uw behoefte, maar als de gegevensindeling niet correct is wanneer u naar [!DNL Oracle Eloqua] wordt geduwd, resulteert dit in een fout. U kunt bijvoorbeeld de naamruimte **[!UICONTROL Source field]** identity `contact key` , `ABC ID` enz. toewijzen. to **[!UICONTROL Target field]** : `EloquaId` zorgt u ervoor dat de id-waarden overeenkomen met de indeling die wordt geaccepteerd door [!DNL Oracle Eloqua] .
>* De toewijzing `EloquaID` is verplicht om kenmerken bij te werken die overeenkomen met de identiteit.
>* De toewijzing `emailAddress` is vereist. Zonder deze API genereert de API een fout zoals hieronder wordt weergegeven:
>
>```json
>{
>     "type":"ObjectValidationError",
>     "container":{
>           "type":"ObjectKey",
>           "objectType":"Contact"
>     },
>     "property":"emailAddress",
>     "requirement":{
>           "type":"EmailAddressRequirement"
>     },
>     "value":"<null>"
>}
>```

Wanneer u klaar bent met het opgeven van de toewijzingen voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

>[!NOTE]
>
>Het doel plaatst automatisch een unieke id achter de geselecteerde publieksnamen bij elke uitvoering wanneer de gegevens van het contactveld naar [!DNL Oracle Eloqua] worden verzonden. Dit zorgt ervoor dat de namen van de contactgebieden die overeenkomen met uw publieksnamen elkaar niet overlappen. Verwijs naar [&#x200B; de uitvoer van gegevens &#x200B;](#exported-data) van het sectiescherm van een [!DNL Oracle Eloqua] pagina van de Details van het Contact met het gebied van het douanecontact dat gebruikend de publieksnamen wordt gecreeerd bevestigen.

## Gegevens exporteren valideren {#exported-data}

Volg onderstaande stappen om te controleren of u de bestemming correct hebt ingesteld:

1. Selecteer **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** en navigeer naar de lijst met doelen.
1. Selecteer vervolgens het doel en schakel over naar het tabblad **[!UICONTROL Activation data]** en selecteer een publieksnaam.
   ![&#x200B; het schermschot van Experience Platform UI die de Gegevens van de Activering van Doelen toont.](../../assets/catalog/email-marketing/oracle-eloqua-api/destinations-activation-data.png)

1. Controleer het publieksoverzicht en zorg ervoor dat de telling van profielen aan de telling binnen het segment beantwoordt.
   ![&#x200B; het schermschot van Experience Platform UI die Segment toont.](../../assets/catalog/email-marketing/oracle-eloqua-api/segment.png)

1. Meld u aan bij de [!DNL Oracle Eloqua] -website en navigeer naar de **[!UICONTROL Contacts Overview]** -pagina om te controleren of de profielen van het publiek zijn toegevoegd. Blader omlaag naar een **[!UICONTROL Contact Detail]** -pagina en controleer of het contactveld met de naam van het geselecteerde publiek als voorvoegsel is gemaakt om de publieksstatus weer te geven.

{het schermschot van 0} Oracle Eloqua UI die de pagina van de Details van het Contact met het gebied van het douanecontract toont dat met de publieksnaam wordt gecreeerd.![&#128279;](../../assets/catalog/email-marketing/oracle-eloqua-api/contact.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, zie het [&#x200B; overzicht van het Beleid van Gegevens &#x200B;](/help/data-governance/home.md).

## Fouten en problemen oplossen {#errors-and-troubleshooting}

Wanneer u het doel maakt, ontvangt u mogelijk een van de volgende foutberichten: `400: There was a validation error` of `400 BAD_REQUEST` . Dit gebeurt wanneer u de 250 grens van de gebieden van het douanecontact overschrijdt, zoals die in de [&#x200B; wordt beschreven guardrails &#x200B;](#guardrails) sectie. U kunt deze fout verhelpen door de limiet van het aangepaste contactveld in [!DNL Oracle Eloqua] niet te overschrijden.
{het schermschot van 0} Experience Platform UI die fout toont.![&#128279;](../../assets/catalog/email-marketing/oracle-eloqua-api/error.png)

Verwijs naar de [[!DNL Oracle Eloqua]  de statuscodes van HTTP &#x200B;](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPStatusCodes.html) en [[!DNL Oracle Eloqua]  fouten van de Bevestiging &#x200B;](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPValidationErrors.html) pagina&#39;s voor een uitvoerige lijst van status en foutencodes met verklaringen.

## Aanvullende bronnen {#additional-resources}

Zie de documentatie van [!DNL Oracle Eloqua] voor meer informatie:

* [&#x200B; Oracle Eloqua Marketing Automation &#x200B;](https://docs.oracle.com/en/cloud/saas/marketing/eloqua.html)
* [&#x200B; REST API voor de Dienst van Marketing Cloud van Oracle Eloqua &#x200B;](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/rest-endpoints.html)

### Changelog

Deze sectie vangt de functionaliteit en de significante documentatieupdates aan deze bestemmingsschakelaar worden aangebracht die.

+++ Wijzigingen weergeven

| Releasedatum | Type bijwerken | Beschrijving |
|---|---|---|
| April 2023 | Documentatie bijgewerkt | <ul><li>Wij hebben de [&#x200B; gebruik-gevallen &#x200B;](#use-cases) sectie met een duidelijker voorbeeld bijgewerkt van wanneer de klanten van het gebruiken van deze bestemming zouden profiteren.</li> <li>Wij hebben de [&#x200B; afbeelding &#x200B;](#mapping-considerations-example) sectie met duidelijke voorbeelden van zowel verplichte als facultatieve afbeeldingen bijgewerkt.</li> <li>Wij hebben [&#x200B; bijgewerkt verbind met de bestemmings &#x200B;](#connect) sectie met een voorbeeld op hoe te om de samengevoegde waarde voor het **[!UICONTROL Username]** gebied te construeren gebruikend de [!DNL Oracle Eloqua] Naam van het Bedrijf en [!DNL Oracle Eloqua] Gebruikersnaam. (PLATIR-28343)</li><li>Wij hebben de  [!DNL Oracle Eloqua]  geloofsbrieven [&#128279;](#gather-credentials) van de Vergroting  bijgewerkt en [&#x200B; vullen in de secties van bestemmingsdetails &#x200B;](#destination-details) met begeleiding op [!DNL Oracle Eloqua] **[!UICONTROL Pod]** selectie. De *&quot;Pod&quot;* waarde wordt gebruikt door de bestemming om de basis URL voor de API vraag te construeren. De [[!DNL Oracle Eloqua]  eerste vereisten &#x200B;](#prerequisites-destination) sectie werd ook bijgewerkt met begeleiding bij het toewijzen van *&quot;Geavanceerde Gebruikers - de toestemmingen van de Marketing&quot;* als vereiste *&quot;Groepen van de Veiligheid&quot;* voor uw [!DNL Oracle Eloqua] instantie.</li></ul> |
| Maart 2023 | Eerste release | Oorspronkelijke doelversie en documentatie publiceren. |

{style="table-layout:auto"}

+++