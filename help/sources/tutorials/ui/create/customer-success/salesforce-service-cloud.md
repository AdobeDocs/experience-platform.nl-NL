---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een Salesforce Service Cloud-bronconnector maken in de gebruikersinterface
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# Een Salesforce Service Cloud-bronconnector maken in de gebruikersinterface

De bronschakelaars in het Platform van de Ervaring van Adobe verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie biedt stappen voor het maken van een Salesforce Service Cloud-bronconnector (hierna &quot;SSC&quot; genoemd) met behulp van de gebruikersinterface van het platform.

## Aan de slag

Voor deze zelfstudie is een goed begrip vereist van de volgende componenten van het Adobe Experience Platform:

* [XDM-systeem](../../../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor het Platform van de Ervaring gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [Klantprofiel](../../../../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u reeds een geldige verbinding SSC hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan bij het [vormen van een dataflow](../../dataflow/customer-success.md)

### Vereiste referenties verzamelen

Als u toegang wilt krijgen tot uw SSC-account op Platform, moet u de volgende waarden opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `username` | De gebruikersnaam voor de gebruikersaccount. |
| `password` | Het wachtwoord voor de gebruikersaccount. |
| `securityToken` | Het beveiligingstoken voor de gebruikersaccount. |

Raadpleeg [dit document](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm)van de Salesforce Service Cloud voor meer informatie over aan de slag gaan.

## Uw Salesforce Service Cloud-account verbinden

Zodra u uw vereiste geloofsbrieven hebt verzameld, kunt u de stappen volgen hieronder om een nieuwe rekening tot stand te brengen SSC om met Platform te verbinden.

Meld u aan bij <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> en selecteer vervolgens **Bronnen** in de linkernavigatiebalk voor toegang tot de werkruimte *Bronnen* . Het scherm van de *Catalogus* toont een verscheidenheid van bronnen waarvoor u binnenkomende rekening kunt tot stand brengen, en elke bron toont het aantal bestaande rekeningen en datasetstromen verbonden aan hen.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer in de categorie *Klantsucces* de optie **Salesforce Service Cloud** om een informatiebalk aan de rechterkant van het scherm weer te geven. De informatiebalk bevat een korte beschrijving van de geselecteerde bron en opties voor het maken van verbinding met de bron of het bekijken van de documentatie. Selecteer **Connect-bron** als u een nieuwe binnenkomende verbinding wilt maken.

![catalogus](../../../../images/tutorials/create/ssc/catalog.png)

De pagina *Verbinding maken met de Salesforce-service Cloud* wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **Nieuw account** als u nieuwe referenties gebruikt. Geef in het invoerformulier dat wordt weergegeven, de verbinding een naam, een optionele beschrijving en uw SSC-referenties. Als u klaar bent, selecteert u **Connect** en laat u de nieuwe account enige tijd beginnen.

![verbinden](../../../../images/tutorials/create/ssc/connect.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de SSC-account waarmee u verbinding wilt maken en selecteert u **Volgende** om door te gaan.

![bestaand](../../../../images/tutorials/create/ssc/existing.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een verbinding met uw SSC-account tot stand gebracht. U kunt nu verdergaan naar de volgende zelfstudie en een gegevensstroom [configureren om de gegevens van Klant met succes over te brengen naar Platform](../../dataflow/customer-success.md).