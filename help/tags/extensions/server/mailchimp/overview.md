---
title: Overzicht van Mailchimp-extensie
description: Met het doorsturen van gebeurtenissen kunt u e-mailberichten van Mailchimp activeren.
type: Documentation
feature: Data Collection, Event Forwarding
level: Beginner
role: User, Developer, Admin
topic: Integrations
exl-id: a52870c4-10e6-45a0-a502-f48da3398f3f
source-git-commit: bfbad3c11df64526627e4ce2d766b527df678bca
workflow-type: tm+mt
source-wordcount: '1290'
ht-degree: 1%

---

# Overzicht door:sturen van mailchimp-gebeurtenis

>[!NOTE]
>  
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html) voor een geconsolideerde referentie van de terminologische wijzigingen.

Mailchimp [gebeurtenis doorsturen](../../../ui/event-forwarding/overview.md) De extensie verzendt gebeurtenissen naar de Mailchimp Marketing-API die e-mails voor Mailchimp-marketingcampagnes, -reizen of -transacties kan activeren.

In dit document wordt beschreven hoe u de extensie instelt en regels configureert met de handeling Gebeurtenis toevoegen.

## Vereisten

In dit document wordt ervan uitgegaan dat u bekend bent met de relevante Mailchimp-producten die door de extensie zijn gebruikt. Voor meer informatie, gelieve te zien de de hulpdocumentatie van Mailchimp voor [campagnes](https://mailchimp.com/help/getting-started-with-campaigns/), [reizen](https://mailchimp.com/help/about-customer-journeys/), en [transacties](https://mailchimp.com/help/transactional/).

Een rekening Mailchimp wordt vereist om deze uitbreiding te gebruiken. U kunt zich aanmelden voor een account [hier](https://login.mailchimp.com/signup/). Noteer in het dashboard voor de Mailchimp-account de volgende waarden voor gebruik in deze handleiding:

- Uw Mailchimp-domeinvoorvoegsel
- Uw API-sleutel
- De publiek-id
- Het standaard e-mailadres &#39;van&#39;

Afhankelijk van uw plan van de Rekening van Mailchimp, kunt u beperkte toegang tot de hulpmiddelen van de Reizen van de Klant van Mailchimp hebben.

>[!TIP]
>  
>Als u de automatisering van Mailchimp zoals transactie e-mails of de Reizen van de Klant gebruikt, kunnen de stappen en de schermen lichtjes verschillend zijn dan hier vermeld. U hebt echter nog steeds dezelfde informatie nodig om deze extensie te gebruiken als hierboven is beschreven. Zie de [Mailchimp Help Center](https://mailchimp.com/help/) voor meer informatie over deze waarden voor uw specifieke account en abonnement.

### Domeinvoorvoegsel

Na het aanmelden bij Mailchimp en het landen op de mening van het Dashboard, zou de adresbar van uw browser URL als moeten tonen `https://us11.admin.mailchimp.com` of alleen `us11.admin.mailchimp.com`. In dit voorbeeld wordt het voorvoegsel `us11` is slechts een placeholder en uw waarde zal verschillend zijn. Neem de URL op met het voorvoegsel voor een latere stap.

### API-sleutel

Om de API sleutel voor uw rekening te vinden, selecteer uw profielpictogram in Mailchimp UI, dan uitgezocht **Profiel**. U moet een URL zien zoals `https://us11.admin.mailchimp.com/account/profile/` maar met **uw** voorvoegsel in plaats van `us11`.

Selecteren **Extra&#39;s** vervolgens **API-sleutels**:

![Menu Extra&#39;s, koppeling API-sleutels](../../../images/extensions/server/mailchimp/menu-API-keys.png)

Onder **Uw API-sleutels**, kunt u een bestaande toets kiezen of **Een sleutel maken** om een nieuwe te maken. U kunt een nieuwe sleutel tot stand brengen om specifiek met deze uitbreiding te gebruiken. Kopieer de API-sleutel en sla deze op voor een latere stap. Voor meer details, zie de documentatie van Mailchimp over hoe te [API-sleutel genereren](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key).

### Auditie-id en Van adres

Selecteren **Publiek** in de linkernavigatie, dan **Publiek-dashboard**. Selecteer vervolgens het publiek dat u wilt gebruiken met deze extensie. Om meer te leren, zie het document van de Brievenbus op [een publiek maken](https://mailchimp.com/help/create-audience/).

Selecteer de doelgroep **Publiek beheren** vervolgkeuzelijst en kies **Instellingen**. In dit scherm ziet u verschillende instellingen voor uw publiek.

Onder aan het scherm Instellingen ziet u `Unique id for audience [audience name]` waar `[audience name]` Dit is de naam van het werkelijke publiek. Kopieer de publiek-id en sla deze voor een latere stap op.

Selecteren **Auditienaam en standaardwaarden** en bevestigt dat **Standaard van e-mailadres** heeft de juiste waarde voor uw campagnes. De publiek-id wordt ook boven aan deze pagina vermeld en is dezelfde waarde die u in de laatste stap hebt gekopieerd.

## Mailchimp-automatisering

Afhankelijk van uw plan Mailchimp en of u transactiemails, de Reizen van de Klant, of andere automatiseringen van Mailchimp gebruikt, kunnen uw specifieke reismontages variëren.

>[!IMPORTANT]
>  
>De gebeurtenisnaam u verkoos om uw automatisering of reis in Mailchimp teweeg te brengen is de zelfde gebeurtenisnaam u met deze uitbreiding moet verzenden. Noteer de naam van de gebeurtenis in de automatisering van Mailchimp en sla deze voor een latere stap op.

## Installatie en configuratie

In deze sectie worden de stappen beschreven voor het installeren en configureren van de extensie. Om de sleutel van de Mailchimp API veilig te bewaren, moet u gebeurtenis gebruiken door:sturen [geheimen](../../../ui/event-forwarding/secrets.md).

### Een geheim en gegevenselement maken

In een gebeurtenis die bezit door:sturen, [een [!UICONTROL Token] geheim](../../../ui/event-forwarding/secrets.md#token) gebeld `Mailchimp API Key`.

Volgende, [een gegevenselement maken](../../../ui/managing-resources/data-elements.md#create-a-data-element) met de [!UICONTROL Core] en [!UICONTROL Secret] het elementtype van gegevens om naar `Mailchimp API Key` geheim dat je zojuist hebt gemaakt. Enter `Mailchimp Token` als de naam van het gegevenselement.

### De extensie installeren en configureren

In de zelfde gebeurtenis die bezit door:sturen, uitgezocht **[!UICONTROL Extensions],** dan **[!UICONTROL Catalog]** om de extensies weer te geven die beschikbaar zijn voor installatie. Van hier, onderzoek naar de uitbreiding Mailchimp en selecteer **[!UICONTROL Install]**.

![Mailchimp-extensie installeren](../../../images/extensions/server/mailchimp/install.png)

Het configuratiescherm wordt weergegeven. Onder **[!UICONTROL Mailchimp Server Prefix Domain Name]**, ga het domein in u vroeger van uw rekening Mailchimp, met inbegrip van uw uniek domeinprefix kopieerde.

>[!IMPORTANT]
>
>Niet opnemen `http://` of `https://` op dit gebied.

![Extensieconfiguratie](../../../images/extensions/server/mailchimp/mailchimp-domain.png)

Onder **[!UICONTROL Mailchimp token]**, selecteert u het pictogram van het gegevenselement en kiest u de optie `Mailchimp Token` gegevenselement dat u eerder hebt gemaakt. Selecteren **[!UICONTROL Save]** om de wijzigingen op te slaan.

De extensie is nu geïnstalleerd en geconfigureerd voor gebruik in uw eigenschap.

## Gegevensverzameling

Wanneer u deze extensie in een [regel](../../../ui/managing-resources/rules.md), zijn er verscheidene gegevenswaarden die de uitbreiding naar Mailchimp met elke gebeurtenis verzendt. Voor een typische implementatie, kunt u vormen [Adobe Experience Platform Web SDK-extensie](../../client/sdk/overview.md) om die gegevens naar [!DNL Platform Edge Network] voor gebruik door de uitbreiding in de gebeurtenis die bezit door:sturen.

De gegevens die door deze uitbreiding worden vereist kunnen van Web SDK als of gegevens worden verzonden XDM of niet-XDM. Raadpleeg de documentatie voor meer informatie over [XDM-gegevens verzenden](../../../../edge/fundamentals/tracking-events.md#sending-non-xdm-data).

Als een klant bijvoorbeeld een aankoop doet of zich registreert voor een gebeurtenis op uw site, kunt u een bevestigingsbericht verzenden via Mailchimp met deze extensie. Zodra u de vereiste informatie van Web SDK naar het Netwerk van de Rand verzendt, brengt de uitbreiding e-mail met Mailchimp in werking.

![Configuratie van gebeurtenisactie toevoegen](../../../images/extensions/server/mailchimp/action-configurations.png)

### Gegevenselementen

Het schermafbeelding in de vorige sectie toont de gegevens die u met elke gebeurtenis van deze extensie naar Mailchimp kunt verzenden. Zodra u het Web SDK vormt om deze gegevens naar het Netwerk van de Rand te verzenden, kunt u gegevenselementen in het gebeurtenis creëren door:sturen bezit zodat kan de uitbreiding tot die waarden toegang hebben.

In de onderstaande tabel vindt u meer details voor elke mogelijke waarde.

| Naam | Voorbeeldpad | Type | Beschrijving | Vereist | Limieten |
|:---|:---:|:---:|:---|:---:|:---|
| `email` | `arc.event.xdm._tenant.emailId`<br /> of<br /> `arc.event.data._tenant.emailId` | Tekenreeks | Het adres dat de e-mail ontvangt | **Ja** | Moet in het Publiek Mailchimp bestaan |
| `listId` | `arc.event.xdm._tenant.listId`<br /> of<br /> `arc.event.data._tenant.listid` | Tekenreeks | Id van publiek | **Ja** | Moet overeenkomen met een bestaande publiek-id |
| `name` | `arc.event.xdm._tenant.name`<br /> of<br /> `arc.event.data._tenant.name` | Tekenreeks | De naam van de gebeurtenis | **Ja** | 2-30 tekens lang |
| `properties` | `arc.event.xdm._tenant.properties`<br /> of<br /> `arc.event.data._tenant.properties` | Object | Een optionele lijst met eigenschappen in JSON-indeling met informatie over de gebeurtenis | Nee |  |
| `isSyncing` | `arc.event.xdm._tenant.isSyncing`<br /> of<br /> `arc.event.data._tenant.isSyncing` | boolean | Gebeurtenissen gemaakt met `is_syncing` instellen op `true` **niet** triggerautomatisering | Nee |  |
| `occurredAt` | `arc.event.xdm._tenant.occuredAt`<br /> of `arc.event.data._tenant.occuredAt` | Tekenreeks | Een ISO 8601-tijdstempel van wanneer de gebeurtenis heeft plaatsgevonden | Nee |  |

{style=&quot;table-layout:auto&quot;}

>[!IMPORTANT]
>  
>De **Voorbeeldpad** bovenstaande waarden zijn alleen voorbeelden. De veldnamen en [paden](../../../ui/event-forwarding/overview.md#data-element-path) van verwijzingen voorzien in die gegevenselementen kunnen in uw bezit verschillend zijn, afhankelijk van hoe u genoemd en Web SDK in de stappen hierboven vormde.

In uw gebeurtenis die bezit door:sturen, kunt u een gegevenselement voor elk van de hierboven geschetste gebieden tot stand brengen. Nadat u de gegevenselementen hebt gemaakt, kunt u verwijzen naar de gegevenselementen in het dialoogvenster [!UICONTROL Add Event] actie van deze verlenging.

![Configuratie van gebeurtenisactie toevoegen](../../../images/extensions/server/mailchimp/action-configurations.png)

U kunt deze extensie en de handeling Gebeurtenis toevoegen nu gebruiken om mailchimp-e-mails voor uw publiek te activeren.

## Gegevensvalidatie

Wanneer u werkt met het doorsturen van extensies voor gebeurtenissen, [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) is zeer nuttig. In de sectie Logs, onder de logboeken van de Rand kunt u de verzoeken zien die door uw gebeurtenis door:sturen regels worden gemaakt nadat zij worden teweeggebracht. De volgende schermafbeeldingen tonen een verzoek dat aan Mailchimp API door de uitbreiding wordt gedaan.

![Adobe Experience Platform Debugger](../../../images/extensions/server/mailchimp/debugger-edge-logs.png)

In het dashboard van Mailchimp, op de mening van de Voeding van de Activiteit van uw Publiek of Lid van het Publiek, wordt een lijst van gebeurtenissen voor dat Publiek of Lid van het Publiek verstrekt. Dit moet overeenkomen met de gebeurtenissen die door de extensie zijn verzonden en met eventuele optionele gegevens die samen met de e-mail of campagne zijn verzonden die ze hebben ontvangen. Zie de [Hulplijnen voor Help bij Mailchimp Automation](https://mailchimp.com/help/automation/) voor meer informatie .
