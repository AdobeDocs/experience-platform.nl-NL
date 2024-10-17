---
title: Dynamische gegevensstroomconfiguraties maken
description: Leer hoe te om dynamische configuraties tot stand te brengen datastream, om uw gegevens aan diverse diensten van het Experience Cloud te leiden, die op regels worden gebaseerd.
hide: true
hidefromtoc: true
badge: label="Beta" type="Informative"
source-git-commit: 86416dc11f92a774cda5d95365d3981a637a5595
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 0%

---


# Dynamische gegevensstroomconfiguraties maken

>[!AVAILABILITY]
>
>* De optie voor het definiëren van dynamische gegevensstroomconfiguraties is momenteel in Beta beschikbaar voor een beperkt aantal klanten. Neem contact op met uw Adobe als u toegang wilt tot deze functie. De documentatie en de functionaliteit kunnen worden gewijzigd.

Door gebrek, verzendt de Edge Network van het Experience Platform alle gebeurtenissen die een gegevensstroom aan alle Experience Cloud [ diensten ](configure.md#add-services) bereiken die u voor uw gegevensstromen hebt toegelaten. Dit is wellicht niet altijd de ideale workflow voor u, afhankelijk van uw gebruiksgevallen.

De dynamische configuraties van gegevensstroom richten deze zorg door gebruiker-configureerbare reeksen regels die u voor elke dienst bepaalt die voor uw gegevensstroom wordt toegelaten, die dicteert welke oplossing van het Experience Cloud elk type van gegevens zou moeten ontvangen.

## Vereisten {#prerequisites}

Om een dynamische configuratie voor uw gegevensstroom tot stand te brengen, zijn er twee voorwaarden u moet ontmoeten:

* U moet *minstens* één gegevensstroom hebben gecreeerd om met te werken. Zie de documentatie over hoe te [ een datastream ](configure.md) voor gedetailleerde informatie tot stand brengen.
* U moet *minstens* hebben één die de dienst van het Experience Cloud aan uw gegevensstroom wordt toegevoegd. Zie de documentatie over hoe te [ om de dienst ](configure.md#add-services) aan een datastream voor gedetailleerde informatie toe te voegen.

Nadat u een datastream hebt gecreeerd en de dienst van het Experience Cloud aan het toegevoegd, kunt u dan [ een dynamische configuratie ](#create-dynamic-configuration) creëren.

## Een dynamische gegevensstroomconfiguratie maken {#create-dynamic-configuration}

Nadat u [ een datastream ](configure.md) hebt gecreeerd en [ de dienst ](configure.md#add-services) aan het toegevoegd, volg de stappen hieronder om een dynamische configuratie aan de dienst toe te voegen.

1. Ga naar de pagina **[!UICONTROL Data Collection]** > **[!UICONTROL Datastreams]** en selecteer de gegevensstroom die u hebt gemaakt.

   ![ Beeld van het gebruikersinterface dat van gegevensstromen de lijst van gegevensstromen toont.](assets/configure-dynamic-datastream/select-datastream.png)

1. Selecteer de optie **[!UICONTROL Edit]** op de service waarvoor u een dynamische configuratie wilt definiëren.

   ![ Beeld van het gebruikersinterface van gegevensstromen die de diensten tonen aan een gegevensstroom worden toegevoegd.](assets/configure-dynamic-datastream/select-service.png)

1. Selecteer **[!UICONTROL Save and Edit Dynamic Configuration]** op de pagina **[!UICONTROL Configure]** .

   ![ Beeld van het gebruikersinterface van gegevensstromen die de pagina van de gegevensstroomconfiguratie tonen.](assets/configure-dynamic-datastream/save-and-edit.png)

1. Selecteer **[!UICONTROL Add Dynamic Configuration]**.

   ![ Beeld van het gebruikersinterface van gegevensstromen die de dynamische configuratie op regel toevoegen bericht tonen.](assets/configure-dynamic-datastream/add-dynamic-config.png)

1. Sleep vanuit het deelvenster **[!UICONTROL Resources]** de items waarmee u de lijn wilt maken naar de rechterkant van het venster. U kunt veelvoudige middelen combineren om complexe regels te bouwen.

   Gebruik de opties van elke bron, zoals **[!UICONTROL equals]** , **[!UICONTROL does not equal]** , **[!UICONTROL exists]** en meer, om de regels te perfectioneren.

   ![ Beeld van het gebruikersinterface van gegevensstromen die de dynamische configuratieregel tonen.](assets/configure-dynamic-datastream/drag-resources.png)

1. Schakel in de sectie **[!UICONTROL Configuration]** de services in of uit die u voor elke regel wilt in- of uitschakelen, afhankelijk van het feit of u de gegevens naar elke service wilt verzenden. Als u de knevel weg zet, wordt de regel onbruikbaar gemaakt en *alle gegevens* zullen naar de stroomopwaartse dienst worden verzonden.

   ![ Beeld van het gebruikersinterface van gegevensstromen die de dynamische configuratieregel tonen.](assets/configure-dynamic-datastream/enable-service.png)

1. Wanneer u klaar bent met het configureren van de regels, selecteert u **[!UICONTROL Save]** .

## Prioriteitsoverwegingen voor regels {#considerations}

U kunt veelvoudige regels voor elke dynamische configuratie van de gegevensstroom bepalen. Als uw gegevens echter overeenkomen met de voorwaarden van meerdere regels, wordt alleen de eerste overeenkomende regel in de lijst in aanmerking genomen en worden alle andere overeenkomende regels genegeerd.

Om de gewenste gegevens te bereiken die gedrag verpletteren, let op de orde waarin u de regels schikt.

Om de regelorde te vormen, kunt u de regelvensters in de orde slepen u wilt.

![ GIF die tonen hoe te om de orde van regels door belemmering en daling te veranderen.](assets/configure-dynamic-datastream/move-rules.gif)