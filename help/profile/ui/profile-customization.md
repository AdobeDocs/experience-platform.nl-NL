---
keywords: Experience Platform;profiel;realtime klantprofiel;gebruikersinterface;UI;aanpassing;profieldetails;details
title: Aanpassen hoe u profielen weergeeft in de gebruikersinterface
description: 'Deze handleiding bevat stapsgewijze instructies voor het aanpassen van de manier waarop gegevens van het realtime-klantprofiel worden weergegeven in de gebruikersinterface van Adobe Experience Platform. '
topic: guide
translation-type: tm+mt
source-git-commit: e6ecc5dac1d09c7906aa7c7e01139aa194ed662b
workflow-type: tm+mt
source-wordcount: '1185'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] detailaanpassing  {#profile-detail-customization}

In de Adobe Experience Platform-gebruikersinterface kunt u [!DNL Real-time Customer Profile]-gegevens weergeven en ermee werken in de vorm van klantprofielen. De profielgegevens die in de gebruikersinterface worden weergegeven, zijn samengevoegd vanuit meerdere profielfragmenten en vormen één weergave van elke afzonderlijke klant. Dit omvat details zoals basiskenmerken, gekoppelde identiteiten en kanaalvoorkeuren. De standaardvelden in profielen kunnen ook op organisatorisch niveau worden gewijzigd, zodat de voorkeurskenmerken [!DNL Profile] worden weergegeven. Deze gids verstrekt geleidelijke instructies voor het aanpassen van de manier waarin [!DNL Profile] de gegevens binnen Platform UI worden getoond.

Voor een volledige gids aan de UI van Profielen, te bezoeken gelieve [de gids van het Profiel UI](user-guide.md).

## Kaarten opnieuw rangschikken en formaat wijzigen {#reorder-and-resize-cards}

Op het tabblad **[!UICONTROL Details]** van het klantprofiel kunt u **[!UICONTROL Het dashboard wijzigen]** selecteren om het formaat en de volgorde van bestaande kaarten te wijzigen.

![](../images/profile-customization/profiles-modify-dashboard.png)

Nadat u het dashboard hebt gewijzigd, kunt u de kaarten opnieuw rangschikken door de kaarttitel te selecteren en de kaarten in de gewenste volgorde te slepen. U kunt het formaat van een kaart ook wijzigen door het hoeksymbool in de rechterbenedenhoek van de kaart (`⌟`) te selecteren en de kaart naar de gewenste grootte te slepen. In dit voorbeeld wordt de grootte van de **[!UICONTROL Basic-kenmerken]**-kaart gewijzigd.

![](../images/profile-customization/profiles-resize-cards.png)

De geselecteerde kaart wordt aangepast aan de gewenste grootte en de omringende kaarten worden dynamisch verplaatst. Hierdoor kunnen sommige kaarten naar extra rijen worden verplaatst, waardoor u omlaag moet schuiven om alle kaarten weer te geven. Wanneer bijvoorbeeld de grootte van de &quot;[!UICONTROL Basic attributes]&quot;-kaart wordt gewijzigd, is de kaart &quot;[!UICONTROL Linked identities]&quot; niet meer zichtbaar op de bovenste rij en wordt deze nu weergegeven op een nieuwe tweede rij in het profiel (niet weergegeven). Als u de kaart &quot;[!UICONTROL Gekoppelde identiteiten]&quot; wilt retourneren naar de bovenste rij, kunt u deze naar de huidige positie van de kaart &quot;[!UICONTROL Kanaalvoorkeuren]&quot; slepen.

![](../images/profile-customization/profiles-card-resized.png)

## Kaarten bewerken en verwijderen

Naast het wijzigen van het formaat en het opnieuw ordenen van kaarten, kunt u de inhoud van bepaalde kaarten bewerken en enkele kaarten volledig uit het dashboard verwijderen. Selecteer de ovalen (`...`) in de rechterbovenhoek van de kaart om deze te bewerken of te verwijderen. Hiermee wordt een vervolgkeuzelijst geopend met opties voor het bewerken of verwijderen van de kaart, afhankelijk van de eigenschappen van de geselecteerde kaart.

>[!NOTE]
>
>Niet alle kaarten kunnen worden bewerkt of verwijderd. Dit komt omdat sommige kaarten alleen-lezen of vereiste informatie bevatten. Als een kaart geen ellipsen in de hoger-juiste hoek heeft, bevat het read-only EN vereiste informatie en kan niet worden uitgegeven noch kan het worden verwijderd. Als een kaart ovalen in de hoek heeft en u deze selecteert, wordt alleen een optie voor het verwijderen van de kaart weergegeven. De kaartgegevens zijn alleen-lezen en kunnen dan niet worden bewerkt.

![](../images/profile-customization/profiles-edit-remove-resized.png)

Selecteer **[!UICONTROL Bewerken]** in het vervolgkeuzemenu om de werkruimte **[!UICONTROL Widget bewerken]** te openen, waar u de kaarttitel kunt bijwerken, de zichtbare kenmerken opnieuw kunt ordenen of eruit kunt verwijderen, of extra kenmerken kunt toevoegen met de knop **[!UICONTROL Kenmerken toevoegen]**.

![](../images/profile-customization/profiles-edit-widget-basic-attributes.png)

## Kenmerken {#add-attributes} toevoegen

Selecteer **[!UICONTROL Kenmerken toevoegen]** in de rechterbovenhoek van de kaart in het scherm **[!UICONTROL Widget]** bewerken om kenmerken aan die kaart toe te voegen.

![](../images/profile-customization/profiles-edit-widget-basic-add-attributes.png)

Wanneer het **[!UICONTROL Uitgezochte gebied van het unieschema]** dialoog opent, toont de linkerkant van de dialoog volledig [!UICONTROL XDM Individueel Profiel] verenigingsschema, met gebieden onder genest. Raadpleeg voor meer informatie over samenvoegingsschema&#39;s de sectie [union schema&#39;s in de  [!DNL Profile] gebruikershandleiding](user-guide.md#union-schema).

In de sectie **[!UICONTROL Geselecteerde kenmerken]** aan de rechterkant van het dialoogvenster ziet u de kenmerken die momenteel zijn opgenomen in de kaart die u bewerkt. U kunt hier ook kenmerken verwijderen en opnieuw ordenen. Het totale aantal geselecteerde kenmerken en het maximumaantal kenmerken (20) dat aan één kaart kan worden toegevoegd, worden weergegeven.

![](../images/profile-customization/profiles-select-field-before.png)

U kunt om het even welke beschikbare gebieden van het unieschema selecteren om de attributen op de kaart aan te passen die u uitgeeft. Geselecteerde velden worden weergegeven met een vinkje ernaast en worden automatisch toegevoegd aan de lijst met geselecteerde kenmerken. Nadat u alle kenmerken hebt toegevoegd die u op de kaart wilt weergeven, kiest u **[!UICONTROL Selecteren]** om terug te keren naar het scherm **[!UICONTROL Widget]** bewerken.

![](../images/profile-customization/profiles-select-field-after.png)

Wanneer u terugkeert naar het **[!UICONTROL scherm Edit widget]**, zou de lijst van attributen op de kaart nu moeten worden bijgewerkt om op uw keuzen te wijzen. U kunt de kaartkenmerken nog steeds verwijderen of opnieuw rangschikken of de kaarttitel desgewenst bewerken. Als uw bewerkingen zijn voltooid, selecteert u **[!UICONTROL Opslaan]** om uw wijzigingen op te slaan.

![](../images/profile-customization/profiles-edit-widget-new-attributes.png)

Nadat u het document hebt opgeslagen, gaat u terug naar het tabblad **[!UICONTROL Details]** waar de bijgewerkte kaart en kenmerken zichtbaar zijn.

![](../images/profile-customization/profiles-resized-card-new-attributes.png)

## Nieuwe kaart toevoegen {#add-a-new-card}

Als u de weergave van profielen in het Experience Platform verder wilt aanpassen, kunt u ervoor kiezen nieuwe kaarten aan het dashboard toe te voegen en de kenmerken te selecteren die u op die kaarten wilt weergeven. Selecteer **[!UICONTROL Het dashboard wijzigen]** op het **[!UICONTROL tabblad Details]** om te beginnen.

![](../images/profile-customization/profiles-modify-dashboard.png)

Selecteer vervolgens **[!UICONTROL Widget toevoegen]** in de linkerbovenhoek van het dashboard.

![](../images/profile-customization/profiles-add-widget.png)

Als u een nieuwe kaart wilt toevoegen, wordt het scherm **[!UICONTROL Widget bewerken]** geopend, waarin u een titel voor de nieuwe kaart kunt opgeven en de kenmerken kunt kiezen die de kaart moet weergeven. Selecteer **[!UICONTROL Kenmerken toevoegen]** om kenmerken aan de kaart toe te voegen.

![](../images/profile-customization/profiles-edit-new-widget.png)

Wanneer het **[!UICONTROL Uitgezochte gebied van het unieschema]** dialoogvenster opent, toont de linkerkant van de dialoog volledige [!UICONTROL XDM Individueel Profiel] verenigingsschema en **[!UICONTROL Geselecteerde Attributes]** sectie op de rechterkant van de dialoog toont de attributen die u voor uw kaart selecteert. Zie de sectie [over het toevoegen van kenmerken](#add-attributes) in dit document voor meer informatie over het toevoegen van kenmerken.

Het totale aantal geselecteerde kenmerken en het maximumaantal kenmerken (20) dat aan één kaart kan worden toegevoegd, worden weergegeven. U kunt de geselecteerde kenmerken ook uit dit scherm verwijderen en opnieuw rangschikken. Nadat u alle kenmerken hebt toegevoegd die u op de kaart wilt weergeven, kiest u **[!UICONTROL Selecteren]** om terug te keren naar het **[!UICONTROL Widget]**-scherm bewerken.

![](../images/profile-customization/profiles-add-fields-new-widget.png)

Wanneer u terugkeert naar het **[!UICONTROL scherm Edit widget]**, zou de lijst van attributen op de kaart uw keuzen van het vorige scherm moeten weerspiegelen. U kunt ook de kaartkenmerken naar wens opnieuw rangschikken en verwijderen.

Als u uw nieuwe kaart wilt opslaan, moet u eerst een **[!UICONTROL Kaarttitel]** opgeven, dan kunt u **[!UICONTROL Opslaan]** selecteren en het maken van de kaart voltooien.

![](../images/profile-customization/profiles-edit-new-widget-with-fields.png)

Nadat u de kaart hebt opgeslagen, gaat u terug naar het tabblad **[!UICONTROL Details]** waar uw nieuwe kaart en kenmerken zichtbaar zijn.

![](../images/profile-customization/profiles-detail-new-widget.png)

## Standaardkaarten herstellen

Als u op een gegeven moment besluit dat u de standaardkaarten die sindsdien zijn verwijderd, wilt herstellen, kunt u dit snel en eenvoudig doen. Selecteer eerst **[!UICONTROL Het dashboard wijzigen]** en selecteer vervolgens **[!UICONTROL Standaardkaarten herstellen]**. Als de standaardkaarten zichtbaar zijn, kunt u **[!UICONTROL Opslaan]** selecteren om uw wijzigingen op te slaan of **[!UICONTROL Annuleren]** selecteren als u de standaardkaarten niet wilt herstellen.

![](../images/profile-customization/profiles-restore-default.png)

## Volgende stappen

Als u dit document volgt, kunt u nu de profielweergave voor uw organisatie bijwerken, zoals kaarten toevoegen en verwijderen, kaartdetails en kenmerken bewerken en kaarten opnieuw ordenen en vergroten of verkleinen. Raadpleeg de [[!DNL Profile] gebruikershandleiding](user-guide.md) voor meer informatie over het werken met [!DNL Profile]-gegevens in de interface van het Experience Platform.