---
title: (API) Oracle Eloqua-verbinding
description: Met de Eloqua-bestemming (API) van het Oracle kunt u uw accountgegevens exporteren en activeren binnen Oracle Eloqua voor uw bedrijfsbehoeften.
last-substantial-update: 2023-03-14T00:00:00Z
exl-id: 97ff41a2-2edd-4608-9557-6b28e74c4480
source-git-commit: 8e37ff057ec0fb750bc7b4b6f566f732d9fe5d68
workflow-type: tm+mt
source-wordcount: '2085'
ht-degree: 0%

---


# [!DNL (API) Oracle Eloqua] verbinding

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) laat marketers toe om campagnes te plannen en uit te voeren terwijl het leveren van een gepersonaliseerde klantenervaring voor hun vooruitzichten. Dankzij geïntegreerd beheer van leads en het eenvoudig maken van campagnes, kunnen marketers op het juiste moment het juiste publiek betrekken bij de reis van hun koper en schalen ze elegant om het publiek te bereiken via verschillende kanalen, zoals e-mail, display, search, video en mobile. Verkoopteams kunnen meer deals sluiten in een sneller tempo, waardoor het marketingrendement toeneemt dankzij realtime inzicht.

Dit [!DNL Adobe Experience Platform] [doel](/help/destinations/home.md) gebruikt de [Een contactpersoon bijwerken](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-id-put.html) van de [!DNL Oracle Eloqua] REST API, waarmee u **identiteiten bijwerken** binnen een publiek in [!DNL Oracle Eloqua].

