---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creeer een ServiceNow bronschakelaar in UI
topic: overview
translation-type: tm+mt
source-git-commit: cada7c7eff7597015caa7333559bef16a59eab65
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 0%

---


# Creeer een ServiceNow bronschakelaar in UI

>[!NOTE]
>De aansluiting ServiceNow is in bèta. Zie het [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om extern gesourceerde gegevens op een geplande basis in te voeren. Deze zelfstudie biedt stappen voor het maken van een ServiceNow-bronconnector met behulp van de gebruikersinterface van het Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Adobe Experience Platform:

* [XDM-systeem](../../../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [Klantprofiel](../../../../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u reeds een verbinding ServiceNow hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan bij het [vormen van een dataflow](../../dataflow/customer-success.md)

### Vereiste referenties verzamelen

Om tot uw rekening ServiceNow op Platform toegang te hebben, moet u de volgende waarden verstrekken:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `endpoint` | Het eindpunt van de server ServiceNow. |
| `username` | De gebruikersnaam die wordt gebruikt om verbinding te maken met de ServiceNow-server voor verificatie. |
| `password` | Het wachtwoord om met de server te verbinden ServiceNow voor authentificatie. |

Voor meer informatie over begonnen worden, verwijs naar [dit document](https://developer.servicenow.com/app.do#!/rest_api_doc?v=newyork&amp;id=r_TableAPI-GET)ServiceNow.

## Sluit uw ServiceNow-account aan

Zodra u uw vereiste geloofsbrieven hebt verzameld, kunt u de stappen volgen hieronder om een nieuwe rekening te creëren ServiceNow om met Platform te verbinden.

Login aan <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> en selecteer dan **Bronnen** van de linkernavigatiebar om tot de werkruimte van *Bronnen* toegang te hebben. Het scherm van de *Catalogus* toont een verscheidenheid van bronnen waarvoor u een rekening kunt tot stand brengen, en elke bron toont het aantal bestaande rekeningen en datasetstromen verbonden aan hen.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de categorie *Klantsucces* selecteert u **ServiceNow** om een informatiebalk aan de rechterkant van het scherm weer te geven. De informatiebalk bevat een korte beschrijving van de geselecteerde bron en opties voor het maken van verbinding met de bron of het bekijken van de documentatie. Selecteer **Connect-bron** als u een nieuwe account wilt maken.

![](../../../../images/tutorials/create/servicenow/catalog.png)

De pagina *Verbinding maken met ServiceNow* wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **Nieuw account** als u nieuwe referenties gebruikt. Geef op het invoerformulier dat wordt weergegeven, de verbinding een naam, een optionele beschrijving en uw referenties ServiceNow. Als u klaar bent, selecteert u **Connect** en laat u de nieuwe account enige tijd beginnen.

![](../../../../images/tutorials/create/servicenow/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de ServiceNow-account waarmee u verbinding wilt maken en selecteert u **Volgende** om door te gaan.

![](../../../../images/tutorials/create/servicenow/existing.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een verbinding met uw account ServiceNow tot stand gebracht. U kunt nu verdergaan aan het volgende leerprogramma en een dataflow [vormen om gegevens in Platform](../../dataflow/customer-success.md)te brengen.
