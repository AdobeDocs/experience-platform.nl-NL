---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creeer een HubSpot bronschakelaar in UI
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# Creeer een HubSpot bronschakelaar in UI

De bronschakelaars in het Platform van de Ervaring van Adobe verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Dit leerprogramma verstrekt stappen voor het creëren van een HubSpot bronschakelaar gebruikend het gebruikersinterface van het Platform.

## Aan de slag

Voor deze zelfstudie is een goed begrip vereist van de volgende componenten van het Adobe Experience Platform:

* [XDM-systeem](../../../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor het Platform van de Ervaring gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [Klantprofiel](../../../../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u reeds een HubSpot basisverbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan bij het [vormen van een marketing automatiseringsdataflow](../../dataflow/marketing-automation.md).

### Vereiste referenties verzamelen

om tot uw rekening HubSpot op Platform toegang te hebben, moet u de volgende waarden verstrekken:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `clientId` | De cliënt identiteitskaart verbonden aan uw toepassing HubSpot. |
| `clientSecret` | Het cliëntgeheim verbonden aan uw toepassing HubSpot. |
| `accessToken` | Het toegangstoken werd verkregen toen aanvankelijk het voor authentiek verklaren van uw integratie OAuth. |
| `refreshToken` | Het vernieuwingstoken dat wordt verkregen toen aanvankelijk het voor authentiek verklaren van uw integratie OAuth. |

Voor meer informatie over begonnen worden, verwijs naar dit [document](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview)HubSpot.

## Sluit uw HubSpot-account aan

Zodra u uw vereiste geloofsbrieven hebt verzameld, kunt u de stappen hieronder volgen om een nieuwe binnenkomende basisverbinding tot stand te brengen om uw rekening HubSpot aan Platform te verbinden.

Meld u aan bij <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> en selecteer vervolgens **Bronnen** in de linkernavigatiebalk voor toegang tot de werkruimte *Bronnen* . In het scherm *Catalogus* worden diverse bronnen weergegeven waarvoor u binnenkomende basisverbindingen kunt maken met. Elke bron toont het aantal bestaande basisverbindingen dat aan deze verbindingen is gekoppeld.

Onder de categorie van de automatisering *van de* Marketing, uitgezochte **HubSpot** om een informatiebar op de rechterkant van uw scherm bloot te stellen. De informatiebalk bevat een korte beschrijving van de geselecteerde bron en opties voor het maken van verbinding met de bron of het bekijken van de documentatie. Selecteer **Connect-bron** als u een nieuwe binnenkomende basisverbinding wilt maken.

![catalogus](../../../../images/tutorials/create/hubspot/catalog.png)

De pagina *Verbinden met HubSpot* verschijnt. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **Nieuw account** als u nieuwe referenties gebruikt. Voor de inputvorm die verschijnt, verstrek de basisverbinding met een naam, een facultatieve beschrijving, en uw geloofsbrieven HubSpot. Als u klaar bent, selecteert u **Connect** en laat u de nieuwe basisverbinding enige tijd tot stand brengen.

![verbinden](../../../../images/tutorials/create/hubspot/connect.png)

### Bestaande account

Om een bestaande rekening aan te sluiten, selecteer de rekening HubSpot u met wilt verbinden, dan **daarna** selecteren te werk te gaan.

![bestaand](../../../../images/tutorials/create/hubspot/existing.png)

## Volgende stappen

Door dit leerprogramma te volgen, hebt u een basisverbinding aan uw rekening HubSpot gevestigd. U kunt nu doorgaan met de volgende zelfstudie en een gegevensstroom [configureren om de gegevens van het marketingautomatiseringssysteem over te brengen naar Platform](../../dataflow/marketing-automation.md).