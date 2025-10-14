---
title: Google Ads Source - Overzicht
description: Leer hoe u Google Ads met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface.
exl-id: 1f6257e0-213c-4723-a240-511c11c5833c
source-git-commit: ac90eea69f493bf944a8f9920426a48d62faaa6c
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 0%

---

# [!DNL Google Ads] bron

>[!NOTE]
>
>De bron [!DNL Google Ads] is in bèta. Zie het [&#x200B; Bronoverzicht &#x200B;](../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen en biedt u de mogelijkheid om inkomende gegevens te structureren, labelen en verbeteren met behulp van Experience Platform-services. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, opslag in de cloud, databases en vele andere.

Experience Platform biedt ondersteuning voor het opnemen van gegevens uit een derde-advertentiesysteem. Tot de ondersteuning voor advertentieproviders behoren [!DNL Google Ads] .

## Vereisten {#prerequisites}

### IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de [&#128279;](../../ip-address-allow-list.md) pagina van de lijst van gewenste personen van het 0&rbrace; IP adres &lbrace;voor meer informatie.

### Machtigingen configureren voor Experience Platform

U moet zowel **[!UICONTROL View Sources]** - als **[!UICONTROL Manage Sources]** -machtigingen hebben ingeschakeld voor uw account om uw [!DNL Google Ads] -account te kunnen verbinden met Experience Platform. Neem contact op met de productbeheerder om de benodigde machtigingen te verkrijgen. Voor meer informatie, lees de [&#x200B; gids UI van de toegangscontrole &#x200B;](../../../access-control/ui/overview.md).

### Vereiste referenties verzamelen

U moet de juiste waarden opgeven voor de volgende referenties om uw [!DNL Google Ads] -account met Experience Platform te kunnen verbinden.

| Credentials | Beschrijving |
| --- | --- |
| `clientCustomerId` | De klant-id is het accountnummer dat overeenkomt met de [!DNL Google Ads] client-account die u wilt beheren met de [!DNL Google Ads] -API. Deze id volgt de sjabloon van `123-456-7890` . |
| `loginCustomerId` | De inlogklant-id is het accountnummer dat overeenkomt met uw [!DNL Google Ads] manager-account en wordt gebruikt om rapportgegevens van een specifieke operationele klant op te halen. Voor meer informatie over login klant identiteitskaart, lees de [[!DNL Google Ads]  API documentatie &#x200B;](https://developers.google.com/search-ads/reporting/concepts/login-customer-id). |
| `developerToken` | Met de ontwikkelaarstoken hebt u toegang tot de API van [!DNL Google Ads] . Met dezelfde ontwikkelaarstoken kunt u aanvragen indienen voor al uw [!DNL Google Ads] -accounts. Haal uw ontwikkelaarstoken door [&#x200B; het programma openen aan uw managerrekening &#x200B;](https://ads.google.com/home/tools/manager-accounts/) op en navigeert dan aan de [!DNL API Center] pagina. |
| `refreshToken` | Het token Vernieuwen maakt deel uit van [!DNL OAuth2] -verificatie. Dit teken staat u toe om uw toegangstokens na het verlopen opnieuw te produceren. |
| `clientId` | De client-id wordt gebruikt in combinatie met het clientgeheim als onderdeel van [!DNL OAuth2] -verificatie. Met de client-id en het clientgeheim kan uw toepassing samen namens uw account werken door uw toepassing aan te duiden op [!DNL Google] . |
| `clientSecret` | Het clientgeheim wordt gebruikt in combinatie met de client-id als onderdeel van [!DNL OAuth2] -verificatie. Met de client-id en het clientgeheim kan uw toepassing samen namens uw account werken door uw toepassing aan te duiden op [!DNL Google] . |
| `googleAdsApiVersion` | De huidige API-versie die wordt ondersteund door [!DNL Google Ads] . De meest recente versie is `v18` , maar de meest recente ondersteunde versie op Experience Platform is `v17` . |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Google Ads] is: `d771e9c1-4f26-40dc-8617-ce58c4b53702` . Deze waarde is vereist als u uw [!DNL Google Ads] -account aansluit met de [!DNL Flow Service] API. |

## Verbinden [!DNL Google Ads] met Experience Platform

In de onderstaande documentatie vindt u informatie over het tot stand brengen van een verbinding tussen [!DNL Google Ads] en Experience Platform via API&#39;s of de gebruikersinterface:

### API&#39;s gebruiken

* [Een Google Ads-basisverbinding maken met de Flow Service API](../../tutorials/api/create/advertising/ads.md)
* [Gegevenstabellen verkennen met de Flow Service API](../../tutorials/api/explore/tabular.md)
* [Een dataflow maken voor een advertentiebron met behulp van de Flow Service API](../../tutorials/api/collect/advertising.md)

### UI gebruiken

* [Een Google Ads-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/advertising/ads.md)
* [Een gegevensstroom maken voor een verbinding met een advertentiebron in de gebruikersinterface](../../tutorials/ui/dataflow/advertising.md)
