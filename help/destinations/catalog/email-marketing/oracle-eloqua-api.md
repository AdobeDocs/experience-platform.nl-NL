---
title: (API) Oracle Eloqua-verbinding
description: Met de Eloqua-bestemming (API) van het Oracle kunt u uw accountgegevens exporteren en activeren binnen Oracle Eloqua voor uw bedrijfsbehoeften.
last-substantial-update: 2023-03-14T00:00:00Z
source-git-commit: 3197eddcf9fef2870589fdf9f09276a333f30cd1
workflow-type: tm+mt
source-wordcount: '1431'
ht-degree: 0%

---

# [!DNL (API) Oracle Eloqua] verbinding

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) laat marketers toe om campagnes te plannen en uit te voeren terwijl het leveren van een gepersonaliseerde klantenervaring voor hun vooruitzichten. Dankzij geïntegreerd beheer van leads en het eenvoudig maken van campagnes, kunnen marketers op het juiste moment het juiste publiek betrekken bij de reis van hun koper en schalen ze elegant om het publiek te bereiken via verschillende kanalen, zoals e-mail, display, search, video en mobile. Verkoopteams kunnen meer deals sluiten in een sneller tempo, waardoor het marketingrendement toeneemt dankzij realtime inzicht.

Dit [!DNL Adobe Experience Platform] [doel](/help/destinations/home.md) gebruikt de [Een contactpersoon bijwerken](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-id-put.html) van de [!DNL Oracle Eloqua] REST API, waarmee u identiteiten binnen een segment kunt bijwerken naar [!DNL Oracle Eloqua].

[!DNL Oracle Eloqua] gebruik [Basisverificatie](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html) om te communiceren met de [!DNL Oracle Eloqua] REST API. Instructies voor verificatie aan uw [!DNL Oracle Eloqua] de instantie is verder onderaan, in de [Verifiëren voor bestemming](#authenticate) sectie.

## Gebruiksscenario’s {#use-cases}

Als markeerteken kunt u uw gebruikers een persoonlijke ervaring bieden op basis van kenmerken uit hun Adobe Experience Platform-profielen. U kunt segmenten maken van uw offlinegegevens en deze segmenten verzenden naar [!DNL Oracle Eloqua], om in de feeds van de gebruikers weer te geven zodra de segmenten en profielen in Adobe Experience Platform zijn bijgewerkt.

## Vereisten {#prerequisites}

### Voorwaarden voor Experience Platforms {#prerequisites-in-experience-platform}

Voordat u gegevens activeert naar de [!DNL Oracle Eloqua] doel, u moet een [schema](/help/xdm/schema/composition.md), [gegevensset](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), en [segmenten](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) gemaakt in [!DNL Experience Platform].

Raadpleeg de documentatie bij het Experience Platform voor [Segment Membership Details schema groep](/help/xdm/field-groups/profile/segmentation.md) als u begeleiding op segmentstatussen nodig hebt.

### [!DNL Oracle Eloqua] voorwaarden {#prerequisites-destination}

Als u gegevens van Platform wilt exporteren naar uw [!DNL Oracle Eloqua] account die u nodig hebt [!DNL Oracle Eloqua] account.

#### Gather [!DNL Oracle Eloqua] geloofsbrieven {#gather-credentials}

Noteer de onderstaande items voordat u deze verifieert voor de [!DNL Oracle Eloqua] bestemming:

| Credentials | Beschrijving |
| --- | --- |
| `Username` | De gebruikersnaam van uw [!DNL Oracle Eloqua] account. |
| `Password` | Het wachtwoord van uw [!DNL Oracle Eloqua] account. |

## Guardrails {#guardrails}

>[!NOTE]
>
>* [!DNL Oracle Eloqua] aangepaste contactvelden worden automatisch gemaakt met de namen van de segmenten die tijdens de **[!UICONTROL Select segments]** stap.


* [!DNL Oracle Eloqua] heeft een maximale limiet van 250 aangepaste contactvelden.
* Voordat u nieuwe segmenten exporteert, moet u ervoor zorgen dat het aantal segmenten van het Platform en het aantal bestaande segmenten binnen [!DNL Oracle Eloqua] deze limiet niet overschrijden.
* Als deze limiet wordt overschreden, treedt er een fout op in het Experience Platform. Dit komt omdat de [!DNL Oracle Eloqua] API kan de aanvraag niet valideren en reageert met een - *400: Er is een validatiefout opgetreden* - foutbericht met een beschrijving van het probleem.
* Als u de hierboven opgegeven limiet hebt bereikt, moet u bestaande toewijzingen verwijderen uit uw bestemming en de bijbehorende aangepaste contactvelden in uw [!DNL Oracle Eloqua] voordat u meer segmenten kunt exporteren.

* Zie de [Oracle Eloqua maken van contactvelden](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/ContactFields/Tasks/CreatingContactFields.htm) pagina voor informatie over extra limieten.

## Ondersteunde identiteiten {#supported-identities}

[!DNL Oracle Eloqua] ondersteunt het bijwerken van de identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](/help/identity-service/namespaces.md).

