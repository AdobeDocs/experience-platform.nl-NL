---
keywords: Experience Platform;kleinhandelsrecept;Data Science Workspace;populaire onderwerpen;recepten
solution: Experience Platform
title: Het detailhandelsschema en de gegevensset maken
type: Tutorial
description: Deze zelfstudie biedt u de voorwaarden en elementen die vereist zijn voor alle andere zelfstudies van Adobe Experience Platform Data Science Workspace. Na voltooiing, zullen het Retailschema en de datasets van de Verkoop voor u en leden van uw organisatie op Experience Platform beschikbaar zijn.
exl-id: 1b868c8c-7c92-4f99-8486-54fd7aa1af48
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 0%

---


# Het detailhandelschema en de dataset maken

>[!NOTE]
>
>Data Science Workspace kan niet meer worden aangeschaft.
>
>Deze documentatie is bedoeld voor bestaande klanten met eerdere rechten op Data Science Workspace.

Deze zelfstudie biedt u de voorwaarden en elementen die vereist zijn voor alle andere zelfstudies van [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] . Na voltooiing, zullen het Retailschema en de datasets van de Verkoop voor u en leden van uw organisatie op [!DNL Experience Platform] beschikbaar zijn.

## Aan de slag

Voordat u deze zelfstudie kunt starten, moet u aan de volgende voorwaarden voldoen:

- Toegang tot [!DNL Adobe Experience Platform] . Als u geen toegang hebt tot een organisatie in [!DNL Experience Platform] , neemt u contact op met uw systeembeheerder voordat u verdergaat.
- Autorisatie om [!DNL Experience Platform] API-aanroepen uit te voeren. Voltooi [ verifieer en toegang Adobe Experience Platform APIs ](https://www.adobe.com/go/platform-api-authentication-en) leerprogramma om de volgende waarden te verkrijgen om dit leerprogramma te voltooien:
   - Autorisatie: `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{ORG_ID}`
   - Clientgeheim: `{CLIENT_SECRET}`
   - Clientcertificaat: `{PRIVATE_KEY}`
- De gegevens van de steekproef en brondossiers voor [ Recipe van de Verkoop van de Kleinhandel ](../pre-built-recipes/retail-sales.md). Download de activa die voor dit en andere [!DNL Data Science Workspace] leerprogramma&#39;s van de [ openbare bewaarplaats van het Git van Adobe ](https://github.com/adobe/experience-platform-dsw-reference/) worden vereist.
- [ Python >= 2.7 ](https://www.python.org/downloads/) en de volgende [!DNL Python] pakketten:
   - [ pip ](https://pypi.org/project/pip/)
   - [ PyYAML ](https://pyyaml.org/)
   - [ dictor ](https://pypi.org/project/dictor/)
   - [ JWT ](https://pypi.org/project/jwt/)
- Een goed begrip van de volgende concepten die in deze zelfstudie worden gebruikt:
   - [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)
   - [Basisbeginselen van de schemacompositie](../../xdm/schema/field-dictionary.md)

## Handelsschema en gegevensset maken

Het schema en de datasets van de Verkoop van de detailhandel worden gecreeerd automatisch door het verstrekte laarzentrekkermanuscript te gebruiken. Voer onderstaande stappen uit in de volgorde:

### Bestanden configureren

1. Navigeer in het bronnenpakket van [!DNL Experience Platform] naar de map `bootstrap` en open `config.yaml` met een geschikte teksteditor.
2. Voer onder de sectie `Enterprise` de volgende waarden in:

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {ORG_ID}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. Bewerk de waarden in de sectie `Platform` Voorbeeld hieronder:

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway`: Het basispad voor API-aanroepen. Wijzig deze waarde niet.
   - `ims_token`: Uw `{ACCESS_TOKEN}` komt hier.
   - `ingest_data`: In deze zelfstudie stelt u deze waarde in als `"True"` om de detailhandelsverkoopschema&#39;s en -gegevenssets te maken. Met de waarde `"False"` worden alleen de schema&#39;s gemaakt.
   - `build_recipe_artifacts`: In deze zelfstudie stelt u deze waarde in als `"False"` om te voorkomen dat het script een Recipe-artefact genereert.
   - `kernel_type`: Het uitvoeringstype van het Recipe-artefact. Laat deze waarde ongewijzigd `Python` als `build_recipe_artifacts` is ingesteld als `"False"` . Geef anders het juiste uitvoeringstype op.

4. Geef onder de sectie `Titles` de volgende informatie op die geschikt is voor de voorbeeldgegevens van de detailhandel, sla het bestand op en sluit het nadat de bewerkingen zijn uitgevoerd. Voorbeeld hieronder:

   ```yaml
   Titles:
       input_class_title: retail_sales_input_class
       input_mixin_title: retail_sales_input_mixin
       input_mixin_definition_title: retail_sales_input_mixin_definition
       input_schema_title: retail_sales_input_schema
       input_dataset_title: retail_sales_input_dataset
       file_replace_tenant_id: DSWRetailSalesForXDM0.9.9.9.json
       file_with_tenant_id: DSWRetailSales_with_tenant_id.json
       is_output_schema_different: "True"
       output_mixin_title: retail_sales_output_mixin
       output_mixin_definition_title: retail_sales_output_mixin_definition
       output_schema_title: retail_sales_output_title
       output_dataset_title: retail_sales_output_dataset
   ```

### Het opstartscript uitvoeren

1. Open de terminaltoepassing en navigeer naar de bronnenmap van [!DNL Experience Platform] .
2. Stel de map `bootstrap` in als het huidige tijdelijke pad en voer het script `bootstrap.py` [!DNL Python] uit door de volgende opdracht in te voeren:

   ```bash
   python bootstrap.py
   ```

   >[!NOTE]
   >
   >Het script kan enkele minuten duren.

## Volgende stappen

Na succesvolle voltooiing van het laarzentrekkerscript kunnen de invoer- en uitvoerschema&#39;s en datasets van de detailhandel op [!DNL Experience Platform] worden weergegeven. Zie het [ leerprogramma van de voorproefschemagegevens ](./preview-schema-data.md)
voor meer informatie .

U hebt ook met succes de gegevens van de steekproef van de Verkoop van de Handel in [!DNL Experience Platform] opgenomen gebruikend het verstrekte laarsmanuscript.

U kunt als volgt met de opgenomen gegevens blijven werken:

- [Uw gegevens analyseren met Jupyter-laptops](../jupyterlab/analyze-your-data.md)
   - Gebruik Jupyter-laptops in Data Science Workspace om toegang te krijgen tot uw gegevens, deze te verkennen, te visualiseren en te begrijpen.
- [Bronbestanden in een pakket plaatsen in een ontvanger](./package-source-files-recipe.md)
   - Volg deze zelfstudie om te leren hoe u uw eigen model in [!DNL Data Science Workspace] kunt plaatsen door bronbestanden in een importeerbaar Recipe-bestand te verpakken.
