---
title: Sluit uw PathFactory-account aan op Experience Platform via de gebruikersinterface
description: Leer hoe u uw PathFactory-account met Experience Platform kunt verbinden via de gebruikersinterface.
badge: Beta
exl-id: 859dd0c1-8c4b-43e3-a87b-84c879460bc0
source-git-commit: ca17854830edabaf2bd74265258d6f0096f2888e
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 1%

---

# Verbind uw [!DNL PathFactory] account aan Experience Platform via de gebruikersinterface

Deze zelfstudie bevat stappen voor het tot stand brengen van een verbinding met uw [!DNL PathFactory] Bezoekers, sessies en paginaweergavegegevens naar Adobe Experience Platform via de gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waarbinnen [!DNL Experience Platform] organiseert de gegevens van de klantenervaring.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie Schema-editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe u aangepaste schema&#39;s maakt met de gebruikersinterface van de Schema-editor.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u al een [!DNL PathFactory] account, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie op [het brengen van de gegevens van de marketing automatisering aan Experience Platform gebruikend UI](../../dataflow/marketing-automation.md).

### Vereiste referenties verzamelen {#gather-credentials}

Om tot uw rekening PathFactory op het Platform toegang te hebben, moet u de volgende waarden verstrekken:

| Credentials | Beschrijving |
| ---------- | ----------- |
| Gebruikersnaam | De gebruikersnaam van uw PathFactory-account. Dit is essentieel voor het identificeren van uw account in het systeem. |
| Wachtwoord | Het wachtwoord dat aan uw PathFactory-account is gekoppeld. Zorg ervoor dat dit veilig blijft om ongeoorloofde toegang te voorkomen. |
| Domein | Het domein dat aan uw PathFactory-account is gekoppeld. Dit verwijst typisch naar het unieke herkenningsteken binnen uw PathFactory URL. |
| Toegangstoken | Een uniek token dat wordt gebruikt voor API-verificatie voor veilige communicatie tussen uw systemen en PathFactory. |
| API-eindpunten | Specifieke API-eindpunten voor toegang tot gegevens: Bezoekers, Sessies en Paginaweergaven. Elk eindpunt komt overeen met verschillende gegevenssets die u kunt ophalen. **Opmerking:** Deze worden vooraf gedefinieerd door [!DNL PathFactory] en zijn specifiek voor de gegevens die u wilt gebruiken: <ul><li>**Eindpunt van bezoekers**: `/api/public/v3/data_lake_apis/visitors.json`</li><li>**Sessieeindpunt**: `/api/public/v3/data_lake_apis/sessions.json`</li><li>**Eindpunt van paginaweergaven**: `/api/public/v3/data_lake_apis/page_views.json`</li></ul> |

Voor gedetailleerde begeleiding op hoe te om uw geloofsbrieven te beveiligen en te gebruiken, en voor informatie over het verkrijgen van en het verfrissen van uw toegangstoken, bezoek [Ondersteuningscentrum voor PathFactory](https://support.pathfactory.com/categories/adobe/). Deze bron bevat uitgebreide handleidingen voor het beheer van uw referenties en voor een effectieve en veilige API-integratie.


## Verbind uw [!DNL PathFactory] account

Selecteer in de interface Platform de optie **[!UICONTROL Sources]** van de linkernavigatie om tot [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] Hiermee geeft u diverse bronnen weer die door het Experience Platform worden ondersteund.

U kunt de juiste categorie selecteren in de lijst met categorieën. U kunt de zoekbalk ook gebruiken om te filteren op een bepaalde bron.

Onder de [!UICONTROL Marketing automation] categorie, selecteert u **[!UICONTROL PathFactory]** en selecteer vervolgens **[!UICONTROL Set up]**.

![De broncatalogus met de bron PathFactory geselecteerd.](../../../../images/tutorials/create/pathfactory/catalog.png)

De **[!UICONTROL Connect to PathFactory]** wordt weergegeven. Op deze pagina kunt u een nieuw account maken of een bestaand account gebruiken.

### Nieuwe account

Als u een nieuwe account wilt maken, selecteert u **[!UICONTROL New account]** en geef een naam voor uw account op, een optionele beschrijving en de verificatiegegevens die overeenkomen met uw [!DNL PathFactory] account.

Selecteer **[!UICONTROL Connect to source]** en laat dan wat tijd voor de nieuwe verbinding tot stand brengen.

![De nieuwe accountinterface waar u een nieuwe account voor PathFactory kunt verifiëren.](../../../../images/tutorials/create/pathfactory/new.png)

### Bestaande account

Als u al een bestaande account hebt, selecteert u **[!UICONTROL Existing account]** en selecteer vervolgens de account die u wilt gebruiken in de lijst die wordt weergegeven.

![De bestaande accountinterface waarin u een keuze kunt maken uit een lijst met bestaande PathFactory-accounts.](../../../../images/tutorials/create/pathfactory/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht tussen uw [!DNL PathFactory] account en Experience Platform. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom maken om uw gegevens over marketingautomatisering in Experience Platform te brengen](../../dataflow/marketing-automation.md).
