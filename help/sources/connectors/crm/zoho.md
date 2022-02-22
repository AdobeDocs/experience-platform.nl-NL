---
keywords: Experience Platform;home;populaire onderwerpen;Zoho CRM;zoho crm;Zoho;zoho
solution: Experience Platform
title: Zoho CRM Source Connector Overzicht
topic-legacy: overview
description: Leer hoe u Zoho CRM aan Adobe Experience Platform verbindt gebruikend APIs of het gebruikersinterface.
exl-id: 4a010453-3d09-4a47-b04e-5789ae4af48c
source-git-commit: 46b2fd6bc715bf1d8ccfeed576a2a2d193f92edd
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---

# [!DNL Zoho CRM]

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van [!DNL Platform] diensten. U kunt gegevens van diverse bronnen, zoals Adobe-toepassingen, cloudopslag, databases en vele andere, invoeren.

Experience Platform biedt ondersteuning voor het opnemen van gegevens van een CRM-systeem van derden. Ondersteuning voor CRM-providers omvat [!DNL Zoho CRM].

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de [IP adres lijst van gewenste personen](../../ip-address-allow-list.md) voor meer informatie.

## Vraag uw verificatiereferenties op voor [!DNL Zoho CRM]

Voordat u gegevens van uw [!DNL Zoho CRM] account aan Platform, moet u eerst uw gegevens ophalen om uw [!DNL Zoho CRM] bron. Voer de onderstaande stappen uit om uw client-id, clientgeheim, toegangstoken op te halen en token te vernieuwen.

### Uw toepassing registreren

De eerste stap bij het ophalen van uw verificatiegegevens bestaat uit het registreren van uw toepassing met de [[!DNL Zoho CRM] ontwikkelaarsconsole](https://accounts.zoho.com/). Om uw toepassing te registreren, moet u uw cliënttype selecteren van: JavaScript, webgebaseerd, mobiel, niet-browser mobiele toepassingen of zelfclient. Geef vervolgens waarden op voor de naam van de toepassing, de URL van de webpagina en een geautoriseerde omleidings-URI die [!DNL Zoho CRM] U kunt dan gebruiken om u met een giftetoken om te leiden.

Een geslaagde registratie retourneert uw client-id en clientgeheim.

### Een autorisatieverzoek maken

Vervolgens moet u een [autorisatieverzoek](https://www.zoho.com/crm/developer/docs/api/v2/auth-request.html) via een webtoepassing of een zelfclient. Het vergunningsverzoek keert uw subsidieteken terug, dat beurtelings u toestaat om uw toegangstoken terug te winnen.

Wanneer u een autorisatieaanvraag maakt, moet u waarden voor beide invullen **bereik** en **toegangstype**. Zie dit [[!DNL Zoho CRM] document](https://www.zoho.com/crm/developer/docs/api/v2/scopes.html) voor meer informatie over het bereik, terwijl uw **toegangstype** moet altijd worden ingesteld op `offline`.

### Uw toegangs- en vernieuwingstolken genereren

Zodra u uw subsidie-teken hebt teruggewonnen, kunt u uw [tokens openen en vernieuwen](https://www.zoho.com/crm/developer/docs/api/v2/access-refresh.html) door een POST aan te vragen `{ACCOUNTS_URL}/oauth/v2/token` terwijl het verstrekken van uw cliëntidentiteitskaart, cliëntgeheim, giftetoken, en herleidt URI. Tijdens deze stap moet u ook `grant_type` als parameter, en de waarde instellen als `"authorization_code"`.

Een succesvol verzoek keert uw toegang terug en verfrist tekenen, die u dan kunt gebruiken om voor authentiek te verklaren.

Raadpleeg voor gedetailleerde stappen over het verkrijgen van uw referenties de [[!DNL Zoho CRM] verificatiegids](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## Verbinden [!DNL Zoho CRM] tot [!DNL Platform] gebruiken, API&#39;s

In de onderstaande documentatie vindt u informatie over het maken van een verbinding [!DNL Zoho CRM] Platforms met behulp van API&#39;s of de gebruikersinterface:

- [Een [!DNL Zoho CRM] basisverbinding met de Flow Service API](../../tutorials/api/create/crm/zoho.md)
- [Onderzoek de gegevensstructuur en de inhoud van een bron van CRM gebruikend de Dienst API van de Stroom](../../tutorials/api/explore/crm.md)
- [Creeer een dataflow voor een bron van CRM gebruikend de Dienst API van de Stroom](../../tutorials/api/collect/crm.md)

## Verbinden [!DNL Zoho CRM] tot [!DNL Platform] gebruiken van UI

- [Een [!DNL Zoho CRM] bronverbinding in de gebruikersinterface](../../tutorials/ui/create/crm/zoho.md)
- [Een gegevensstroom maken voor een CRM-bronverbinding in de gebruikersinterface](../../tutorials/ui/dataflow/crm.md)
