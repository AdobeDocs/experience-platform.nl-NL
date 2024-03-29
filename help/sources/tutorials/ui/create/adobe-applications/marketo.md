---
title: Creeer een Verbinding van de Bron van het Marketo Engage en Dataflow in UI
description: Deze zelfstudie biedt stappen voor het maken van een Marketo Engage-bronverbinding en gegevensstroom in de gebruikersinterface om B2B-gegevens naar Adobe Experience Platform te brengen.
exl-id: a6aa596b-9cfa-491e-86cb-bd948fb561a8
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1607'
ht-degree: 0%

---

# Een [!DNL Marketo Engage] bronverbinding en gegevensstroom in de gebruikersinterface

>[!IMPORTANT]
>
>Voordat u een [!DNL Marketo Engage] bronverbinding en een gegevensstroom, moet u eerst ervoor zorgen dat u hebt [aan uw organisatie-id voor Adobe toegewezen](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html) in [!DNL Marketo]. Bovendien moet u ervoor zorgen dat u hebt voltooid [automatisch vullen van uw [!DNL Marketo] B2B-naamruimten en -schema&#39;s](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md) voordat u een bronverbinding en een gegevensstroom maakt.

Deze zelfstudie bevat stappen voor het maken van een [!DNL Marketo Engage] (hierna &quot;[!DNL Marketo]&quot;) bronaansluiting in de gebruikersinterface om B2B-gegevens naar Adobe Experience Platform te brengen.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [B2B-naamruimten en hulpprogramma voor automatisch genereren van schema&#39;s](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md): Het B2B-hulpprogramma voor naamruimten en automatisch genereren van schema maakt het mogelijk om [!DNL Postman] om automatisch waarden te genereren voor uw B2B-naamruimten en -schema&#39;s. U moet eerst uw B2B-naamruimten en -schema&#39;s voltooien voordat u een [!DNL Marketo] bronverbinding en gegevensstroom.
* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de platformservices.
* [Experience Data Model (XDM)](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor Experience Platform gegevens van de klantenervaring organiseert.
   * [Schema&#39;s maken en bewerken in de gebruikersinterface](../../../../../xdm/ui/resources/schemas.md): Leer om schema&#39;s in UI tot stand te brengen en uit te geven.
* [Identiteitsnaamruimten](../../../../../identity-service/features/namespaces.md): Identiteitsnaamruimten zijn een component van [!DNL Identity Service] die dienen als indicatoren van de context waarop een identiteit betrekking heeft. Een volledig gekwalificeerde identiteit omvat een waarde van identiteitskaart en een namespace.
* [[!DNL Real-Time Customer Profile]](/help/profile/home.md): Biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één platforminstantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

### Vereiste referenties verzamelen

Voor toegang tot uw [!DNL Marketo] account op Platform, moet u de volgende waarden opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `munchkinId` | De Munchkin-id is de unieke id voor een specifieke [!DNL Marketo] -instantie. |
| `clientId` | De unieke client-id van uw [!DNL Marketo] -instantie. |
| `clientSecret` | Het unieke clientgeheim van uw [!DNL Marketo] -instantie. |

Voor meer informatie over het verkrijgen van deze waarden raadpleegt u de [[!DNL Marketo] verificatiehandleiding](../../../../connectors/adobe-applications/marketo/marketo-auth.md).

Nadat u de vereiste gegevens hebt verzameld, kunt u de stappen in de volgende sectie volgen.

## Verbind uw [!DNL Marketo] account

Selecteer in de interface Platform de optie **[!UICONTROL Sources]** van de linkernavigatiebalk voor toegang tot de [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekbalk.

Onder de [!UICONTROL Adobe applications] categorie, selecteert u **[!UICONTROL Marketo Engage]**. Selecteer vervolgens **[!UICONTROL Add data]** om een nieuwe [!DNL Marketo] dataflow.

![catalogus](../../../../images/tutorials/create/marketo/catalog.png)

De **[!UICONTROL Connect Marketo Engage account]** wordt weergegeven. Op deze pagina kunt u een nieuw account gebruiken of een bestaand account openen.

### Bestaande account

Als u een gegevensstroom met een bestaande account wilt maken, selecteert u **[!UICONTROL Existing account]** en selecteert u vervolgens de [!DNL Marketo] account dat u wilt gebruiken. Selecteren **[!UICONTROL Next]** om verder te gaan.

![bestaand](../../../../images/tutorials/create/marketo/existing.png)

### Nieuwe account

Als u een nieuwe account maakt, selecteert u **[!UICONTROL New account]**. Geef op het invoerformulier dat wordt weergegeven een accountnaam, een optionele beschrijving en uw [!DNL Marketo] verificatiegegevens. Selecteer **[!UICONTROL Connect to source]** en laat dan wat tijd voor de nieuwe verbinding tot stand brengen.

![new](../../../../images/tutorials/create/marketo/new.png)

## Een gegevensset selecteren

Nadat u uw [!DNL Marketo] account, biedt de volgende stap een interface om te verkennen [!DNL Marketo] datasets.

De linkerhelft van de interface is een directorybrowser, die de 10 weergeeft [!DNL Marketo] datasets. Een volledig functionerende [!DNL Marketo] bronverbinding vereist de opname van de negen verschillende datasets. Als u ook de [!DNL Marketo] account-based marketing (ABM) eigenschap, dan moet u ook een tiende gegevensstroom creëren om op te nemen [!UICONTROL Named Accounts] dataset.

>[!NOTE]
>
>Voor beknoptheid wordt de volgende zelfstudie gebruikt [!UICONTROL Opportunities] als voorbeeld, maar de hieronder beschreven stappen zijn van toepassing op om het even welke 10 [!DNL Marketo] datasets.

Selecteer eerst de gegevensset die u wilt invoeren en selecteer vervolgens **[!UICONTROL Next]**.

![select-data](../../../../images/tutorials/create/marketo/select-data.png)

## Gegevens over gegevensstroom opgeven {#provide-dataflow-details}

De [!UICONTROL Dataflow detail] De pagina staat u toe om te selecteren of u een bestaande dataset of een nieuwe dataset wilt gebruiken. Tijdens dit proces kunt u ook instellingen configureren voor [!UICONTROL Profile dataset], [!UICONTROL Error diagnostics], [!UICONTROL Partial ingestion], en [!UICONTROL Alerts].

![details gegevensstroom](../../../../images/tutorials/create/marketo/dataflow-details.png)

>[!BEGINTABS]

>[!TAB Een bestaande gegevensset gebruiken]

Om gegevens in een bestaande dataset in te voeren, selecteer **[!UICONTROL Existing dataset]**. U kunt of een bestaande dataset terugwinnen gebruikend [!UICONTROL Advanced search] of door door de lijst van bestaande datasets in het dropdown menu te scrollen. Zodra u een dataset hebt geselecteerd, verstrek een naam en een beschrijving voor uw gegevensstroom.

![bestaande gegevensset](../../../../images/tutorials/create/marketo/existing-dataset.png)

>[!TAB Een nieuwe gegevensset gebruiken]

Om in een nieuwe dataset in te gaan, selecteer **[!UICONTROL New dataset]** en geef vervolgens een naam voor de uitvoergegevensset en een optionele beschrijving op. Selecteer vervolgens het schema waaraan u wilt toewijzen [!UICONTROL Advanced search] of door door de lijst van bestaande schema&#39;s in het dropdown menu te scrollen. Nadat u een schema hebt geselecteerd, geeft u een naam en een beschrijving voor de gegevensstroom op.

![new-dataset](../../../../images/tutorials/create/marketo/new-dataset.png)

>[!ENDTABS]

### Inschakelen [!DNL Profile] en foutdiagnose

Selecteer vervolgens de **[!UICONTROL Profile dataset]** schakelen om uw gegevensset in te schakelen voor [!DNL Profile]. Hierdoor kunt u een holistische weergave maken van de kenmerken en het gedrag van een entiteit. Gegevens van alle [!DNL Profile]- de toegelaten datasets zullen in worden omvat [!DNL Profile] en wijzigingen worden toegepast wanneer u de gegevensstroom opslaat.

[!UICONTROL Error diagnostics] laat gedetailleerde foutenmelding generatie voor om het even welke onjuiste verslagen toe die in uw dataflow voorkomen, terwijl [!UICONTROL Partial ingestion] kunt u gegevens met fouten opnemen tot een bepaalde drempel die u handmatig definieert. Zie de [gedeeltelijke batch-opname, overzicht](../../../../../ingestion/batch-ingestion/partial.md) voor meer informatie .

>[!IMPORTANT]
>
>De [!DNL Marketo] de bron gebruikt batch-opname om alle historische records in te voeren en gebruikt streaming opname voor realtime updates. Hierdoor kan de bron doorgaan met streamen terwijl onjuiste records worden ingeslikt. De optie **[!UICONTROL Partial ingestion]** schakelen en vervolgens instellen [!UICONTROL Error threshold %] maximaal gebruiken om te voorkomen dat de gegevensstroom mislukt.

![profiel-en-fouten](../../../../images/tutorials/create/marketo/profile-and-errors.png)

### Waarschuwingen inschakelen

U kunt waarschuwingen inschakelen om meldingen te ontvangen over de status van uw gegevensstroom. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op berichten voor bronnen met behulp van de gebruikersinterface](../../alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw gegevensstroom, selecteert u **[!UICONTROL Next]**.

![waarschuwingen](../../../../images/tutorials/create/marketo/alerts.png)

### Niet-geclaimde accounts overslaan bij het invoeren van bedrijfsgegevens

Wanneer het creëren van een dataflow om gegevens van de bedrijfsdataset in te voeren, kunt u vormen [!UICONTROL Exclude unclaimed accounts] om niet-geclaimde accounts uit te sluiten of op te nemen.

Wanneer personen een formulier invullen, [!DNL Marketo] leidt tot een fantoomrekeningsverslag dat op de Naam van het Bedrijf wordt gebaseerd dat geen andere gegevens bevat. Voor nieuwe gegevensstromen, wordt de knevel om niet geclaimde rekeningen uit te sluiten toegelaten door gebrek. Voor bestaande gegevensstromen, kunt u de eigenschap toelaten of onbruikbaar maken, met veranderingen die op nieuw opgenomen gegevens en niet bestaande gegevens van toepassing zijn.

![niet-opgevraagde rekeningen](../../../../images/tutorials/create/marketo/unclaimed-accounts.png)

## Uw kaart toewijzen [!DNL Marketo] Gegevenssetbronvelden naar doel-XDM-velden

De [!UICONTROL Mapping] de stap verschijnt, die u van een interface voorziet om de brongebieden van uw bronschema aan hun aangewezen doelXDM gebieden in het doelschema in kaart te brengen.

Elk [!DNL Marketo] dataset heeft zijn eigen specifieke toewijzingsregels om te volgen. Zie het volgende voor meer informatie over hoe u kunt toewijzen [!DNL Marketo] datasets voor XDM:

* [Activiteiten](../../../../connectors/adobe-applications/mapping/marketo.md#activities)
* [Programma&#39;s](../../../../connectors/adobe-applications/mapping/marketo.md#programs)
* [Lidmaatschap van programma](../../../../connectors/adobe-applications/mapping/marketo.md#program-memberships)
* [Bedrijven](../../../../connectors/adobe-applications/mapping/marketo.md#companies)
* [Statische lijsten](../../../../connectors/adobe-applications/mapping/marketo.md#static-lists)
* [Statische lijstlidmaatschappen](../../../../connectors/adobe-applications/mapping/marketo.md#static-list-memberships)
* [Benoemde accounts](../../../../connectors/adobe-applications/mapping/marketo.md#named-accounts)
* [Kansen](../../../../connectors/adobe-applications/mapping/marketo.md#opportunities)
* [Contactrollen opportunity](../../../../connectors/adobe-applications/mapping/marketo.md#opportunity-contact-roles)
* [Personen](../../../../connectors/adobe-applications/mapping/marketo.md#persons)

Op basis van uw behoeften kunt u ervoor kiezen om velden rechtstreeks toe te wijzen of gegevens prep-functies te gebruiken om brongegevens om berekende of berekende waarden af te leiden. Voor uitvoerige stappen bij het gebruiken van de kaartinterface, zie [UI-hulplijn voor gegevensvoorinstelling](../../../../../data-prep/ui/mapping.md).

![toewijzing](../../../../images/tutorials/create/marketo/mapping.png)

Als uw toewijzingssets gereed zijn, selecteert u **[!UICONTROL Next]** en kan de nieuwe gegevensstroom enkele ogenblikken maken.

## Controleer uw gegevensstroom

De **[!UICONTROL Review]** wordt weergegeven, zodat u de nieuwe gegevensstroom kunt controleren voordat deze wordt gemaakt. De details worden gegroepeerd in de volgende categorieën:

* **[!UICONTROL Connection]**: Hiermee geeft u het brontype, het relevante pad van de gekozen bronentiteit en de hoeveelheid kolommen in die bronentiteit weer.
* **[!UICONTROL Assign dataset & map fields]**: Toont welke dataset de brongegevens worden opgenomen in, met inbegrip van het schema dat de dataset volgt.

Nadat u de gegevensstroom hebt gecontroleerd, selecteert u **[!UICONTROL Save & ingest]** en laat enige tijd voor de gegevensstroom worden gecreeerd.

![revisie](../../../../images/tutorials/create/marketo/review.png)

## Uw gegevensstroom controleren

Zodra uw gegevensstroom is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen om informatie over innamepercentages, succes, en fouten te zien. Voor meer informatie over hoe te om dataflows te controleren, zie het leerprogramma op [gegevens controleren in de gebruikersinterface](../../../../../dataflows/ui/monitor-sources.md).

## Uw kenmerken verwijderen

Aangepaste kenmerken in gegevenssets kunnen niet retroactief worden verborgen of verwijderd. Als u een douaneattribuut van een bestaande dataset wilt verbergen of verwijderen, dan moet u een nieuwe dataset zonder dit douaneattribuut, een nieuw schema XDM tot stand brengen, en een nieuwe dataflow voor de nieuwe dataset vormen die u creeert. U moet de originele dataflow ook onbruikbaar maken of schrappen die uit de dataset met de douanekenmerken bestaat u wilt verbergen of verwijderen.

## Uw gegevensstroom verwijderen

U kunt gegevensstromen schrappen die niet meer noodzakelijk of verkeerd gecreeerd gebruikend zijn **[!UICONTROL Delete]** functie beschikbaar in de [!UICONTROL Dataflows] werkruimte. Raadpleeg de zelfstudie voor meer informatie over het verwijderen van gegevensstromen [gegevens verwijderen in de gebruikersinterface](../../delete.md).

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een gegevensstroom gemaakt die u wilt gebruiken [!DNL Marketo] gegevens. Inkomende gegevens kunnen nu worden gebruikt door downstreamplatformdiensten zoals [!DNL Real-Time Customer Profile] en [!DNL Data Science Workspace]. Raadpleeg de volgende documenten voor meer informatie:

* [[!DNL Real-Time Customer Profile]-overzicht](/help/profile/home.md)
* [[!DNL Data Science Workspace]-overzicht](/help/data-science-workspace/home.md)

## Bijlage {#appendix}

De volgende secties bevatten aanvullende richtlijnen die u kunt volgen bij het gebruik van de [!DNL Marketo] bron.

### Foutberichten in de gebruikersinterface {#error-messages}

De volgende foutberichten worden weergegeven in de gebruikersinterface wanneer Platform problemen detecteert met uw installatie:

#### [!DNL Munchkin ID] is niet toegewezen aan de desbetreffende organisatie

Verificatie wordt geweigerd als uw [!DNL Munchkin ID] wordt niet toegewezen aan de organisatie van het Platform die u gebruikt. Vorm de afbeelding tussen uw [!DNL Munchkin ID] en uw organisatie die [[!DNL Marketo] interface](https://app-sjint.marketo.com/#MM0A1).

![Een foutbericht met de mededeling dat de Marketo-instantie niet correct is toegewezen aan de Adobe organisatie.](../../../../images/tutorials/create/marketo/munchkin-not-mapped.png)

#### Primaire identiteit ontbreekt

Een dataflow kan niet worden opgeslagen en opgenomen als een primaire identiteit ontbreekt. Zorg ervoor dat [er bestaat een primaire identiteit binnen uw XDM-schema](../../../../../xdm/tutorials/create-schema-ui.md), voordat u probeert een gegevensstroom te configureren.

![Een foutbericht waarin wordt aangegeven dat de primaire identiteit ontbreekt in het XDM-schema.](../../../../images/tutorials/create/marketo/no-primary-identity.png)

