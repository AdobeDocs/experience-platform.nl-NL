---
title: Extensie Google Ads Enhanced Conversies
description: Meer informatie over de extensie Google Ads Enhanced Conversions voor het doorsturen van gebeurtenissen in Adobe Experience Platform.
exl-id: 65cdff40-276f-4481-9621-6c6861dbd412
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 1c417744518a7ac7cfb9c65d6af8219dcbc70d46
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 0%

---

# [!DNL Google Ads] Verbeterde extensie Conversies

Gebruikend [!DNL Google Ads] API, kunt u hefboomwerking [ verbeterde omzettingen ](https://support.google.com/google-ads/answer/9888656) door de gegevens van de eerste partijklant in de vorm van omzettingsaanpassingen te verzenden. Google gebruikt deze aanvullende gegevens om de rapportage van uw online conversies via ad-interacties te verbeteren.

De [[!DNL Google Ads]  Verbeterde gebeurtenis die van Conversies uitbreiding ](https://exchange.adobe.com/apps/ec/108630/google-ads-enhanced-conversions) door:sturen (die nu als [!DNL Enhanced Conversions] uitbreiding wordt bedoeld) verstrekt een gebruikersvriendelijk malplaatje om verbeterde omzettingen voor [!DNL Google Ads] API gemakkelijk uit te voeren.

>[!IMPORTANT]
>
>Verbeterde conversies werken alleen voor conversietypen waarbij klantgegevens aanwezig zijn, zoals abonnementen, aanmeldingsgegevens en aankopen. Één of meerdere van de volgende stukken van klantengegevens moeten beschikbaar zijn, aangezien zij wanneer [ worden vereist vormend een omzettingsactie ](#conversion-action-event-forwarding) voor een gebeurtenis die regel door:sturen:
>
>* E-mailadres (voorkeur)
>* Naam en huisadres (straatadres, woonplaats, land/regio en postcode)
>* Telefoonnummer (moet naast een van de twee andere bovenstaande gegevens worden verstrekt)

## Overzicht van implementatie

Verbeterde conversies maken gebruik van de API van [!DNL Google Ads] om gegevens van de eerste partij toe te voegen aan een conversie die op een clientapparaat, meestal een website, heeft plaatsgevonden. Dit betekent dat er twee stappen zijn om verbeterde omzettingen uit te voeren:

1. Een conversie verzenden vanaf de client.
1. Het gebeurtenis door:sturen van het gebruik om extra eerste-partijgegevens te verzenden die de omzettingsgegevens verbeteren die van de cliënt worden verzonden.

>[!TIP]
>
>Om de cliënt-zijomzettingsgebeurtenis met de eerste partijgegevens te associëren die van gebeurtenis door:sturen worden verzonden, moet `transaction_ID` het zelfde in beide vraag zijn. Voor meer informatie over waar deze waarde voor elke dienst moet worden verstrekt, zie de secties bij het vormen omzettingsacties voor [ markeringen ](#conversion-action-tags) en [ gebeurtenis door:sturen ](#conversion-action-event-forwarding), respectievelijk.

Aangezien het verzenden van omzettingsgebeurtenissen zowel een cliënt-kant als server-zijimplementatie impliceert, behandelt dit document de eerste vereiste stappen voor vestiging de cliënt-kant [[!DNL Google Global Site Tag]  (gtag) uitbreiding ](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag) naast de [!DNL Enhanced Conversions] uitbreiding voor gebeurtenis door:sturen.

In de volgende video wordt een inleiding gegeven op de extensie [!DNL Enhanced Conversions] en worden de implementatiestappen op hoog niveau doorlopen:

>[!VIDEO](https://video.tv.adobe.com/v/3411365?quality=12&learn=on)

## Conversie verzenden met tags

[!DNL Google Global Site Tag] (gtag) moet worden geïmplementeerd om een conversiegebeurtenis van een website te verzenden. U kunt dit bereiken door de extensie [!DNL Google Global Site Tag] (gtag) te configureren en te installeren.

### De extensie [!DNL Google Global Site Tag] configureren en installeren

Navigeer naar de gebruikersinterface van [!UICONTROL Data Collection] of het Experience Platform en selecteer **[!UICONTROL Tags]** in de linkernavigatie. Selecteer de eigenschap tag waarop u de extensie wilt installeren en selecteer vervolgens **[!UICONTROL Extensions]** in de linkernavigatie. Zoek onder het tabblad **[!UICONTROL Catalog]** de extensie [!UICONTROL Google Global Site Tag (gtag)] en selecteer **[!UICONTROL Install]** .

![ de [!UICONTROL Google Global Site Tag (gtag)] uitbreiding die onder de [!UICONTROL Extensions] mening in [!UICONTROL Data Collection] UI wordt geselecteerd.](../../../images/extensions/server/google-ads-enhanced-conversions/install-gtag-extension.png)

Het installatiedialoogvenster wordt weergegeven. Selecteer **[!UICONTROL Add Account]** hier en geef de volgende waarden op wanneer u hierom wordt gevraagd:

| Account, eigenschap | Beschrijving |
| --- | --- |
| Accountnaam | Een unieke naam voor het account. Deze naam wordt alleen gebruikt binnen de interface voor tags. |
| Account-id | Uw [!DNL Google Ads] account-id. U kunt deze waarde zoeken door u aan te melden bij [!DNL Google Ads] en naar **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Install the Tag yourself]** te navigeren. De account-id-tekenreeks vindt u in het venster met het codefragment dat begint met `AW-` of `d` . |
| Product | Selecteer **[!UICONTROL Google Ads (AdWords)]**. |

{style="table-layout:auto"}

Als u klaar bent, selecteert u **[!UICONTROL Add Account]** en vervolgens **[!UICONTROL Save]** .

### Een actie voor het verzenden van conversies toevoegen {#conversion-action-tags}

Nadat u de extensie hebt geïnstalleerd, kunt u beginnen met het opnemen van conversieacties in de tagregels. Selecteer **[!UICONTROL Add]** onder [!UICONTROL Actions] wanneer u een regel maakt of bewerkt die luistert naar de conversie die u wilt verbeteren. Selecteer in het volgende dialoogvenster **[!UICONTROL Google Global Site Tag (gtag)]** in de vervolgkeuzelijst [!UICONTROL Extension] en selecteer vervolgens **[!UICONTROL Send an event]** onder [!UICONTROL Action Type] .

![ het [!UICONTROL Send an event] actietype dat binnen de mening van de actieconfiguratie van de regel het uitgeven werkschema wordt geselecteerd.](../../../images/extensions/server/google-ads-enhanced-conversions/select-client-action.png)

Er verschijnen extra besturingselementen waarmee u de gebeurtenis [!DNL gtag] kunt configureren. De volgende velden moeten ten minste worden ingevuld:

1. **[!UICONTROL Event Name (Action)]**: voer `conversion` in als de waarde.
1. Voeg een nieuw gebied toe waar de sleutel `transaction_id` is en de waarde a [ gegevenselement ](../../../ui/managing-resources/data-elements.md) is dat de [ waarde van identiteitskaart van de transactie ](https://support.google.com/google-ads/answer/6386790) bevat.
1. **[!UICONTROL Conversion Label]**: voer het juiste conversielabel vanuit uw [!DNL Google Ads] -account in. Als u deze waarde wilt zoeken, meldt u zich aan bij Google Ads en navigeert u naar **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Use Google Tag Manager]** . Het conversielabel vindt u onder [!DNL Instructions] .
   >[!IMPORTANT]
   >
   >Zorg dat de uitgebreide conversies zijn ingeschakeld terwijl u zich in het instellingsgebied voor tags van uw [!DNL Google Ads] -account bevindt. Hiervoor controleert u de Servicevoorwaarden en accepteert u **[!DNL Turn on enhanced conversions]** en **[!DNL API]** als implementatiemethode.

Nadat u de actie hebt gevormd, uitgezocht **[!UICONTROL Keep Changes]** om de actie aan de regelconfiguratie toe te voegen. Selecteer **[!UICONTROL Save to Library]** als u tevreden bent met de regel.

Tot slot publiceer een nieuwe [ bouwstijl ](../../../ui/publishing/builds.md) om de veranderingen in de bibliotheek toe te laten.

## Gegevens van de eerste partij verzenden met behulp van gebeurtenis doorsturen

Wanneer u conversiegebeurtenissen vanaf de client kunt verzenden, kunt u deze conversies verbeteren met de extensie [!DNL Enhanced Conversions] voor het doorsturen van gebeurtenissen.

### Een Google OAuth 2-geheim en gegevenselement maken {#create-secret-data-element}

Voordat u de extensie configureert, moet u een toegangstoken maken bij het doorsturen van gebeurtenissen om te verifiëren met de API van [!DNL Google Ads] .

Zie de gids bij [ het creëren van gebeurtenis die geheimen ](../../../ui/event-forwarding/secrets.md) voor gedetailleerde stappen door:sturen. Zorg ervoor dat u **[!UICONTROL Google OAuth 2]** selecteert als geheim type. Ga door met het volgen van de aanwijzingen en selecteer wanneer u wordt gevraagd een Google-accountprofiel te selecteren, de account die toegang heeft tot de conversieactie die u configureert.

Zodra het geheim wordt gecreeerd, [ creeer een nieuw gegevenselement ](../../../ui/managing-resources/data-elements.md#create-a-data-element) en selecteer **[!UICONTROL Secret]** voor het type van gegevenselement. Selecteer het juiste Google OAuth 2-geheim voor elke omgeving en selecteer **[!UICONTROL Save to Library]** .

### De extensie [!DNL Enhanced Conversions] configureren en installeren {#install-enhanced-conversions}

Zoek de extensie [!UICONTROL Google Ads Enhanced Conversions] in de door:sturen catalogus van de gebeurtenis en selecteer **[!UICONTROL Install]** .

![ de [!UICONTROL Google Ads Enhanced Conversions] uitbreiding die onder de [!UICONTROL Extensions] mening in [!UICONTROL Data Collection] UI wordt geselecteerd.](../../../images/extensions/server/google-ads-enhanced-conversions/install-enhanced-conversions.png)

Als u de extensie wilt configureren, moet u de twee vereiste velden invullen:

1. **[!UICONTROL Customer ID]**: De id die uw [!DNL Google Ads] -account uniek identificeert. U kunt deze waarde zoeken door u aan te melden bij [!DNL Google Ads] en naar **[!DNL Help]** > **[!DNL Customer ID]** te navigeren.
1. **[!UICONTROL Access Token Data Element]**: Selecteer het pictogram van het gegevenselement (![ het elementenpictogram van Gegevens ](../../../images/extensions/server/google-ads-enhanced-conversions/data-element-icon.png)) en kies Google OAuth 2 geheim gegevenselement dat u [ in de vorige stap ](#create-secret-data-element) van het menu vormde.

Als u klaar bent, selecteert u **[!UICONTROL Save]** om de extensie te installeren.

### Een handeling [!UICONTROL Send Conversion] aan een regel toevoegen {#conversion-action-event-forwarding}

Nadat de extensie is geïnstalleerd, kunt u beginnen met het opnemen van [!UICONTROL Send Conversion] -acties in uw gebeurtenisverzendregels. Selecteer **[!UICONTROL Add]** onder [!UICONTROL Actions] wanneer u een regel maakt of bewerkt die luistert naar de conversie die u wilt verbeteren. Selecteer in het volgende dialoogvenster **[!UICONTROL Google Ads Enhanced Conversions]** in de vervolgkeuzelijst [!UICONTROL Extension] en selecteer vervolgens **[!UICONTROL Send Conversion]** onder [!UICONTROL Action Type] .

![ het [!UICONTROL Send Conversion] actietype dat binnen de mening van de actieconfiguratie van de regel het uitgeven werkschema wordt geselecteerd.](../../../images/extensions/server/google-ads-enhanced-conversions/select-server-action.png)

De nieuwe controles verschijnen in het juiste paneel dat u toestaat om uw omzetting te vormen. Ten minste de volgende velden moeten worden ingevuld:

**Informatie van de Omzetting**

| Invoer | Beschrijving |
| --- | --- |
| Klant-id | Uw [!DNL Google Ads] klant-id. De gebreken aan klantenidentiteitskaart u inging toen [ het installeren van de uitbreiding ](#install-enhanced-conversions). |
| Conversie-id of conversielabel | Waarden bijhouden die zijn opgehaald uit [!DNL Google Ads] bij het instellen van bijhouden van conversie. Waarden beginnen met `AW-` .<br><br> voor details op hoe te om deze waarden te vinden, verwijs naar de [[!DNL Google Ads]  documentatie ](https://support.google.com/tagmanager/answer/6105160?hl=en). |
| Transactie-id | Selecteer een gegevenselement dat de zelfde waarde van transactieidentiteitskaart heeft die [ van de cliëntkant ](#conversion-action-tags) wordt verzonden gebruikend de [!DNL Google Global Site Tag] uitbreiding. |

**Identificatie van de Gebruiker**

* Ten minste een van de drie gebruikersidentificatoren moet worden opgenomen:
   * Email
   * Telefoonnummer
   * Volledig adres

>[!TIP]
>
>De identificatiegegevens van de gebruiker moeten worden gehasht alvorens het naar Google wordt verzonden. Als de gegevens niet worden gehasht wanneer het door:sturen van de gebeurtenis het ontvangt, selecteer **[!UICONTROL Normalize & Hash]** knevel op een bepaald gebied om de uitbreiding op te dragen om de waarde te hakken.
>
>![ de [!UICONTROL Normalize & Hash] knevel voor de [!UICONTROL Email] input binnen de [!UICONTROL Send Conversion] vorm van de actieconfiguratie wordt toegelaten die.](../../../images/extensions/server/google-ads-enhanced-conversions/hash-user-id-values.png)

Als u klaar bent, selecteert u **[!UICONTROL Keep Changes]** om de handeling aan de regelconfiguratie toe te voegen. Selecteer **[!UICONTROL Save to Library]** als u tevreden bent met de regel.

Tot slot publiceer een nieuwe gebeurtenis door:sturen [ bouwt ](../../../ui/publishing/builds.md) om de veranderingen in de bibliotheek toe te laten.

## Volgende stappen

In deze handleiding wordt beschreven hoe conversiegebeurtenissen naar [!DNL Google Ads] worden verzonden met behulp van de [!DNL Enhanced Conversions] -extensie voor het doorsturen van gebeurtenissen. Voor meer informatie over gebeurtenis die mogelijkheden in Experience Platform door:sturen, verwijs naar de [ gebeurtenis die overzicht ](../../../ui/event-forwarding/overview.md) door:sturen.
