---
title: Overzicht van NetSuite-bron in oracle
description: Leer hoe u Oracle NetSuite met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface.
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 053cf0af327b39830f025686e0f8f67c27f1c45c
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---

# [!DNL Oracle NetSuite]

>[!NOTE]
>
>De [!DNL Oracle NetSuite] De bron is in bèta. Lees de [overzicht van bronnen](../../home.md#terms-and-conditions) voor meer informatie over het gebruik van bronnen met een bètalabel.

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de platformservices. U kunt gegevens uit diverse bronnen invoeren, zoals toepassingen voor Adobe, opslag in de cloud, databases en vele andere.

Experience Platform biedt ondersteuning voor het invoeren van gegevens van derden voor het automatiseren van de marketing. De ondersteuning voor leveranciers van marketingautomatisering omvat [!DNL Oracle NetSuite].

[[!DNL Oracle NetSuite]](https://www.netsuite.com/) is een cloudgebaseerde bedrijfsbeheersuite die ERP/financial-, CRM- en e-commerce-oplossingen omvat.

U kunt twee verschillende bronnen gebruiken om gegevens in te voeren van [!DNL Oracle NetSuite] naar Experience Platform:

* Gebruik de [!DNL Oracle NetSuite Activities] bron voor het opnemen van gebeurtenisgegevens.
* Gebruik de [!DNL Oracle NetSuite Entities] bron om klant en contactgegevens in te voeren.

De volgende tabel weergeven voor meer informatie over de twee [!DNL Oracle NetSuite] bronnen.

| Bron | Type | Beschrijving |
| --- | --- | --- |
| [[!DNL Oracle NetSuite Activities]](#oracle-netsuite-activities) | Gebeurtenis | Haal geplande activiteiten op die aan uw kalender zijn toegevoegd. |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | Klant | Haal specifieke klantgegevens op, zoals klantnamen, adressen en toetsidentificatoren. |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | Contact | Haal contactnamen, e-mails, telefoonnummers en eventuele aangepaste contactvelden die aan klanten zijn gekoppeld op. |

## IP adres lijst van gewenste personen {#ip-allow-list}

Een lijst van IP adressen kan vereisen om aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de [IP adres lijst van gewenste personen](../../ip-address-allow-list.md) voor meer informatie.

## Vereisten {#prerequisites}

Voordat u uw [!DNL Oracle NetSuite] gegevens aan Experience Platform, moet u eerst ervoor zorgen dat u het volgende hebt:

* **An [!DNL Oracle NetSuite] account**.
   * Contact [[!DNL Oracle NetSuite]](https://www.NetSuite.com/portal/company/contactus.shtml) als u nog geen geldige account hebt.
* An **actief abonnement** aan [!DNL Oracle NetSuite] product.
* An **account-id**.
   * De [!DNL Oracle NetSuite] bron gebruikt OAuth 2.0 om met [!DNL Oracle NetSuite] API&#39;s. Als u geen account-id hebt, gaat u naar de [!DNL Oracle] documentatie over [hoe u uw account-id ophaalt](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_1498754928.html#Finding-Your-NetSuite-Account-ID).
* A **client-id** en **clientgeheim** combinatie.
   * De client-id en het clientgeheim zijn vereist voor toegang [!DNL Oracle NetSuite] API&#39;s. Tijdens deze stap, moet u ook ervoor zorgen dat uw beheerder heeft:
      * Toegelaten de eigenschap OAuth 2.0 en opstelling de aangewezen rollen OAuth 2.0.
      * Toegewezen gebruikers aan OAuth 2.0 rollen en creeerde de noodzakelijke integratieverslagen.
* An **toegangstoken** en **token vernieuwen**.
   * Zie de [!DNL Oracle] hulplijn aan [OAuth 2.0 Authorization Code Grant Flow](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158074210415.html#OAuth-2.0-Authorization-Code-Grant-Flow) voor informatie over hoe te om uw toegang te produceren en tokens te verfrissen.

### Vereiste referenties verzamelen {#gather-credentials}

Om verbinding te maken [!DNL Oracle NetSuite] aan Platform, moet u waarden voor de volgende verbindingseigenschappen verstrekken:

| Credentials | Beschrijving | Voorbeeld |
| --- | --- | --- |
| Client-id | De client-id-waarde die wordt gegenereerd wanneer u de integratie-record maakt in [!DNL Oracle NetSuite]. Lees de [!DNL Oracle] gids over hoe te [integratiecords maken](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981) voor meer informatie . | `7fce.....b42f`<br>De waarde bestaat uit een tekenreeks van 64 tekens. |
| Clientgeheim | De waarde van het clientgeheim die wordt gegenereerd wanneer u de integratierecord maakt. Lees de [!DNL Oracle] gids over hoe te [integratiecords maken](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981) voor meer informatie . | `5c98.....1b46`<br>De waarde bestaat uit een tekenreeks van 64 tekens. |
| Autorisatietest-URL | (Optioneel) Uw [!DNL NetSuite] autorisatietest-URL. | `https://{ACCOUNT_ID}.app.netsuite.com<br>/app/login/oauth2/authorize.nl?response_type=code<br>&redirect_uri=https%3A%2F%2Fapi.github.com<br>&scope=rest_webservices<br>&state=ykv2XLx1BpT5Q0F3MRPHb94j<br>&client_id={CLIENT_ID}` |
| Toegangstoken | Het toegangstoken is in formaat JSON Web Token (JWT) en is slechts geldig voor 60 minuten. Lees voor meer informatie over het ophalen van uw toegangstoken het [!DNL Oracle] hulplijn aan [OAuth 2.0-autorisatie voor NetSuite](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint). | `eyJr......f4V0`<br> De waarde bestaat uit een tekenreeks van 1024 tekens die is opgemaakt als JSON Web Token (JWT). |
| Token vernieuwen | Gebruik verfrissen zich om een nieuw toegangstoken te produceren, nadat uw toegangstoken verloopt. De token Vernieuwen is zeven dagen geldig. Lees voor meer informatie over het ophalen van uw toegangstoken het [!DNL Oracle] hulplijn aan [OAuth 2.0-autorisatie voor NetSuite](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint). | `eyJr......dmxM`<br> De waarde bestaat uit een tekenreeks van 1024 tekens die is opgemaakt als JSON Web Token (JWT). |
| Toegang tot token-URL | Het symbolische eindpunt waar de toepassing de verzoeken van de POST naar verzendt. | `https://{ACCOUNT_ID}.suitetalk.api.netsuite.com<br>/services/rest/auth/oauth2/v1/token` |

>[!IMPORTANT]
>
>Nadat een vernieuwingstoken verloopt, moet u een nieuw rekening in Experience Platform met uw bijgewerkte tokens tot stand brengen.

## Verbinden [!DNL Oracle NetSuite Activities] naar platform {#oracle-netsuite-activities}

In de onderstaande documentatie vindt u informatie over de verbinding [!DNL Oracle NetSuite Activities] naar Platform met API&#39;s of de gebruikersinterface:

* [Een bronverbinding en gegevensstroom maken voor [!DNL Oracle NetSuite Activities] gegevens naar platform met API&#39;s](../../tutorials/api/create/marketing-automation/oracle-netsuite-activities.md).
* [Verbind uw [!DNL Oracle NetSuite Activities] account aan Experience Platform met behulp van de gebruikersinterface](../../tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md).
* [Een gegevensstroom maken voor een bronverbinding met behulp van de gebruikersinterface](../../tutorials/ui/dataflow/marketing-automation.md).

## Verbinden [!DNL Oracle NetSuite Entities] naar platform {#oracle-netsuite-entities}

In de onderstaande documentatie vindt u informatie over de verbinding [!DNL Oracle NetSuite Entities] naar Platform met API&#39;s of de gebruikersinterface:

* [Een bronverbinding en gegevensstroom maken voor [!DNL Oracle NetSuite Entities] gegevens naar platform met API&#39;s](../../tutorials/api/create/marketing-automation/oracle-netsuite-entities.md).
* [Verbind uw [!DNL Oracle NetSuite Entities] account aan Experience Platform met behulp van de gebruikersinterface](../../tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md).
* [Een gegevensstroom maken voor een bronverbinding met behulp van de gebruikersinterface](../../tutorials/ui/dataflow/marketing-automation.md).
