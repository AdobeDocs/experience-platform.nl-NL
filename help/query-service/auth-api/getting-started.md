---
keywords: Experience Platform; de Dienst van de Vraag; IP toegangsbeheer; vergunning; API; begonnen worden
title: API-handleiding voor queryservice
description: Leer hoe te beginnen voor vergunning en IP waaierbeperkingen voor veilige gegevenstoegang binnen de Dienst van de Vraag van Adobe Experience Platform.
role: Developer
source-git-commit: eb6558c2cc3faebb2cb14f49f7517227d57f7162
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# Handleiding voor de API voor queryservice

De API van de Vergunning van de Dienst van de Vraag voorziet organisaties van striktere controle over gegevenstoegang via de SQL interface in Adobe Experience Platform. U kunt deze API gebruiken om IP beperkingen te bepalen, gegevenstoegang tot gespecificeerde netwerken te beperken, en veiligheid controle te verbeteren.

Deze gids schetst hoe te opstelling de toestemmingsgeloofsbrieven en de toestemmingen die worden vereist om vraag aan de Vergunning API van de Dienst van de Vraag te maken.

## Aan de slag {#getting-started}

De volgende secties verstrekken informatie over het voorbereiden van de vereiste vergunningswaarden en het doen van uw eerste verzoeken aan de Vergunning API van de Dienst van de Vraag.

### Vereiste machtigingen {#required-permissions}

Om de beperkingen van de veilige gegevenstoegang in de Dienst van de Vraag toe te laten, hebt u de **[!UICONTROL Manage Allowed List]** toestemming nodig. Deze toestemming staat organisaties toe om specifieke IP waaiers (in formaat IPv4 of IPv6) te bepalen die aan toegangsgegevens in Platform via de SQL interface worden gemachtigd. De toegang wordt beheerd op het zandbakniveau, waar de gebruikers een lijst van goedgekeurde IP adressen of blokken kunnen vormen CIDR die toegang slechts tot toegelaten netwerken beperken.

>[!NOTE]
>
>De Beheerders van het systeem kunnen opstellings gebruikerstoestemmingen van de Adobe [ Admin Console ](https://adminconsole.adobe.com/). Voor meer informatie, zie de [ gebruikersgids van de Admin Console ](https://helpx.adobe.com/nl/enterprise/using/admin-console.html).

De volgende functies zijn beschikbaar met de machtiging **[!UICONTROL Manage Allowed List]** :

- **bepaalt toegestane IP waaiers**: Slechts IP adressen of de blokken CIDR van deze bepaalde waaiers kunnen tot gegevens in Platform toegang hebben gebruikend SQL door de Dienst van de Vraag.
- **afdwingen IP waaiercontroles**: De verbindingen van IPs buiten de toegestane waaiers worden ontkend.
- **Controle en alarmerende mogelijkheden**: Alle toegangspogingen, met inbegrip van ontkende verbindingen, worden geregistreerd als controlegebeurtenissen. Deze gebeurtenissen zijn beschikbaar in de [ Logboeken van de Controle van Adobe Experience Platform ](../../landing/governance-privacy-security/audit-logs/overview.md), toelatend controle van potentiële veiligheidsbreuken.

### Waarden verzamelen voor vereiste koppen {#gather-values-for-required-headers}

Om vraag aan de Vergunning API van de Dienst van de Vraag te maken, moet u het [ de authentificatieleerprogramma van het Platform API ](../../landing/api-authentication.md) voltooien, dat waarden voor vereiste kopballen in API vraag verstrekt. Neem de volgende kopteksten op in elke aanvraag:

- **Vergunning**: `Bearer {ACCESS_TOKEN}`
- **x-api-sleutel**: `{API_KEY}`
- **x-gw-ims-org-id**: `{ORG_ID}`
- **x-zandbak-naam**: `{SANDBOX_NAME}`

>[!NOTE]
>
> Voor meer informatie over zandbakken, zie de [ documentatie van het zandbakoverzicht ](../../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen ook deze kopbal:

- **inhoud-Type**: `application/json`

### Volgende stappen

Met de vereiste toestemmingen en verzamelde kopbalwaarden, bent u bereid beginnen IP beperkingen voor de Dienst van de Vraag te vormen. Ga verder naar de eindpuntdocumentatie voor gedetailleerde voorbeelden van CRUD verrichtingen, die omvatten:

- API-indeling en voorbeelden van verzoek-/responsparen.
- Kopteksten, ladingen, en reactiecodes voor elke verrichting.

Elk API vraagvoorbeeld toont aan hoe te om verzoeken te formatteren en reacties te interpreteren, die u veilige toegang tot uw gegevens in de Dienst van de Vraag helpen afdwingen.

Voor specifieke instructies bij het vormen van en het bevestigen van IP beperkingen, verwijs naar de [ IP documentatie van het eindpunt van de Toegang ](./ip-access.md) en de [ IP documentatie van het eindpunt van de Bevestiging ](./validate.md).
