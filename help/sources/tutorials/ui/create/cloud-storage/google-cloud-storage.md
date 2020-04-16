---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een Google Cloud Storage-bronconnector maken in de gebruikersinterface
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# Een Google Cloud Storage-bronconnector maken in de gebruikersinterface

De bronschakelaars in het Platform van de Ervaring van Adobe verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie bevat stappen voor het maken van een GCS-bronconnector (Google Cloud Storage) via de gebruikersinterface van Platform.

## Aan de slag

Voor deze zelfstudie is een goed begrip vereist van de volgende componenten van het Adobe Experience Platform:

* [XDM-systeem](../../../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor het Platform van de Ervaring gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [Klantprofiel](../../../../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u reeds een GCS basisverbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan bij het [vormen van een gegevensstroom](../../dataflow/cloud-storage.md).

### Ondersteunde bestandsindelingen

Het Experience Platform ondersteunt de volgende bestandsindelingen die in externe opslagruimten kunnen worden opgenomen:

* Door scheidingstekens gescheiden waarden (DSV): De ondersteuning voor gegevensbestanden met DSV-indeling is momenteel beperkt tot door komma&#39;s gescheiden waarden. De waarde van veldkoppen in bestanden met DSV-indeling mag alleen bestaan uit alfanumerieke tekens en onderstrepingstekens. Algemene DSV-bestanden worden in de toekomst ondersteund.
* JavaScript Object Notation (JSON): Gegevensbestanden met JSON-indeling moeten XDM-compatibel zijn.
* Apache Parquet: Gegevensbestanden met Parketindeling moeten XDM-compatibel zijn.

### Vereiste referenties verzamelen

Als u toegang wilt krijgen tot uw GCS-gegevens op Platform, moet u een geldige GCS **Access Key ID** en **Secret** opgeven. U kunt meer informatie over hoe u deze waarden kunt verkrijgen door de handleiding voor <a href="https://cloud.google.com/docs/authentication/production" target="_blank">serververificatie voor Google Cloud te lezen</a> .

## Sluit uw GCS-account aan

Nadat u de vereiste gegevens hebt verzameld, voert u de onderstaande stappen uit om een nieuwe binnenkomende basisverbinding te maken waarmee u uw GCS-account kunt koppelen aan Platform.

Meld u aan bij <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> en selecteer vervolgens **Bronnen** in de linkernavigatiebalk voor toegang tot de werkruimte *Bronnen* . In het scherm *Catalogus* worden diverse bronnen weergegeven waarvoor u binnenkomende basisverbindingen kunt maken met. Elke bron toont het aantal bestaande basisverbindingen dat aan deze verbindingen is gekoppeld.

Selecteer in de categorie *Cloudopslag* de optie **Google Cloud Storage** om een informatiebalk aan de rechterkant van het scherm weer te geven. De informatiebalk bevat een korte beschrijving van de geselecteerde bron en opties voor het maken van een verbinding met de bronweergave, de documentatie bij de bron of voor het tot stand brengen van een verbinding met de bron. Klik op **Verbindingsbron** om een nieuwe binnenkomende basisverbinding te maken.

![](../../../../images/tutorials/create/google-cloud-storage/sources-catalog.png)

Het dialoogvenster _Verbinding maken met Google Cloud Storage_ wordt weergegeven. Geef in het invoerformulier een naam, een optionele beschrijving en uw GCS-referenties op voor de basisverbinding. Wanneer u klaar bent, klikt u op **Connect** en laat u de nieuwe basisverbinding enige tijd tot stand brengen.

![](../../../../images/tutorials/create/google-cloud-storage/gcs-credentials.png)

Zodra een basisverbinding wordt gevestigd, kunt u op de volgende sectie verdergaan en een dataflow vormen om gegevens in Platform te brengen.

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een basisverbinding met uw GCS-account tot stand gebracht. U kunt nu doorgaan met de volgende zelfstudie en een gegevensstroom [configureren om gegevens over te brengen naar Platform](../../dataflow/cloud-storage.md).