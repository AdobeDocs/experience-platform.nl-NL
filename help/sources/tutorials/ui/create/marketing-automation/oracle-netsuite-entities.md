---
title: Creeer a [!DNL Oracle NetSuite Entities]  bronverbinding in UI
description: Leer hoe u een Oracle NetSuite Entities-bronverbinding maakt met de Adobe Experience Platform-gebruikersinterface.
exl-id: ce0ea37f-16e0-4aef-9809-72c0b11e0440
source-git-commit: 40c3745920204983f5388de6cba1402d87eda71c
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 1%

---

# Een [!DNL Oracle NetSuite Entities] bronverbinding maken in de gebruikersinterface

Lees de volgende zelfstudie om te leren hoe u contactpersonen en klantgegevens van uw [!DNL Oracle NetSuite Entities] -account naar Adobe Experience Platform in de gebruikersinterface kunt brengen.

## Aan de slag {#getting-started}

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u reeds een geldige [!DNL Oracle NetSuite] rekening hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [ vormend een dataflow ](../../dataflow/marketing-automation.md).

>[!TIP]
>
>Lees het [[!DNL Oracle NetSuite]  overzicht ](../../../../connectors/marketing-automation/oracle-netsuite.md) voor informatie over hoe te om uw authentificatiegeloofsbrieven terug te winnen.

## Sluit uw [!DNL Oracle NetSuite Activities] -account aan {#connect-account}

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van [!UICONTROL Sources] . U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de *categorie van de Automatisering van de Marketing*, selecteer **[!DNL Oracle NetSuite Entities]**, en selecteer dan **[!UICONTROL Add data]**.

![ het schermschot van Experience Platform UI voor catalogus met de kaart van de Entiteiten van Oracle NetSuite ](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-entities/catalog-card.png)

De pagina **[!UICONTROL Connect Oracle NetSuite Entities account]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

>[!IMPORTANT]
>
>Het vernieuwingstoken verloopt na zeven dagen. Zodra uw token verlopen, moet u op Experience Platform een account maken met uw bijgewerkte token. Als u geen nieuw account maakt met uw bijgewerkte token, wordt mogelijk het volgende foutbericht weergegeven: `The request could not be processed. Error from flow provider: The request could not be processed. Rest call failed with client error, status code 401 Unauthorized, please check your activity settings.`

### Bestaande account {#existing-account}

Als u een bestaande account wilt gebruiken, selecteert u de [!DNL Oracle NetSuite Entities] -account waarmee u een nieuwe gegevensstroom wilt maken en selecteert u vervolgens **[!UICONTROL Next]** om door te gaan.

![ het schermschot van Experience Platform UI om de rekening van Entiteiten van Oracle NetSuite met een bestaande rekening te verbinden ](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-entities/existing.png)

### Nieuwe account {#new-account}

Als u een nieuwe account maakt, selecteert u **[!UICONTROL New account]** en geeft u een naam, een optionele beschrijving en uw referenties op. Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![ het schermschot van Experience Platform UI om de rekening van Entiteiten van Oracle NetSuite met een nieuwe rekening te verbinden ](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-entities/new.png)

### Gegevens selecteren

Selecteer vervolgens het objecttype dat u aan Experience Platform wilt toevoegen.

| Type entiteit | Beschrijving |
| --- | --- |
| Contact | Haal contactnamen, e-mails, telefoonnummers en eventuele aangepaste contactvelden die aan klanten zijn gekoppeld op. |
| Klant | Haal specifieke klantgegevens op, zoals klantnamen, adressen en toetsidentificatoren. |

>[!BEGINTABS]

>[!TAB  Contact ]

{het schermschot van 0} Experience Platform UI voor de Entiteiten die van Oracle Netsuite configuratie met geselecteerde optie van het Contact tonen ![](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-entities/select-data-contact.png)

>[!TAB  Klant ]

{het schermschot van 0} Experience Platform UI voor de Entiteiten van Oracle Netsuite die configuratie met geselecteerde optie van de Klant tonen ![](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-entities/select-data-customer.png)

>[!ENDTABS]

## Volgende stappen {#next-steps}

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Oracle NetSuite Entities] -account. U kunt nu aan het volgende leerprogramma verdergaan en [ een dataflow vormen om de gegevens van de marketing automatisering in Experience Platform ](../../dataflow/marketing-automation.md) te brengen.

## Aanvullende bronnen {#additional-resources}

De onderstaande secties bevatten aanvullende bronnen waarnaar u kunt verwijzen wanneer u de [!DNL Oracle NetSuite Entities] -bron gebruikt.

### Toewijzing {#mapping}

Experience Platform biedt intelligente aanbevelingen voor automatisch toegewezen velden op basis van het doelschema of de gegevensset die u hebt geselecteerd. U kunt toewijzingsregels handmatig aanpassen aan uw gebruiksgevallen. Op basis van uw behoeften kunt u ervoor kiezen om velden rechtstreeks toe te wijzen of gegevens prep-functies te gebruiken om brongegevens om berekende of berekende waarden af te leiden. Voor uitvoerige stappen bij het gebruiken van de kaartperinterface en berekende gebieden, zie de [ gids UI van de Prep van Gegevens ](../../../../../data-prep/ui/mapping.md).

>[!NOTE]
>
>De weergegeven velden zijn afhankelijk van de abonnementen waartoe uw [!DNL Oracle NetSuite] -account toegang heeft. Als u bijvoorbeeld geen toegang hebt tot facturering, worden de betreffende velden voor facturering niet weergegeven.

### Planning {#scheduling}

Wanneer u de gegevensstroom [!DNL Oracle NetSuite Entities] wilt plannen voor opname, moet u de volgende frequentie- en intervalconfiguratie selecteren:

| Frequentie | Interval |
| --- | --- |
| `Once` | 1 |

Tijdens het ophalen van gegevens reageert [!DNL Oracle NetSuite] met de laatst gewijzigde of gemaakte datum als datumnotatie in plaats van als tijdstempel. De planning is daarom beperkt tot één dag.

Als u de waarden voor uw schema hebt opgegeven, selecteert u **[!UICONTROL Next]** .

![ de het plannen stap van het bronwerkschema.](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-entities/scheduling.png)
