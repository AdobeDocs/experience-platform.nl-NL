---
title: Een Zendesk Source Connection maken in de gebruikersinterface
description: Leer hoe u een Zendesk-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
exl-id: 75d303b0-2dcd-4202-987c-fe3400398d90
source-git-commit: 6f8abca8f0db8a559fe62e6c143f2d0506d3b886
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 0%

---

# Een [!DNL Zendesk] bronverbinding maken in de gebruikersinterface

Deze zelfstudie bevat stappen voor het maken van een [!DNL Zendesk] -bronverbinding met de Adobe Experience Platform-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

### Vereiste referenties verzamelen

Als u toegang wilt krijgen tot uw [!DNL Zendesk] -account op Platform, moet u waarden opgeven voor de volgende referenties:

| Credentials | Beschrijving | Voorbeeld |
| --- | --- | --- |
| Subdomein | Het unieke domein dat specifiek is voor uw account dat tijdens het registratieproces is gemaakt. | `yoursubdomain` |
| Toegangstoken | Zendesk API-token. | `0lZnClEvkJSTQ7olGLl7PMhVq99gu26GTbJtf` |

Voor meer informatie bij het voor authentiek verklaren van uw [!DNL Zendesk] bron, zie het [[!DNL Zendesk]  bronoverzicht ](../../../../connectors/customer-success/zendesk.md).

