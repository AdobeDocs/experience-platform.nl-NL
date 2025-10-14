---
keywords: bestemmingsaccount bijwerken, bestemmingsaccounts, accounts bijwerken, doel bijwerken
title: Doelaccounts bijwerken
type: Tutorial
description: Deze zelfstudie bevat een overzicht van de stappen voor het bijwerken van bestemmingsaccounts in de gebruikersinterface van Adobe Experience Platform
exl-id: afb41878-4205-4c64-af4d-e2740f852785
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---

# Doelaccounts bijwerken

## Overzicht {#overview}

Op het tabblad **[!UICONTROL Accounts]** ziet u details over de verbindingen die u hebt gemaakt met verschillende doelen. Verwijs naar het [&#x200B; overzicht van Rekeningen &#x200B;](../ui/destinations-workspace.md#accounts) voor alle informatie u op elke bestemmingsrekening kunt krijgen.

Deze zelfstudie behandelt de stappen om de details van de bestemmingsrekening bij te werken door het Experience Platform UI te gebruiken.

U kunt de details van de bestemmingsrekening bijwerken om geloofsbrieven voor uw huidige of verlopen rekeningen voor bestemmingen te verfrissen en opnieuw voor authentiek te verklaren u momenteel gebruikt. Typisch, hebben OAuth en dragertokens een beperkt leven, afhankelijk van het bestemmingsplatform. Wanneer deze tokens verlopen, kunt u ze in de hieronder beschreven workflow vernieuwen. Deze workflow geeft u de opdracht de OAuth-workflow te doorlopen of een token opnieuw in te voegen. Op dezelfde manier als een wachtwoord of gebruikerstoegang in het stroomafwaartse platform zijn veranderd, kunt u geloofsbrieven verfrissen.

Voor batchbestemmingen kunt u de toegang of de geheime sleutel bijwerken als een van deze wijzigingen is gewijzigd. Als u uw bestanden verder wilt coderen, kunt u bovendien een openbare RSA-sleutel invoegen en worden uw geëxporteerde bestanden vervolgens versleuteld.

![&#x200B; Rekeningen tabel &#x200B;](../assets/ui/update-accounts/destination-accounts.png)

## Accounts bijwerken {#update}

Voer de onderstaande stappen uit om verbindingsgegevens bij te werken naar bestaande doelen.

1. Login aan het [&#x200B; Experience Platform UI &#x200B;](https://platform.adobe.com/) en selecteert **[!UICONTROL Destinations]** van de linkernavigatiebar. Selecteer **[!UICONTROL Accounts]** in de bovenste koptekst om uw bestaande accounts weer te geven.

   ![&#x200B; Rekeningen tabel &#x200B;](../assets/ui/update-accounts/accounts-tab.png)

2. Selecteer het filterpictogram ![&#x200B; filter-pictogram &#x200B;](/help/images/icons/filter.png) op de bovenkant verlaten om het soortpaneel te lanceren. Het deelvenster Sorteren bevat een lijst met al uw doelen. U kunt meer dan één bestemming van de lijst selecteren om een gefilterde selectie van rekeningen te zien verbonden aan de geselecteerde bestemmingen.

   ![&#x200B; de bestemmingsrekeningen van de Filter &#x200B;](../assets/ui/update-accounts/filter-accounts.png)

3. Selecteer de ovalen (`...`) naast de naam van de account die u wilt bijwerken. Er verschijnt een pop-upvenster met opties voor **[!UICONTROL Activate audiences]** , **[!UICONTROL Edit details]** en **[!UICONTROL Delete]** de account. Selecteer ![&#x200B; uitgeven detailknoop &#x200B;](/help/images/icons/edit.png) **[!UICONTROL Edit details]** knoop om de rekeningsinformatie uit te geven.

   ![&#x200B; geef rekening &#x200B;](../assets/ui/update-accounts/accounts-edit.png) uit

4. Voer uw bijgewerkte accountgegevens in.

   * Voor accounts die een `OAuth1` - of `OAuth2` verbindingstype gebruiken, selecteert u **[!UICONTROL Reconnect OAuth]** om uw accountgegevens te vernieuwen. U kunt ook de naam en beschrijving van uw account bijwerken.

   ![&#x200B; geef details OAuth &#x200B;](../assets/ui/update-accounts/edit-details-oauth.png) uit

   * Voor accounts die een verbindingstype `Access Key` of `ConnectionString` gebruiken, kunt u de verificatiegegevens van uw account bewerken, zoals toegang-id, geheime sleutels of verbindingstekenreeksen. U kunt ook de naam en beschrijving van uw account bijwerken.

   ![&#x200B; geef de Sleutel van de Toegang van details uit &#x200B;](../assets/ui/update-accounts/edit-details-key.png)

   * Voor accounts die een verbindingstype `Bearer token` gebruiken, kunt u indien nodig een nieuw token voor toonder invoeren. U kunt ook de naam en beschrijving van uw account bijwerken.

   ![&#x200B; geeft het teken van de Details Drager uit &#x200B;](../assets/ui/update-accounts/edit-details-bearer.png)

   * Voor accounts die een verbindingstype `Server to server` gebruiken, kunt u de naam en beschrijving van uw account bijwerken.

   ![&#x200B; geeft details Server-aan-server &#x200B;](../assets/ui/update-accounts/edit-details-s2s.png) uit

5. Selecteer **[!UICONTROL Save]** om de update van de accountdetails te voltooien.

## Volgende stappen

Door deze zelfstudie te volgen, hebt u de werkruimte van **[!UICONTROL destinations]** gebruikt om bestaande accounts bij te werken.

Voor meer informatie over bestemmingen, verwijs naar het [&#x200B; overzicht van bestemmingen &#x200B;](../catalog/overview.md).