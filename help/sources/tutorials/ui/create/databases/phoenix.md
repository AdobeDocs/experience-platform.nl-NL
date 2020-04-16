---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een Phoenix-bronaansluiting maken in de gebruikersinterface
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# Een Phoenix-bronaansluiting maken in de gebruikersinterface

De bronschakelaars in het Platform van de Ervaring van Adobe verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie bevat stappen voor het maken van een Phoenix-bronconnector met behulp van de gebruikersinterface van Platform.

## Aan de slag

Voor deze zelfstudie is een goed begrip vereist van de volgende componenten van het Adobe Experience Platform:

* [XDM-systeem](../../../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor het Platform van de Ervaring gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [Klantprofiel](../../../../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u reeds een geldige verbinding Phoenix hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan bij het [vormen van een dataflow](../../dataflow/databases.md)

### Vereiste referenties verzamelen

Als u toegang wilt tot uw Phoenix-account op Platform, moet u de volgende waarden opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | Het IP-adres of de hostnaam van de Phoenix-server. |
| `port` | De TCP-poort die de Phoenix-server gebruikt om te luisteren naar clientverbindingen. Als u verbinding maakt met Azure HDInsights, geeft u de poort op als 443. |
| `httpPath` | De gedeeltelijke URL die overeenkomt met de Phoenix-server. Geef /hbasephoenix0 op als u de Azure HDInsights-cluster gebruikt. |
| `username` | De gebruikersnaam die u gebruikt om toegang te krijgen tot de Phoenix-server. |
| `password` | Het wachtwoord dat overeenkomt met de gebruiker. |
| `enableSsl` | Een schakeloptie waarmee wordt opgegeven of de verbindingen met de server via SSL zijn gecodeerd. |

Raadpleeg [dit Phoenix-document](https://python-phoenixdb.readthedocs.io/en/latest/api.html)voor meer informatie over aan de slag gaan.

## Uw Phoenix-account verbinden

Nadat u de vereiste gegevens hebt verzameld, voert u de onderstaande stappen uit om een nieuwe Phoenix-account te maken voor verbinding met Platform.

Meld u aan bij <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> en selecteer vervolgens **Bronnen** in de linkernavigatiebalk voor toegang tot de werkruimte *Bronnen* . Het scherm van de *Catalogus* toont een verscheidenheid van bronnen waarvoor u binnenkomende rekening kunt tot stand brengen, en elke bron toont het aantal bestaande rekeningen en datasetstromen verbonden aan hen.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de categorie *Databases* selecteert u **Phoenix** om een informatiebalk aan de rechterkant van het scherm weer te geven. De informatiebalk bevat een korte beschrijving van de geselecteerde bron en opties voor het maken van verbinding met de bron of het bekijken van de documentatie. Selecteer **Connect-bron** als u een nieuwe binnenkomende verbinding wilt maken.

![catalogus](../../../../images/tutorials/create/phoenix/catalog.png)

De pagina *Verbinding maken met Phoenix* wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **Nieuw account** als u nieuwe referenties gebruikt. Geef in het invoerformulier dat wordt weergegeven, de verbinding een naam, een optionele beschrijving en uw Phoenix-referenties. Als u klaar bent, selecteert u **Connect** en laat u de nieuwe account enige tijd beginnen.

![verbinden](../../../../images/tutorials/create/phoenix/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de Phoenix-account waarmee u verbinding wilt maken en selecteert u **Volgende** om door te gaan.

![bestaand](../../../../images/tutorials/create/phoenix/existing.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een verbinding met uw Phoenix-account tot stand gebracht. U kunt nu doorgaan met de volgende zelfstudie en een gegevensstroom [configureren om gegevens over te brengen naar Platform](../../dataflow/databases.md).