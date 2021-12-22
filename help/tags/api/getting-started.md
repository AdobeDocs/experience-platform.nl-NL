---
title: Aan de slag met de Reactor-API
description: Leer hoe u aan de slag kunt met de Reactor-API, inclusief stappen voor het genereren van de vereiste toegangsreferenties.
exl-id: fc1acc1d-6cfb-43c1-9ba9-00b2730cad5a
source-git-commit: 04e778d3318d60733772c2042c8bb272f0c87d5c
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 0%

---

# Aan de slag met de Reactor-API

Voor het gebruik van de [Reactor-API](https://www.adobe.io/experience-platform-apis/references/reactor/), moet elke aanvraag de volgende verificatieheaders bevatten:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

In deze handleiding wordt uitgelegd hoe u de Adobe Developer Console kunt gebruiken om de waarden voor elk van deze kopteksten te verzamelen, zodat u aanroepen kunt starten naar de Reactor-API.

## Toegang voor ontwikkelaars tot Adobe Experience Platform

Voordat u verificatiewaarden voor de Reactor-API kunt genereren, moet u ontwikkelaarstoegang tot het Experience Platform hebben. Volg de eerste stappen in het dialoogvenster [Zelfstudie over verificatie van Experience Platforms](https://www.adobe.com/go/platform-api-authentication-en). Zodra u bij de stap &quot;Genereer toegangsgeloofsbrieven in de Console van de Ontwikkelaar van de Adobe&quot;aankomt, terugkeer aan dit leerprogramma om de geloofsbrieven te produceren specifiek voor Reactor API.

## Toegangsreferenties genereren

Gebruikend de Console van de Ontwikkelaar van Adobe, moet u de volgende drie toegangsgeloofsbrieven produceren:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

De id van uw IMS-organisatie (`{IMS_ORG}`) en API-sleutel (`{API_KEY}`) kan in toekomstige API-aanroepen opnieuw worden gebruikt nadat deze zijn gegenereerd. Nochtans, uw toegangstoken (`{ACCESS_TOKEN}`) is tijdelijk en moet om de 24 uur opnieuw worden gegenereerd.

De stappen voor het genereren van deze waarden worden hieronder in detail besproken.

### Eenmalige installatie

Ga naar [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) en meld u aan met uw Adobe ID. Voer vervolgens de stappen uit die in de zelfstudie worden beschreven [een leeg project maken](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) in de documentatie van de Developer Console.

Als u een project hebt gemaakt, selecteert u **API toevoegen** op de **Overzicht van project** scherm.

![](../images/api/getting-started/add-api-button.png)

De **Een API toevoegen** wordt weergegeven. Selecteren **Experience Platform Reactor-API** uit de lijst met beschikbare API&#39;s voordat u **Volgende**.

![](../images/api/getting-started/add-launch-api.png)

Op het volgende scherm, wordt u ertoe aangezet om een geloofsbrieven tot stand te brengen JSON Web Token (JWT) of een nieuw sleutelpaar produceren of uw eigen openbare sleutel uploaden. Selecteer voor deze zelfstudie de optie **Een sleutelpaar genereren** en selecteert u vervolgens **Keypair genereren** in de rechterbenedenhoek.

![](../images/api/getting-started/create-jwt.png)

Het volgende scherm bevestigt dat het sleutelpaar met succes heeft geproduceerd, en een samengeperste omslag die een openbaar certificaat en een privé sleutel bevat wordt automatisch gedownload aan uw machine. Deze persoonlijke sleutel wordt vereist in een recentere stap om een toegangstoken te produceren.

Selecteren **Volgende** om door te gaan.

![](../images/api/getting-started/keypair-generated.png)

In het volgende scherm wordt u gevraagd een of meer productprofielen te selecteren die u aan de API-integratie wilt koppelen.

>[!NOTE]
>
>Productprofielen worden door uw organisatie beheerd via de Adobe Admin Console en bevatten specifieke sets rechten voor korrelfuncties. Productprofielen en hun machtigingen kunnen alleen worden beheerd door gebruikers met beheerdersrechten binnen uw organisatie. Neem contact op met de beheerder als u niet zeker weet welke productprofielen u voor de API moet selecteren.

Selecteer in de lijst de gewenste productprofielen en selecteer vervolgens **geconfigureerde API opslaan** om de API-registratie te voltooien.

![](../images/api/getting-started/select-product-profile.png)

Zodra API aan het project is toegevoegd, verschijnt de projectpagina opnieuw op de Experience Platform Reactor API pagina. Hier omlaag schuiven naar de **Serviceaccount (JWT)** sectie, die de volgende toegangsgeloofsbrieven verstrekt die in alle vraag aan Reactor API worden vereist:

* **CLIENT-ID**: De client-id is vereist `{API_KEY}` die in de `x-api-key` header.
* **ORGANISATIE-ID**: De organisatie-id is de `{IMS_ORG}` waarde die moet worden gebruikt in de `x-gw-ims-org-id` header.

![](../images/api/getting-started/access-creds.png)

### Verificatie voor elke sessie

Nu hebt u uw `{API_KEY}` en `{IMS_ORG}` waarden, de laatste stap genereert een `{ACCESS_TOKEN}` waarde.

>[!NOTE]
>
>Deze tokens verlopen na 24 uur. Als u deze integratie voor een toepassing gebruikt, is het een goed idee om uw token programmatically uit uw toepassing te verkrijgen.

U hebt twee opties om uw toegangstokens te produceren, afhankelijk van uw gebruiksgeval:

* [Tkens handmatig genereren](#manual)
* [Tkens programmatisch genereren](#program)

#### Handmatig toegangstekens genereren {#manual}

Open de persoonlijke sleutel die u eerder hebt gedownload in een teksteditor of browser en kopieer de inhoud ervan. Navigeer vervolgens terug naar de Developer Console en plak de persoonlijke sleutel in het dialoogvenster **Toegangstoken genereren** sectie over de Reactor API-pagina voor uw project voordat u **Token genereren**.

![](../images/api/getting-started/paste-private-key.png)

Er wordt een nieuw toegangstoken gegenereerd en er wordt een knop opgegeven waarmee het token naar het klembord kan worden gekopieerd. Deze waarde wordt gebruikt voor de vereiste `Authorization` en moet worden opgegeven in de vorm `Bearer {ACCESS_TOKEN}`.

![](../images/api/getting-started/token-generated.png)

#### Toegangstokens programmatisch genereren {#program}

Als u uw integratie voor een toepassing gebruikt, kunt u programmatically toegangstokens door API verzoeken produceren. Hiervoor hebt u de volgende waarden nodig:

* Client-id (`{API_KEY}`)
* Clientgeheim (`{SECRET}`)
* Een JSON-webtoken (`{JWT}`)

Uw client-id en geheim zijn te vinden op de hoofdpagina voor uw project, zoals in het dialoogvenster [vorige stap](#one-time-setup).

![](../images/api/getting-started/auto-access-creds.png)

Navigeer naar om uw JWT-referentie te verkrijgen **Serviceaccount (JWT)** in de linkernavigatie, dan selecteer **JWT genereren** tab. Op deze pagina, onder **Aangepaste JWT genereren**, plakt u de inhoud van de persoonlijke sleutel in het tekstvak dat u opgeeft, en selecteert u **Token genereren**.

![](../images/api/getting-started/generate-jwt.png)

De gegenereerde JWT verschijnt hieronder zodra de verwerking is voltooid, samen met een voorbeeld-URL-opdracht waarmee u het token desgewenst kunt testen. Gebruik de **Kopiëren** om het token naar het klembord te kopiëren.

![](../images/api/getting-started/jwt-generated.png)

Zodra u uw geloofsbrieven hebt verzameld, kunt u de API vraag hieronder in uw toepassing integreren om toegangstokens programmatically te produceren.

**Verzoek**

Het verzoek moet een `multipart/form-data` lading, die uw authentificatiegeloofsbrieven verstrekken zoals hieronder getoond:

```shell
curl -X POST \
  https://ims-na1.adobelogin.com/ims/exchange/jwt/ \
  -H 'Content-Type: multipart/form-data' \
  -F 'client_id={API_KEY}' \
  -F 'client_secret={SECRET}' \
  -F 'jwt_token={JWT}'
```

**Antwoord**

Een succesvolle reactie keert een nieuw toegangstoken, evenals het aantal seconden terug tot het verloopt.

```json
{
  "token_type": "bearer",
  "access_token": "{ACCESS_TOKEN}",
  "expires_in": 86399999
}
```

| Eigenschap | Beschrijving |
| :-- | :-- |
| `access_token` | De zojuist gegenereerde waarde van het toegangstoken. Deze waarde wordt gebruikt voor de vereiste `Authorization` en moet worden opgegeven in de vorm `Bearer {ACCESS_TOKEN}`. |
| `expires_in` | De resterende tijd tot het token verloopt, in milliseconden. Nadat een token is verlopen, moet er een nieuw token worden gegenereerd. |

{style=&quot;table-layout:auto&quot;}

## Volgende stappen

Als u de stappen in deze zelfstudie uitvoert, hebt u geldige waarden voor `{IMS_ORG}`, `{API_KEY}`, en `{ACCESS_TOKEN}`. U kunt deze waarden nu testen door ze te gebruiken in een eenvoudig cURL-verzoek aan de Reactor-API.

Begin door te proberen een API vraag te maken aan [lijst alle bedrijven](./endpoints/companies.md#list).

>[!NOTE]
>
>Mogelijk hebt u geen bedrijven in uw organisatie. In dat geval is de reactie HTTP-status 404 (Niet gevonden). Zolang u geen fout van 403 (Verboden) krijgt, zijn uw toegangsgeloofsbrieven geldig en werkend.

Nadat u hebt bevestigd dat uw toegangsreferenties werken, gaat u verder met de documentatie van de andere API-naslaggids om de vele mogelijkheden van de API te leren kennen.

## Aanvullende bronnen

JWT-bibliotheken en SDK&#39;s: [https://jwt.io/](https://jwt.io/)

Ontwikkeling van de Postman-API: [https://www.postman.com/](https://www.postman.com/)
