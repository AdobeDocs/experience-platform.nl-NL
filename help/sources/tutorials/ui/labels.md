---
title: Toegangslabels toepassen om gebruikerstoegang tot brongegevens in UI te beheren
description: Leer hoe u de gebruikersinterface van Experience Platform gebruikt om toegangslabels toe te passen en gebruikerstoegang tot uw gegevensstromen van bronnen te beheren.
exl-id: 7aab9706-2f43-43c7-9878-1959d5a8a6b0
source-git-commit: f57fa04e668fa9c61b9b15778e74969edffae0fa
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# Toegangslabels toepassen om gebruikerstoegang tot brongegevens in UI te beheren

U kunt de functies gebruiken die door [ op attributen-gebaseerde toegangscontrole ](../../../access-control/abac/overview.md) in Real-Time CDP worden verstrekt om etiketten op uw brongegevens toe te passen. Met deze eigenschap, kunt u ervoor zorgen dat slechts een ondergroep van gebruikers in uw organisatie toegang tot specifieke brongegevens krijgt.

Wanneer u een toegangslabel aan een bepaalde gegevensstroom toevoegt, slechts kunnen de gebruikers die toegang tot een rol hebben die dat etiket wordt toegewezen dat dataflow bekijken en uitgeven. Als een gegevensstroom van bronnen niet met om het even welke etiketten wordt gemerkt, is het zichtbaar aan alle gebruikers die tot uw organisatie behoren. Als u bijvoorbeeld het label C12 toepast op een gegevensstroom, kunnen gebruikers die zijn toegewezen aan een rol die niet het label C12 heeft, de gegevensstroom niet weergeven en bewerken met het label C12.

Lees deze handleiding voor informatie over het toepassen van toegangslabels op uw gegevensstromen van bronnen die de gebruikersinterface van Adobe Experience Platform gebruiken.

## Aan de slag

Alvorens met de etiketten van de toegangscontrole te werken, zorg ervoor dat u zich eerst met de mogelijkheden van op attribuut-gebaseerde toegangsbeheer vertrouwt. Raadpleeg de volgende documentatie voor meer informatie:

* [Overzicht van toegangsbeheer op basis van kenmerken](../../../access-control/abac/overview.md)
* [Op attributen-gebaseerde toegangsbeheergids van begin tot eind](../../../access-control/abac/end-to-end-guide.md)
* [Labels beheren met de gebruikersinterface voor machtigingen](../../../access-control/abac/ui/labels.md)
* [Verklarende woordenlijst met gegevensgebruikslabels](../../../data-governance/labels/reference.md)

## Toegangslabels toepassen op gegevensstromen van bronnen

>[!NOTE]
>
>* U kunt geen labels toepassen op een flowuitvoering. De flowuitvoering neemt echter alle labels over die u op de bovenliggende gegevensstroom toepast.
>
>* Als u geen meningstoegang tot een dataflow hebt, dan zult u ook niet kunnen bekijken het overeenkomstige stroomlooppas is.

Als u toegangslabels wilt toepassen op de gegevensstroom van uw bronnen, navigeert u naar **[!UICONTROL Sources]** > **[!UICONTROL Dataflows]** en zoekt u de gegevensstroom die u wilt bijwerken en beperkt u de gebruikerstoegang tot deze gegevens.

Selecteer vervolgens de ellips (`...`) in de [!UICONTROL Name] -kolom en selecteer **[!UICONTROL Apply access labels]** om labels voor de geselecteerde gegevensstroom toe te voegen en te beheren.

![ dataflows pagina in bronnen met de &quot;Apply toegangsetiketten&quot;geselecteerde optie.](../../images/tutorials/labels/apply_access_labels.png)

Het venster [!UICONTROL Apply access and data governance labels] wordt weergegeven. Gebruik dit venster om de etiketten te selecteren die u op uw gegevensstroom wilt toepassen. U kunt labels ook filteren op het type. Selecteer **[!UICONTROL Save]** als u klaar bent.

![ het venster van de etiketten van het gegevensbeheer met het C2 geselecteerde etiket.](../../images/tutorials/labels/labels_window.png)

Zodra u met succes toegangslabels aan uw gegevensstroom hebt gevormd, om het even welke gebruiker die geen toegang tot dat etiket heeft kan niet meer dataflow terugwinnen. U kunt ook de kolom [!UICONTROL Access Labels] gebruiken om de labels weer te geven die op een bepaalde gegevensstroom zijn toegepast.

## Volgende stappen

U weet nu hoe u toegangslabels op de gegevensstromen van uw bronnen kunt toepassen. U kunt er nu voor zorgen dat alleen een specifieke groep gebruikers in uw organisatie toegang heeft tot bepaalde gegevensstromen van bronnen. Lees de volgende documentatie voor meer informatie:

* [Toegangslabels toepassen op gegevensstromen van bronnen in de API](../api/labels.md)
* [Overzicht van toegangsbeheer](../../../access-control/home.md)
