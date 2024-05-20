---
title: Creeer een Verbinding van de Bron van het Marketo Engage en Dataflow in UI
description: Deze zelfstudie biedt stappen voor het maken van een Marketo Engage-bronverbinding en gegevensstroom in de gebruikersinterface om B2B-gegevens naar Adobe Experience Platform te brengen.
exl-id: a6aa596b-9cfa-491e-86cb-bd948fb561a8
source-git-commit: 744098777141c61ac27fe6f150c05469d5705dee
workflow-type: tm+mt
source-wordcount: '1766'
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

Voor toegang tot uw [!DNL Marketo] account op Experience Platform, moet u de volgende waarden opgeven:

| Credentials | Beschrijving |
| ---- | ---- |
| `munchkinId` | De Munchkin-id is de unieke id voor een specifieke [!DNL Marketo] -instantie. |
| `clientId` | De unieke client-id van uw [!DNL Marketo] -instantie. |
| `clientSecret` | Het unieke clientgeheim van uw [!DNL Marketo] -instantie. |

Voor meer informatie over het verkrijgen van deze waarden raadpleegt u de [[!DNL Marketo] verificatiehandleiding](../../../../connectors/adobe-applications/marketo/marketo-auth.md).

Nadat u de vereiste gegevens hebt verzameld, kunt u de stappen in de volgende sectie volgen.

## Verbind uw [!DNL Marketo] account

Selecteer in de interface Platform de optie **[!UICONTROL Sources]** van de linkernavigatie om tot [!UICONTROL Sources] werkruimte. U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de *Adoben* categorie, selecteert u **[!UICONTROL Marketo Engage]** en selecteer vervolgens **[!UICONTROL Add data]**.

>[!TIP]
>
>De bronnen in de broncatalogus geven de **[!UICONTROL Set up]** als een bepaalde bron nog geen geverifieerde account heeft. Als er eenmaal een geverifieerd account is, wordt deze optie gewijzigd in **[!UICONTROL Add data]**.

![De broncatalogus met het geselecteerde Marketo Engage.](../../../../images/tutorials/create/marketo/catalog.png)

De **[!UICONTROL Connect Marketo Engage account]** wordt weergegeven. Op deze pagina kunt u een nieuw account gebruiken of een bestaand account openen.

>[!BEGINTABS]

>[!TAB Een nieuwe account maken]

Als u een nieuwe account wilt maken, selecteert u **[!UICONTROL New account]** en geef een naam, een optionele beschrijving en uw referenties op.

Selecteer **[!UICONTROL Connect to source]** en laat dan wat tijd voor de nieuwe verbinding tot stand brengen.

![De nieuwe accountinterface voor het verifiëren van een nieuwe Marketo-account.](../../../../images/tutorials/create/marketo/new.png)

>[!TAB Een bestaande account gebruiken]

Als u een bestaande account wilt gebruiken, selecteert u **[!UICONTROL Existing account]** en selecteer vervolgens de account die u wilt gebruiken in de bestaande accountcatalogus.

Selecteren **[!UICONTROL Next]** om verder te gaan.

![De bestaande accountinterface waarin u een bestaande Marketo-account kunt selecteren.](../../../../images/tutorials/create/marketo/existing.png)

>[!ENDTABS]

## Een gegevensset selecteren

Nadat u uw [!DNL Marketo] account, biedt de volgende stap een interface om te verkennen [!DNL Marketo] datasets.

De linkerhelft van de interface is een directorybrowser, die de 10 weergeeft [!DNL Marketo] datasets. Een volledig functionerende [!DNL Marketo] bronverbinding vereist de opname van de negen verschillende datasets. Als u ook de [!DNL Marketo] account-based marketing (ABM) eigenschap, dan moet u ook een tiende gegevensstroom creëren om op te nemen [!UICONTROL Named Accounts] dataset.

>[!NOTE]
>
>Voor beknoptheid wordt de volgende zelfstudie gebruikt [!UICONTROL Opportunities] als voorbeeld, maar de hieronder beschreven stappen zijn van toepassing op om het even welke 10 [!DNL Marketo] datasets.

Selecteer de dataset die u wilt opnemen. Dit werkt de interface bij om een voorproef van uw dataset te tonen. Selecteer **[!UICONTROL Next]**.

