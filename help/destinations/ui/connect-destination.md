---
keywords: doel verbinden;doel verbindt;hoe te bestemming verbinden
title: Een nieuwe doelverbinding maken
type: Tutorial
description: In deze zelfstudie worden de stappen beschreven die u moet uitvoeren om verbinding te maken met een doel in Adobe Experience Platform
exl-id: 56d7799a-d1da-4727-ae79-fb2c775fe5a5
source-git-commit: f4721d3f114357b25517e4e66f1f626f82621c34
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 1%

---

# Een nieuwe doelverbinding maken

## Overzicht {#overview}

Voordat u publieksgegevens naar een bestemming kunt verzenden, moet u een verbinding naar het doelplatform instellen. In dit artikel ziet u hoe u een nieuwe bestemming instelt via de Adobe Experience Platform-gebruikersinterface.

## Een nieuwe doelverbinding maken {#setup}

1. Ga naar **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** en selecteer het tabblad **[!UICONTROL Catalog]**.

   ![Cataloguspagina](../assets/ui/connect-destinations/catalog.png)

1. Afhankelijk van of u een bestaande verbinding aan uw bestemming hebt, kunt u of een **[!UICONTROL Set up]** of een **[!UICONTROL Activate segments]** knoop op de bestemmingskaart zien. Raadpleeg voor meer informatie over het verschil tussen **[!UICONTROL Activate segments]** en **[!UICONTROL Set up]** de sectie [Catalog](../ui/destinations-workspace.md#catalog) van de documentatie van de doelwerkruimte.

   Selecteer **[!UICONTROL Set up]** of **[!UICONTROL Activate segments]**, afhankelijk van welke knoop aan u beschikbaar is.

   ![Cataloguspagina](../assets/ui/connect-destinations/set-up.png)

   ![Segmenten activeren](../assets/ui/connect-destinations/activate-segments.png)

1. Als u **[!UICONTROL Set up]** hebt geselecteerd, gaat u verder met de volgende stap.

   Als u **[!UICONTROL Activate segments]** selecteerde, kunt u een lijst van bestaande bestemmingsverbindingen nu zien.

   Selecteer **[!UICONTROL Configure new destination]**.

   ![Nieuwe bestemming configureren](../assets/ui/connect-destinations/configure-new-destination.png)

1. Voer de verbindingsgegevens van het doelplatform in en selecteer **[!UICONTROL Connect to destination]**.

   >[!NOTE]
   >
   >De onderstaande afbeelding wordt alleen ter illustratie gebruikt. De details van de bestemmingsverbinding variëren tussen bestemmingen. Zie de sectie **Verbindingsparameters** in elke [doelcatalogus](../catalog/overview.md)-pagina (bijvoorbeeld [Google Customer Match](..//catalog/advertising/google-customer-match.md#parameters)) voor gedetailleerde informatie over de verbindingsdetails voor uw bestemming.

   ![Verbinden met doel](../assets/ui/connect-destinations/connect-destination.png)

1. Selecteer **[!UICONTROL Next]**.

   ![Verbinden met doel](../assets/ui/connect-destinations/next.png)

1. Selecteer de marketingacties die van toepassing zijn op de gegevens die u naar de bestemming wilt exporteren. Marketingsacties geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door Adobe gedefinieerde marketingacties of u kunt uw eigen marketingactie maken. Zie de pagina [Beleid voor gegevensgebruik overzicht](../../data-governance/policies/overview.md) voor meer informatie over marketingacties.

   ![marketingacties selecteren](../assets/ui/connect-destinations/governance.png)

1. Selecteer **[!UICONTROL Save & Exit]** om de bestemmingsconfiguratie te bewaren, of **[!UICONTROL Next]** te selecteren om aan de publieksgegevens [activeringsstroom](activation-overview.md) te werk te gaan.