---
title: Oracle NetSuite Source - Overzicht
description: Leer hoe u Oracle NetSuite met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface.
last-substantial-update: 2024-01-30T00:00:00Z
exl-id: 1dd30660-c990-4d3f-a64f-2a17e426f56d
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 0%

---

# [!DNL Oracle NetSuite]

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen en biedt u de mogelijkheid om inkomende gegevens te structureren, labelen en verbeteren met behulp van Experience Platform-services. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, opslag in de cloud, databases en vele andere.

Experience Platform biedt ondersteuning voor het invoeren van gegevens van derden voor marketingautomatisering. Ondersteuning voor marketingautomatiseringsproviders omvat [!DNL Oracle NetSuite] .

[[!DNL Oracle NetSuite] ](https://www.netsuite.com/) is een op wolk-gebaseerde bedrijfsbeheerreeks die ERP/financiële, CRM en e-commerce oplossingen omvat.

U kunt twee verschillende bronnen gebruiken om gegevens in te voeren van [!DNL Oracle NetSuite] naar Experience Platform:

* Gebruik de bron [!DNL Oracle NetSuite Activities] om gebeurtenisgegevens in te voeren.
* Gebruik de [!DNL Oracle NetSuite Entities] -bron om gegevens van klanten en contactpersonen in te voeren.

In de volgende tabel vindt u meer informatie over de twee [!DNL Oracle NetSuite] -bronnen.

| Bron | Type | Beschrijving |
| --- | --- | --- |
| [[!DNL Oracle NetSuite Activities]](#oracle-netsuite-activities) | Gebeurtenis | Haal geplande activiteiten op die aan uw kalender zijn toegevoegd. |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | Klant | Haal specifieke klantgegevens op, zoals klantnamen, adressen en toetsidentificatoren. |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | Contact | Haal contactnamen, e-mails, telefoonnummers en eventuele aangepaste contactvelden die aan klanten zijn gekoppeld op. |

## IP adres lijst van gewenste personen {#ip-allow-list}

U moet gebied-specifieke IP adressen aan uw lijst van gewenste personen toevoegen alvorens uw bronnen aan Experience Platform aan te sluiten. Voor meer informatie, lees de gids op [ voegend op lijst van gewenste personen IP adressen om met Experience Platform ](../../ip-address-allow-list.md) voor meer informatie te verbinden.

## Vereisten {#prerequisites}

Voordat u uw [!DNL Oracle NetSuite] -gegevens naar Experience Platform kunt overbrengen, moet u eerst controleren of het volgende mogelijk is:

* **een [!DNL Oracle NetSuite] rekening**.
   * Neem contact op met [[!DNL Oracle NetSuite] ](https://www.NetSuite.com/portal/company/contactus.shtml) als u nog geen geldig account hebt.
* Een **actief abonnement** aan om het even welk [!DNL Oracle NetSuite] product.
* Een **rekeningidentiteitskaart**.
   * De bron [!DNL Oracle NetSuite] gebruikt OAuth 2.0 om te communiceren met de API&#39;s van [!DNL Oracle NetSuite] . Als u uw rekeningidentiteitskaart niet hebt, bezoek de [!DNL Oracle] documentatie op [ hoe te om uw accountidentiteitskaart ](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_1498754928.html#Finding-Your-NetSuite-Account-ID) terug te winnen.
* A **cliëntidentiteitskaart** en **cliënt geheime** combinatie.
   * De client-id en het clientgeheim zijn vereist voor toegang tot API&#39;s van [!DNL Oracle NetSuite] . Tijdens deze stap, moet u ook ervoor zorgen dat uw beheerder heeft:
      * Toegelaten de eigenschap OAuth 2.0 en opstelling de aangewezen rollen OAuth 2.0.
      * Toegewezen gebruikers aan OAuth 2.0 rollen en creeerde de noodzakelijke integratieverslagen.
* Een **toegangstoken** en a **verfrissen teken**.
   * Verwijs naar de [!DNL Oracle] gids op [ OAuth 2.0 de Stroom van de Verlening van de Code van de Vergunning ](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158074210415.html#OAuth-2.0-Authorization-Code-Grant-Flow) voor informatie over hoe te om uw toegang te produceren en tokens te verfrissen.

### Vereiste referenties verzamelen {#gather-credentials}

Als u [!DNL Oracle NetSuite] wilt verbinden met Experience Platform, moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving | Voorbeeld |
| --- | --- | --- |
| Client-id | De client-id-waarde die wordt gegenereerd wanneer u de integratierecord maakt in [!DNL Oracle NetSuite] . Lees de [!DNL Oracle] gids op hoe te [ integratieverslagen ](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981) voor meer informatie tot stand brengen. | `7fce.....b42f`<br> de waarde is een 64 karakterkoord. |
| Clientgeheim | De waarde van het clientgeheim die wordt gegenereerd wanneer u de integratierecord maakt. Lees de [!DNL Oracle] gids op hoe te [ integratieverslagen ](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981) voor meer informatie tot stand brengen. | `5c98.....1b46`<br> de waarde is een 64 karakterkoord. |
| Autorisatietest-URL | (Optioneel) Test-URL voor uw [!DNL NetSuite] -autorisatietest. | `https://{ACCOUNT_ID}.app.netsuite.com<br>/app/login/oauth2/authorize.nl?response_type=code<br>&redirect_uri=https%3A%2F%2Fapi.github.com<br>&scope=rest_webservices<br>&state=ykv2XLx1BpT5Q0F3MRPHb94j<br>&client_id={CLIENT_ID}` |
| Toegangstoken | Het toegangstoken is in formaat JSON Web Token (JWT) en is slechts geldig voor 60 minuten. Voor meer informatie over hoe te om uw toegangstoken terug te winnen, lees de [!DNL Oracle] gids over [ OAuth 2.0 vergunning voor NetSuite ](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint). | `eyJr......f4V0`<br> De waarde bestaat uit een tekenreeks van 1024 tekens die is opgemaakt als JSON Web Token (JWT). |
| Token vernieuwen | Gebruik verfrissen zich om een nieuw toegangstoken te produceren, nadat uw toegangstoken verloopt. De token Vernieuwen is zeven dagen geldig. Voor meer informatie over hoe te om uw toegangstoken terug te winnen, lees de [!DNL Oracle] gids over [ OAuth 2.0 vergunning voor NetSuite ](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint). | `eyJr......dmxM`<br> De waarde bestaat uit een tekenreeks van 1024 tekens die is opgemaakt als JSON Web Token (JWT). |
| Toegang tot token-URL | Het symbolische eindpunt waar de toepassing de POST- verzoeken naar verzendt. | `https://{ACCOUNT_ID}.suitetalk.api.netsuite.com<br>/services/rest/auth/oauth2/v1/token` |

>[!IMPORTANT]
>
>Nadat een vernieuwingstoken verloopt, moet u een nieuw account in Experience Platform maken met uw bijgewerkte tokens.

## Verbinden [!DNL Oracle NetSuite Activities] met Experience Platform {#oracle-netsuite-activities}

In de onderstaande documentatie vindt u informatie over het tot stand brengen van een verbinding tussen [!DNL Oracle NetSuite Activities] en Experience Platform via API&#39;s of de gebruikersinterface:

* [ creeer een bronverbinding en dataflow om  [!DNL Oracle NetSuite Activities]  gegevens aan Experience Platform te brengen gebruikend APIs ](../../tutorials/api/create/marketing-automation/oracle-netsuite-activities.md).
* [ verbind uw  [!DNL Oracle NetSuite Activities]  rekening met Experience Platform gebruikend UI ](../../tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md).
* [ creeer een dataflow voor een bronverbinding gebruikend UI ](../../tutorials/ui/dataflow/marketing-automation.md).

## Verbinden [!DNL Oracle NetSuite Entities] met Experience Platform {#oracle-netsuite-entities}

In de onderstaande documentatie vindt u informatie over het tot stand brengen van een verbinding tussen [!DNL Oracle NetSuite Entities] en Experience Platform via API&#39;s of de gebruikersinterface:

* [ creeer een bronverbinding en dataflow om  [!DNL Oracle NetSuite Entities]  gegevens aan Experience Platform te brengen gebruikend APIs ](../../tutorials/api/create/marketing-automation/oracle-netsuite-entities.md).
* [ verbind uw  [!DNL Oracle NetSuite Entities]  rekening met Experience Platform gebruikend UI ](../../tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md).
* [ creeer een dataflow voor een bronverbinding gebruikend UI ](../../tutorials/ui/dataflow/marketing-automation.md).