| Doelidentiteit | Voorbeeld | Beschrijving | Verplicht |
|---|---|---|---|
| `EloquaId` | `111111` | Unieke id van het contact. | Ja |

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

Within **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** zoeken naar [!DNL (API) Oracle Eloqua]. U kunt de locatie ook onder de **[!UICONTROL Email Marketing]** categorie.

### Verifiëren voor bestemming {#authenticate}

Vul de vereiste velden hieronder in. Zie de [Gather [!DNL Oracle Eloqua] geloofsbrieven](#gather-credentials) voor eventuele richtsnoeren.
* **[!UICONTROL Password]**: Het wachtwoord van uw [!DNL Oracle Eloqua] account.
* **[!UICONTROL Username]**: De gebruikersnaam van uw [!DNL Oracle Eloqua] account.

Om voor authentiek te verklaren aan de bestemming, selecteer **[!UICONTROL Connect to destination]**.
![Het schermschot van het Platform UI die toont hoe te voor authentiek te verklaren.](../../assets/catalog/email-marketing/oracle-eloqua-api/authenticate-destination.png)

Als de verstrekte gegevens geldig zijn, geeft de interface een **[!UICONTROL Connected]** status met een groen vinkje. Vervolgens kunt u verdergaan met de volgende stap.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.
![Het schermschot van het Platform UI die de bestemmingsdetails toont.](../../assets/catalog/email-marketing/oracle-eloqua-api/destination-details.png)

* **[!UICONTROL Name]**: Een naam waarmee u deze bestemming in de toekomst zult erkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over waarschuwingen raadpleegt u de handleiding over [het abonneren aan bestemmingen alarm gebruikend UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Segmenten naar dit doel activeren {#activate}

>[!IMPORTANT]
>
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Lezen [Profielen en segmenten activeren voor streaming segmentexportdoelen](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

### Afbeeldingsoverwegingen en voorbeeld {#mapping-considerations-example}

Als u uw publieksgegevens correct vanuit Adobe Experience Platform naar de [!DNL Oracle Eloqua] doel, moet u door de stap van de gebiedstoewijzing gaan. Toewijzing bestaat uit het maken van een koppeling tussen de schemavelden van uw Experience Data Model (XDM) in uw Platform-account en de bijbehorende equivalenten van de doelbestemming.

`EloquaID` is vereist om kenmerken bij te werken die overeenkomen met de identiteit. De `emailAddress` is ook nodig omdat de API zonder deze fout een fout genereert, zoals hieronder wordt aangegeven:

```json
{
   "type":"ObjectValidationError",
   "container":{
      "type":"ObjectKey",
      "objectType":"Contact"
   },
   "property":"emailAddress",
   "requirement":{
      "type":"EmailAddressRequirement"
   },
   "value":"<null>"
}
```

Kenmerken die zijn opgegeven in het dialoogvenster **[!UICONTROL Target field]** zou precies moeten worden genoemd zoals die in de lijst van de attributenafbeeldingen wordt beschreven aangezien deze attributen verzoeklichaam zullen vormen.

Kenmerken die zijn opgegeven in het dialoogvenster **[!UICONTROL Source field]** zich niet aan een dergelijke beperking houden. U kunt deze toewijzen op basis van uw behoefte, maar als de gegevensindeling niet correct is wanneer u naar [!DNL Oracle Eloqua] resulteert in een fout.

U kunt bijvoorbeeld een toewijzing maken **[!UICONTROL Source field]** naamruimte identity `contact key`, `ABC ID` enz. tot **[!UICONTROL Target field]** : `EloquaID` nadat de id-waarden in overeenstemming zijn met de indeling die is geaccepteerd door [!DNL Oracle Eloqua].

Uw XDM-velden op de juiste wijze toewijzen aan de [!DNL Oracle Eloqua] doelvelden, voer de volgende stappen uit:

1. In de **[!UICONTROL Mapping]** stap, selecteren **[!UICONTROL Add new mapping]**. Er verschijnt een nieuwe toewijzingsrij op het scherm.
1. In de **[!UICONTROL Select source field]** venster, kiest u de **[!UICONTROL Select attributes]** en selecteer het XDM-kenmerk of kies de **[!UICONTROL Select identity namespace]** en selecteer een identiteit.
1. In de **[!UICONTROL Select target field]** venster, kiest u de **[!UICONTROL Select identity namespace]** en selecteer een identiteit of kies **[!UICONTROL Select custom attributes]** en selecteer een kenmerk.
   * Herhaal deze stappen om de volgende toewijzingen tussen uw XDM-profielschema en uw [!DNL Oracle Eloqua] instantie: |Bronveld|Doelveld| Verplicht| |—|—|—| |`xdm: personalEmail.address`|`Attribute: emailAddress`| Ja | |`IdentityMap: Eid`|`Identity: EloquaId`| Ja |

   * Hieronder ziet u een voorbeeld waarin deze toewijzingen worden gebruikt:
      ![Voorbeeld van schermopname met gebruikersinterface van Platform met kenmerktoewijzingen.](../../assets/catalog/email-marketing/oracle-eloqua-api/mappings.png)

      >[!IMPORTANT]
      >
      >Beide `emailAddress` en `EloquaId` toewijzen van doelkenmerken is verplicht.

Wanneer u klaar bent met het opgeven van de toewijzingen voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

>[!NOTE]
>
>De bestemming plaatst automatisch een unieke herkenningsteken aan de geselecteerde segmentnamen op elke uitvoering wanneer het verzenden van de informatie van het contactgebied aan [!DNL Oracle Eloqua]. Dit zorgt ervoor dat de namen van de contactgebieden die overeenkomen met uw segmentnamen elkaar niet overlappen. Zie de [Gegevens exporteren valideren](#exported-data) voorbeeld van een sectiescherm van een [!DNL Oracle Eloqua] De pagina van Details van het contact met het gebied van het douanecontact dat gebruikend de segmentnamen wordt gecreeerd.

## Gegevens exporteren valideren {#exported-data}

Volg onderstaande stappen om te controleren of u de bestemming correct hebt ingesteld:

1. Selecteren **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** en navigeer naar de lijst met bestemmingen.
1. Selecteer vervolgens de bestemming en schakel over naar de **[!UICONTROL Activation data]** selecteert u vervolgens een segmentnaam.
   ![Het het schermschot van het Platform UI die de Gegevens van de Activering van Doelen toont.](../../assets/catalog/email-marketing/oracle-eloqua-api/destinations-activation-data.png)

1. Controleer de samenvatting van het segment en zorg ervoor dat de telling van profielen aan de telling binnen het segment beantwoordt.
   ![Platform UI-screenshot voorbeeld met segment.](../../assets/catalog/email-marketing/oracle-eloqua-api/segment.png)

1. Aanmelden bij de [!DNL Oracle Eloqua] website, navigeer vervolgens naar de **[!UICONTROL Contacts Overview]** pagina om te controleren of de profielen van het segment zijn toegevoegd. Om de segmentstatus te zien, boor neer in een **[!UICONTROL Contact Detail]** pagina en controleer of het contactveld met de naam van het geselecteerde segment als voorvoegsel is gemaakt.

![Schermopname Eloqua UI van het oracle die de pagina van Details van het Contact met het gebied van het douanecontact toont dat met de segmentnaam wordt gecreeerd.](../../assets/catalog/email-marketing/oracle-eloqua-api/contact.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] handhaaft gegevensbeheer, zie [Overzicht van gegevensbeheer](/help/data-governance/home.md).

## Fouten en problemen oplossen {#errors-and-troubleshooting}

Wanneer u het doel maakt, ontvangt u mogelijk een van de volgende foutberichten: `400: There was a validation error` of `400 BAD_REQUEST`. Dit gebeurt wanneer u de limiet van 250 aangepaste contactvelden overschrijdt, zoals wordt beschreven in het dialoogvenster [guardrails](#guardrails) sectie. Als u deze fout wilt corrigeren, moet u ervoor zorgen dat u de limiet van het aangepaste contactveld niet overschrijdt in [!DNL Oracle Eloqua].
![Fout in schermopname van Platform-interface.](../../assets/catalog/email-marketing/oracle-eloqua-api/error.png)

Zie de [[!DNL Oracle Eloqua] HTTP-statuscodes](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPStatusCodes.html) en [[!DNL Oracle Eloqua] Validatiefouten](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPValidationErrors.html) pagina&#39;s voor een uitgebreide lijst met status- en foutcodes met uitleg.

## Aanvullende bronnen {#additional-resources}

Aanvullende nuttige informatie uit de [!DNL Oracle ELoqua] de documentatie is hieronder:
* [Oracle Eloqua Marketing Automation](https://docs.oracle.com/en/cloud/saas/marketing/eloqua.html)
* [REST API voor Oracle Eloqua Marketing Cloud Service](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/rest-endpoints.html)