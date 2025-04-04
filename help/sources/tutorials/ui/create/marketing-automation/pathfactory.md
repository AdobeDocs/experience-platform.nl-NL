---
title: Uw PathFactory-account verbinden met Experience Platform via de gebruikersinterface
description: Leer hoe u uw PathFactory-account via de gebruikersinterface met Experience Platform kunt verbinden.
badge: Beta
exl-id: 859dd0c1-8c4b-43e3-a87b-84c879460bc0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---

# Sluit uw [!DNL PathFactory] -account aan op Experience Platform via de gebruikersinterface

Deze zelfstudie bevat stappen voor het tot stand brengen van een verbinding tussen de gegevens van [!DNL PathFactory] Bezoekers, Sessies en Paginaweergaven en Adobe Experience Platform via de gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u reeds een [!DNL PathFactory] rekening hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan [ brengend de gegevens van de marketing automatisering aan Experience Platform gebruikend UI ](../../dataflow/marketing-automation.md).

### Vereiste referenties verzamelen {#gather-credentials}

U moet de volgende waarden opgeven om toegang te krijgen tot uw PathFactory-account op de Experience Platform:

| Credentials | Beschrijving |
| ---------- | ----------- |
| Gebruikersnaam | De gebruikersnaam van uw PathFactory-account. Dit is essentieel voor het identificeren van uw account in het systeem. |
| Wachtwoord | Het wachtwoord dat aan uw PathFactory-account is gekoppeld. Zorg ervoor dat dit veilig blijft om ongeoorloofde toegang te voorkomen. |
| Domein | Het domein dat aan uw PathFactory-account is gekoppeld. Dit verwijst typisch naar het unieke herkenningsteken binnen uw PathFactory URL. |
| Toegangstoken | Een uniek token dat wordt gebruikt voor API-verificatie voor veilige communicatie tussen uw systemen en PathFactory. |
| API-eindpunten | Specifieke API-eindpunten voor toegang tot gegevens: Bezoekers, Sessies en Paginaweergaven. Elk eindpunt komt overeen met verschillende gegevenssets die u kunt ophalen. **Nota:** deze zijn vooraf bepaald door [!DNL PathFactory] en zijn specifiek voor de gegevens u van plan bent toegang te hebben: <ul><li>**Eindpunt van Bezoekers**: `/api/public/v3/data_lake_apis/visitors.json`</li><li>**Eindpunt van zittingen**: `/api/public/v3/data_lake_apis/sessions.json`</li><li>**Eindpunt van de Mening van de Pagina**: `/api/public/v3/data_lake_apis/page_views.json`</li></ul> |

Voor gedetailleerde begeleiding op hoe te om uw geloofsbrieven te beveiligen en te gebruiken, en voor informatie over het verkrijgen en het verfrissen van uw toegangstoken, bezoek het [ Centrum van de Steun PathFactory ](https://support.pathfactory.com/categories/adobe/). Deze bron bevat uitgebreide handleidingen voor het beheer van uw referenties en voor een effectieve en veilige API-integratie.


## Sluit uw [!DNL PathFactory] -account aan

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van [!UICONTROL Sources] . In [!UICONTROL Catalog] worden diverse bronnen weergegeven die door Experience Platform worden ondersteund.

U kunt de juiste categorie selecteren in de lijst met categorieën. U kunt de zoekbalk ook gebruiken om te filteren op een bepaalde bron.

Selecteer onder de categorie [!UICONTROL Marketing automation] de optie **[!UICONTROL PathFactory]** en selecteer vervolgens **[!UICONTROL Set up]** .

![ de broncatalogus met de geselecteerde bron PathFactory.](../../../../images/tutorials/create/pathfactory/catalog.png)

De pagina **[!UICONTROL Connect to PathFactory]** wordt weergegeven. Op deze pagina kunt u een nieuw account maken of een bestaand account gebruiken.

### Nieuwe account

Als u een nieuwe account wilt maken, selecteert u **[!UICONTROL New account]** en geeft u een naam voor uw account, een optionele beschrijving en de verificatiereferenties die overeenkomen met uw [!DNL PathFactory] -account.

Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![ de nieuwe rekeningsinterface waar u een nieuwe rekening voor PathFactory voor authentiek kunt verklaren.](../../../../images/tutorials/create/pathfactory/new.png)

### Bestaande account

Als u al een bestaande account hebt, selecteert u **[!UICONTROL Existing account]** en selecteert u vervolgens de account die u wilt gebruiken in de lijst die wordt weergegeven.

![ de bestaande rekeningsinterface waar u van een lijst van bestaande rekeningen kunt selecteren PathFactory.](../../../../images/tutorials/create/pathfactory/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht tussen uw [!DNL PathFactory] -account en Experience Platform. U kunt nu aan het volgende leerprogramma verdergaan en [ een dataflow creëren om uw gegevens van de marketing automatisering in Experience Platform ](../../dataflow/marketing-automation.md) te brengen.
