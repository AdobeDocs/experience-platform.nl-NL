---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Maak een Apache Spark op de Azure HDInsights-bronconnector in de gebruikersinterface
topic: overview
translation-type: tm+mt
source-git-commit: ae059f93f09dbbae4f1ef46f68901071afba9729

---


# Maak een Apache Spark op de Azure HDInsights-bronconnector in de gebruikersinterface

De bronschakelaars in het Platform van de Ervaring van Adobe verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie biedt stappen voor het maken van een Apache Spark op de Azure HDInsights-bronconnector met behulp van de Platform-gebruikersinterface.

## Aan de slag

Voor deze zelfstudie is een goed begrip vereist van de volgende componenten van het Adobe Experience Platform:

* [XDM-systeem](../../../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor het Platform van de Ervaring gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [Klantprofiel](../../../../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u reeds een geldige verbinding van de Vonk hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan bij het [vormen van een dataflow](../../dataflow/databases.md)

### Vereiste referenties verzamelen

Om tot uw rekening van de Vonk op Platform toegang te hebben, moet u de volgende waarden verstrekken:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | Het IP adres of hostname van de server van de Vonk. |
| `username` | De gebruikersnaam die u gebruikt om tot de server van de Vonk toegang te hebben. |
| `password` | Het wachtwoord dat overeenkomt met de gebruiker. |

Voor meer informatie over begonnen worden verwijs naar [dit document](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-overview)van Vonk.

## Verbinding maken met uw Spark-account

Zodra u uw vereiste geloofsbrieven hebt verzameld, kunt u de stappen volgen hieronder om een nieuwe rekening van de Vonk tot stand te brengen om met Platform te verbinden.

Meld u aan bij <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> en selecteer vervolgens **Bronnen** in de linkernavigatiebalk voor toegang tot de werkruimte *Bronnen* . Het scherm van de *Catalogus* toont een verscheidenheid van bronnen waarvoor u binnenkomende rekening kunt tot stand brengen, en elke bron toont het aantal bestaande rekeningen en datasetstromen verbonden aan hen.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de categorie *Databases* selecteert u **Vonk** om een informatiebalk aan de rechterkant van het scherm weer te geven. De informatiebalk bevat een korte beschrijving van de geselecteerde bron en opties voor het maken van verbinding met de bron of het bekijken van de documentatie. Selecteer **Connect-bron** als u een nieuwe binnenkomende verbinding wilt maken.

![catalogus](../../../../images/tutorials/create/spark/catalog.png)

De pagina *Verbinden met Vonk* wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **Nieuw account** als u nieuwe referenties gebruikt. Geef op het invoerformulier dat wordt weergegeven, de verbinding een naam, een optionele beschrijving en uw Vonk-gegevens. Als u klaar bent, selecteert u **Connect** en laat u de nieuwe account enige tijd beginnen.

![new](../../../../images/tutorials/create/spark/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de Spark-account waarmee u verbinding wilt maken en selecteert u **Volgende** om door te gaan.

![bestaand](../../../../images/tutorials/create/spark/existing.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een verbinding met uw account van de Vonk tot stand gebracht. U kunt nu doorgaan met de volgende zelfstudie en een gegevensstroom [configureren om gegevens over te brengen naar Platform](../../dataflow/databases.md).