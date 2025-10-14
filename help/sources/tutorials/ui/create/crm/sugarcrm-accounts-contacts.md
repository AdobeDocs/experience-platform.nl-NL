---
title: Een SugarCRM-bronverbinding voor accounts en contactpersonen maken in de gebruikersinterface
description: Leer hoe u een SugarCRM-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
exl-id: 45840d7e-4c19-4720-8629-be446347862d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 0%

---

# Een [!DNL SugarCRM Accounts & Contacts] bronverbinding maken in de gebruikersinterface

Deze zelfstudie bevat stappen voor het maken van een [!DNL SugarCRM Accounts & Contacts] -bronverbinding met de Adobe Experience Platform-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem &#x200B;](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   * [&#x200B; Grondbeginselen van schemacompositie &#x200B;](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [&#x200B; het leerprogramma van de Redacteur van het Schema &#x200B;](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u reeds een geldige [!DNL SugarCRM] rekening hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [&#x200B; vormend een dataflow &#x200B;](../../dataflow/crm.md).

### Vereiste referenties verzamelen

Als u [!DNL SugarCRM Accounts & Contacts] wilt verbinden met Experience Platform, moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `Host` | Het SugarCRM API eindpunt de bron verbindt met. | `developer.salesfusion.com` |
| `Username` | Uw gebruikersnaam voor de SugarCRM-ontwikkelaarsaccount. | `abc.def@example.com@sugarmarketdemo000.com` |
| `Password` | Wachtwoord voor uw SugarCRM-ontwikkelaarsaccount. | `123456789` |

### Een Experience Platform-schema maken

Voordat u een [!DNL SugarCRM] -bronverbinding maakt, moet u er ook voor zorgen dat u eerst een Experience Platform-schema voor uw bron maakt. Zie het leerprogramma op [&#x200B; creërend een schema van Experience Platform &#x200B;](../../../../../xdm/schema/composition.md) voor uitvoerige stappen op hoe te om een schema tot stand te brengen.

De [!DNL SugarCRM Accounts & Contacts] ondersteunt meerdere API&#39;s. Dit betekent dat u een afzonderlijk schema moet maken, afhankelijk van het objecttype dat u gebruikt. Zie de voorbeelden hieronder voor zowel rekeningen als contactschema&#39;s:

>[!BEGINTABS]

>[!TAB  Rekeningen ]

{het schermschot van 0} Experience Platform UI die een voorbeeldschema voor Rekeningen ![&#128279;](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarcrm-schema-accounts.png) toont

>[!TAB  Contacten ]

{het schermschot van 0} Experience Platform UI die een voorbeeldschema voor Contacten ![&#128279;](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarcrm-schema-contacts.png) toont

>[!ENDTABS]

## Sluit uw [!DNL SugarCRM Accounts & Contacts] -account aan

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatiebalk voor toegang tot de werkruimte van [!UICONTROL Sources] . In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de *CRM* categorie, selecteer **[!UICONTROL SugarCRM Accounts & Contacts]**, en selecteer dan **[!UICONTROL Add data]**.

![&#x200B; het schermschot van Experience Platform UI voor catalogus met de Rekeningen &amp; de kaart van Contacten SugarCRM &#x200B;](../../../../images/tutorials/create/sugarcrm-accounts-contacts/catalog-sugarcrm-accounts-contacts.png)

De pagina **[!UICONTROL Connect SugarCRM Accounts & Contacts account]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt gebruiken, selecteert u de [!DNL SugarCRM Accounts & Contacts] -account waarmee u een nieuwe gegevensstroom wilt maken en selecteert u vervolgens **[!UICONTROL Next]** om door te gaan.

![&#x200B; het schermschot van Experience Platform voor Connect SugarCRM- Rekeningen &amp; van Contacten rekening met een bestaande rekening &#x200B;](../../../../images/tutorials/create/sugarcrm-accounts-contacts/existing.png)

### Nieuwe account

Als u een nieuwe account maakt, selecteert u **[!UICONTROL New account]** en geeft u een naam, een optionele beschrijving en uw referenties op. Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![&#x200B; het schermschot van Experience Platform voor Connect SugarCRM- Rekeningen &amp; rekening van Contacten met een nieuwe rekening &#x200B;](../../../../images/tutorials/create/sugarcrm-accounts-contacts/new.png)

### Gegevens selecteren

Tot slot moet u het objecttype selecteren dat u aan Experience Platform wilt toevoegen.

| Objecttype | Beschrijving |
| --- | --- |
| `Accounts` | De bedrijven waarmee uw organisatie een relatie heeft. |
| `Contacts` | De individuele mensen met wie uw organisatie een gevestigde verhouding heeft. |

>[!BEGINTABS]

>[!TAB  Rekeningen ]

{het schermschot van 0} Experience Platform UI voor de Rekeningen van SugarCRM &amp; Contacten die configuratie met geselecteerde optie van de Rekening tonen ![&#128279;](../../../../images/tutorials/create/sugarcrm-accounts-contacts/configuration-accounts.png)

>[!TAB  Contacten ]

{het schermschot van 0} Experience Platform UI voor de Rekeningen van SugarCRM &amp; Contacten die configuratie met geselecteerde optie van Contacten tonen ![&#128279;](../../../../images/tutorials/create/sugarcrm-accounts-contacts/configuration-contacts.png)

>[!ENDTABS]

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL SugarCRM Accounts & Contacts] -account. U kunt nu aan het volgende leerprogramma verdergaan en [&#x200B; een dataflow vormen om gegevens in Experience Platform &#x200B;](../../dataflow/crm.md) te brengen.

## Aanvullende bronnen

De onderstaande secties bevatten aanvullende bronnen waarnaar u kunt verwijzen wanneer u de [!DNL SugarCRM] -bron gebruikt.

### Guardrails {#guardrails}

De snelheid van de API van [!DNL SugarCRM] is 90 vraag per minuut of 2000 vraag per dag, welke eerste gebeurt. Deze beperking is echter omzeild door een parameter toe te voegen aan de verbindingsspecificatie die de aanvraagtijd vertraagt zodat de tarieflimiet nooit wordt bereikt.

### Validatie {#validation}

Volg onderstaande stappen om te controleren of u de bron juist hebt ingesteld en of [!DNL SugarCRM Accounts & Contacts] -gegevens worden ingevoerd:

* Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL View Dataflows]** naast het kaartmenu [!DNL SugarCRM Accounts & Contacts] in de catalogus met bronnen. Selecteer vervolgens **[!UICONTROL Preview dataset]** om de gegevens te verifiëren die zijn ingevoerd.

* Afhankelijk van het objecttype waarmee u werkt, kunt u de samengevoegde gegevens vergelijken met de tellingen die op de pagina&#39;s [!DNL SugarMarket] Accounts of Contacts hieronder worden weergegeven:

>[!BEGINTABS]

>[!TAB  Rekeningen ]

![&#x200B; Scherenshot van de pagina van de Rekeningen SugarMarket tonend lijst van rekeningen &#x200B;](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarmarket-accounts.png)

>[!TAB  Contacten ]

![&#x200B; Schermafbeelding van de pagina Contacten SugarMarket die lijst van contacten toont &#x200B;](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarmarket-contacts.png)

>[!ENDTABS]

>[!NOTE]
>
>Op de pagina&#39;s van [!DNL SugarMarket] staan geen aantallen verwijderde objecten. De gegevens die via deze bron worden opgehaald, bevatten echter ook het verwijderde aantal. Deze gegevens worden gemarkeerd met een verwijderde vlag.