![De voorvertoningsinterface](../../../../images/tutorials/create/marketo/preview.png)

## Gegevensset en gegevens over gegevensstroom opgeven {#provide-dataset-and-dataflow-details}

Daarna, moet u informatie over uw dataset en uw gegevensstroom verstrekken.

### Gegevens over gegevensset {#dataset-details}

Een dataset is een opslag en beheersconstructie voor een inzameling van gegevens, typisch een lijst, die een schema (kolommen) en gebieden (rijen) bevat. De gegevens die met succes in Experience Platform worden opgenomen worden opgeslagen binnen het gegevensmeer als datasets. Tijdens deze stap, kunt u een nieuwe dataset tot stand brengen of een bestaande dataset gebruiken.

>[!BEGINTABS]

>[!TAB Een nieuwe gegevensset gebruiken]

Als u een nieuwe gegevensset wilt gebruiken, selecteert u **[!UICONTROL New dataset]** en geef vervolgens een naam en een optionele beschrijving voor uw gegevensset op. U moet ook een schema van het Model van de Gegevens van de Ervaring (XDM) selecteren dat uw dataset volgt aan.

![De nieuwe interface van de datasetselectie.](../../../../images/tutorials/create/marketo/new-dataset.png)

>[!TAB Een bestaande gegevensset gebruiken]

Als u al een bestaande dataset hebt, selecteert u **[!UICONTROL Existing dataset]** en gebruikt vervolgens de **[!UICONTROL Advanced search]** optie om een venster van alle datasets in uw organisatie, met inbegrip van hun respectieve details, zoals te bekijken of zij voor opname aan het Profiel van de Klant in real time of niet worden toegelaten.

![De bestaande interface voor de selectie van gegevenssets.](../../../../images/tutorials/create/marketo/existing-dataset.png)

>[!ENDTABS]

### Dataflow-configuraties {#dataflow-configurations}

>[!IMPORTANT]
>
>De [!DNL Marketo] de bron gebruikt batch-opname om alle historische records in te voeren en gebruikt streaming opname voor realtime updates. Hierdoor kan de bron doorgaan met streamen terwijl onjuiste records worden ingeslikt. De optie **[!UICONTROL Partial ingestion]** schakelen en vervolgens instellen [!UICONTROL Error threshold %] maximaal gebruiken om te voorkomen dat de gegevensstroom mislukt.

Als uw dataset voor het Profiel van de Klant in real time wordt toegelaten, dan tijdens deze stap, kunt u van een knevel voorzien **[!UICONTROL Profile dataset]** om uw gegevens in te schakelen voor profielopname. U kunt deze stap ook gebruiken om **[!UICONTROL Error diagnostics]** en **[!UICONTROL Partial ingestion]**.

* **[!UICONTROL Error diagnostics]**: Select **[!UICONTROL Error diagnostics]** om de bron op te dragen om foutendiagnostiek te veroorzaken die u wanneer het controleren van uw datasetactiviteit en dataflow status kunt later van verwijzingen voorzien.
* **[!UICONTROL Partial ingestion]**: [Gedeeltelijke batch ingestie](../../../../../ingestion/batch-ingestion/partial.md) is de capaciteit om gegevens in te voeren die fouten, tot een bepaalde configureerbare drempel bevatten. Met deze functie kunt u al uw nauwkeurige gegevens in het Experience Platform opnemen, terwijl al uw onjuiste gegevens afzonderlijk worden opgeslagen met informatie over waarom deze niet geldig zijn.

Tijdens deze stap kunt u **[!UICONTROL Sample dataflow]** het beperken van de inname van gegevens en het vermijden van extra kosten die gepaard gaan met het inslikken van alle historische gegevens, met inbegrip van persoonlijke identiteiten.

>[!BEGINSHADEBOX]

**Snelle handleiding voor het gebruik van voorbeeldgegevens**

Gegevensstroom van voorbeeld is een configuratie die u voor uw [!DNL Marketo] gegevensstroom om uw innamesnelheid te beperken en dan de eigenschappen van het Experience Platform uit te proberen zonder het moeten grote hoeveelheden gegevens innemen.

