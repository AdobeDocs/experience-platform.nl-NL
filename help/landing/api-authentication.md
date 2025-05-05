---
solution: Experience Platform
title: Experience Platform API's verifiëren en openen
type: Tutorial
description: Dit document biedt een stapsgewijze zelfstudie voor het verkrijgen van toegang tot een Adobe Experience Platform-ontwikkelaarsaccount om aanroepen uit te voeren naar Experience Platform API's.
role: Developer
feature: API
exl-id: dfe8a7be-1b86-4d78-a27e-87e4ed8b3d42
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2409'
ht-degree: 1%

---


# Experience Platform-API&#39;s verifiëren en openen

Dit document biedt een stapsgewijze zelfstudie voor het verkrijgen van toegang tot een Adobe Experience Platform-ontwikkelaarsaccount om aanroepen uit te voeren naar Experience Platform API&#39;s. Aan het einde van deze zelfstudie hebt u de volgende gegevens gegenereerd of verzameld die als headers zijn vereist voor alle Experience Platform API-aanroepen:

* `{ACCESS_TOKEN}`
* `{API_KEY}`
* `{ORG_ID}`

>[!TIP]
>
>Naast de drie bovenstaande referenties, vereisen veel Experience Platform API&#39;s ook een geldig `{SANDBOX_NAME}` dat als header moet worden opgegeven. Zie het [ zandbakenoverzicht ](../sandboxes/home.md) voor meer informatie over zandbakken en het [ zandbakbeheereindpunt ](/help/sandboxes/api/sandboxes.md#list) documentatie voor informatie over het van een lijst maken van de zandbakken beschikbaar aan uw organisatie.

Om de veiligheid van uw toepassingen en gebruikers te handhaven, moeten alle verzoeken aan Experience Platform APIs voor authentiek worden verklaard en worden gemachtigd gebruikend normen zoals OAuth.

In deze zelfstudie wordt uitgelegd hoe u de vereiste referenties kunt verzamelen voor het verifiëren van Experience Platform API-aanroepen, zoals hieronder in het stroomschema wordt beschreven. U kunt de meeste vereiste geloofsbrieven in eerste éénmalige opstelling verzamelen. Het toegangstoken, echter, moet om de 24 uur worden verfrist.

![ de vereisten van de authentificatiestroom voor de éénmalige aanvankelijke opstelling en elke verdere zitting.](./images/api-authentication/authentication-flowchart.png)

## Vereisten {#prerequisites}

Als u aanroepen naar Experience Platform API&#39;s wilt uitvoeren, moet u over het volgende beschikken:

* Een organisatie met toegang tot Adobe Experience Platform.
* Een Admin Console-beheerder die u als ontwikkelaar en gebruiker voor een productprofiel kan toevoegen.
* Een systeembeheerder van Experience Platform die u de noodzakelijke attributengebaseerde toegangscontroles kan verlenen om lees uit te voeren of verrichtingen op verschillende delen van Experience Platform door APIs te schrijven.

U moet ook over een Adobe ID beschikken om deze zelfstudie te voltooien. Als u geen Adobe ID hebt, kunt u er een maken door de volgende stappen uit te voeren:

