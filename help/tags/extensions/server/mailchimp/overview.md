---
title: Overzicht van Mailchimp-extensie
description: Met het doorsturen van gebeurtenissen kunt u e-mailberichten van Mailchimp activeren.
type: Documentation
feature: Data Collection, Event Forwarding
level: Beginner
role: User, Developer, Admin
topic: Integrations
exl-id: a52870c4-10e6-45a0-a502-f48da3398f3f
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '1205'
ht-degree: 0%

---

# Overzicht door:sturen van mailchimp-gebeurtenis

De gebeurtenis die van de Brievenchimp [ ](../../../ui/event-forwarding/overview.md) uitbreiding door:sturen verzendt gebeurtenissen naar de Marketing API van Mailchimp die e-mails voor de marketing van Mailchimp campagnes, reizen, of transacties kan teweegbrengen.

In dit document wordt beschreven hoe u de extensie instelt en regels configureert met de handeling Gebeurtenis toevoegen.

## Vereisten

In dit document wordt ervan uitgegaan dat u bekend bent met de relevante Mailchimp-producten die door de extensie zijn gebruikt. Voor meer informatie, te zien gelieve de de hulpdocumentatie van Mailchimp voor [ campagnes ](https://mailchimp.com/help/getting-started-with-campaigns/), [ reizen ](https://mailchimp.com/help/about-customer-journeys/), en [ transacties ](https://mailchimp.com/help/transactional/).

Een rekening Mailchimp wordt vereist om deze uitbreiding te gebruiken. U kunt omhoog voor een rekening [ hier ](https://login.mailchimp.com/signup/) ondertekenen. Noteer in het dashboard voor de Mailchimp-account de volgende waarden voor gebruik in deze handleiding:

- Uw Mailchimp-domeinvoorvoegsel
- Uw API-sleutel
- De publiek-id
- Het standaard e-mailadres &#39;van&#39;

Afhankelijk van uw plan van de Rekening van Mailchimp, kunt u beperkte toegang tot de hulpmiddelen van de Reizen van de Klant van Mailchimp hebben.

>[!TIP]
>  
>Als u de automatisering van Mailchimp zoals transactie e-mails of de Reizen van de Klant gebruikt, kunnen de stappen en de schermen lichtjes verschillend zijn dan hier vermeld. U hebt echter nog steeds dezelfde informatie nodig om deze extensie te gebruiken als hierboven is beschreven. Zie het [ Centrum van de Hulp van Mailchimp ](https://mailchimp.com/help/) voor details op elk van deze waarden voor uw specifieke rekening en plan.

### Domeinvoorvoegsel

Nadat u zich hebt aangemeld bij Mailchimp en hebt gepost op de dashboardweergave, geeft de adresbalk van uw browser een URL weer zoals `https://us11.admin.mailchimp.com` of alleen `us11.admin.mailchimp.com` . In dit voorbeeld is het voorvoegsel `us11` slechts een plaatsaanduiding en is de waarde anders. Neem de URL op met het voorvoegsel voor een latere stap.

### API-sleutel

Om de API sleutel voor uw rekening te vinden, selecteer uw profielpictogram in Mailchimp UI, dan uitgezocht **Profiel**. U zou een URL als `https://us11.admin.mailchimp.com/account/profile/` maar met **moeten zien uw** prefix in plaats van `us11`.

Selecteer **Extra&#39;s**, toen **API sleutels**:

![ het menu van Extra&#39;s, API sleutelverbinding ](../../../images/extensions/server/mailchimp/menu-API-keys.png)

Onder **Uw API sleutels**, kunt u een bestaande sleutel kiezen of u kunt selecteren **een Sleutel** creëren om nieuwe tot stand te brengen. U kunt een nieuwe sleutel tot stand brengen om specifiek met deze uitbreiding te gebruiken. Kopieer de API-sleutel en sla deze op voor een latere stap. Voor meer details, zie de documentatie van Mailchimp op hoe te [ uw API sleutel ](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key) produceren.

### Auditie-id en Van adres

Selecteer **Publiek** in de linkernavigatie, toen **het dashboard van de Publiek**. Selecteer vervolgens het publiek dat u wilt gebruiken met deze extensie. Om meer te leren, zie het document van de Brievenbus op [ creërend een publiek ](https://mailchimp.com/help/create-audience/).

Met uw die publiek wordt gecreeerd en wordt geselecteerd, selecteer **leiden Publiek** dropdown en kies **Montages**. In dit scherm ziet u verschillende instellingen voor uw publiek.

Onder aan het scherm Instellingen ziet u `Unique id for audience [audience name]` waar `[audience name]` de naam van het werkelijke publiek is. Kopieer de publiek-id en sla deze voor een latere stap op.

Selecteer {de naam en de gebreken van het publiek 0} publiek **en bevestig dat** Gebrek van e-mailadres **de correcte waarde voor uw campagnes heeft.** De publiek-id wordt ook boven aan deze pagina vermeld en is dezelfde waarde die u in de laatste stap hebt gekopieerd.

## Mailchimp-automatisering

Afhankelijk van uw plan Mailchimp en of u transactiemails, de Reizen van de Klant, of andere automatiseringen van Mailchimp gebruikt, kunnen uw specifieke reismontages variëren.

>[!IMPORTANT]
>  
>De gebeurtenisnaam u verkoos om uw automatisering of reis in Mailchimp teweeg te brengen is de zelfde gebeurtenisnaam u met deze uitbreiding moet verzenden. Noteer de naam van de gebeurtenis in de automatisering van Mailchimp en sla deze voor een latere stap op.

## Installatie en configuratie

In deze sectie worden de stappen beschreven voor het installeren en configureren van de extensie. Om veilig de sleutel van de Brievenchimp API te bewaren, moet u gebeurtenis gebruiken door:sturen [ geheimen ](../../../ui/event-forwarding/secrets.md).

### Een geheim en gegevenselement maken

In een gebeurtenis die bezit door:sturen, [ creeer a [!UICONTROL Token] geheim ](../../../ui/event-forwarding/secrets.md#token) geroepen `Mailchimp API Key`.

Daarna, [ creeer een gegevenselement ](../../../ui/managing-resources/data-elements.md#create-a-data-element) gebruikend de [!UICONTROL Core] uitbreiding en een [!UICONTROL Secret] type van gegevenselement om naar het `Mailchimp API Key` geheim te verwijzen u enkel creeerde. Voer `Mailchimp Token` in als de naam van het gegevenselement.

### De extensie installeren en configureren

In de zelfde gebeurtenis die bezit door:sturen, uitgezocht **[!UICONTROL Extensions],** toen **[!UICONTROL Catalog]** om de uitbreidingen te tonen beschikbaar voor installatie. Van hier, onderzoek naar de uitbreiding Mailchimp en selecteer **[!UICONTROL Install]**.

![ installeer de uitbreiding van Mailchimp ](../../../images/extensions/server/mailchimp/install.png)

Het configuratiescherm wordt weergegeven. Voer onder **[!UICONTROL Mailchimp Server Prefix Domain Name]** het domein in dat u eerder van uw Mailchimp-account hebt gekopieerd, inclusief het unieke domeinvoorvoegsel.

>[!IMPORTANT]
>
>Neem `http://` of `https://` niet op in dit veld.

![ de configuratie van de Uitbreiding ](../../../images/extensions/server/mailchimp/mailchimp-domain.png)

Selecteer onder **[!UICONTROL Mailchimp token]** het pictogram voor het gegevenselement en kies het `Mailchimp Token` -gegevenselement dat u eerder hebt gemaakt. Selecteer **[!UICONTROL Save]** om de wijzigingen op te slaan.

De extensie is nu geïnstalleerd en geconfigureerd voor gebruik in uw eigenschap.

## Dataverzameling

Wanneer het gebruiken van deze uitbreiding in a [ regel ](../../../ui/managing-resources/rules.md), zijn er verscheidene gegevenswaarden die de uitbreiding naar Mailchimp met elke gebeurtenis verzendt. Voor een typische implementatie, kunt u de [ uitbreiding van SDK van het Web van Adobe Experience Platform ](../../client/web-sdk/overview.md) vormen om die gegevens naar [!DNL Experience Platform Edge Network] voor gebruik door de uitbreiding in de gebeurtenis te verzenden die bezit door:sturen.

De gegevens die door deze extensie worden vereist, kunnen vanuit Web SDK worden verzonden als XDM-gegevens (met behulp van het [`xdm`](/help/collection/js/commands/sendevent/xdm.md) -object) of als niet-XDM-gegevens (met behulp van het [`data`](/help/collection/js/commands/sendevent/data.md) -object).

Als een klant bijvoorbeeld een aankoop doet of zich registreert voor een gebeurtenis op uw site, kunt u een bevestigingsbericht verzenden via Mailchimp met deze extensie. Zodra u de vereiste informatie van Web SDK naar Edge Network verzendt, teweegbrengt de uitbreiding e-mail met Mailchimp in werking.

![ voeg de actieconfiguratie van de Gebeurtenis ](../../../images/extensions/server/mailchimp/action-configurations.png) toe

### Gegevenselementen

Het schermafbeelding in de vorige sectie toont de gegevens die u met elke gebeurtenis van deze extensie naar Mailchimp kunt verzenden. Zodra u SDK van het Web vormt om deze gegevens naar Edge Network te verzenden, kunt u gegevenselementen in de gebeurtenis tot stand brengen die bezit door:sturen zodat kan de uitbreiding tot die waarden toegang hebben.

In de onderstaande tabel vindt u meer details voor elke mogelijke waarde.

| Naam | Voorbeeldpad | Type | Beschrijving | Vereist | Limieten |
|:---|:---:|:---:|:---|:---:|:---|
| `email` | `arc.event.xdm._tenant.emailId`<br /> of <br /> `arc.event.data._tenant.emailId` | String | Het adres dat de e-mail ontvangt | **ja** | Moet in het Publiek Mailchimp bestaan |
| `listId` | `arc.event.xdm._tenant.listId`<br /> of <br /> `arc.event.data._tenant.listid` | String | Id van publiek | **ja** | Moet overeenkomen met een bestaande publiek-id |
| `name` | `arc.event.xdm._tenant.name`<br /> of <br /> `arc.event.data._tenant.name` | String | De naam van de gebeurtenis | **ja** | 2-30 tekens lang |
| `properties` | `arc.event.xdm._tenant.properties`<br /> of <br /> `arc.event.data._tenant.properties` | Object | Een optionele lijst met eigenschappen in JSON-indeling met informatie over de gebeurtenis | Nee |  |
| `isSyncing` | `arc.event.xdm._tenant.isSyncing`<br /> of <br /> `arc.event.data._tenant.isSyncing` | boolean | Gebeurtenissen die zijn gemaakt met `is_syncing` ingesteld op `true` **, activeren geen** signaalautomatisering | Nee |  |
| `occurredAt` | `arc.event.xdm._tenant.occuredAt`<br /> of `arc.event.data._tenant.occuredAt` | String | Een ISO 8601-tijdstempel van wanneer de gebeurtenis heeft plaatsgevonden | Nee |  |

{style="table-layout:auto"}

>[!IMPORTANT]
>  
>De **hierboven waarden van de weg van het 0} Voorbeeld {zijn slechts voorbeelden.** De gebiedsnamen en [ wegen ](../../../ui/event-forwarding/overview.md#data-element-path) die in die gegevenselementen van verwijzingen worden voorzien kunnen in uw bezit verschillend zijn, afhankelijk van hoe u genoemd en Web SDK in de stappen hierboven vormde.

In uw gebeurtenis die bezit door:sturen, kunt u een gegevenselement voor elk van de hierboven geschetste gebieden tot stand brengen. Nadat u een extensie hebt gemaakt, kunt u verwijzen naar de gegevenselementen in de handeling [!UICONTROL Add Event] van deze extensie.

![ voeg de actieconfiguratie van de Gebeurtenis ](../../../images/extensions/server/mailchimp/action-configurations.png) toe

U kunt deze extensie en de handeling Gebeurtenis toevoegen nu gebruiken om mailchimp-e-mails voor uw publiek te activeren.

## Gegevensvalidatie

Wanneer het werken met gebeurtenis die uitbreidingen door:sturen, is [ Adobe Experience Platform Debugger ](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) zeer nuttig. In de sectie Logs, onder de logboeken van Edge kunt u de verzoeken zien die door uw gebeurtenis door:sturen regels worden gemaakt nadat zij worden teweeggebracht. De volgende schermafbeeldingen tonen een verzoek dat aan Mailchimp API door de uitbreiding wordt gedaan.

![ Adobe Experience Platform Debugger ](../../../images/extensions/server/mailchimp/debugger-edge-logs.png)

In het dashboard van Mailchimp, op de mening van de Voeding van de Activiteit van uw Publiek of Lid van het Publiek, wordt een lijst van gebeurtenissen voor dat Publiek of Lid van het Publiek verstrekt. Dit moet overeenkomen met de gebeurtenissen die door de extensie zijn verzonden en met eventuele optionele gegevens die samen met de e-mail of campagne zijn verzonden die ze hebben ontvangen. Zie de [ gidsen van de Hulp van de Automatisering van de Brievenjakimp ](https://mailchimp.com/help/automation/) voor meer details.
