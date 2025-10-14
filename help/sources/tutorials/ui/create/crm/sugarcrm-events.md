---
title: Een SugarCRM-bronverbinding maken in de gebruikersinterface
description: Leer hoe u een SugarCRM-bronverbinding maakt met de Adobe Experience Platform-gebruikersinterface.
exl-id: db346ec0-2c57-4b82-8a39-f15d4cd377d4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---

# Een [!DNL SugarCRM Events] bronverbinding maken in de gebruikersinterface

Deze zelfstudie bevat stappen voor het maken van een [!DNL SugarCRM Events] -bronverbinding met de Adobe Experience Platform-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem &#x200B;](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   * [&#x200B; Grondbeginselen van schemacompositie &#x200B;](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [&#x200B; het leerprogramma van de Redacteur van het Schema &#x200B;](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u reeds een geldige [!DNL SugarCRM] rekening hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [&#x200B; vormend een dataflow &#x200B;](../../dataflow/crm.md).

### Vereiste referenties verzamelen

Als u [!DNL SugarCRM Events] wilt verbinden met Experience Platform, moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `Host` | Het SugarCRM API eindpunt de bron verbindt met. | `developer.salesfusion.com` |
| `Username` | Uw gebruikersnaam voor de SugarCRM-ontwikkelaarsaccount. | `abc.def@example.com@sugarmarketdemo000.com` |
| `Password` | Wachtwoord voor uw SugarCRM-ontwikkelaarsaccount. | `123456789` |

### Experience Platform-schema maken voor [!DNL SugarCRM]

Voordat u een [!DNL SugarCRM] -bronverbinding maakt, moet u er ook voor zorgen dat u eerst een Experience Platform-schema voor uw bron maakt. Zie het leerprogramma op [&#x200B; creërend een schema van Experience Platform &#x200B;](../../../../../xdm/schema/composition.md) voor uitvoerige stappen op hoe te om een schema tot stand te brengen.

{het schermschot van 0} Experience Platform UI die een voorbeeldschema voor de Gebeurtenissen van SugarCRM ![&#128279;](../../../../images/tutorials/create/sugarcrm-events/sugarcrm-schema-events.png) toont

>[!WARNING]
>
>Wanneer u het schema toewijst, moet u ook de verplichte `event_id` - en `timestamp` -velden toewijzen die door Experience Platform worden vereist.

## Sluit uw [!DNL SugarCRM Events] -account aan

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatiebalk voor toegang tot de werkruimte van [!UICONTROL Sources] . In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de *CRM* categorie, selecteer **[!UICONTROL SugarCRM Events]**, en selecteer dan **[!UICONTROL Add data]**.

{het schermschot van 0} Experience Platform UI voor catalogus met de kaart van Gebeurtenissen SugarCRM ![&#128279;](../../../../images/tutorials/create/sugarcrm-events/catalog-sugarcrm-events.png)

De pagina **[!UICONTROL Connect SugarCRM Events account]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt gebruiken, selecteert u de [!DNL SugarCRM Events] -account waarmee u een nieuwe gegevensstroom wilt maken en selecteert u vervolgens **[!UICONTROL Next]** om door te gaan.

![&#x200B; Experience Platform UI het schermschot voor de rekening van Gebeurtenissen Connect SugarCRM met een bestaande rekening &#x200B;](../../../../images/tutorials/create/sugarcrm-events/existing.png)

### Nieuwe account

Als u een nieuwe account maakt, selecteert u **[!UICONTROL New account]** en geeft u een naam, een optionele beschrijving en uw referenties op. Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![&#x200B; het schermschot van Experience Platform UI voor de rekening van Gebeurtenissen Connect SugarCRM met een nieuwe rekening &#x200B;](../../../../images/tutorials/create/sugarcrm-events/new.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL SugarCRM Events] -account. U kunt nu aan het volgende leerprogramma verdergaan en [&#x200B; een dataflow vormen om gegevens in Experience Platform &#x200B;](../../dataflow/crm.md) te brengen.

## Aanvullende bronnen

De onderstaande secties bevatten aanvullende bronnen waarnaar u kunt verwijzen wanneer u de [!DNL SugarCRM] -bron gebruikt.

### Guardrails {#guardrails}

De snelheid van de API van [!DNL SugarCRM] is 90 vraag per minuut of 2000 vraag per dag, welke eerste gebeurt. Deze beperking is echter omzeild door een parameter toe te voegen aan de verbindingsspecificatie die de aanvraagtijd vertraagt zodat de tarieflimiet nooit wordt bereikt.

### Validatie {#validation}

Volg onderstaande stappen om te controleren of u de bron juist hebt ingesteld en of [!DNL SugarCRM Events] -gegevens worden ingevoerd:

* Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL View Dataflows]** naast het kaartmenu [!DNL SugarCRM Events] in de catalogus met bronnen. Selecteer vervolgens **[!UICONTROL Preview dataset]** om de gegevens te verifiëren die zijn ingevoerd.

* Afhankelijk van het objecttype waarmee u werkt, kunt u de samengevoegde gegevens vergelijken met de tellingen die op de onderstaande pagina Gebeurtenissen van [!DNL SugarMarket] worden weergegeven:

![&#x200B; Scherenshot van de pagina van de Rekeningen SugarMarket tonend lijst van rekeningen &#x200B;](../../../../images/tutorials/create/sugarcrm-events/sugarmarket-events.png)

>[!NOTE]
>
>Op de pagina&#39;s van [!DNL SugarMarket] staan geen aantallen verwijderde objecten. De gegevens die via deze bron worden opgehaald, bevatten echter ook het verwijderde aantal. Deze gegevens worden gemarkeerd met een verwijderde vlag.
