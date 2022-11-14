---
title: Extensie Google Ads Enhanced Conversies
description: Meer informatie over de extensie Google Ads Enhanced Conversions voor het doorsturen van gebeurtenissen in Adobe Experience Platform.
source-git-commit: a279c44ef9df3aa9bfc7763b153b87bde0015d57
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 0%

---

# [!DNL Google Ads] Verbeterde extensie Conversies

Met de [!DNL Google Ads] API, u kunt hefboomwerking [verbeterde omzettingen](https://support.google.com/google-ads/answer/9888656) door de gegevens van de eerste klant in de vorm van conversieaanpassingen te verzenden. Google gebruikt deze aanvullende gegevens om de rapportage van uw online conversies via ad-interacties te verbeteren.

De [[!DNL Google Ads] Verbeterde Conversies-gebeurtenis, extensie doorsturen](https://exchange.adobe.com/apps/ec/108630/google-ads-enhanced-conversions) (hierna de [!DNL Enhanced Conversions] extensie) biedt een gebruiksvriendelijke sjabloon voor het eenvoudig implementeren van verbeterde conversies voor de [!DNL Google Ads] API.

>[!IMPORTANT]
>
>Verbeterde conversies werken alleen voor conversietypen waarbij klantgegevens aanwezig zijn, zoals abonnementen, aanmeldingsgegevens en aankopen. Een of meer van de volgende gegevens van de klant moeten beschikbaar zijn, zoals vereist wanneer [conversieactie configureren](#conversion-action-event-forwarding) voor een gebeurtenis die regel door:sturen:
>
>* E-mailadres (voorkeur)
>* Naam en huisadres (straatadres, woonplaats, land/regio en postcode)
>* Telefoonnummer (moet naast een van de twee andere bovenstaande gegevens worden verstrekt)


## Overzicht van implementatie

Verbeterde conversies maken gebruik van de [!DNL Google Ads] API voor het toevoegen van gegevens van eerste partijen aan een conversie die op een clientapparaat, meestal een website, heeft plaatsgevonden. Dit betekent dat er twee stappen zijn om verbeterde omzettingen uit te voeren:

1. Een conversie verzenden vanaf de client.
1. Het gebeurtenis door:sturen van het gebruik om extra eerste-partijgegevens te verzenden die de omzettingsgegevens verbeteren die van de cliënt worden verzonden.

>[!TIP]
>
>Om de cliënt-zijomzettingsgebeurtenis met de eerste partijgegevens te associëren die van gebeurtenis door:sturen, `transaction_ID` moet het zelfde in beide vraag zijn. Voor meer informatie over waar deze waarde voor elke dienst moet worden verstrekt, zie de secties bij het vormen van omzettingsacties voor [tags](#conversion-action-tags) en [gebeurtenis doorsturen](#conversion-action-event-forwarding), respectievelijk.

Aangezien bij het verzenden van conversiegebeurtenissen zowel een client-side als een server-side implementatie is betrokken, bevat dit document de vereiste stappen voor het instellen van de client-side [[!DNL Google Global Site Tag] (gtag) extensie](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag) naast de [!DNL Enhanced Conversions] extensie voor het doorsturen van gebeurtenissen.

## Conversie verzenden met tags

Een conversiegebeurtenis verzenden vanaf een website [!DNL Google Global Site Tag] (gtag) moet worden geïmplementeerd. U kunt dit bereiken door de tags te configureren en te installeren [!DNL Google Global Site Tag] (gtag).

### Configureer en installeer de [!DNL Google Global Site Tag] extension

Ga naar de [!UICONTROL Data Collection] UI of Experience Platform UI en selecteer **[!UICONTROL Tags]** in de linkernavigatie. Selecteer de eigenschap tag waarop u de extensie wilt installeren en selecteer vervolgens **[!UICONTROL Extensions]** in de linkernavigatie. Onder de **[!UICONTROL Catalog]** tabblad, zoekt u de [!UICONTROL Google Global Site Tag (gtag)] en selecteert u **[!UICONTROL Install]**.

![De [!UICONTROL Google Global Site Tag (gtag)] die onder de [!UICONTROL Extensions] in de [!UICONTROL Data Collection] UI.](../../../images/extensions/google-ads-enhanced-conversions/install-gtag-extension.png)

Het installatiedialoogvenster wordt weergegeven. Selecteer **[!UICONTROL Add Account]** en geef de volgende waarden op wanneer hierom wordt gevraagd:

| Account, eigenschap | Beschrijving |
| --- | --- |
| Accountnaam | Een unieke naam voor het account. Deze naam wordt alleen gebruikt binnen de interface voor tags. |
| Account-id | Uw [!DNL Google Ads] account-id. Meld u aan om deze waarde te vinden [!DNL Google Ads] en navigeer naar: **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Install the Tag yourself]**. De account-id-tekenreeks vindt u in het venster met het codefragment dat begint met `AW-` of `d`. |
| Product | Selecteer **[!UICONTROL Google Ads (AdWords)]**. |

{style=&quot;table-layout:auto&quot;}

Als u klaar bent, selecteert u **[!UICONTROL Add Account]** selecteert u vervolgens **[!UICONTROL Save]**.

### Conversieactie verzenden toevoegen {#conversion-action-tags}

Nadat u de extensie hebt geïnstalleerd, kunt u beginnen met het opnemen van conversieacties in de tagregels. Als u een regel maakt of bewerkt die luistert naar de conversie die u wilt verbeteren, selecteert u **[!UICONTROL Add]** krachtens [!UICONTROL Actions]. Selecteer in het volgende dialoogvenster **[!UICONTROL Google Global Site Tag (gtag)]** van de [!UICONTROL Extension] vervolgkeuzelijst, selecteert u vervolgens **[!UICONTROL Send an event]** krachtens [!UICONTROL Action Type].

![De [!UICONTROL Send an event] actietype dat binnen de mening van de actieconfiguratie van de regel het uitgeven werkschema wordt geselecteerd.](../../../images/extensions/google-ads-enhanced-conversions/select-client-action.png)

De extra controles verschijnen die u toestaan om [!DNL gtag] gebeurtenis. De volgende velden moeten ten minste worden ingevuld:

1. **[!UICONTROL Event Name (Action)]**: Enter `conversion` als de waarde.
1. Een nieuw veld toevoegen waarin de toets is `transaction_id` en de waarde is een [gegevenselement](../../../ui/managing-resources/data-elements.md) die de [transactie-id](https://support.google.com/google-ads/answer/6386790) waarde.
1. **[!UICONTROL Conversion Label]**: Voer het desbetreffende conversielabel in vanuit uw [!DNL Google Ads] account. Als u deze waarde wilt zoeken, meldt u zich aan bij Google Ads en navigeert u naar **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Use Google Tag Manager]**. Het conversielabel vindt u onder [!DNL Instructions].
   >[!IMPORTANT]
   >
   >Terwijl u zich in het instellingsgebied van de tag bevindt [!DNL Google Ads] -account, moet u ervoor zorgen dat verbeterde conversies zijn ingeschakeld. U doet dit door de Servicevoorwaarden te controleren en te accepteren en vervolgens **[!DNL Turn on enhanced conversions]** en **[!DNL API]** als uitvoeringsmethode.

Nadat u de handeling hebt geconfigureerd, selecteert u **[!UICONTROL Keep Changes]** om de actie aan de regelconfiguratie toe te voegen. Als u tevreden bent met de regel, selecteert u **[!UICONTROL Save to Library]**.

Tot slot publiceer een nieuwe [build](../../../ui/publishing/builds.md) om de wijzigingen in de bibliotheek in te schakelen.

## Gegevens van de eerste partij verzenden met behulp van gebeurtenis doorsturen

Wanneer u conversiegebeurtenissen vanaf de client kunt verzenden, kunt u deze conversies verbeteren met de opdracht [!DNL Enhanced Conversions] gebeurtenis die uitbreiding door:sturen.

### Een Google OAuth 2-geheim en gegevenselement maken {#create-secret-data-element}

Voordat u de extensie configureert, moet u een toegangstoken maken in gebeurtenis die wordt doorgestuurd om te verifiëren [!DNL Google Ads] API.

Zie de handleiding op [maken, gebeurtenis die geheimen doorstuurt](../../../ui/event-forwarding/secrets.md) voor gedetailleerde stappen. Zorg ervoor dat u **[!UICONTROL Google OAuth 2]** als het geheime type. Ga door met het volgen van de aanwijzingen en selecteer wanneer u wordt gevraagd een Google-accountprofiel te selecteren, de account die toegang heeft tot de conversieactie die u configureert.

Zodra het geheim is gemaakt, [een nieuw gegevenselement maken](../../../ui/managing-resources/data-elements.md#create-a-data-element) en selecteert u **[!UICONTROL Secret]** voor het gegevenstype data. Selecteer het juiste Google OAuth 2-geheim voor elke omgeving en selecteer **[!UICONTROL Save to Library]**.

### Configureer en installeer de [!DNL Enhanced Conversions] extension {#install-enhanced-conversions}

Zoek de [!UICONTROL Google Ads Enhanced Conversions] extensie in de gebeurtenis die de catalogus doorstuurt, selecteert u **[!UICONTROL Install]**.

![De [!UICONTROL Google Ads Enhanced Conversions] die onder de [!UICONTROL Extensions] in de [!UICONTROL Data Collection] UI.](../../../images/extensions/google-ads-enhanced-conversions/install-enhanced-conversions.png)

Als u de extensie wilt configureren, moet u de twee vereiste velden invullen:

1. **[!UICONTROL Customer ID]**: De id die uw [!DNL Google Ads] account. Meld u aan om deze waarde te vinden [!DNL Google Ads] en navigeer naar **[!DNL Help]** > **[!DNL Customer ID]**.
1. **[!UICONTROL Access Token Data Element]**: Selecteer het pictogram voor het gegevenselement (![Pictogram gegevenselement](../../../images/extensions/google-ads-enhanced-conversions/data-element-icon.png)) en kiest u het Google OAuth 2 geheime gegevenselement dat u [geconfigureerd in de vorige stap](#create-secret-data-element) in het menu.

Als u klaar bent, selecteert u **[!UICONTROL Save]** om de extensie te installeren.

### Voeg een [!UICONTROL Send Conversion] handeling aan een regel {#conversion-action-event-forwarding}

Nadat de extensie is geïnstalleerd, kunt u beginnen met opnemen [!UICONTROL Send Conversion] acties in uw gebeurtenis die regels door:sturen. Als u een regel maakt of bewerkt die luistert naar de conversie die u wilt verbeteren, selecteert u **[!UICONTROL Add]** krachtens [!UICONTROL Actions]. Selecteer in het volgende dialoogvenster **[!UICONTROL Google Ads Enhanced Conversions]** van de [!UICONTROL Extension] vervolgkeuzelijst, selecteert u vervolgens **[!UICONTROL Send Conversion]** krachtens [!UICONTROL Action Type].

![De [!UICONTROL Send Conversion] actietype dat binnen de mening van de actieconfiguratie van de regel het uitgeven werkschema wordt geselecteerd.](../../../images/extensions/google-ads-enhanced-conversions/select-server-action.png)

De nieuwe controles verschijnen in het juiste paneel dat u toestaat om uw omzetting te vormen. Ten minste de volgende velden moeten worden ingevuld:

**Conversiegegevens**

| Invoer | Beschrijving |
| --- | --- |
| Klant-id | Uw [!DNL Google Ads] klant-id. Wordt standaard ingesteld op de klant-id die u hebt ingevoerd toen [installeren, extensie](#install-enhanced-conversions). |
| Conversie-id of conversielabel | Waarden bijhouden die zijn verkregen uit [!DNL Google Ads] bij het instellen van bijhouden van conversie. Waarden beginnen met `AW-`.<br><br>Voor meer informatie over het vinden van deze waarden raadpleegt u de [[!DNL Google Ads] documentatie](https://support.google.com/tagmanager/answer/6105160?hl=en). |
| Transactie-id | Selecteer een gegevenselement dat dezelfde transactie-id-waarde heeft als [vanuit de clientzijde verzonden](#conversion-action-tags) met de [!DNL Google Global Site Tag] extensie. |

**Gebruikersidentificatie**

* Ten minste een van de drie gebruikersidentificatoren moet worden opgenomen:
   * Email
   * Telefoonnummer
   * Volledig adres

>[!TIP]
>
>De identificatiegegevens van de gebruiker moeten worden gehasht alvorens het naar Google wordt verzonden. Als de gegevens niet gehasht zijn wanneer het door:sturen van de gebeurtenis het ontvangt, selecteer **[!UICONTROL Normalize & Hash]** Schakel een bepaald veld in om de extensie te instrueren de waarde te hashen.
>
>![De [!UICONTROL Normalize & Hash] schakelen ingeschakeld voor de [!UICONTROL Email] invoer binnen de [!UICONTROL Send Conversion] actieconfiguratieformulier.](../../../images/extensions/google-ads-enhanced-conversions/hash-user-id-values.png)

Als u klaar bent, selecteert u **[!UICONTROL Keep Changes]** om de actie aan de regelconfiguratie toe te voegen. Als u tevreden bent met de regel, selecteert u **[!UICONTROL Save to Library]**.

Ten slotte publiceert u een nieuwe gebeurtenis die wordt doorgestuurd [build](../../../ui/publishing/builds.md) om de wijzigingen in de bibliotheek in te schakelen.

## Volgende stappen

In deze handleiding wordt beschreven hoe conversiegebeurtenissen worden verzonden naar [!DNL Google Ads] met de [!DNL Enhanced Conversions] gebeurtenis die uitbreiding door:sturen. Voor meer informatie over gebeurtenis die mogelijkheden in Experience Platform door:sturen, verwijs naar [overzicht van gebeurtenissen doorsturen](../../../ui/event-forwarding/overview.md).
