---
keywords: bestemmingsaccount bijwerken, bestemmingsaccounts, accounts bijwerken, doel bijwerken
title: Doelaccounts bijwerken
type: Tutorial
description: Deze zelfstudie bevat een overzicht van de stappen voor het bijwerken van bestemmingsaccounts in de gebruikersinterface van Adobe Experience Platform
exl-id: afb41878-4205-4c64-af4d-e2740f852785
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---

# Doelaccounts bijwerken

## Overzicht {#overview}

Op het tabblad **[!UICONTROL Accounts]** ziet u details over de verbindingen die u hebt gemaakt met verschillende doelen. Verwijs naar het [ overzicht van Rekeningen ](../ui/destinations-workspace.md#accounts) voor alle informatie u op elke bestemmingsrekening kunt krijgen.

Deze zelfstudie behandelt de stappen om de details van de bestemmingsrekening bij te werken door het Experience Platform UI te gebruiken.

U kunt de details van de bestemmingsrekening bijwerken om geloofsbrieven voor uw huidige of verlopen rekeningen voor bestemmingen te verfrissen en opnieuw voor authentiek te verklaren u momenteel gebruikt. Typisch, hebben OAuth en dragertokens een beperkt leven, afhankelijk van het bestemmingsplatform. Wanneer deze tokens verlopen, kunt u ze in de hieronder beschreven workflow vernieuwen. Deze workflow geeft u de opdracht de OAuth-workflow te doorlopen of een token opnieuw in te voegen. Op dezelfde manier als een wachtwoord of gebruikerstoegang in het stroomafwaartse platform zijn veranderd, kunt u geloofsbrieven verfrissen.

Voor batchbestemmingen kunt u de toegang of de geheime sleutel bijwerken als een van deze wijzigingen is gewijzigd. Als u uw bestanden verder wilt coderen, kunt u bovendien een openbare RSA-sleutel invoegen en worden uw geëxporteerde bestanden vervolgens versleuteld.

![ Rekeningen tabel ](../assets/ui/update-accounts/destination-accounts.png)

## Accounts bijwerken {#update}

Voer de onderstaande stappen uit om verbindingsgegevens bij te werken naar bestaande doelen.

1. Login aan het [ Experience Platform UI ](https://platform.adobe.com/) en selecteert **[!UICONTROL Destinations]** van de linkernavigatiebar. Selecteer **[!UICONTROL Accounts]** in de bovenste koptekst om uw bestaande accounts weer te geven.

   ![ Rekeningen tabel ](../assets/ui/update-accounts/accounts-tab.png)

2. Selecteer het filterpictogram ![ filter-pictogram ](../assets/ui/update-accounts/filter.png) op de bovenkant verlaten om het soortpaneel te lanceren. Het deelvenster Sorteren bevat een lijst met al uw doelen. U kunt meer dan één bestemming van de lijst selecteren om een gefilterde selectie van rekeningen te zien verbonden aan de geselecteerde bestemmingen.

   ![ de bestemmingsrekeningen van de Filter ](../assets/ui/update-accounts/filter-accounts.png)

3. Selecteer de ovalen (`...`) naast de naam van de account die u wilt bijwerken. Er verschijnt een pop-upvenster met opties voor **[!UICONTROL Activate audiences]** , **[!UICONTROL Edit details]** en **[!UICONTROL Delete]** de account. Selecteer ![ uitgeven detailknoop ](../assets/ui/workspace/pencil-icon.png) **[!UICONTROL Edit details]** knoop om de rekeningsinformatie uit te geven.

   ![ geef rekening ](../assets/ui/update-accounts/accounts-edit.png) uit

4. Voer uw bijgewerkte accountgegevens in.

   * Voor accounts die een `OAuth1` - of `OAuth2` verbindingstype gebruiken, selecteert u **[!UICONTROL Reconnect OAuth]** om uw accountgegevens te vernieuwen. U kunt ook de naam en beschrijving van uw account bijwerken.

   ![ geef details OAuth ](../assets/ui/update-accounts/edit-details-oauth.png) uit

   * Voor accounts die een verbindingstype `Access Key` of `ConnectionString` gebruiken, kunt u de verificatiegegevens van uw account bewerken, zoals toegang-id, geheime sleutels of verbindingstekenreeksen. U kunt ook de naam en beschrijving van uw account bijwerken.

   ![ geef de Sleutel van de Toegang van details uit ](../assets/ui/update-accounts/edit-details-key.png)

   * Voor accounts die een verbindingstype `Bearer token` gebruiken, kunt u indien nodig een nieuw token voor toonder invoeren. U kunt ook de naam en beschrijving van uw account bijwerken.

   ![ geeft het teken van de Details Drager uit ](../assets/ui/update-accounts/edit-details-bearer.png)

   * Voor accounts die een verbindingstype `Server to server` gebruiken, kunt u de naam en beschrijving van uw account bijwerken.

   ![ geeft details Server-aan-server ](../assets/ui/update-accounts/edit-details-s2s.png) uit

5. Selecteer **[!UICONTROL Save]** om de update van de accountdetails te voltooien.

## Volgende stappen

Door deze zelfstudie te volgen, hebt u de werkruimte van **[!UICONTROL destinations]** gebruikt om bestaande accounts bij te werken.

Voor meer informatie over bestemmingen, verwijs naar het [ overzicht van bestemmingen ](../catalog/overview.md).