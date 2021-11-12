---
keywords: Experience Platform;home;populaire onderwerpen;Marketo-bronaansluiting;Marketo-aansluiting;Marketo-bron;Marketo
solution: Experience Platform
title: Creeer een Marketo Engage bronschakelaar in UI
topic-legacy: overview
type: Tutorial
description: Deze zelfstudie biedt stappen voor het maken van een Marketo Engage-bronconnector in de UI om B2B-gegevens over te brengen naar Adobe Experience Platform.
exl-id: a6aa596b-9cfa-491e-86cb-bd948fb561a8
source-git-commit: 21617c6ec364fc05d7b8b6d00daa68608d1ed318
workflow-type: tm+mt
source-wordcount: '1272'
ht-degree: 0%

---

# Een [!DNL Marketo Engage] bronschakelaar in UI

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

De **[!UICONTROL Connect to Marketo Engage]** wordt weergegeven. Op deze pagina kunt u een nieuw account gebruiken of een bestaand account openen.

### Nieuwe account

Als u een nieuwe account maakt, selecteert u **[!UICONTROL New account]**. Geef op het invoerformulier dat wordt weergegeven een accountnaam, een optionele beschrijving en uw [!DNL Marketo] verificatiereferenties. Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat dan wat tijd voor de nieuwe verbinding tot stand brengen.

![nieuwe rekening](../../../../images/tutorials/create/marketo/new.png)

### Bestaande account

Als u een gegevensstroom met een bestaande account wilt maken, selecteert u **[!UICONTROL Existing account]** en selecteer vervolgens de [!DNL Marketo] account dat u wilt gebruiken. Selecteren **[!UICONTROL Next]** om verder te gaan.

![bestaand](../../../../images/tutorials/create/marketo/existing.png)

## Een gegevensset selecteren

Nadat u uw [!DNL Marketo] account, biedt de volgende stap een interface om te verkennen [!DNL Marketo] datasets.

De linkerhelft van de interface is een directorybrowser, die de 10 weergeeft [!DNL Marketo] datasets. Een volledig functionerende [!DNL Marketo] bronverbinding vereist de opname van de negen verschillende datasets. Als u ook de [!DNL Marketo] account-based marketing (ABM) eigenschap, dan moet u ook een tiende gegevensstroom creëren om op te nemen [!UICONTROL Named Accounts] dataset.

>[!NOTE]
>
>Voor beknoptheid wordt de volgende zelfstudie gebruikt [!UICONTROL Named Accounts] als voorbeeld, maar de hieronder beschreven stappen zijn van toepassing op om het even welke 10 [!DNL Marketo] datasets.

Selecteer eerst de gegevensset die u wilt invoeren en selecteer vervolgens **[!UICONTROL Next]**.

![select-data](../../../../images/tutorials/create/marketo/select-data.png)

## Kaart [!DNL Marketo] schema&#39;s voor Platform

De [!UICONTROL Mapping] stap verschijnt, die een interface verstrekken om in kaart te brengen [!DNL Marketo] schema&#39;s voor Platform.

Kies een dataset voor binnenkomende gegevens waarin moeten worden opgenomen. U kunt of een bestaande dataset gebruiken of een nieuwe dataset tot stand brengen.

### Een bestaande gegevensset gebruiken

Om gegevens in een bestaande dataset in te voeren, selecteer **[!UICONTROL Existing dataset]** selecteert u vervolgens het pictogram voor de gegevensset.

![bestaande gegevensset](../../../../images/tutorials/create/marketo/existing-dataset.png)

De **[!UICONTROL Select dataset]** wordt weergegeven. Zoek de dataset met het aangewezen schema u wenst te gebruiken, het selecteren, dan selecteren **[!UICONTROL Confirm]**.

![select-existing-dataset](../../../../images/tutorials/create/marketo/select-dataset.png)

### Een nieuwe gegevensset gebruiken

Om gegevens in een nieuwe dataset in te voeren, selecteer **[!UICONTROL New dataset]** en voert een naam en een beschrijving voor de gegevensset in de opgegeven velden in.

