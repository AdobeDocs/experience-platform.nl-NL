---
keywords: Experience Platform;attribution ai;access scores;popular topics
solution: Experience Platform
title: Muziek openen in Attribution AI
topic: Accessing scores
translation-type: tm+mt
source-git-commit: 0f6424c5afbf9b23016e1c40d156f6226f853cd6

---


# Muziek openen in Attribution AI

>[!IMPORTANT] Neem contact op met attributionai-support@adobe.com voor meer informatie over downloads van onbewerkte scores voor het bulksgewijs exporteren van gegevens.

De toegang tot scores voor Attribution AI wordt gedaan door Snowflake. U moet momenteel een e-mail sturen naar de ondersteuning van Adobe op attributionai-support@adobe.com om de aanmeldingsgegevens voor Snowflake in te stellen en deze naar uw lezeraccount te ontvangen.

Nadat uw verzoek door Adobe-ondersteuning is verwerkt, ontvangt u een URL voor het lezeraccount voor Snowflake en de bijbehorende referenties hieronder:

- Sneeuwvlok-URL
- Gebruikersnaam
- Wachtwoord

>[!NOTE] De lezeraccount is bedoeld voor het opvragen van gegevens met SQL-clients, werkbladen en BI-oplossingen die JDBC-connector ondersteunen.

Zodra u uw geloofsbrieven en URL hebt, kunt u de modellijsten, of in hun ruwe formaat vragen., samengevoegd door touchpoint datum, of omzettingsdatum.

## Schema zoeken in Snowflake

Meld u aan bij Snowflake met de opgegeven referenties. Klik op het tabblad **Werkbladen** in de hoofdnavigatie linksboven en navigeer naar de databasemap in het linkerdeelvenster.

![Werkbladen en navigatie](./images/download-scores/edited_snowflake_1.png)

Klik vervolgens op Schema **** selecteren in de rechterbovenhoek van het scherm. Bevestig in de pop-up die wordt weergegeven dat u de juiste database hebt geselecteerd. Klik vervolgens op het vervolgkeuzemenu *Schema* en selecteer een van de weergegeven schema&#39;s. U kunt rechtstreeks zoeken vanuit de scoretabellen die onder het geselecteerde schema staan.

![zoeken naar een schema](./images/download-scores/edited_snowflake_2.png)

## Raw-scores downloaden van Sneeuwvlok

Neem contact op met attributionai-support@adobe.com voor meer informatie over downloads van onbewerkte scores.

## PowerBI aansluiten op sneeuwvlok (optioneel)

Uw Sneeuwvloke-referenties kunnen worden gebruikt om een verbinding tot stand te brengen tussen PowerBI Desktop- en Snowflake-databases.

Typ eerst in het vak *Server* onder Sneeuwvlok-URL. Vervolgens typt u onder *Winkel*&quot;XSMALL&quot;. Typ vervolgens uw gebruikersnaam en wachtwoord.

![voorbeeld van POWERBI](./images/download-scores/powerbi-snowflake.png)

Nadat de verbinding tot stand is gebracht, selecteert u de Snowflake-database en selecteert u het gewenste schema. U kunt nu alle tabellen laden.

Nadat u het schema hebt geselecteerd, worden tabellen weergegeven met de toewijzingsscores.

| Tabel | Beschrijving |
| ----- | ----------- |
| APP_{APP_ID} | Onbewerkte toewijzingsscore. |
| APP_{APP_ID}_BY_CONV_DATE | Onbewerkte toewijzingsscore geaggregeerd op het niveau van de conversiedatum. |
| APP_{APP_ID}_BY_TP_DATE | Onbewerkte toewijzingsscore geaggregeerd op aanraakpuntdatumniveau. |

## Volgende stappen

In dit document worden de stappen beschreven die zijn vereist voor het opvragen van gegevens en het openen van scores voor Attribution AI. U kunt nu door de andere [Intelligente Diensten](../home.md) en gidsen blijven bladeren die worden aangeboden.