---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creeer de Dynamiek van Microsoft of Salesforce bronschakelaar in UI
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# Creeer de Dynamiek van Microsoft of Salesforce bronschakelaar in UI

Bronconnectors in het Adobe Experience Platform bieden de mogelijkheid om volgens een schema extern gesourceerde CRM-gegevens in te voeren. Deze zelfstudie biedt stappen voor het maken van een Microsoft Dynamics (hierna &quot;Dynamics&quot; genoemd) of Salesforce-bronconnector met behulp van de gebruikersinterface van het platform.

## Aan de slag

Voor deze zelfstudie is een goed begrip vereist van de volgende componenten van het Adobe Experience Platform:

* [XDM-systeem](../../../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor het Platform van de Ervaring gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [Klantprofiel](../../../../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u reeds een de basisverbinding van de Dynamiek of van Salesforce van Microsoft hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan bij het [vormen van een dataflow](../../dataflow/crm.md).

### Vereiste referenties verzamelen

Om tot uw rekening van de Dynamiek op Platform toegang te hebben, moet u een **Dienst URI**, **gebruikersbenaming**, en **wachtwoord** verstrekken.

Op dezelfde manier vereist de toegang tot van uw rekening Salesforce op Platform u een **milieu URL**, **gebruikersbenaming**, **wachtwoord**, en **veiligheidstoken**.

## Maak verbinding met uw Dynamics of Salesforce-account

Met de geloofsbrieven van uw systeem van CRM klaar, kunt u de hieronder stappen volgen om een nieuwe binnenkomende basisverbinding tot stand te brengen om uw rekening van de Dynamiek of van Salesforce aan Platform te verbinden.

Meld u aan bij <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> en selecteer vervolgens **Bronnen** in de linkernavigatiebalk voor toegang tot de werkruimte Bronnen. In het scherm *Catalogus* worden diverse bronnen weergegeven waarvoor u binnenkomende basisverbindingen kunt maken met. Elke bron toont het aantal bestaande basisverbindingen dat aan deze verbindingen is gekoppeld.

Onder de categorie *CRM* selecteert u **Microsoft Dynamics** of **Salesforce** om een informatiebalk aan de rechterkant van het scherm weer te geven. De informatiebalk bevat een korte beschrijving van de geselecteerde bron en opties voor het weergeven van de documentatie of het maken van een verbinding met de bron. Klik op **Verbindingsbron** om een nieuwe binnenkomende basisverbinding te maken.

![](../../../../images/tutorials/create/salesforce/sf_sources_catalog.png)

Geef in het invoerformulier een naam, een optionele beschrijving en de gegevens voor Dynamics of Salesforce op voor de basisverbinding. Klik ten slotte op **Verbinden** en laat enige tijd de nieuwe basisverbinding tot stand brengen.

![](../../../../images/tutorials/create/salesforce/sf_credentials.png)

Zodra een basisverbinding met uw systeem van CRM wordt gevestigd, kunt u op de volgende sectie verdergaan en een dataflow vormen om de gegevens van CRM in Platform te brengen.

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een basisverbinding aan uw Dynamiek of rekening Salesforce gevestigd. U kunt nu doorgaan met de volgende zelfstudie en een gegevensstroom [configureren om gegevens over te brengen naar Platform](../../dataflow/crm.md).