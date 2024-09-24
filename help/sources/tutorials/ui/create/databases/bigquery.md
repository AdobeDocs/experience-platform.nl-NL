---
title: Een Google Big Query Source Connection maken in de gebruikersinterface
description: Leer hoe u een Google Big Query-bronverbinding maakt met de Adobe Experience Platform-gebruikersinterface.
badgeUltimate: label="Ultieme" type="Positive"
exl-id: 3c0902de-48b9-42d8-a4bd-0213ca85fc7f
source-git-commit: ae322ee421edd73cd5a3fb8499267cd417491318
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 0%

---

# Een [!DNL Google BigQuery] bronverbinding maken in de gebruikersinterface

>[!IMPORTANT]
>
>De [!DNL Google BigQuery] -bron is in de broncatalogus beschikbaar voor gebruikers die Real-time Customer Data Platform Ultimate hebben aangeschaft.

Lees deze zelfstudie om te leren hoe u uw [!DNL Google BigQuery] -account kunt verbinden met Adobe Experience Platform via de gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u reeds een geldige [!DNL Google BigQuery] verbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [ vormend een dataflow ](../../dataflow/databases.md).

### Vereiste referenties verzamelen

Lees de [[!DNL Google BigQuery]  authentificatiegids ](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials) voor gedetailleerde stappen bij het verzamelen van uw vereiste geloofsbrieven.

## Sluit uw Google BigQuery-account aan

Selecteer in de gebruikersinterface van het platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van [!UICONTROL Sources] . In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken. U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekbalk.

Selecteer onder de categorie [!UICONTROL Databases] de optie **[!UICONTROL Google BigQuery]** en selecteer vervolgens **[!UICONTROL Add data]** .

>[!TIP]
>
>Bronnen in de catalogus met bronnen geven de optie **[!UICONTROL Set up]** weer wanneer een bepaalde bron nog geen geverifieerde account heeft. Zodra een geverifieerd account bestaat, verandert deze optie in **[!UICONTROL Add data]** .

![ de broncatalogus met Google BigQuery selecteerde.](../../../../images/tutorials/create/google-big-query/catalog.png)

De pagina **[!UICONTROL Connect to Google Big Query]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de [!DNL Google BigQuery] -account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![ de bestaande rekeningspagina waar een lijst van bestaande rekeningen wordt voorgesteld.](../../../../images/tutorials/create/google-big-query/existing.png)

### Nieuwe account

Als u een nieuwe account maakt, selecteert u **[!UICONTROL New account]** en geeft u een naam en een optionele beschrijving voor uw nieuwe [!DNL Google BigQuery] -account.

![ de nieuwe rekeningsinterface in het bronwerkschema.](../../../../images/tutorials/create/google-big-query/new.png)

>[!BEGINTABS]

>[!TAB  Basisauthentificatie van het Gebruik ]

Om basisauthentificatie te gebruiken, selecteer **[!UICONTROL Basic Authentication]** en verstrek waarden voor uw [ project, cliënt identiteitskaart, cliëntgeheim, verfrist teken, en (facultatieve) identiteitskaart van de resultaatdataset ](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials). Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat de verbinding enkele ogenblikken tot stand komen.

![ de nieuwe rekeningsinterface waar de basisauthentificatie wordt geselecteerd.](../../../../images/tutorials/create/google-big-query/basic_auth.png)

>[!TAB  de dienstauthentificatie van het Gebruik ]

Om de dienstauthentificatie te gebruiken, selecteer **[!UICONTROL Service Authentication]** en verstrek waarden voor uw [ project identiteitskaart, zeer belangrijke dossierinhoud, en (facultatieve) grote identiteitskaart van de resultaatdataset ](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials). Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat de verbinding enkele ogenblikken tot stand komen.

![ de nieuwe rekeningsinterface waar de dienstauthentificatie wordt geselecteerd.](../../../../images/tutorials/create/google-big-query/service_auth.png)

>[!ENDTABS]

### Voorvertoning van voorbeeldgegevens overslaan {#skip-preview-of-sample-data}

Tijdens de stap voor gegevensselectie kan er een time-out optreden wanneer u grote tabellen of bestanden met gegevens opgeeft. U kunt gegevensvoorvertoning overslaan om de time-out te omzeilen en toch uw schema weer te geven, zij het zonder voorbeeldgegevens. Als u de gegevensvoorvertoning wilt overslaan, schakelt u de schakeloptie **[!UICONTROL Skip previewing sample data]** in.

De rest van de workflow blijft ongewijzigd. Het enige voorbehoud is dat bij het overslaan van de gegevensvoorvertoning berekende en vereiste velden mogelijk niet automatisch worden gevalideerd tijdens de toewijzingsstap. Vervolgens moet u deze velden handmatig valideren tijdens de toewijzing.

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Google BigQuery] -account. U kunt nu aan het volgende leerprogramma verdergaan en [ een dataflow vormen om gegevens in Platform ](../../dataflow/databases.md) te brengen.
