---
title: Overzicht van RainFocus-bron
description: Leer hoe u gebeurtenisbeheer- en analysegegevens van uw RainFocus-account naar Experience Platform kunt brengen
last-substantial-update: 2023-06-21T00:00:00Z
badge: Beta
exl-id: 88e333e3-2b93-4d66-8412-efadea58ac46
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 0%

---

# [!DNL RainFocus]

>[!NOTE]
>
>De bron [!DNL RainFocus] is in bèta. Gelieve te lezen het [ overzicht van bronnen ](../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde bronnen.

[!DNL RainFocus] is een platform dat u kunt gebruiken om uw gebeurtenissen te promoten en uw publiek op te bouwen. Met [!DNL RainFocus] kunt u prachtige promotiepagina&#39;s maken, de prestaties van campagnes bijhouden en de omzettingen van registraties optimaliseren.

Gebruik de [!DNL RainFocus] -bron in Adobe Experience Platform en Real-time Customer Data Platform om uw gegevensprofielen van klanten automatisch te verrijken met gebeurtenissen in real-time voor deelnemers. Zodra toegelaten, worden de ervaringsgebeurtenissen automatisch gestroomd in Real-Time CDP, die voor krachtige publiekssegmentatie, gegevensanalyse, en activering van de deelnemersreis met stroomafwaartse bestemmingen en toepassingen zoals Customer Journey Analytics en Adobe Journey Optimizer toestaan.

>[!IMPORTANT]
>
>Deze bronaansluiting en documentatiepagina worden gemaakt en onderhouden door het team van [!DNL RainFocus] . Voor om het even welke onderzoeken of updateverzoeken, gelieve hen direct bij cliëntcare <span> te contacteren@rainfocus.com of het [[!DNL RainFocus]  Centrum van de Hulp ](https://help.rainfocus.com/hc/en-us) te bezoeken

## Vereisten

U moet aan de volgende voorwaarden voldoen voordat u de [!DNL RainFocus] -integratie op het Experience Platform kunt activeren:

[ creeer een Rekening van de Dienst van Adobe (JWT) in het Portaal van Adobe Developer ](https://developer.adobe.com/developer-console/docs/guides/authentication/ServiceAccountIntegration/)

>[!IMPORTANT]
>
>Adobe heeft onlangs aangekondigd dat JWT-tokens ten gunste van OAuth zijn afgeschaft. Om deze wijziging aan te kunnen, zal de [!DNL RainFocus] -bron in de nabije toekomst naar OAuth migreren.

### Vereiste referenties verzamelen

Als u [!DNL RainFocus] wilt verbinden met een Experience Platform, moet u waarden opgeven voor de volgende verbindingseigenschappen in [!DNL RainFocus] :

| Credentials | Beschrijving | Voorbeeld |
| --- | --- | --- |
| Client-id | De client-id is verkrijgbaar via de Adobe Service-account in de Adobe Developer Portal. | `b9c32a63e7d41a0f87d3e8b52a16e7a2` |
| Clientgeheim | Het clientgeheim kan worden verkregen via de Adobe Service-account in de Adobe Developer Portal. | `k1b-p-umplcjtg_arnw-R-Bx44bybu` |
| Technisch account-id | De technische account-id kunt u verkrijgen via de Adobe Service-account op de Adobe Developer Portal. | `B3F9D2E8A64C573D21ABFE97@techacct.adobe.com` |
| Organisatie-ID | De organisatie-id is verkrijgbaar via de Adobe Service-account in de Adobe Developer Portal | `D9A6F3BCE82FD147C50E3A19@techacct.adobe.com` |

### Een XDM-schema maken en het identiteitsveld definiëren {#create-an-xdm-schema-and-define-the-identity-field}

Als u de Experience Events vanaf [!DNL RainFocus] in het Experience Platform wilt opslaan, moet u een XDM-schema (Experience Data Model) maken om een gegevensset te beschrijven die de mogelijke velden en gegevenstypen kan opslaan die vanuit [!DNL RainFocus] worden verzonden.

[!DNL RainFocus] raadt de volgende velden aan, die alle mogelijke gegevens bestrijken die standaard worden verzonden.

De volgende veldgroepen worden ook aanbevolen (aangeduid met een voorvoegsel):

* Aanwezigen
* Exhibitor
* Lood
* Sessie
* SessionTime

**het schema zou de volgende gebieden moeten bevatten:**

| Veld | Type | Voorbeeld | Beschrijving |
| --- | --- | --- | --- |
| `attendee.registered` | String | Ja | Een markering die bepaalt of de deelnemer wordt beschouwd als geregistreerd. |
| `attendee.attendeeId` | String | 1619119968857001fvLB | De deelnemer-id in [!DNL RainFocus] . |
| `attendee.externalId` | String | 1666809456617001wyPj | De externe id die door een organisatie is opgegeven. |
| `attendee.clientId` | String | 8EFC1F57631CAFE70A495ECB@8f3f1f5c631caf3e495fd8.e | De client-id van de SSO-deelnemer. |
| `attendee.email` | String | gebruiker<span>@company.com | Het e-mailadres van de deelnemer. |
| `transmissionId` | String | 1680309557133001YHhz | Een unieke id die wordt gebruikt voor gegevenspush. |
| `eventType` | String | SessionScheduled | De naam van de gebeurtenis Deelnemerervaring. |
| `timestamp` | DateTime | 2023-04-01T00 :41: 57.000Z | De tijdstempel van de gegevenspush. |
| `event.name` | String | Adobe Summit 2023 | De naam van de gebeurtenis waarin een overdracht heeft plaatsgevonden. |
| `exhibitor.exhibitorId` | String | 1680309557133001YHhz | De [!DNL RainFocus] -id van de exposant. |
| `exhibitor.externalId` | String | 1666809514105001lSJN | De id voor de exposant in het clientsysteem. |
| `exhibitor.name` | String | IBM | De naam van de exposant. |
| `lead.leadId` | String | 1666809456617001wyPj | De [!DNL RainFocus] -id voor de lead. |
| `lead.note` | String | | |
| `session.sessionId` | String | 1666809373585001t4aV | De [!DNL RainFocus]-id voor de sessie. |
| `session.externalId` | String | 1666809456617001wyPj | De id voor de sessie in het clientsysteem. |
| `session.code` | String | GS3 | De code voor de sessie. |
| `session.title` | String | Inspiration Keynote | De titel van de sessie. |
| `session.length` | Geheel | 90 | De duur van de sessie. |
| `sessiontime.sessiontimeId` | String | 1673033149739001OJLZ | De [!DNL RainFocus]-id voor de sessietijd. |
| `sessiontime.startTime` | String | 2023-03-22 10 :00: 00 | De begintijd van de sessie. |
| `sessiontime.endTime` | String | 2023-03-22 10 :00: 00 | De eindtijd van de sessie. |
| `sessiontime.room` | String | B32 | De ruimte die voor de sessie wordt gebruikt. |

{style="table-layout:auto"}

Als u uw schema voor [!DNL RainFocus] gegevens wilt maken, leest u de volgende documentatie voor stappen over het maken van een schema met behulp van API&#39;s of de gebruikersinterface.

* [Het schema maken met de gebruikersinterface](../../../xdm/tutorials/create-schema-ui.md)
* [Het schema maken met de API](../../../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>* Het schema moet de **klasse uitbreiden XDM ExperienceEvent.**
>* U moet ervoor zorgen dat het schema a **primaire identiteit** omvat, en **toegelaten voor Profiel** is. Voor meer informatie, lees de gids op [ bepalende identiteitsgebieden in UI ](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/fields/identity.html)
>* U kunt de voorbeeldidentiteit (e-mail) vervangen voor een andere relevante id, zoals een sha256-e-mail of ECID.

### Een integratieprofiel maken in RainFocus {#create-an-integration-profile-in-rainfocus}

Zodra uw serviceaccount en uw XDM-schema klaar zijn, kunt u [!DNL Integration Profile] nu activeren via het [!DNL RainFocus] -platform. De [!DNL Integration Profile] is verantwoordelijk voor het streamen van gegevens naar het Experience Platform.

Logboek in het [[!DNL RainFocus]  platform ](https://app.rainfocus.com). Selecteer in de primaire navigatie **[!DNL Libraries]** en selecteer vervolgens **[!DNL Integration Profiles]**

![ RainFocus UI met Geselecteerde Bibliotheken en de Profielen van de Integratie.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile.png)

Om een nieuw profiel tot stand te brengen, selecteer **(`+`)** pictogram. Daarna, selecteer **Adobe Real-time Customer Data Platform** en selecteer dan **O.K.**.

![ creeer het venster van het integratieprofiel in RainFocus UI.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-select.png)

Geef vervolgens de gegevens op die u hebt opgehaald in het Adobe Developer Portal-project:

* **identiteitskaart van de Cliënt**
* **Geheim van de Cliënt**
* **identiteitskaart van de Technische Rekening**
* **identiteitskaart van de Organisatie**

Nadat de referenties zijn opgegeven, selecteert u **[!DNL Save]** . U ziet nu de nieuwe [!DNL Integration Profile] in het dashboard van [!DNL RainFocus] .

Selecteer [!DNL Integration Profile] dat u enkel creeerde om een lijst van vooraf bepaalde **duw types** te zien reeds gevormd. Dit zijn de [ Gebeurtenissen van de Ervaring ](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/experienceevent.html) die naar Experience Platform zullen worden verzonden wanneer zij voorkomen.

![ een lijst van vooraf bepaalde duptypes in het dashboard RainFocus.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-setup.png)

Selecteer **[!DNL Sample JSON Payload]** als u een kopie van de JSON-voorbeeldlading wilt ophalen. Daarna, benadruk en kopieer de steekproefJSON nuttige lading en **bewaar het in een nieuw dossier met een uitbreiding .json**. Dit zal later in Experience Platform voor [ kaartconfiguraties ](../../tutorials/ui/create/analytics/rainfocus.md#mapping) worden gebruikt.

![ een steekproefJSON nuttige lading in het dashboard RainFocus.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-json.png)

>[!TIP]
>
>**Opstelling is nog niet volledig**: Zodra uw dataflow wordt gecreeerd, zult u aan het [!DNL RainFocus] dashboard moeten terugkeren om uw [!DNL Integration Profile] te voltooien door uw **het stromen eindpunt URL** en **dataflow identiteitskaart** te verstrekken.

## Volgende stappen

Door dit document te lezen, hebt u de vereiste instellingen voltooid om gegevens van uw [!DNL RainFocus] -account naar het Experience Platform te kunnen streamen. U kunt aan de gids nu te werk gaan op [ verbindend  [!DNL RainFocus]  met Experience Platform gebruikend het gebruikersinterface ](../../tutorials/ui/create/analytics/rainfocus.md).
