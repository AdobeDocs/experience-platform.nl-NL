---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een Google Ads-bronconnector maken in de gebruikersinterface
topic: overview
translation-type: tm+mt
source-git-commit: 3b5821d641d35e1190ea9fecfd4def5beced6ecc

---


# Een Google Ads-bronconnector maken in de gebruikersinterface

De bronschakelaars in het Platform van de Ervaring van Adobe verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie bevat stappen voor het maken van een Google Ads-bronconnector via de gebruikersinterface van Platform.

## Aan de slag

Voor deze zelfstudie is een goed begrip vereist van de volgende componenten van het Adobe Experience Platform:

* [XDM-systeem](../../../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor het Platform van de Ervaring gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [Klantprofiel](../../../../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een basisverbinding van Google Ads hebt, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie over het [configureren van een gegevensstroom](../../dataflow/payments.md)

### Vereiste referenties verzamelen

U moet de volgende waarden opgeven om toegang te krijgen tot uw Google Ads-accountplatform:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `clientCustomerId` | De klant-id van de client voor het account Advertentie. |
| `developerToken` | Het ontwikkelaarstoken verbonden aan de managerrekening. |
| `refreshToken` | Het vernieuwingstoken dat bij Google is verkregen voor het toestaan van toegang tot advertenties. |
| `clientId` | De client-id van de Google-toepassing waarmee de vernieuwingstoken wordt aangeschaft. |
| `clientSecret` | Het clientgeheim van de Google-toepassing die wordt gebruikt om het vernieuwingstoken te verkrijgen. |

Raadpleeg dit [Google Ads-document](https://developers.google.com/adwords/api/docs/guides/authentication)voor meer informatie over aan de slag gaan.

## Maak verbinding met uw Google Ads-account

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om een nieuwe binnenkomende basisverbinding te maken voor de koppeling van uw Google Ads-account aan Platform.

Meld u aan bij <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> en selecteer vervolgens **Bronnen** in de linkernavigatiebalk voor toegang tot de werkruimte *Bronnen* . In het scherm *Catalogus* worden diverse bronnen weergegeven waarvoor u binnenkomende basisverbindingen kunt maken met. Elke bron toont het aantal bestaande basisverbindingen dat aan deze verbindingen is gekoppeld.

Selecteer onder de categorie *Adverteren* de optie **Google Ads** om een informatiebalk aan de rechterkant van het scherm weer te geven. De informatiebalk bevat een korte beschrijving van de geselecteerde bron en opties voor het maken van verbinding met de bron of het bekijken van de documentatie. Selecteer **Connect-bron** als u een nieuwe binnenkomende basisverbinding wilt maken.

![catalogus](../../../../images/tutorials/create/ads/catalog.png)

De pagina *Connect to Google Ads* wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **Nieuw account** als u nieuwe referenties gebruikt. Geef op het invoerformulier dat wordt weergegeven, de basisverbinding een naam, een optionele beschrijving en uw Google Ads-referenties. Als u klaar bent, selecteert u **Connect** en laat u de nieuwe basisverbinding enige tijd tot stand brengen.

![verbinden](../../../../images/tutorials/create/ads/connect.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u het Google Ads-account waarmee u verbinding wilt maken en selecteert u **Volgende** om door te gaan.

![bestaand](../../../../images/tutorials/create/ads/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een basisverbinding met uw Google Ads-account tot stand gebracht. U kunt nu doorgaan met de volgende zelfstudie en een gegevensstroom [configureren om advertentiegegevens over te brengen naar Platform](../../dataflow/advertising.md).