1. Ga naar [ Adobe Developer Console ](https://console.adobe.io).
2. Selecteer **[!UICONTROL Create a new account]**.
3. Voltooi het aanmeldingsproces.

## Profiteer van toegang voor ontwikkelaars en gebruikers van Experience Platform {#gain-developer-user-access}

Voordat u integratie op Adobe Developer Console kunt maken, moet uw account ontwikkelings- en gebruikersmachtigingen hebben voor een Experience Platform-productprofiel in Adobe Admin Console.

### Toegang voor ontwikkelaars verkrijgen {#gain-developer-access}

Neem contact op met een Admin Console-beheerder in uw organisatie om u als ontwikkelaar toe te voegen aan een Experience Platform-productprofiel. Zie de documentatie van Admin Console voor specifieke instructies op hoe te [ ontwikkelaartoegang voor productprofielen ](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html) beheren.

Zodra u als ontwikkelaar wordt toegewezen, kunt u beginnen integraties in [ Adobe Developer Console ](https://www.adobe.com/go/devs_console_ui) tot stand te brengen. Deze integratie is een pijplijn van externe apps en services naar Adobe API&#39;s.

### Toegang tot gebruikers verkrijgen {#gain-user-access}

Uw Admin Console-beheerder moet u ook als gebruiker toevoegen aan hetzelfde productprofiel. Met gebruikerstoegang, kunt u in UI het resultaat van de API verrichtingen zien die u uitvoert.

Zie de gids op [ het leiden gebruikersgroepen in Admin Console ](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/user-groups.ug.html) voor meer informatie.

## Een API-sleutel (client-id) en organisatie-id genereren {#generate-credentials}

>[!NOTE]
>
>Als u dit document van de [ Privacy Service API gids ](../privacy-service/api/getting-started.md) volgt, kunt u aan die gids nu terugkeren om de toegangsgeloofsbrieven te produceren uniek aan [!DNL Privacy Service].

Nadat u ontwikkelaars en gebruikers via Admin Console toegang hebt verleend tot Experience Platform, bestaat de volgende stap uit het genereren van uw `{ORG_ID}` - en `{API_KEY}` -referenties in Adobe Developer Console. Deze gegevens hoeven slechts eenmaal te worden gegenereerd en kunnen in toekomstige Experience Platform API-aanroepen opnieuw worden gebruikt.

>[!TIP]
>
>In plaats van naar Developer Console te gaan, kunt u alle verificatiereferenties die u nodig hebt om met Experience Platform API&#39;s te werken, rechtstreeks ophalen via de API-documentatiepagina&#39;s. [Lees meer](#get-credentials-functionality) over de nieuwe functionaliteit.

### Experience Platform toevoegen aan een project {#add-platform-to-project}

Ga naar [ Adobe Developer Console ](https://www.adobe.com/go/devs_console_ui) en teken binnen met uw Adobe ID. Daarna, volg de stappen die in het leerprogramma worden geschetst op [ creërend een leeg project ](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) in de documentatie van Adobe Developer Console.

Wanneer u een nieuw project hebt gemaakt, selecteert u **[!UICONTROL Add API]** op het **[!UICONTROL Project Overview]** -scherm.

>[!TIP]
>
>Als u provisioned voor verscheidene organisaties bent, gebruik de organisatieselecteur in de hogere juiste hoek van de interface om ervoor te zorgen dat u in de organisatie bent u nodig hebt.

![ het scherm van Developer Console met Add wordt benadrukt API optie.](./images/api-authentication/add-api.png)

Het scherm **[!UICONTROL Add an API]** wordt weergegeven. Selecteer het productpictogram voor **[!UICONTROL Adobe Experience Platform]** en kies **[!UICONTROL Experience Platform API]** voordat u **[!UICONTROL Next]** selecteert.

![ Uitgezochte Experience Platform API in Add een API scherm.](./images/api-authentication/platform-api.png)

>[!TIP]
>
>Selecteer de **[!UICONTROL View docs]** optie om in een afzonderlijk browser venster aan de volledige [ Experience Platform API verwijzingsdocumentatie ](https://developer.adobe.com/experience-platform-apis/) te navigeren.

### Selecteer het verificatietype [!UICONTROL OAuth Server-to-Server] {#select-oauth-server-to-server}

Selecteer vervolgens het verificatietype **[!UICONTROL OAuth Server-to-Server]** dat u wilt gebruiken voor het genereren van toegangstokens en het openen van de Experience Platform API. Geef uw referentie een betekenisvolle naam in het tekstveld **[!UICONTROL Credential name]** voordat u **[!UICONTROL Next]** selecteert.

>[!IMPORTANT]
>
>De methode **[!UICONTROL OAuth Server-to-Server]** is de enige ondersteunde methode voor het genereren van tokens die vooruit gaat. De eerder ondersteunde **[!UICONTROL Service Account (JWT)]** -methode is vervangen en kan niet worden geselecteerd voor nieuwe integraties. Hoewel bestaande integratie met behulp van de JWT-verificatiemethode tot 30 juni 2025 blijft werken, raadt Adobe u ten zeerste aan om vóór die datum bestaande integratie te migreren naar de nieuwe [!UICONTROL OAuth Server-to-Server] -methode. Krijg meer informatie in de sectie [!BADGE &#x200B; Afgekeurd &#x200B;]{type=negative}[ produceer een Token van het Web JSON (JWT) ](#jwt).

![ selecteer de server-aan-Server authentificatiemethode OAuth voor Experience Platform API.](./images/api-authentication/oauth-authentication-method.png)

### Selecteer de productprofielen voor uw integratie {#select-product-profiles}

Selecteer in het scherm **[!UICONTROL Configure API]** de optie **[!UICONTROL AEP-Default-All-Users]** , samen met eventuele aanvullende productprofielen waartoe u toegang wilt krijgen.

>[!IMPORTANT]
>
>Om toegang tot bepaalde eigenschappen in Experience Platform te krijgen, hebt u ook een systeembeheerder nodig om u de noodzakelijke op attribuut-gebaseerde toegangsbeheertoestemmingen te verlenen. Lees meer in de sectie [ krijgt de noodzakelijke op attributen-gebaseerde toegangsbeheertoestemmingen ](#get-abac-permissions).

![ Uitgezochte productprofielen voor uw integratie.](./images/api-authentication/select-product-profiles.png)

Selecteer **[!UICONTROL Save configured API]** wanneer u klaar bent.

In de onderstaande videozelfstudie vindt u een analyse van de hierboven beschreven stappen voor het instellen van integratie met de Experience Platform API:

>[!VIDEO](https://video.tv.adobe.com/v/28832/?learn=on)

### Referenties verzamelen {#gather-credentials}

Zodra API aan het project is toegevoegd, **[!UICONTROL OAuth Server-to-Server]** toont de pagina voor het project de volgende geloofsbrieven die in alle vraag aan Experience Platform APIs worden vereist:

![ de informatie van de Integratie na het toevoegen van API in de Console van de Ontwikkelaar.](./images/api-authentication/api-integration-information.png)

* `{API_KEY}` ([!UICONTROL Client ID])
* `{ORG_ID}` ([!UICONTROL Organization ID])

<!--

![](././images/api-authentication/api-key-ims-org.png)

<!--

In addition to the above credentials, you also need the generated **[!UICONTROL Client Secret]** for a future step. Select **[!UICONTROL Retrieve client secret]** to reveal the value, and then copy it for later use.

![](././images/api-authentication/client-secret.png)

-->

## Een toegangstoken genereren {#generate-access-token}

De volgende stap bestaat uit het genereren van een `{ACCESS_TOKEN}` -referentie voor gebruik in Experience Platform API-aanroepen. In tegenstelling tot de waarden voor `{API_KEY}` en `{ORG_ID}` , moet om de 24 uur een nieuw token worden gegenereerd om Experience Platform API&#39;s te kunnen blijven gebruiken. Selecteer **[!UICONTROL Generate access token]** die het toegangstoken produceert, zoals hieronder wordt getoond.

![ toon hoe te om toegangstoken ](././images/api-authentication/generate-access-token.png) te produceren

>[!TIP]
>
>U kunt ook een Postman-omgeving en -verzameling gebruiken om toegangstokens te genereren. Voor meer informatie, lees de sectie over [ gebruikend Postman om API vraag ](#use-postman) voor authentiek te verklaren en te testen.

## Verificatiegegevens rechtstreeks in de API-naslagdocumentatie maken en ophalen {#get-credentials-functionality}

Vanaf de release van november 2024 van Experience Platform kunt u referenties ophalen om de Experience Platform API&#39;s rechtstreeks vanaf de API-referentiepagina&#39;s te gebruiken, zonder dat u naar [!UICONTROL Developer Console] hoeft te gaan. Bekijk het voorbeeld hieronder van de [ Dienst API van de Stroom - de pagina van Doelen ](https://developer.adobe.com/experience-platform-apis/references/destinations/).

![ krijgt geloofsbrieven die bij de bovenkant van een API verwijzingspagina worden benadrukt.](././images/api-authentication/get-credentials-highlighted.png)

Als u referenties wilt ophalen om Experience Platform API&#39;s aan te roepen, navigeert u naar een willekeurige Experience Platform API-referentiepagina en selecteert u **[!UICONTROL Sign in]** boven aan de pagina. Meld u aan met uw **[!UICONTROL Personal Account]** of **[!UICONTROL Company or School Account]** .

Nadat u zich hebt aangemeld, selecteert u **[!UICONTROL Create new credential]** om een nieuwe set referenties te maken voor toegang tot Experience Platform API&#39;s.

![ creeer nieuwe geloofsbrieven om tot Experience Platform APIs toegang te hebben.](././images/api-authentication/create-credentials.gif)

Gebruik vervolgens de keuzelijst om het venster met referenties te openen, een toegangstoken te genereren en uw API-sleutel en organisatie-id op te halen. Kopieer de referenties naar de blokken [**[!UICONTROL Try it]**](/help/release-notes/2024/may-2024.md#interactive-api-documentation) op de API-referentiepagina&#39;s om te gaan werken met Experience Platform API&#39;s.

![ gebruik dropdown selecteur om geloofsbrieven te bekijken en een toegangstoken te produceren.](././images/api-authentication/view-copy-credentials.gif)

>[!TIP]
>
>Het onderwerpblok van de bovenste pagina blijft zichtbaar wanneer u navigeert tussen verschillende eindpuntpagina&#39;s in de Experience Platform API-naslagdocumentatie.

## [!BADGE &#x200B; Vervangen &#x200B;] &lbrace;type=negative&rbrace; produceer een Symbolisch van het Web JSON (JWT) {#jwt}

>[!WARNING]
>
>De JWT-methode voor het genereren van toegangstokens is afgekeurd. Alle nieuwe integraties moeten worden gecreeerd gebruikend de [ Server-aan-Server authentificatiemethode ](#select-oauth-server-to-server). Adobe vereist ook dat u uw bestaande integratie aan de methode OAuth tegen 30 juni 2025 migreert opdat uw integratie blijft werken. Lees de volgende belangrijke documentatie:
> 
>* [ gids van de Migratie voor uw toepassingen van JWT aan OAuth ](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)
>* [ gids van de Implementatie voor nieuwe en oude toepassingen met OAuth ](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/)
>* [ Voordelen om de Server-aan-Server geloofsbrieven te gebruiken OAuth methode ](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#why-oauth-server-to-server-credentials)

+++ Vervangen gegevens weergeven

De volgende stap bestaat uit het genereren van een JSON Web Token (JWT) op basis van uw accountgegevens. Deze waarde wordt gebruikt om uw `{ACCESS_TOKEN}` -referentie te genereren voor gebruik in Experience Platform API-aanroepen, die elke 24 uur opnieuw moeten worden gegenereerd.

>[!IMPORTANT]
>
>In deze zelfstudie wordt beschreven hoe u een JWT kunt genereren in Developer Console. Deze generatiemethode mag echter alleen voor test- en evaluatiedoeleinden worden gebruikt.
>
>Voor normaal gebruik moet de JWT automatisch worden gegenereerd. Voor meer informatie over hoe te om JWTs programmatically te produceren, zie de [ gids van de de authentificatieauthentificatie van de de dienstrekening ](https://www.adobe.io/developer-console/docs/guides/authentication/JWT/) op Adobe Developer.

Selecteer **[!UICONTROL Service Account (JWT)]** in de linkernavigatie en selecteer vervolgens **[!UICONTROL Generate JWT]** .

![](././images/api-authentication/generate-jwt.png)

Plak in het tekstvak onder **[!UICONTROL Generate custom JWT]** de inhoud van de persoonlijke sleutel die u eerder hebt gegenereerd toen u de Experience Platform API aan uw serviceaccount toevoegde. Selecteer vervolgens **[!UICONTROL Generate Token]** .

![](././images/api-authentication/paste-key.png)

De pagina wordt bijgewerkt om de gegenereerde JWT weer te geven, samen met een voorbeeld-URL-opdracht waarmee u een toegangstoken kunt genereren. In deze zelfstudie selecteert u **[!UICONTROL Copy]** naast **[!UICONTROL Generated JWT]** om de token naar het klembord te kopiëren.

![](././images/api-authentication/copy-jwt.png)

**produceer een toegangstoken**

Nadat u een JWT hebt gegenereerd, kunt u deze in een API-aanroep gebruiken om de `{ACCESS_TOKEN}` -aanroep te genereren. In tegenstelling tot de waarden voor `{API_KEY}` en `{ORG_ID}` , moet om de 24 uur een nieuw token worden gegenereerd om Experience Platform API&#39;s te kunnen blijven gebruiken.

**Verzoek**

Het volgende verzoek genereert een nieuwe `{ACCESS_TOKEN}` op basis van de referenties die in de payload zijn opgegeven. Dit eindpunt accepteert alleen formuliergegevens als nuttige last en daarom moet het een `Content-Type` header van `multipart/form-data` krijgen.

```shell
curl -X POST https://ims-na1.adobelogin.com/ims/exchange/jwt \
  -H 'Content-Type: multipart/form-data' \
  -F 'client_id={API_KEY}' \
  -F 'client_secret={SECRET}' \
  -F 'jwt_token={JWT}'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `{API_KEY}` | `{API_KEY}` ([!UICONTROL Client ID]) die u in a [ vorige stap ](#api-ims-secret) terugwende. |
| `{SECRET}` | Het cliëntgeheim dat u in a [ vorige stap ](#api-ims-secret) terughaalde. |
| `{JWT}` | JWT die u in a [ vorige stap ](#jwt) produceerde. |

>[!NOTE]
>
>U kunt dezelfde API-sleutel, clientgeheim en JWT gebruiken om een nieuw toegangstoken voor elke sessie te genereren. Hierdoor kunt u het genereren van toegangstoken in uw toepassingen automatiseren.

**Reactie**

```json
{
  "token_type": "bearer",
  "access_token": "{ACCESS_TOKEN}",
  "expires_in": 86399992
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `token_type` | Het type of token dat wordt geretourneerd. Voor toegangstokens is deze waarde altijd `bearer` . |
| `access_token` | De gegenereerde `{ACCESS_TOKEN}` . Deze waarde, voorafgegaan door het woord `Bearer` , is vereist als de `Authentication` -header voor alle Experience Platform API-aanroepen. |
| `expires_in` | Het aantal milliseconden dat resteert tot het toegangstoken verloopt. Zodra deze waarde 0 bereikt, moet een nieuw toegangstoken worden geproduceerd om Experience Platform APIs te blijven gebruiken. |

+++

## Toegangsreferenties testen {#test-credentials}

Nadat u alle drie vereiste gegevens hebt verzameld (toegangstoken, API-sleutel en organisatie-id), kunt u de volgende API-aanroep proberen te maken. Deze vraag maakt een lijst van alle standaard [!DNL Experience Data Model] (XDM) klassen beschikbaar aan uw organisatie. De invoer en voert de vraag in [ Postman ](#use-postman) uit.

>[!BEGINSHADEBOX]

**Verzoek**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}'
```

**Reactie**

Als uw reactie vergelijkbaar is met de hieronder weergegeven reactie, zijn uw gegevens geldig en werken ze. (Deze reactie is afgebroken voor de ruimte.)

```JSON
{
  "results": [
    {
        "title": "XDM ExperienceEvent",
        "$id": "https://ns.adobe.com/xdm/context/experienceevent",
        "meta:altId": "_xdm.context.experienceevent",
        "version": "1"
    },
    {
        "title": "XDM Individual Profile",
        "$id": "https://ns.adobe.com/xdm/context/profile",
        "meta:altId": "_xdm.context.profile",
        "version": "1"
    }
  ]
}
```

>[!ENDSHADEBOX]

>[!IMPORTANT]
>
>Terwijl de vraag hierboven volstaat om uw toegangsgeloofsbrieven te testen, ben zich ervan bewust dat u niet tot verscheidene middelen zult kunnen toegang hebben of wijzigen zonder het hebben van de juiste op attribuut-gebaseerde toegangsbeheertoestemmingen. Lees meer in **krijgt de noodzakelijke op attributen-gebaseerde toestemmingen van de toegangscontrole** hieronder sectie.

## Krijg de noodzakelijke op attributen-gebaseerde toegangsbeheertoestemmingen {#get-abac-permissions}

Om tot verscheidene middelen binnen Experience Platform toegang te hebben of te wijzigen, moet u de aangewezen toegangsbeheertoestemmingen hebben. De beheerders van het systeem kunnen u de [ toestemmingen verlenen u ](/help/access-control/ui/permissions.md) nodig hebt. Krijg meer informatie in de sectie over [ het leiden API geloofsbrieven voor een rol ](/help/access-control/abac/ui/permissions.md#manage-api-credentials-for-role).

Gedetailleerde informatie over hoe een systeembeheerder de vereiste machtigingen voor toegang tot Experience Platform-bronnen via de API kan verlenen, is ook beschikbaar in de onderstaande videozelfstudie:

>[!VIDEO](https://video.tv.adobe.com/v/28832/?learn=on&t=159)

## Postman gebruiken om API-aanroepen te verifiëren en te testen {#use-postman}

[ Postman ](https://www.postman.com/) is een populair hulpmiddel dat ontwikkelaars toestaat om RESTful APIs te onderzoeken en te testen. Met Experience Platform Postman-verzamelingen en -omgevingen kunt u uw werk versnellen met Experience Platform API&#39;s. Lees meer over [ het gebruiken van Postman in Experience Platform ](/help/landing/postman.md) en het worden begonnen met inzamelingen en milieu&#39;s.

Gedetailleerde informatie over het gebruik van Postman met Experience Platform-verzamelingen en -omgevingen is ook beschikbaar in de volgende videozelfstudies:

**Download en voer een milieu van Postman in om met Experience Platform APIs te gebruiken**

>[!VIDEO](https://video.tv.adobe.com/v/28832/?learn=on&t=106)

**Gebruik een inzameling van Postman om toegangstokens** te produceren

Download de [ inzameling van Postman van de Dienst van Identity Management ](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims?lang=nl) en bekijk de video hieronder om te leren hoe te om toegangstokens te produceren.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?learn=on)

**de inzamelingen van Experience Platform API Postman van de Download en interactie met APIs**

>[!VIDEO](https://video.tv.adobe.com/v/29704/?learn=on)

<!--
This [Medium post](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) describes how you can set up Postman to automatically perform JWT authentication and use it to consume Experience Platform APIs.
-->

## Systeembeheerders: toegangsbeheer voor ontwikkelaars en API&#39;s verlenen met Experience Platform-machtigingen {#grant-developer-and-api-access-control}

Voordat u integratie op Adobe Developer Console kunt maken, moet uw account ontwikkelings- en gebruikersmachtigingen voor een Experience Platform-productprofiel hebben.

>[!NOTE]
>
>Alleen systeembeheerders kunnen API-referenties weergeven en beheren in Machtigingen.

### Ontwikkelaars toevoegen aan productprofiel {#add-developers-to-product-profile}

Navigeer aan [ Admin Console ](https://adminconsole.adobe.com/) en teken binnen met uw Adobe ID.

Selecteer **[!UICONTROL Products]** op de navigatiebalk en selecteer vervolgens **[!UICONTROL Adobe Experience Platform]** in de lijst met producten.

![ de productpagina op Adobe Admin Console met het benadrukte product van Adobe Experience Platform.](././images/api-authentication/products.png)

Selecteer op het tabblad **[!UICONTROL Product Profiles]** de optie **[!UICONTROL AEP-Default-All-Users]** . U kunt ook de zoekbalk gebruiken om het productprofiel te zoeken door de naam in te voeren.

![ de pagina van productprofielen met de onderzoeksbar en AEP-gebrek-Alle-Gebruikers benadrukte product.](././images/api-authentication/select-product-profile.png)

Selecteer de tab **[!UICONTROL Developers]** en selecteer vervolgens **[!UICONTROL Add Developer]** .

![ het lusje van ontwikkelaars wordt getoond met de Add benadrukte ontwikkelaarsoptie, ](././images/api-authentication/add-developer1.png)

Het dialoogvenster **[!UICONTROL Add developers]** wordt weergegeven. Voer de naam **[!UICONTROL Email or username]** van de ontwikkelaar in. Een geldige [!UICONTROL Email or username] geeft de details van de ontwikkelaar weer. Selecteer **[!UICONTROL Save]**.

![ Add ontwikkelaars dialoog met een binnen gevulde ontwikkelaarsinformatie en sparen benadrukte optie.](././images/api-authentication/add-developer-email.png)

De ontwikkelaar is toegevoegd en wordt weergegeven op het tabblad **[!UICONTROL Developers]** .

![ het lusje dat van ontwikkelaars de lijst van alle toegevoegde ontwikkelaars met de onlangs toegevoegde benadrukte ontwikkelaar toont.](././images/api-authentication/developer-added.png)

### API-referenties toewijzen aan een rol

>[!NOTE]
>
>Alleen een systeembeheerder kan API&#39;s toewijzen aan rollen in de gebruikersinterface van Experience Platform.

Als een systeembeheerder bewerkingen op Experience Platform API&#39;s wil gebruiken en uitvoeren, moet hij de API-referenties toevoegen naast de machtigingen die een rol heeft gegeven. Krijg meer informatie in de sectie over [ het leiden API geloofsbrieven voor een rol ](../access-control/abac/ui/permissions.md#manage-api-credentials-for-a-role).

Een analyse van de hierboven beschreven stappen voor het toevoegen van ontwikkelaars aan productprofielen en het toewijzen van APIs aan rollen is ook beschikbaar in de videozelfstudie hieronder:

>[!VIDEO](https://video.tv.adobe.com/v/3426407/?learn=on)

## Aanvullende bronnen {#additional-resources}

Raadpleeg de aanvullende bronnen die hieronder zijn gekoppeld voor meer hulp bij het starten met Experience Platform API&#39;s

* [ verifieer en toegang Experience Platform APIs ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/platform-api-authentication.html?lang=nl) videoleerprogramma&#39;s pagina
* [ de Inzameling van Postman van de Dienst van Identity Management ](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims?lang=nl) voor het produceren van toegangstokens
* [ Experience Platform API Postman Collections ](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)

## Volgende stappen {#next-steps}

Door dit document te lezen, hebt u uw toegangsgegevens voor Experience Platform API&#39;s verzameld en getest. U kunt nu samen met de voorbeeld API vraag volgen die door de [ documentatie ](../landing/documentation/overview.md) wordt verstrekt.

Naast de verificatiewaarden die u in deze zelfstudie hebt verzameld, vereisen veel Experience Platform API&#39;s ook een geldig `{SANDBOX_NAME}` dat als koptekst moet worden opgegeven. Zie het [sandboxoverzicht](../sandboxes/home.md) voor meer informatie.