U kunt naar een schema zoeken door de naam ervan in te voeren in het dialoogvenster **[!UICONTROL Select schema]** zoekbalk. U kunt ook het vervolgkeuzepictogram selecteren om een lijst met bestaande schema&#39;s weer te geven. U kunt ook **[!UICONTROL Advanced search]** toegang tot pagina&#39;s van bestaande schema&#39;s, met inbegrip van hun respectieve details.

Schakelen tussen **[!UICONTROL Profile dataset]** knoop om uw doeldataset voor toe te laten [!DNL Profile], waarmee u een holistische weergave kunt maken van de kenmerken en het gedrag van een entiteit. Gegevens van alle [!DNL Profile]- de toegelaten datasets zullen in worden omvat [!DNL Profile] en wijzigingen worden toegepast wanneer u de gegevensstroom opslaat.

![create-new-dataset](../../../../images/tutorials/create/marketo/new-dataset-schema.png)

Als u een schema hebt geselecteerd, schuift u omlaag om het toewijzingsdialoogvenster weer te geven en de afbeelding toe te wijzen [!DNL Marketo] datasetgebieden aan hun aangewezen doelXDM gebieden.

### Uw kaart toewijzen [!DNL Marketo] Gegevenssetbronvelden naar doel-XDM-velden

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

Selecteren **[!UICONTROL Preview data]** om toewijzingsresultaten te zien die op uw geselecteerde dataset worden gebaseerd.

![toewijzing](../../../../images/tutorials/create/marketo/mapping.png)

De [!UICONTROL Preview] popover verstrekt u een interface om afbeeldingsresultaten van maximaal 100 rijen steekproefgegevens van de geselecteerde dataset te onderzoeken.

![voorvertoning](../../../../images/tutorials/create/marketo/mapping-preview.png)

Als de bronvelden zijn toegewezen aan de desbetreffende doelvelden, selecteert u **[!UICONTROL Close]**.

## Gegevens over gegevensstroom opgeven

De [!UICONTROL Dataflow detail] wordt weergegeven, zodat u een naam en een korte beschrijving van de nieuwe gegevensstroom kunt opgeven.

![dataFlow-detail](../../../../images/tutorials/create/marketo/dataflow-detail.png)

De optie **[!UICONTROL Error diagnostics]** Schakel deze optie in om het genereren van gedetailleerde foutberichten voor nieuw opgenomen batches mogelijk te maken. Deze kunt u downloaden via de API. Raadpleeg de zelfstudie voor meer informatie [diagnoses voor gegevensinvoer ophalen](../../../../../ingestion/quality/error-diagnostics.md).

![fouten](../../../../images/tutorials/create/marketo/errors.png)

De [!DNL Marketo] de schakelaar gebruikt batch-opname om alle historische verslagen in te voeren en gebruikt het stromen ingestie voor updates in real time. Hierdoor kan de connector doorgaan met streamen terwijl onjuiste records worden ingeslikt. De optie **[!UICONTROL Partial ingestion]** schakelen en vervolgens instellen [!UICONTROL Error threshold %] maximaal gebruiken om te voorkomen dat de gegevensstroom mislukt.

**[!UICONTROL Partial ingestion]** biedt de mogelijkheid om gegevens met fouten tot een bepaalde drempel in te voeren. Zie voor meer informatie de [gedeeltelijke batch-opname, overzicht](../../../../../ingestion/batch-ingestion/partial.md).

Als u de gegevens in de gegevensstroom hebt ingevoerd en de drempel voor een fout op max. hebt ingesteld, selecteert u **[!UICONTROL Next]**.

![gedeeltelijke inname](../../../../images/tutorials/create/marketo/partial-ingestion.png)

## Controleer uw gegevensstroom

De **[!UICONTROL Review]** wordt weergegeven, zodat u de nieuwe gegevensstroom kunt controleren voordat deze wordt gemaakt. De details worden gegroepeerd in de volgende categorieën:

* **[!UICONTROL Connection]**: Toont het brontype, de relevante weg van de gekozen bronentiteit, en de hoeveelheid kolommen binnen die bronentiteit.
* **[!UICONTROL Assign dataset & map fields]**: Toont welke dataset de brongegevens worden opgenomen in, met inbegrip van het schema dat de dataset zich aan houdt.

Nadat u de gegevensstroom hebt gecontroleerd, selecteert u **[!UICONTROL Finish]** en laat enige tijd voor de gegevensstroom worden gecreeerd.

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