* Schakel voorbeeldgegevensstroom in om historische gegevens te beperken door maximaal 100 k (van de grootste record-id) records op te nemen of tot de laatste 10 dagen van activiteit tijdens de back-uptaak.
* Wanneer het gebruiken van de configuratie van de steekproefgegevens voor alle B2B entiteiten, moet u in overweging nemen dat het mogelijk is dat sommige verwante verslagen kunnen ontbreken omdat de volledige geschiedenis van de brongegevens niet wordt opgenomen.

>[!ENDSHADEBOX]

![De sectie met gegevensstroomconfiguraties van de pagina met gegevensstroomdetails.](../../../../images/tutorials/create/marketo/dataflow-configurations.png)

Bovendien, als u gegevens van de bedrijvendataset opneemt, kunt u toelaten **[!UICONTROL Exclude unclaimed accounts]** om niet-geclaimde accounts uit te sluiten van inname.

Wanneer personen een formulier invullen, [!DNL Marketo] leidt tot een fantoomrekeningsverslag dat op de Naam van het Bedrijf wordt gebaseerd dat geen andere gegevens bevat. Voor nieuwe gegevensstromen, wordt de knevel om niet geclaimde rekeningen uit te sluiten toegelaten door gebrek. Voor bestaande gegevensstromen, kunt u de eigenschap toelaten of onbruikbaar maken, met veranderingen die op nieuw opgenomen gegevens en niet bestaande gegevens van toepassing zijn.

![Niet-geclaimde accounts uitsluiten](../../../../images/tutorials/create/marketo/unclaimed-accounts.png)

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

![De toewijzingsinterface voor Marketo-gegevens.](../../../../images/tutorials/create/marketo/mapping.png)

Als uw toewijzingssets gereed zijn, selecteert u **[!UICONTROL Next]** en kan de nieuwe gegevensstroom enkele ogenblikken maken.

## Controleer uw gegevensstroom

De **[!UICONTROL Review]** wordt weergegeven, zodat u de nieuwe gegevensstroom kunt controleren voordat deze wordt gemaakt. De details worden gegroepeerd in de volgende categorieën:

* **[!UICONTROL Connection]**: Hiermee geeft u het brontype, het relevante pad van de gekozen bronentiteit en de hoeveelheid kolommen in die bronentiteit weer.
* **[!UICONTROL Assign dataset & map fields]**: Toont welke dataset de brongegevens worden opgenomen in, met inbegrip van het schema dat de dataset volgt.

Nadat u de gegevensstroom hebt gecontroleerd, selecteert u **[!UICONTROL Save & ingest]** en laat enige tijd voor de gegevensstroom worden gecreeerd.

![De overzichtspagina waar u details van uw gegevensstroom kunt bevestigen alvorens in te gaan.](../../../../images/tutorials/create/marketo/review.png)

## Uw gegevensstroom controleren

Zodra uw gegevensstroom is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen om informatie over innamepercentages, succes, en fouten te zien. Voor meer informatie over hoe te om dataflows te controleren, zie het leerprogramma op [gegevens controleren in de gebruikersinterface](../../../../../dataflows/ui/monitor-sources.md).

## Uw kenmerken verwijderen

Aangepaste kenmerken in gegevenssets kunnen niet retroactief worden verborgen of verwijderd. Als u een douaneattribuut van een bestaande dataset wilt verbergen of verwijderen, dan moet u een nieuwe dataset zonder dit douaneattribuut, een nieuw schema XDM tot stand brengen, en een nieuwe dataflow voor de nieuwe dataset vormen die u creeert. U moet de originele dataflow ook onbruikbaar maken of schrappen die uit de dataset met de douanekenmerken bestaat u wilt verbergen of verwijderen.

## Uw gegevensstroom verwijderen

U kunt gegevensstromen schrappen die niet meer noodzakelijk of verkeerd gecreeerd gebruikend zijn **[!UICONTROL Delete]** functie beschikbaar in de [!UICONTROL Dataflows] werkruimte. Raadpleeg de zelfstudie voor meer informatie over het verwijderen van gegevensstromen [gegevens verwijderen in de gebruikersinterface](../../delete.md).

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een gegevensstroom gemaakt om B2B-gegevens van uw [!DNL Marketo Engage] bron naar Experience Platform.

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

