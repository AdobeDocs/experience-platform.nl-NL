---
keywords: Experience Platform;retail sales recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Het detailhandelschema en de dataset maken
topic: Tutorial
translation-type: tm+mt
source-git-commit: 83e74ad93bdef056c8aef07c9d56313af6f4ddfd
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---


# Het detailhandelschema en de dataset maken

Deze zelfstudie biedt u de voorwaarden en elementen die vereist zijn voor alle andere zelfstudies over de [!DNL Adobe Experience Platform] Data Science Workspace. Na voltooiing, zullen het Retailschema en de datasets van de Verkoop voor u en leden van uw organisatie IMS op het Platform van de Ervaring beschikbaar zijn.

## Aan de slag

Voordat u deze zelfstudie kunt starten, moet u aan de volgende voorwaarden voldoen:
- Toegang tot [!DNL Adobe Experience Platform]. Als u geen toegang tot een IMS Organisatie in het Platform van de Ervaring hebt, gelieve met uw systeembeheerder te spreken alvorens te werk te gaan.
- Toestemming voor het maken van API-aanroepen van Experience Platform. Voltooi de zelfstudie voor het [verifiëren en openen van de API&#39;s](../../tutorials/authentication.md) van het Adobe Experience Platform voor het verkrijgen van de volgende waarden om deze zelfstudie te voltooien:
   - Autorisatie: `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{IMS_ORG}`
   - Klantgeheim: `{CLIENT_SECRET}`
   - Clientcertificaat: `{PRIVATE_KEY}`
- Voorbeeldgegevens en bronbestanden voor de [Retail Sales Recipe](../pre-built-recipes/retail-sales.md). Download de benodigde middelen voor deze en andere zelfstudies voor de Data Science Workspace van de [Adobe Public Git-opslagplaats](https://github.com/adobe/experience-platform-dsw-reference/).
- [Python >= 2,7](https://www.python.org/downloads/) en de volgende Python-verpakkingen:
   - [pip](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [dictor](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- Een goed begrip van de volgende concepten die in deze zelfstudie worden gebruikt:
   - [Experience Data Model (XDM)](../../xdm/home.md)
   - [Basisbeginselen van de schemacompositie](../../xdm/schema/field-dictionary.md)

## Handelsschema en gegevensset maken

Het schema en de datasets van de Verkoop van de detailhandel worden gecreeerd automatisch door het verstrekte laarzentrekkermanuscript te gebruiken. Voer onderstaande stappen uit in de volgorde:

### Bestanden configureren

1. Navigeer in het bronnenpakket van het Experience Platform naar de map `bootstrap``config.yaml` en open de map met een geschikte teksteditor.
2. Voer onder de `Enterprise` sectie de volgende waarden in:

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {IMS_ORG}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. Bewerk de waarden in de `Platform` sectie, Voorbeeld hieronder:

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway` : Het basispad voor API-aanroepen. Wijzig deze waarde niet.
   - `ims_token` : Je `{ACCESS_TOKEN}` gaat hier.
   - `ingest_data` : Voor dit leerprogramma, plaats deze waarde zoals `"True"` om de Retailverkoopschema&#39;s en datasets tot stand te brengen. Een waarde van `"False"` zal slechts tot de schema&#39;s leiden.
   - `build_recipe_artifacts` : Voor deze zelfstudie stelt u deze waarde zo in dat het script geen Recipe-artefact genereert. `"False"`
   - `kernel_type` : Het uitvoeringstype van het Recipe-artefact. Laat deze waarde ongewijzigd `Python` of `build_recipe_artifacts` is ingesteld als `"False"`, anders geef je het juiste uitvoeringstype op.

4. Geef onder de `Titles` sectie de volgende informatie op die geschikt is voor de voorbeeldgegevens van de detailhandel, sla het bestand op en sluit het nadat de bewerkingen zijn uitgevoerd. Voorbeeld hieronder:

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

1. Open uw eindtoepassing en navigeer naar de folder van het Leerprogramma van het Platform van de Ervaring.
2. Stel de `bootstrap` map in als het huidige tijdelijke pad en voer het `bootstrap.py` pythonscript uit door de volgende opdracht in te voeren:

   ```bash
   python bootstrap.py
   ```

   > [!NOTE] Het script kan enkele minuten duren.

## Volgende stappen

Na succesvolle voltooiing van het laarzentrekkerscript, kunnen de de input en outputschema&#39;s en datasets van de Handel op het Platform van de Ervaring worden bekeken. Zie de [voorbeeldschemagegevenszelfstudie](./preview-schema-data.md)voor meer informatie.

U hebt ook met succes de met succes gegevens van de steekproef van de Verkoop van de Handel in het Platform van de Ervaring opgenomen gebruikend het verstrekte laarzentrekkerscript.

U kunt als volgt met de opgenomen gegevens blijven werken:
- [Uw gegevens analyseren met Jupyter-laptops](../jupyterlab/analyze-your-data.md)
   - Gebruik Jupyter-laptops in de Data Science Workspace voor toegang tot, verkenning, visualisatie en begrip van uw gegevens.
- [Bronbestanden in een pakket plaatsen in een ontvanger](./package-source-files-recipe.md)
   - Volg deze zelfstudie om te leren hoe u uw eigen model in de werkruimte van de Wetenschap van Gegevens kunt brengen door bronbestanden in een importeerbaar Recipe-bestand te verpakken.