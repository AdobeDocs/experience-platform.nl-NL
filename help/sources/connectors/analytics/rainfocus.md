---
title: Overzicht van RainFocus-bron
description: Leer hoe u gebeurtenisbeheer- en analysegegevens van uw RainFocus-account naar Experience Platform kunt brengen
last-substantial-update: 2023-06-21T00:00:00Z
badge: Beta
exl-id: 88e333e3-2b93-4d66-8412-efadea58ac46
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 4%

---

# [!DNL RainFocus]

>[!NOTE]
>
>De [!DNL RainFocus] De bron is in bèta. Lees de [overzicht van bronnen](../../home.md#terms-and-conditions) voor meer informatie over het gebruik van bronnen met een bètalabel.

[!DNL RainFocus] is een platform dat u kunt gebruiken om uw gebeurtenissen te promoten en uw publiek op te bouwen. U kunt [!DNL RainFocus] om mooie promotiepagina&#39;s te maken, de campagneprestaties bij te houden en de omzettingen van de registratie te optimaliseren.

Gebruik de [!DNL RainFocus] bron in Adobe Experience Platform en Real-time Customer Data Platform om uw gegevensprofielen voor klanten automatisch te verrijken met gebeurtenissen voor deelnemers in real-time. Zodra toegelaten, worden de ervaringsgebeurtenissen automatisch gestroomd in Real-Time CDP, die voor krachtige publiekssegmentatie, gegevensanalyse, en activering van de deelnemersreis met stroomafwaartse bestemmingen en toepassingen zoals Customer Journey Analytics en Adobe Journey Optimizer toestaan.

>[!IMPORTANT]
>
>Deze bronschakelaar en documentatiepagina worden gecreeerd en gehandhaafd door [!DNL RainFocus] team. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen met de klant<span>@rainfocus.com of ga naar de [[!DNL RainFocus] Help Center](https://help.rainfocus.com/hc/en-us)

## Vereisten

U moet aan de volgende voorwaarden voldoen voordat u de [!DNL RainFocus] integratie op Experience Platform :

[Een Adobe Service-account (JWT) maken in de Adobe Developer Portal](https://developer.adobe.com/developer-console/docs/guides/authentication/ServiceAccountIntegration/)

>[!IMPORTANT]
>
>Adobe heeft onlangs aangekondigd dat JWT-tokens ten gunste van OAuth zijn afgeschaft. Om deze wijziging aan te kunnen, [!DNL RainFocus] de bron zal in de nabije toekomst naar OAuth migreren .

### Vereiste referenties verzamelen

Om verbinding te maken [!DNL RainFocus] aan Experience Platform, moet u waarden voor de volgende verbindingseigenschappen verstrekken in [!DNL RainFocus]:

| Credentials | Beschrijving | Voorbeeld |
| --- | --- | --- |
| Client-id | De client-id is verkrijgbaar via de Adobe Service-account in de Adobe Developer Portal. | `b9c32a63e7d41a0f87d3e8b52a16e7a2` |
| Clientgeheim | Het clientgeheim kan worden verkregen via de Adobe Service-account in de Adobe Developer Portal. | `k1b-p-umplcjtg_arnw-R-Bx44bybu` |
| Technisch account-id | De technische account-id kunt u verkrijgen via de Adobe Service-account op de Adobe Developer Portal. | `B3F9D2E8A64C573D21ABFE97@techacct.adobe.com` |
| Organisatie-ID | De organisatie-id is verkrijgbaar via de Adobe Service-account in de Adobe Developer Portal | `D9A6F3BCE82FD147C50E3A19@techacct.adobe.com` |

### Een XDM-schema maken en het identiteitsveld definiëren {#create-an-xdm-schema-and-define-the-identity-field}

Voor het opslaan van de Experience Events van [!DNL RainFocus] in Experience Platform, moet u een schema van de Gegevens van de Ervaring van het Model (XDM) creëren om een dataset te beschrijven die de mogelijke gebieden en gegevenstypes kan opslaan die van zullen worden verzonden [!DNL RainFocus].

[!DNL RainFocus] beveelt de volgende velden aan, die alle mogelijke gegevens bestrijken die standaard worden verzonden.

De volgende veldgroepen worden ook aanbevolen (aangeduid met een voorvoegsel):

* Aanwezigen
* Exhibitor
* Lood
* Sessie
* SessionTime

**Het schema moet de volgende velden bevatten:**

| Veld | Type | Voorbeeld | Beschrijving |
| --- | --- | --- | --- |
| `attendee.registered` | Tekenreeks | Ja | Een markering die bepaalt of de deelnemer wordt beschouwd als geregistreerd. |
| `attendee.attendeeId` | Tekenreeks | 1619119968857001fvLB | De deelnemer-id in [!DNL RainFocus]. |
| `attendee.externalId` | Tekenreeks | 1666809456617001wyPj | De externe id die door een organisatie is opgegeven. |
| `attendee.clientId` | Tekenreeks | 8EFC1F57631CAFE70A495ECB@8f3f1f5c631caf3e495fd8.e | De client-id van de SSO-deelnemer. |
| `attendee.email` | Tekenreeks | user<span>@company.com | Het e-mailadres van de deelnemer. |
| `transmissionId` | Tekenreeks | 1680309557133001YHhz | Een unieke id die wordt gebruikt voor gegevenspush. |
| `eventType` | Tekenreeks | SessionScheduled | De naam van de gebeurtenis Deelnemerervaring. |
| `timestamp` | DateTime | 2023-04-01T00:41:57.000Z | De tijdstempel van de gegevenspush. |
| `event.name` | Tekenreeks | Adobe Summit 2023 | De naam van de gebeurtenis waarin een overdracht heeft plaatsgevonden. |
| `exhibitor.exhibitorId` | Tekenreeks | 1680309557133001YHhz | De [!DNL RainFocus] id van de exposant. |
| `exhibitor.externalId` | Tekenreeks | 1666809514105001lSJN | De id voor de exposant in het clientsysteem. |
| `exhibitor.name` | Tekenreeks | IBM | De naam van de exposant. |
| `lead.leadId` | Tekenreeks | 1666809456617001wyPj | De [!DNL RainFocus] id voor de lead. |
| `lead.note` | Tekenreeks | | |
| `session.sessionId` | Tekenreeks | 1666809373585001t4aV | De [!DNL RainFocus] id voor de sessie. |
| `session.externalId` | Tekenreeks | 1666809456617001wyPj | De id voor de sessie in het clientsysteem. |
| `session.code` | Tekenreeks | GS3 | De code voor de sessie. |
| `session.title` | Tekenreeks | Inspiration Keynote | De titel van de sessie. |
| `session.length` | Geheel | 90 | De duur van de sessie. |
| `sessiontime.sessiontimeId` | Tekenreeks | 1673033149739001OJLZ | De [!DNL RainFocus] id voor de sessietijd. |
| `sessiontime.startTime` | Tekenreeks | 2023-03-22 10:00:00 | De begintijd van de sessie. |
| `sessiontime.endTime` | Tekenreeks | 2023-03-22 10:00:00 | De eindtijd van de sessie. |
| `sessiontime.room` | Tekenreeks | B32 | De ruimte die voor de sessie wordt gebruikt. |

{style="table-layout:auto"}

Uw schema maken voor [!DNL RainFocus] Lees de volgende documentatie voor stappen over het maken van een schema met behulp van API&#39;s of de gebruikersinterface.

* [Het schema maken met de gebruikersinterface](../../../xdm/tutorials/create-schema-ui.md)
* [Het schema maken met de API](../../../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>* Het schema moet de **XDM ExperienceEvent-klasse.**
>* U moet ervoor zorgen dat het schema een **primaire identiteit**, en is **ingeschakeld voor profiel**. Lees voor meer informatie de handleiding op [identiteitsvelden definiëren in de gebruikersinterface](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/fields/identity.html)
>* U kunt de voorbeeldidentiteit (e-mail) vervangen voor een andere relevante id, zoals een sha256-e-mail of ECID.

### Een integratieprofiel maken in RainFocus {#create-an-integration-profile-in-rainfocus}

Als uw serviceaccount en uw XDM-schema klaar zijn, kunt u nu het [!DNL Integration Profile] via de [!DNL RainFocus] platform. De [!DNL Integration Profile] is verantwoordelijk voor het streamen van gegevens naar het Experience Platform.

Aanmelden bij [[!DNL RainFocus] platform](https://app.rainfocus.com). Selecteer in de primaire navigatie de optie **[!DNL Libraries]** en selecteer vervolgens **[!DNL Integration Profiles]**

![De interface RainFocus met bibliotheken en integratieprofielen geselecteerd.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile.png)

Als u een nieuw profiel wilt maken, selecteert u de **(`+`)** pictogram. Selecteer vervolgens **Adobe Real-time Customer Data Platform** en selecteer vervolgens **OK**.

![Het venster voor het maken van een integratieprofiel in de RainFocus-gebruikersinterface.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-select.png)

Geef vervolgens de gegevens op die u hebt opgehaald in het Adobe Developer Portal-project:

* **Client-id**
* **Clientgeheim**
* **Technisch account-id**
* **Organisatie-ID**

Als de referenties eenmaal zijn opgegeven, selecteert u **[!DNL Save]** U moet nu de nieuwe [!DNL Integration Profile] in de lijst [!DNL RainFocus] dashboard.

Selecteer de [!DNL Integration Profile] die u net hebt gemaakt om een lijst met vooraf gedefinieerde **push-typen** al geconfigureerd. Dit zijn de [Experience Events](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/experienceevent.html) die naar het Experience Platform worden verzonden wanneer zij zich voordoen.

![Een lijst met vooraf gedefinieerde pushtypen in het RainFocus-dashboard.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-setup.png)

Selecteer **[!DNL Sample JSON Payload]**. Markeer en kopieer vervolgens de JSON-voorbeeldlading en **opslaan in een nieuw bestand met de extensie .json**. Dit wordt later in het Experience Platform gebruikt voor [toewijzingsconfiguraties](../../tutorials/ui/create/analytics/rainfocus.md#mapping).

![Een voorbeeld van JSON-lading in het RainFocus-dashboard.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-json.png)

>[!TIP]
>
>**Setup is nog niet voltooid**: Nadat u de gegevensstroom hebt gemaakt, moet u terugkeren naar de map [!DNL RainFocus] dashboard om uw [!DNL Integration Profile] door uw **URL streamingeindpunt** en **dataflow-id**.

## Volgende stappen

Door dit document te lezen, hebt u de vereiste instellingen voltooid die nodig zijn om gegevens te kunnen streamen vanaf uw [!DNL RainFocus] aan Experience Platform. U kunt nu doorgaan naar de handleiding op [verbinden [!DNL RainFocus] naar Experience Platform via de gebruikersinterface](../../tutorials/ui/create/analytics/rainfocus.md).
