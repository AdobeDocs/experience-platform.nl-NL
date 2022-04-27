---
keywords: Experience Platform;home;populaire onderwerpen;Marketo-bronaansluiting;Marketo-aansluiting;Marketo-bron;Marketo
solution: Experience Platform
title: Creeer een Marketo Engage bronschakelaar in UI
topic-legacy: overview
type: Tutorial
description: Deze zelfstudie biedt stappen voor het maken van een Marketo Engage-bronconnector in de UI om B2B-gegevens over te brengen naar Adobe Experience Platform.
exl-id: a6aa596b-9cfa-491e-86cb-bd948fb561a8
source-git-commit: 8d88af787508f9aeaa7966409b33bf0aae488a87
workflow-type: tm+mt
source-wordcount: '1362'
ht-degree: 0%

---

# Een [!DNL Marketo Engage] bronschakelaar in UI

>[!IMPORTANT]
>
>Voordat u een [!DNL Marketo Engage] bronverbinding en een gegevensstroom, moet u eerst ervoor zorgen dat u hebt [Adobe IMS-organisatie-id is toegewezen](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html?lang=en) in [!DNL Marketo]. Bovendien moet u ervoor zorgen dat u hebt voltooid [automatisch vullen [!DNL Marketo] B2B-naamruimten en -schema&#39;s](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md) voordat u een bronverbinding en een gegevensstroom maakt.

Deze zelfstudie bevat stappen voor het maken van een [!DNL Marketo Engage] (hierna &quot;[!DNL Marketo]&quot;) bronaansluiting in de gebruikersinterface om B2B-gegevens naar Adobe Experience Platform te brengen.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de services van Platforms.
* [Experience Data Model (XDM)](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   * [Schema&#39;s maken en bewerken in de gebruikersinterface](../../../../../xdm/ui/resources/schemas.md): Leer om schema&#39;s in UI tot stand te brengen en uit te geven.
* [Identiteitsnaamruimten](../../../../../identity-service/namespaces.md): Identiteitsnaamruimten zijn een component van [!DNL Identity Service] die dienen als indicatoren van de context waarop een identiteit betrekking heeft. Een volledig gekwalificeerde identiteit omvat een waarde van identiteitskaart en een namespace.
* [[!DNL Real-time Customer Profile]](/help/profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

### Vereiste referenties verzamelen

Om toegang te krijgen tot uw [!DNL Marketo] account op Platform, moet u de volgende waarden opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `munchkinId` | De Munchkin-id is de unieke id voor een specifieke [!DNL Marketo] -instantie. |
| `clientId` | De unieke client-id van uw [!DNL Marketo] -instantie. |
| `clientSecret` | Het unieke clientgeheim van uw [!DNL Marketo] -instantie. |

Voor meer informatie over het verkrijgen van deze waarden raadpleegt u de [[!DNL Marketo] verificatiegids](../../../../connectors/adobe-applications/marketo/marketo-auth.md).

Nadat u de vereiste gegevens hebt verzameld, kunt u de stappen in de volgende sectie volgen.

## Verbind uw [!DNL Marketo] account

Selecteer in de gebruikersinterface van het Platform de optie **[!UICONTROL Sources]** van de linkernavigatiebalk voor toegang tot de [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekbalk.

Onder de [!UICONTROL Adobe applications] categorie, selecteert u **[!UICONTROL Marketo Engage]**. Selecteer vervolgens **[!UICONTROL Add data]** om een nieuwe [!DNL Marketo] dataflow.

![catalogus](../../../../images/tutorials/create/marketo/catalog.png)

De **[!UICONTROL Connect Marketo Engage account]** wordt weergegeven. Op deze pagina kunt u een nieuw account gebruiken of een bestaand account openen.

### Bestaande account

Als u een gegevensstroom met een bestaande account wilt maken, selecteert u **[!UICONTROL Existing account]** en selecteer vervolgens de [!DNL Marketo] account dat u wilt gebruiken. Selecteren **[!UICONTROL Next]** om verder te gaan.

![bestaand](../../../../images/tutorials/create/marketo/existing.png)

### Nieuwe account

Als u een nieuwe account maakt, selecteert u **[!UICONTROL New account]**. Geef op het invoerformulier dat wordt weergegeven een accountnaam, een optionele beschrijving en uw [!DNL Marketo] verificatiereferenties. Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat dan wat tijd voor de nieuwe verbinding tot stand brengen.

![new](../../../../images/tutorials/create/marketo/new.png)

## Een gegevensset selecteren

Nadat u uw [!DNL Marketo] account, biedt de volgende stap een interface om te verkennen [!DNL Marketo] datasets.

De linkerhelft van de interface is een directorybrowser, die de 10 weergeeft [!DNL Marketo] datasets. Een volledig functionerende [!DNL Marketo] bronverbinding vereist de opname van de negen verschillende datasets. Als u ook de [!DNL Marketo] account-based marketing (ABM) eigenschap, dan moet u ook een tiende gegevensstroom creëren om op te nemen [!UICONTROL Named Accounts] dataset.

>[!NOTE]
>
>Voor beknoptheid wordt de volgende zelfstudie gebruikt [!UICONTROL Opportunities] als voorbeeld, maar de hieronder beschreven stappen zijn van toepassing op om het even welke 10 [!DNL Marketo] datasets.

Selecteer eerst de gegevensset die u wilt invoeren en selecteer vervolgens **[!UICONTROL Next]**.

![select-data](../../../../images/tutorials/create/marketo/select-data.png)

## Gegevens over gegevensstroom opgeven

De [!UICONTROL Dataflow detail] De pagina staat u toe om te selecteren of u een bestaande dataset of een nieuwe dataset wilt gebruiken. Tijdens dit proces kunt u ook instellingen configureren voor [!UICONTROL Profile dataset], [!UICONTROL Error diagnostics], [!UICONTROL Partial ingestion], en [!UICONTROL Alerts].

![details gegevensstroom](../../../../images/tutorials/create/marketo/dataflow-details.png)

### Een bestaande gegevensset gebruiken

Om gegevens in een bestaande dataset in te voeren, selecteer **[!UICONTROL Existing dataset]**. U kunt of een bestaande dataset terugwinnen gebruikend [!UICONTROL Advanced search] of door door de lijst van bestaande datasets in het dropdown menu te scrollen. Zodra u een dataset hebt geselecteerd, verstrek een naam en een beschrijving voor uw gegevensstroom.

![bestaande gegevensset](../../../../images/tutorials/create/marketo/existing-dataset.png)

### Een nieuwe gegevensset gebruiken

Om in een nieuwe dataset in te gaan, selecteer **[!UICONTROL New dataset]** en geef vervolgens een naam voor de uitvoergegevensset en een optionele beschrijving op. Selecteer vervolgens het schema waaraan u wilt toewijzen [!UICONTROL Advanced search] of door door de lijst van bestaande schema&#39;s in het dropdown menu te scrollen. Nadat u een schema hebt geselecteerd, geeft u een naam en een beschrijving voor de gegevensstroom op.

![new-dataset](../../../../images/tutorials/create/marketo/new-dataset.png)

### Inschakelen [!DNL Profile] en foutdiagnostiek

Selecteer vervolgens de **[!UICONTROL Profile dataset]** schakelen om uw gegevensset in te schakelen voor [!DNL Profile]. Hierdoor kunt u een holistische weergave maken van de kenmerken en het gedrag van een entiteit. Gegevens van alle [!DNL Profile]- de toegelaten datasets zullen in worden omvat [!DNL Profile] en wijzigingen worden toegepast wanneer u de gegevensstroom opslaat.

[!UICONTROL Error diagnostics] laat gedetailleerde foutenmelding generatie voor om het even welke onjuiste verslagen toe die in uw dataflow voorkomen, terwijl [!UICONTROL Partial ingestion] kunt u gegevens met fouten opnemen tot een bepaalde drempel die u handmatig definieert. Zie de [gedeeltelijke batch-opname, overzicht](../../../../../ingestion/batch-ingestion/partial.md) voor meer informatie .

>[!IMPORTANT]
>
>De [!DNL Marketo] de schakelaar gebruikt batch-opname om alle historische verslagen in te voeren en gebruikt het stromen ingestie voor updates in real time. Hierdoor kan de connector doorgaan met streamen terwijl onjuiste records worden ingeslikt. De optie **[!UICONTROL Partial ingestion]** schakelen en vervolgens instellen [!UICONTROL Error threshold %] maximaal gebruiken om te voorkomen dat de gegevensstroom mislukt.

![met profiel en fouten](../../../../images/tutorials/create/marketo/profile-and-errors.png)

### Waarschuwingen inschakelen

U kunt waarschuwingen inschakelen om meldingen te ontvangen over de status van uw gegevensstroom. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over waarschuwingen raadpleegt u de handleiding over [abonneren op berichten voor bronnen met behulp van de gebruikersinterface](../../alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw gegevensstroom, selecteert u **[!UICONTROL Next]**.

![waarschuwingen](../../../../images/tutorials/create/marketo/alerts.png)

## Uw kaart toewijzen [!DNL Marketo] Gegevenssetbronvelden naar doel-XDM-velden

De [!UICONTROL Mapping] de stap verschijnt, die u van een interface voorziet om de brongebieden van uw bronschema aan hun aangewezen doelXDM gebieden in het doelschema in kaart te brengen.

Elk [!DNL Marketo] dataset heeft zijn eigen specifieke toewijzingsregels om te volgen. Zie het volgende voor meer informatie over hoe u kunt toewijzen [!DNL Marketo] datasets voor XDM:

* [Activiteiten](../../../../connectors/adobe-applications/mapping/marketo.md#activities)
* [Programma&#39;s](../../../../connectors/adobe-applications/mapping/marketo.md#programs)
* [Lidmaatschap van programma](../../../../connectors/adobe-applications/mapping/marketo.md#program-memberships)
* [Bedrijven](../../../../connectors/adobe-applications/mapping/marketo.md#companies)
* [Statische lijsten](../../../../connectors/adobe-applications/mapping/marketo.md#static-lists)
* [Statische lijstlidmaatschap](../../../../connectors/adobe-applications/mapping/marketo.md#static-list-memberships)
* [Benoemde accounts](../../../../connectors/adobe-applications/mapping/marketo.md#named-accounts)
* [Kansen](../../../../connectors/adobe-applications/mapping/marketo.md#opportunities)
* [Contactrollen opportunity](../../../../connectors/adobe-applications/mapping/marketo.md#opportunity-contact-roles)
* [Personen](../../../../connectors/adobe-applications/mapping/marketo.md#persons)

Op basis van uw behoeften kunt u ervoor kiezen om velden rechtstreeks toe te wijzen of gegevens prep-functies te gebruiken om brongegevens om berekende of berekende waarden af te leiden. Voor uitvoerige stappen bij het gebruiken van de kaartinterface, zie [UI-hulplijn voor gegevensvoorinstelling](../../../../../data-prep/ui/mapping.md).

![toewijzing](../../../../images/tutorials/create/marketo/mapping.png)

Als uw toewijzingssets gereed zijn, selecteert u **[!UICONTROL Next]** en kan de nieuwe gegevensstroom even worden gemaakt.

## Controleer uw gegevensstroom

De **[!UICONTROL Review]** wordt weergegeven, zodat u de nieuwe gegevensstroom kunt controleren voordat deze wordt gemaakt. De details worden gegroepeerd in de volgende categorieën:

* **[!UICONTROL Connection]**: Toont het brontype, de relevante weg van de gekozen bronentiteit, en de hoeveelheid kolommen binnen die bronentiteit.
* **[!UICONTROL Assign dataset & map fields]**: Toont welke dataset de brongegevens worden opgenomen in, met inbegrip van het schema dat de dataset zich aan houdt.

Nadat u de gegevensstroom hebt gecontroleerd, selecteert u **[!UICONTROL Save & ingest]** en laat enige tijd voor de gegevensstroom worden gecreeerd.

![revisie](../../../../images/tutorials/create/marketo/review.png)

## Uw gegevensstroom controleren

Zodra uw gegevensstroom is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen om informatie over innamepercentages, succes, en fouten te zien. Voor meer informatie over hoe te om dataflows te controleren, zie het leerprogramma op [gegevens controleren in de gebruikersinterface](../../../../../dataflows/ui/monitor-sources.md).

## Uw kenmerken verwijderen

Aangepaste kenmerken in gegevenssets kunnen niet retroactief worden verborgen of verwijderd. Als u een douaneattribuut van een bestaande dataset wilt verbergen of verwijderen, dan moet u een nieuwe dataset zonder dit douaneattribuut, een nieuw schema XDM tot stand brengen, en een nieuwe dataflow voor de nieuwe dataset vormen die u creeert. U moet de originele dataflow ook onbruikbaar maken of schrappen die uit de dataset met de douaneattributen bestaat u wilt verbergen of verwijderen.

## Uw gegevensstroom verwijderen

U kunt gegevensstromen schrappen die niet meer noodzakelijk of verkeerd gecreeerd gebruikend zijn **[!UICONTROL Delete]** functie beschikbaar in de [!UICONTROL Dataflows] werkruimte. Raadpleeg de zelfstudie voor meer informatie over het verwijderen van gegevensstromen [verwijderen, gegevensstromen in de gebruikersinterface](../../delete.md).

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een gegevensstroom gemaakt die u wilt gebruiken [!DNL Marketo] gegevens. Inkomende gegevens kunnen nu worden gebruikt door downstreamdiensten voor Platforms, zoals [!DNL Real-time Customer Profile] en [!DNL Data Science Workspace]. Raadpleeg de volgende documenten voor meer informatie:

* [[!DNL Real-time Customer Profile] - overzicht](/help/profile/home.md)
* [[!DNL Data Science Workspace] - overzicht](/help/data-science-workspace/home.md)
