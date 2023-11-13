---
title: Een Google Big Query Source Connection maken in de gebruikersinterface
description: Leer hoe u een Google Big Query-bronverbinding maakt met de Adobe Experience Platform-gebruikersinterface.
badgeUltimate: label="Ultieme" type="Positive"
exl-id: 3c0902de-48b9-42d8-a4bd-0213ca85fc7f
source-git-commit: 9a8139c26b5bb5ff937a51986967b57db58aab6c
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 1%

---

# Een [!DNL Google Big Query] bronverbinding in de gebruikersinterface

>[!IMPORTANT]
>
>De [!DNL Google BigQuery] De bron is in de broncatalogus beschikbaar voor gebruikers die Real-time Customer Data Platform Ultimate hebben aangeschaft.

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie bevat stappen voor het maken van een [!DNL Google Big Query] bronverbinding via de gebruikersinterface van Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor Experience Platform gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie Schema-editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe u aangepaste schema&#39;s maakt met de gebruikersinterface van de Schema-editor.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u al een geldige [!DNL Google BigQuery] verbinding hebt, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie op [configureren, gegevensstroom](../../dataflow/databases.md).

### Vereiste referenties verzamelen

Voor toegang tot uw [!DNL Google BigQuery] account op Platform, moet u de volgende OAuth 2.0 authentificatiewaarden verstrekken:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `project` | De project-id van de standaardwaarde [!DNL Google BigQuery] project aan vraag tegen. |
| `clientID` | De waarde van identiteitskaart die wordt gebruikt om het vernieuwingstoken te produceren. |
| `clientSecret` | De geheime waarde die wordt gebruikt om het te produceren vernieuwt teken. |
| `refreshToken` | Het vernieuwingstoken dat wordt verkregen van [!DNL Google] gebruikt om toegang te verlenen tot [!DNL Google BigQuery]. |

Zie voor meer informatie over deze waarden [dit [!DNL Google BigQuery] document](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing).

## Sluit uw Google BigQuery-account aan

Selecteer in de interface Platform de optie **[!UICONTROL Sources]** van de linkernavigatie om tot [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekbalk.

Onder de [!UICONTROL Databases] categorie, selecteert u **[!UICONTROL Google BigQuery]** en selecteer vervolgens **[!UICONTROL Add data]**.

![](../../../../images/tutorials/create/google-big-query/catalog.png)

De **[!UICONTROL Connect to Google Big Query]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de optie [!DNL Google BigQuery] account waarmee u verbinding wilt maken, selecteert u **[!UICONTROL Next]** om verder te gaan.

![](../../../../images/tutorials/create/google-big-query/existing.png)

### Nieuwe account

Als u nieuwe referenties gebruikt, selecteert u **[!UICONTROL New account]**. Geef op het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw [!DNL Google BigQuery] referenties. Selecteer **[!UICONTROL Connect to source]** en laat dan wat tijd voor de nieuwe verbinding tot stand brengen.

![](../../../../images/tutorials/create/google-big-query/new.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Google BigQuery] account. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom configureren om gegevens over te brengen naar het platform](../../dataflow/databases.md).