[!DNL Oracle Eloqua] gebruik [Basisverificatie](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html) om te communiceren met [!DNL Oracle Eloqua] REST API. Instructies voor verificatie aan uw [!DNL Oracle Eloqua] de instantie is verder onderaan, in de [Verifiëren voor bestemming](#authenticate) sectie.

## Gebruiksscenario’s {#use-cases}

De marketingafdeling van een onlineplatform wil een marketingcampagne op basis van e-mail uitzenden naar een publiek met nieuwsberichten. Het marketingteam van het platform kan bestaande informatie over leads bijwerken via Adobe Experience Platform, een publiek opbouwen op basis van hun eigen offline gegevens en deze doelgroep naar sturen [!DNL Oracle Eloqua], die vervolgens kan worden gebruikt om de marketingcampagne per e-mail te verzenden.

## Vereisten {#prerequisites}

### Voorwaarden voor Experience Platforms {#prerequisites-in-experience-platform}

Voordat u gegevens activeert naar de [!DNL Oracle Eloqua] doel, u moet een [schema](/help/xdm/schema/composition.md), [gegevensset](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), en [segmenten](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) gemaakt in [!DNL Experience Platform].

Raadpleeg de documentatie bij het Experience Platform voor [Publiek Lidmaatschap Details schema groep](/help/xdm/field-groups/profile/segmentation.md) als u hulp over publieksstatus nodig hebt.

### [!DNL Oracle Eloqua] voorwaarden {#prerequisites-destination}

Als u gegevens van Platform naar uw wilt exporteren [!DNL Oracle Eloqua] account die u nodig hebt [!DNL Oracle Eloqua] account.

Bovendien hebt u minimaal de *&quot;Advanced Users - Marketing permissions&quot;* voor uw [!DNL Oracle Eloqua] -instantie. Zie de *&quot;Beveiligingsgroepen&quot;* de [Beveiligde gebruikerstoegang](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/SecurityOverview/SecuredUserAccess.htm) pagina voor hulp. De toegang wordt vereist door de bestemming programmatically [de basis-URL bepalen](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/DeterminingBaseURL.html) wanneer het aanroepen van [!DNL Oracle Eloqua] API.

#### Gather [!DNL Oracle Eloqua] geloofsbrieven {#gather-credentials}

Noteer de onderstaande items voordat u deze verifieert voor de [!DNL Oracle Eloqua] bestemming:

| Credentials | Beschrijving |
| --- | --- |
| `Company Name` | De bedrijfsnaam die aan uw [!DNL Oracle Eloqua] account. <br>U gebruikt later de `Company Name` en [!DNL Oracle Eloqua] `Username` als een samengevoegde tekenreeks die als de **[!UICONTROL Username]** wanneer [authenticeren aan de bestemming](#authenticate). |
| `Username` | De gebruikersnaam van uw [!DNL Oracle Eloqua] account. |
| `Password` | Het wachtwoord van uw [!DNL Oracle Eloqua] account. |
| `Pod` | [!DNL Oracle Eloqua] ondersteunt meerdere datacenters, elk met een unieke domeinnaam. [!DNL Oracle Eloqua] Deze worden &quot;pods&quot; genoemd. Momenteel zijn er in totaal zeven - p01, p02, p03, p04, p06, p07 en p08. Meld u aan om te bepalen welke POD u hebt ingeschakeld [!DNL Oracle Eloqua] en noteer de URL in uw browser nadat u zich met succes hebt aangemeld. Als de URL van uw browser bijvoorbeeld `secure.p01.eloqua.com` uw `pod` is `p01`. Zie de [de POD bepalen](https://community.oracle.com/topliners/discussion/4470225/determining-your-pod-number-for-oracle-eloqua) pagina voor aanvullende instructies. |

Zie de [Aanmelden bij [!DNL Oracle Eloqua]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/Administration/Tasks/SigningInToEloqua.htm#Signing) ter begeleiding.

## Guardrails {#guardrails}

>[!NOTE]
>
>* [!DNL Oracle Eloqua] aangepaste contactvelden worden automatisch gemaakt met de namen van de doelgroepen die tijdens het **[!UICONTROL Select segments]** stap.

* [!DNL Oracle Eloqua] heeft een maximale limiet van 250 aangepaste contactvelden.
* Voordat u nieuwe doelgroepen exporteert, moet u ervoor zorgen dat het aantal doelgroepen van het platform en het aantal bestaande doelgroepen binnen [!DNL Oracle Eloqua] deze limiet niet overschrijden.
* Als deze limiet wordt overschreden, treedt er een fout op in het Experience Platform. Dit komt omdat de [!DNL Oracle Eloqua] API kan de aanvraag niet valideren en reageert met een - *400: Er is een validatiefout opgetreden* - foutbericht met een beschrijving van het probleem.
* Als u de hierboven opgegeven limiet hebt bereikt, moet u bestaande toewijzingen verwijderen uit uw bestemming en de bijbehorende aangepaste contactvelden in uw [!DNL Oracle Eloqua] voordat u meer segmenten kunt exporteren.

* Zie de [[!DNL Oracle Eloqua] Contactvelden maken](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/ContactFields/Tasks/CreatingContactFields.htm) pagina voor informatie over extra limieten.

## Ondersteunde identiteiten {#supported-identities}

[!DNL Oracle Eloqua] ondersteunt het bijwerken van de identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](/help/identity-service/namespaces.md).

| Doelidentiteit | Beschrijving | Verplicht |
|---|---|---|
| `EloquaId` | Unieke id van het contact. | Ja |

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | <ul><li>U exporteert alle leden van een segment samen met de gewenste schemavelden *(bijvoorbeeld: e-mailadres, telefoonnummer, achternaam)*, op basis van uw veldtoewijzing.</li><li> Voor elk geselecteerd publiek in Platform, het overeenkomstige [!DNL Oracle Eloqua] de segmentstatus wordt bijgewerkt met de publieksstatus van Platform.</li></ul> |
| Exportfrequentie | **[!UICONTROL Streaming]** | <ul><li>Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

Within **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** zoeken naar [!DNL (API) Oracle Eloqua]. U kunt de locatie ook onder de **[!UICONTROL Email Marketing]** categorie.

### Verifiëren voor bestemming {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_apioracleeloqua_companyname_username"
>title="Bedrijfsnaam\Gebruikersnaam"
>abstract="Vul dit gebied met uw bedrijfsnaam en gebruikersbenaming van Oracle Eloqua in de vorm in `{COMPANY_NAME}\{USERNAME}`"

Vul de vereiste velden hieronder in. Zie de [Gather [!DNL Oracle Eloqua] geloofsbrieven](#gather-credentials) voor eventuele richtsnoeren.
* **[!UICONTROL Password]**: Het wachtwoord van uw [!DNL Oracle Eloqua] account.
* **[!UICONTROL Username]**: Een samengevoegde tekenreeks die bestaat uit uw [!DNL Oracle Eloqua] Bedrijfsnaam en de [!DNL Oracle Eloqua] Gebruikersnaam<br>De samengevoegde waarde bestaat uit: `{COMPANY_NAME}\{USERNAME}`.<br> Let op: gebruik geen accolades of spaties en bewaar de `\`. <br>Als u bijvoorbeeld [!DNL Oracle Eloqua] Bedrijfsnaam is `MyCompany` en [!DNL Oracle Eloqua] Gebruikersnaam is `Username`, de samengevoegde waarde die u in het dialoogvenster **[!UICONTROL Username]** field is `MyCompany\Username`.

Om voor authentiek te verklaren aan de bestemming, uitgezocht **[!UICONTROL Connect to destination]**.
![Schermopname van de gebruikersinterface van het platform waarin wordt getoond hoe te voor authentiek te verklaren.](../../assets/catalog/email-marketing/oracle-eloqua-api/authenticate-destination.png)

Als de verstrekte gegevens geldig zijn, geeft de interface een **[!UICONTROL Connected]** status met een groen vinkje. Vervolgens kunt u verdergaan met de volgende stap.

### Doelgegevens invullen {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_apioracleeloqua_pod"
>title="Pod"
>abstract="Meld u aan bij Eloqua Oracle om uw podnummer te vinden. Noteer de URL in uw browser nadat u zich hebt aangemeld. "
>additional-url="https://support.oracle.com/knowledge/Oracle%20Cloud/2307176_1.html" text="Oracle Knowledge Base - ontdek uw podnummer"

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.
![Platform UI het schermschot die de bestemmingsdetails tonen.](../../assets/catalog/email-marketing/oracle-eloqua-api/destination-details.png)

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst wilt herkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Pod]**: te verkrijgen `pod` u bent aan, login aan [!DNL Oracle Eloqua] en noteer de URL in uw browser nadat u zich met succes hebt aangemeld. Als de URL van uw browser bijvoorbeeld `secure.p01.eloqua.com` de `pod` waarde die u moet selecteren, is `p01`. Zie de [Gather [!DNL Oracle Eloqua] geloofsbrieven](#gather-credentials) voor aanvullende richtsnoeren.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.
>* Om te exporteren *identiteiten*, hebt u de **[!UICONTROL View Identity Graph]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). <br> ![Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren."){width="100" zoomable="yes"}

Lezen [Profielen en doelgroepen activeren voor het streamen van doelgroepen voor het exporteren van bestanden](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies voor het activeren van het publiek naar deze bestemming.

### Afbeeldingsoverwegingen en voorbeeld {#mapping-considerations-example}

Als u uw publieksgegevens correct vanuit Adobe Experience Platform naar de [!DNL Oracle Eloqua] doel, moet u door de stap van de gebiedstoewijzing gaan. Toewijzing bestaat uit het maken van een koppeling tussen de schemavelden van uw Experience Data Model (XDM) in uw Platform-account en de bijbehorende equivalenten van de doelbestemming.

Uw XDM-velden toewijzen aan de [!DNL Oracle Eloqua] doelvelden, voer de volgende stappen uit:

1. In de **[!UICONTROL Mapping]** stap, selecteren **[!UICONTROL Add new mapping]**. Er verschijnt een nieuwe toewijzingsrij op het scherm.
1. In de **[!UICONTROL Select source field]** venster, kiest u de **[!UICONTROL Select attributes]** en selecteer het XDM-kenmerk of kies de **[!UICONTROL Select identity namespace]** en selecteer een identiteit.
1. In de **[!UICONTROL Select target field]** venster, kiest u **[!UICONTROL Select identity namespace]** en selecteer een identiteit of kies **[!UICONTROL Select custom attributes]** en typ de gewenste kenmerknaam in het dialoogvenster **[!UICONTROL Attribute name]** veld. De kenmerknaam die u opgeeft, moet overeenkomen met een bestaand contactkenmerk in [!DNL Oracle Eloqua]. Zie [[!DNL create a contact]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html) voor de exacte kenmerknamen die u kunt gebruiken in [!DNL Oracle Eloqua].
   * Herhaal deze stappen om de vereiste en gewenste kenmerktoewijzingen toe te voegen tussen uw XDM-profielschema en [!DNL Oracle Eloqua]: | Bronveld | Doelveld | Verplicht | |—|—|—| |`IdentityMap: Eid`|`Identity: EloquaId`| Ja | |`xdm: personalEmail.address`|`Attribute: emailAddress`| Ja | |`xdm: personName.firstName`|`Attribute: firstName`| | |`xdm: personName.lastName`|`Attribute: lastName`| | |`xdm: workAddress.street1`|`Attribute: address1`| | |`xdm: workAddress.street2`|`Attribute: address2`| | |`xdm: workAddress.street3`|`Attribute: address3`| | |`xdm: workAddress.postalCode`|`Attribute: postalCode`| | |`xdm: workAddress.country`|`Attribute: country`| | |`xdm: workAddress.city`|`Attribute: city`| |

   * Hieronder ziet u een voorbeeld met de bovenstaande toewijzingen:
     ![Voorbeeld van schermopname voor platformgebruikersinterface met kenmerktoewijzingen.](../../assets/catalog/email-marketing/oracle-eloqua-api/mappings.png)

>[!IMPORTANT]
>
>* Kenmerken die zijn opgegeven in het dialoogvenster **[!UICONTROL Target field]** moet een naam hebben die exact overeenkomt met de naam die is opgegeven in het [[!DNL Create a contact]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html) aangezien deze kenmerken de aanvraaginstantie vormen.
>* Kenmerken die zijn opgegeven in het dialoogvenster **[!UICONTROL Source field]** zich niet aan een dergelijke beperking houden. U kunt deze toewijzen op basis van uw behoefte, maar als de gegevensindeling niet correct is wanneer u naar [!DNL Oracle Eloqua] resulteert in een fout. U kunt bijvoorbeeld de **[!UICONTROL Source field]** naamruimte identity `contact key`, `ABC ID` enz. tot **[!UICONTROL Target field]** : `EloquaId` nadat de id-waarden overeenkomen met de indeling die is geaccepteerd door [!DNL Oracle Eloqua].
>* De `EloquaID` toewijzen is verplicht om kenmerken bij te werken die overeenkomen met de identiteit.
>* De `emailAddress` toewijzing is vereist. Zonder deze API genereert de API een fout zoals hieronder wordt weergegeven:
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

Wanneer u klaar bent met het opgeven van de toewijzingen voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

>[!NOTE]
>
>Het doel plaatst automatisch een unieke id achter aan de geselecteerde publieksnamen bij elke uitvoering wanneer het verzenden van de informatie van het contactgebied naar [!DNL Oracle Eloqua]. Dit zorgt ervoor dat de namen van de contactgebieden die overeenkomen met uw publieksnamen elkaar niet overlappen. Zie de [Gegevens exporteren valideren](#exported-data) voorbeeld van een sectiescherm van een [!DNL Oracle Eloqua] De pagina van Details van het contact met het gebied van de douanecontcontact dat gebruikend de publieksnamen wordt gecreeerd.

## Gegevens exporteren valideren {#exported-data}

Volg onderstaande stappen om te controleren of u de bestemming correct hebt ingesteld:

1. Selecteren **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** en navigeer naar de lijst met bestemmingen.
1. Selecteer vervolgens de bestemming en schakel over naar de **[!UICONTROL Activation data]** en selecteert u vervolgens de naam van een publiek.
   ![Het het schermschot van het platform UI die de Gegevens van de Activering van Doelen toont.](../../assets/catalog/email-marketing/oracle-eloqua-api/destinations-activation-data.png)

1. Controleer het publieksoverzicht en zorg ervoor dat de telling van profielen aan de telling binnen het segment beantwoordt.
   ![Voorbeeld van schermopname van platform-UI met segment.](../../assets/catalog/email-marketing/oracle-eloqua-api/segment.png)

1. Aanmelden bij de [!DNL Oracle Eloqua] website, navigeer vervolgens naar de **[!UICONTROL Contacts Overview]** pagina om te controleren of de profielen van het publiek zijn toegevoegd. Als u de status van het publiek wilt zien, gaat u naar een **[!UICONTROL Contact Detail]** pagina en controleer of het contactveld met het geselecteerde publiek als voorvoegsel is gemaakt.

![Schermopname Eloqua UI van het oracle die de pagina van de Details van het Contact met het gebied van het douanecontact toont dat met de publieksnaam wordt gecreeerd.](../../assets/catalog/email-marketing/oracle-eloqua-api/contact.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] handhaaft gegevensbeheer, zie [Overzicht van gegevensbeheer](/help/data-governance/home.md).

## Fouten en problemen oplossen {#errors-and-troubleshooting}

Wanneer u het doel maakt, ontvangt u mogelijk een van de volgende foutberichten: `400: There was a validation error` of `400 BAD_REQUEST`. Dit gebeurt wanneer u de limiet van 250 aangepaste contactvelden overschrijdt, zoals wordt beschreven in het dialoogvenster [guardrails](#guardrails) sectie. Als u deze fout wilt corrigeren, moet u ervoor zorgen dat u de limiet van het aangepaste contactveld niet overschrijdt in [!DNL Oracle Eloqua].
![Fout in schermopname van platforminterface.](../../assets/catalog/email-marketing/oracle-eloqua-api/error.png)

Zie de [[!DNL Oracle Eloqua] HTTP-statuscodes](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPStatusCodes.html) en [[!DNL Oracle Eloqua] Validatiefouten](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPValidationErrors.html) pagina&#39;s voor een uitgebreide lijst met status- en foutcodes met uitleg.

## Aanvullende bronnen {#additional-resources}

Zie voor meer informatie de [!DNL Oracle Eloqua] documentatie:

* [Oracle Eloqua Marketing Automation](https://docs.oracle.com/en/cloud/saas/marketing/eloqua.html)
* [REST API voor Oracle Eloqua Marketing Cloud Service](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/rest-endpoints.html)

### Changelog

Deze sectie vangt de functionaliteit en de significante documentatieupdates aan deze bestemmingsschakelaar worden aangebracht die.

+++ Wijzigingen weergeven

| Releasedatum | Type bijwerken | Beschrijving |
|---|---|---|
| April 2023 | Documentatie bijwerken | <ul><li>We hebben de [gebruikgevallen](#use-cases) een duidelijker voorbeeld van wanneer de klanten van het gebruiken van deze bestemming zouden profiteren.</li> <li>We hebben de [toewijzing](#mapping-considerations-example) met duidelijke voorbeelden van zowel verplichte als optionele toewijzingen.</li> <li>We hebben de [Verbinden met de bestemming](#connect) met een voorbeeld van hoe u de samengevoegde waarde voor de component **[!UICONTROL Username]** veld met de [!DNL Oracle Eloqua] Bedrijfsnaam en de [!DNL Oracle Eloqua] Gebruikersnaam (PLATIR-28343)</li><li>We hebben de [Gather [!DNL Oracle Eloqua] geloofsbrieven](#gather-credentials) en de [Doelgegevens invullen](#destination-details) secties met richtsnoeren over [!DNL Oracle Eloqua] **[!UICONTROL Pod]** selectie. De *&quot;Pod&quot;* De waarde wordt gebruikt door de bestemming om de basis-URL voor de API-aanroepen samen te stellen. De [[!DNL Oracle Eloqua] voorwaarden](#prerequisites-destination) dit gedeelte is ook bijgewerkt met richtlijnen voor het toewijzen van *&quot;Advanced Users - Marketing permissions&quot;* als vereist *&quot;Beveiligingsgroepen&quot;* voor uw [!DNL Oracle Eloqua] -instantie.</li></ul> |
| Maart 2023 | Eerste release | Oorspronkelijke doelversie en documentatie publiceren. |

{style="table-layout:auto"}

+++