![ het teken van Zendesk API ](../../../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

### Een platformschema maken voor [!DNL Zendesk]

Voordat u een [!DNL Zendesk] -bronverbinding maakt, moet u er ook voor zorgen dat u eerst een Platform-schema maakt dat u voor uw bron kunt gebruiken. Zie het leerprogramma op [ creërend een schema van het Platform ](../../../../../xdm/schema/composition.md) voor uitvoerige stappen op hoe te om een schema tot stand te brengen.

Voor extra begeleiding op uw [!DNL Zendesk] schema dat voor [!DNL Zendesk Search API] wordt vereist, verwijs naar de [ grenzen ](#limits) hieronder sectie.

![ creeer Schema ](../../../../images/tutorials/create/zendesk/schema.png)

## Sluit uw [!DNL Zendesk] -account aan

Selecteer in de gebruikersinterface van het platform **[!UICONTROL Sources]** in de linkernavigatiebalk voor toegang tot de werkruimte van [!UICONTROL Sources] . In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de *categorie van het Succes van de Klant 0} {, selecteer **[!UICONTROL Zendesk]**, en selecteer dan **[!UICONTROL Add data]**.*

![ catalogus ](../../../../images/tutorials/create/zendesk/catalog.png)

De pagina **[!UICONTROL Connect Zendesk account]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Om een bestaande rekening te gebruiken, selecteer *Zendesk* rekening u een nieuwe dataflow met wilt tot stand brengen, dan selecteren **[!UICONTROL Next]** te werk te gaan.

![ bestaand ](../../../../images/tutorials/create/zendesk/existing.png)

### Nieuwe account

Als u een nieuwe account maakt, selecteert u **[!UICONTROL New account]** en geeft u een naam, een optionele beschrijving en uw referenties op. Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![ nieuw ](../../../../images/tutorials/create/zendesk/new.png)

### Gegevens selecteren

Nadat de bron is geverifieerd, wordt de pagina bijgewerkt in een interactieve schemastructuur waarmee u de hiërarchie van uw gegevens kunt verkennen en inspecteren. Selecteer **[!UICONTROL Next]** om door te gaan.

![ selecteren-gegevens ](../../../../images/tutorials/create/zendesk/select-data.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een bronverbinding tussen uw [!DNL Zendesk] -account en Platform geverifieerd en gemaakt. U kunt nu aan het volgende leerprogramma verdergaan en [ een dataflow creëren om de gegevens van het klantensucces in Platform ](../../dataflow/customer-success.md) te brengen.

## Aanvullende bronnen

De onderstaande secties bevatten aanvullende bronnen waarnaar u kunt verwijzen wanneer u de [!DNL Zendesk] -bron gebruikt.

### Validatie {#validation}

In de volgende overzichtsstappen kunt u controleren of u de [!DNL Zendesk] -bron hebt verbonden en of [!DNL Zendesk] -profielen worden opgenomen in Platform.

Selecteer in de gebruikersinterface van het platform de optie **[!UICONTROL Datasets]** in de linkernavigatie voor toegang tot de werkruimte van [!UICONTROL Datasets] . In het scherm [!UICONTROL Dataset Activity] worden de details van uitvoeringen weergegeven.

![ pagina van de Activiteit ](../../../../images/tutorials/create/zendesk/dataset-activity.png)

Vervolgens selecteert u de uitvoerings-id van de gegevensstroom die u wilt weergeven voor specifieke details over de gegevensstroom die wordt uitgevoerd.

![ Dataflow pagina ](../../../../images/tutorials/create/zendesk/dataflow-monitoring.png)

Selecteer ten slotte **[!UICONTROL Preview dataset]** om de gegevens weer te geven die zijn ingevoerd.

![ de dataset van Zendesk ](../../../../images/tutorials/create/zendesk/preview-dataset.png)

U kunt ook de gegevens van het platform controleren op basis van de gegevens op de pagina [!DNL Zendesk] > [!DNL Customers] .

![ zendesk-klanten ](../../../../images/tutorials/create/zendesk/zendesk-customers.png)

### Zendesk-schema

In de onderstaande tabel staan de ondersteunde toewijzingen die moeten worden ingesteld voor Zendesk.

>[!TIP]
>
>Zie [ het Onderzoek API van Zendesk > de Resultaten van het Onderzoek van de Uitvoer ](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) voor meer informatie over API.

| Source | Type |
|---|---|
| `results.active` | Boolean |
| `results.alias` | String |
| `results.created_at` | String |
| `results.custom_role_id` | Geheel |
| `results.default_group_id` | Geheel |
| `results.details` | String |
| `results.email` | String |
| `results.external_id` | Geheel |
| `results.iana_time_zone` | String |
| `results.id` | Geheel |
| `results.last_login_at` | String |
| `results.locale` | String |
| `results.locale_id` | Geheel |
| `results.moderator` | Boolean |
| `results.name` | String |
| `results.notes` | String |
| `results.only_private_comments` | Boolean |
| `results.organization_id` | Geheel |
| `results.phone` | String |
| `results.photo` | String |
| `results.report_csv` | Boolean |
| `results.restricted_agent` | Boolean |
| `results.result_type` | String |
| `results.role` | String |
| `results.role_type` | Geheel |
| `results.shared` | Boolean |
| `results.shared_agent` | Boolean |
| `results.shared_phone_number` | Boolean |
| `results.signature` | String |
| `results.suspended` | Boolean |
| `results.ticket_restriction` | String |
| `results.time_zone` | String |
| `results.two_factor_auth_enabled` | Boolean |
| `results.updated_at` | String |
| `results.url` | String |
| `results.verified` | Boolean |

{style="table-layout:auto"}

### Limieten {#limits}

* Het [ Onderzoek API van Zendesk > de Resultaten van het Onderzoek van de Uitvoer ](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) keert een maximum van 1000 verslagen per pagina terug.
   * De waarde voor de parameter ``filter[type]`` wordt ingesteld op ``user`` en vandaar dat de Zendesk-verbinding alleen gebruikers retourneert.
   * Het aantal resultaten per pagina wordt beheerd door de parameter ``page[size]`` . De waarde wordt ingesteld op ``100`` . Dit wordt gedaan om de impact van de door Zendesk vastgestelde snelheidsbeperkingen te verminderen.
   * Zie [ Beperkingen ](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#limits) en [ Paginering ](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#pagination-1).
   * U kunt ook verwijzen naar [ het Pagineren door lijsten gebruikend curseurpaginering ](https://developer.zendesk.com/documentation/developer-tools/pagination/paginating-through-lists-using-cursor-pagination/).
