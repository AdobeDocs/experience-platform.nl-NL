---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creeer een de bronschakelaar van de Dynamica van Microsoft in UI
topic: overview
translation-type: tm+mt
source-git-commit: 44c43afc653c147fa12e3e962904bfc79ee0fc64
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---


# Creeer een de bronschakelaar van de Dynamica van Microsoft in UI

Bronconnectors in het Adobe Experience Platform bieden de mogelijkheid om volgens een schema extern gesourceerde CRM-gegevens in te voeren. Dit leerprogramma verstrekt stappen voor het creëren van een de bronschakelaar van de Dynamiek van Microsoft (hierna genoemd &quot;Dynamica&quot;) gebruikend het gebruikersinterface van het Platform.

## Aan de slag

Voor deze zelfstudie is een goed begrip vereist van de volgende componenten van het Adobe Experience Platform:

* [XDM-systeem](../../../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor het Platform van de Ervaring gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [Klantprofiel](../../../../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een geldige rekening van de Dynamiek hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan bij het [vormen van een gegevensstroom](../../dataflow/crm.md).

### Vereiste referenties verzamelen

| Credentials | Beschrijving |
| ---------- | ----------- |
| `serviceUri` | De service-URL van uw instantie Dynamics. |
| `username` | De gebruikersnaam voor uw gebruikersaccount voor dynamiek. |
| `password` | Het wachtwoord voor uw rekening van de Dynamiek. |

Voor meer informatie over aan de slag gaan, bezoek [dit document](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)van de Dynamiek.

## Sluit uw rekening van de Dynamiek aan

Zodra u uw vereiste geloofsbrieven hebt verzameld, kunt u de stappen volgen hieronder om een nieuwe rekening van de Dynamica tot stand te brengen om met Platform te verbinden.

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer vervolgens **[!UICONTROL Bronnen]** in de linkernavigatiebalk voor toegang tot de werkruimte *[!UICONTROL Bronnen]* . Het scherm van de *[!UICONTROL Catalogus]* toont een verscheidenheid van bronnen waarvoor u een binnenkomende rekening met kunt tot stand brengen, en elke bron toont het aantal bestaande rekeningen en datasetstromen verbonden aan hen.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de categorie *[!UICONTROL Databases]* selecteert u **[!UICONTROL Dynamics]** en klikt u **op het pictogram + (+)** om een nieuwe connector voor dynamiek te maken.

![catalogus](../../../../images/tutorials/create/ms-dynamics/catalog.png)

De pagina *[!UICONTROL Verbinden met dynamiek]* wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL Nieuw account]** als u nieuwe referenties gebruikt. Geef in het invoerformulier dat wordt weergegeven, de verbinding een naam, een optionele beschrijving en de referenties voor de dynamiek. Als u klaar bent, selecteert u **[!UICONTROL Connect]** en laat u de nieuwe account enige tijd beginnen.

![verbinden](../../../../images/tutorials/create/ms-dynamics/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u het account voor dynamiek waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Volgende]** in de rechterbovenhoek om door te gaan.

![bestaand](../../../../images/tutorials/create/ms-dynamics/existing.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een verbinding met uw rekening van de Dynamiek tot stand gebracht. U kunt nu doorgaan met de volgende zelfstudie en een gegevensstroom [configureren om gegevens over te brengen naar Platform](../../dataflow/crm.md).