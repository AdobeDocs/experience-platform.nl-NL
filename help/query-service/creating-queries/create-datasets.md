---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Gegevenssets genereren op basis van queryresultaten
topic: queries
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# Gegevenssets genereren op basis van queryresultaten

De ware macht van de Dienst van de Vraag wordt onthuld wanneer de vragen worden gebruikt om datasets in het gegevensmeer te produceren dat als input in meer vragen of in andere diensten zoals de Werkruimte van de Wetenschap van Gegevens, het Profiel van de Klant In real time, of de Werkruimte van de Analyse moet worden gebruikt.

De Dienst van de vraag staat de verwezenlijking van datasets van UI toe. Voer de volgende stappen uit:

1. Schrijf uw vraag gebruikend een verbonden cliënt en bevestig de output.
2. Meld u aan bij de gebruikersinterface van het platform en ga naar Vragen.
3. Zoek de query in de lijst en houd de muisaanwijzer boven de rij.
4. Klik op Gegevensset **maken**. ![Afbeelding](../images/queries/create-datasets/click-create-dataset.png)
5. Voer een naam voor een gegevensset in, voorafgegaan door uw LDAP-id (hoeft niet uniek of SQL-veilig te zijn). het systeem genereert een &quot;tabelnaam&quot; op basis van de hier gegeven naam).
6. Voer een beschrijving van een gegevensset in en klik op **Query** uitvoeren.![Afbeelding](../images/queries/create-datasets/run-query.png)
7. Bekijk de vraag volledig, en ga dan naar de pagina van de datasetlijst om de dataset te zien u enkel creeerde.

Nadat een dataset wordt gecreeerd, kan het als een andere dataset in het gegevensmeer worden betreden en voor een verscheidenheid van gebruiksgevallen worden gebruikt.

>[!NOTE] In een levende implementatie, moet u de etiketten van de Governance van Gegevens toepassen nadat de dataset wordt gecreeerd.

## Gegevenssets genereren met een vooraf gedefinieerd gegevensmodelschema voor ervaringsgegevens

Om een dataset met een vooraf bepaald schema van de Gegevens van de Ervaring van het Model (XDM) te produceren, zult u de SQL syntaxis moeten gebruiken. Lees voor meer informatie over de syntaxis die u moet gebruiken de handleiding [SQL Syntax](../sql/syntax.md#create-table-as-select).

## Uitvoergegevenssets

Datasets die met deze functie worden gemaakt, worden gegenereerd met een ad-hocschema dat overeenkomt met de structuur van de uitvoergegevens zoals gedefinieerd in de SQL-instructie. Voor sommige downstreamservices zijn gegevenssets met bepaalde XDM-schema&#39;s (Experience Data Model) vereist. Verifieer de gegevens het formatteren vereisten voor de stroomafwaartse diensten alvorens uw vragen te schrijven.