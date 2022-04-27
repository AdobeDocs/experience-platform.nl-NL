---
keywords: doel verbinden;doel verbindt;hoe te bestemming verbinden
title: Een nieuwe doelverbinding maken
type: Tutorial
description: In deze zelfstudie worden de stappen beschreven die u moet uitvoeren om verbinding te maken met een doel in Adobe Experience Platform
exl-id: 56d7799a-d1da-4727-ae79-fb2c775fe5a5
source-git-commit: b275621d9c6552327e0e55c00c8fcf0397088168
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# Een nieuwe doelverbinding maken

## Overzicht {#overview}

Voordat u publieksgegevens naar een bestemming kunt verzenden, moet u een verbinding naar het doelplatform instellen. In dit artikel ziet u hoe u een nieuwe bestemming instelt via de Adobe Experience Platform-gebruikersinterface.

## Een nieuwe doelverbinding maken {#setup}

1. Ga naar **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** en selecteert u de **[!UICONTROL Catalog]** tab.

   ![Cataloguspagina](../assets/ui/connect-destinations/catalog.png)

1. Afhankelijk van of u een bestaande verbinding aan uw bestemming hebt, kunt u of zien **[!UICONTROL Set up]** of **[!UICONTROL Activate segments]** op de doelkaart. Voor meer informatie over het verschil tussen **[!UICONTROL Activate segments]** en **[!UICONTROL Set up]**, verwijst u naar de [Catalogus](../ui/destinations-workspace.md#catalog) in de documentatie van de doelwerkruimte.

   Selecteer **[!UICONTROL Set up]** of **[!UICONTROL Activate segments]**, afhankelijk van de knop die voor u beschikbaar is.

   ![Cataloguspagina](../assets/ui/connect-destinations/set-up.png)

   ![Segmenten activeren](../assets/ui/connect-destinations/activate-segments.png)

1. Als u **[!UICONTROL Set up]**, gaat u verder met de volgende stap.

   Als u **[!UICONTROL Activate segments]** kunt u nu een lijst met bestaande doelverbindingen zien.

   Selecteer **[!UICONTROL Configure new destination]**.

   ![Nieuwe bestemming configureren](../assets/ui/connect-destinations/configure-new-destination.png)

1. Voer de verbindingsgegevens van het doelplatform in en selecteer **[!UICONTROL Connect to destination]**.

   >[!NOTE]
   >
   >De onderstaande afbeelding wordt alleen ter illustratie gebruikt. De details van de bestemmingsverbinding variëren tussen bestemmingen. Voor gedetailleerde informatie over de verbindingsdetails voor uw bestemming, zie **Verbindingsparameters** sectie in elke [doelcatalogus](../catalog/overview.md) pagina (bijvoorbeeld [Google Customer Match](..//catalog/advertising/google-customer-match.md#parameters)).

   ![Verbinden met doel](../assets/ui/connect-destinations/connect-destination.png)

1. (Optioneel) Selecteer de waarschuwingen voor de doelgegevensstroom waarop u zich wilt abonneren. U kunt zich op alarm abonneren wanneer het creëren van een gegevensstroom om waakzame berichten betreffende de status, het succes, of het mislukken van uw looppas te ontvangen. Zie [Abonneren op in-context-bestemmingswaarschuwingen](alerts.md) voor gedetailleerde informatie over waarschuwingen over bestemmingsgegevensstroom.

   ![UI-afbeelding die de in-context bestemmingswaarschuwingen-abonnementsopties weergeeft](../assets/ui/connect-destinations/subscribe-to-alerts.png)

1. Selecteer **[!UICONTROL Next]**.

   ![Verbinden met doel](../assets/ui/connect-destinations/next.png)

1. Selecteer de marketingacties die van toepassing zijn op de gegevens die u naar de bestemming wilt exporteren. Marketingsacties geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door Adobe gedefinieerde marketingacties of u kunt uw eigen marketingactie maken. Zie voor meer informatie over marketingacties de [overzicht van beleidsregels voor gegevensgebruik](../../data-governance/policies/overview.md) pagina.

   ![marketingacties selecteren](../assets/ui/connect-destinations/governance.png)

1. Selecteren **[!UICONTROL Save & Exit]** om de bestemmingsconfiguratie te bewaren, of te selecteren **[!UICONTROL Next]** om door te gaan naar de publieksgegevens [activeringsstroom](activation-overview.md).