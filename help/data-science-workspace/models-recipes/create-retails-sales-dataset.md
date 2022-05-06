---
keywords: Experience Platform;winkelrecept;Data Science Workspace;populaire onderwerpen;recepten
solution: Experience Platform
title: Het detailhandelsschema en de gegevensset maken
topic-legacy: tutorial
type: Tutorial
description: Deze zelfstudie biedt u de voorwaarden en elementen die vereist zijn voor alle andere zelfstudies voor de Adobe Experience Platform Data Science Workspace. Na voltooiing, zullen het Retailschema en de datasets van de Verkoop voor u en leden van uw organisatie IMS op Experience Platform beschikbaar zijn.
exl-id: 1b868c8c-7c92-4f99-8486-54fd7aa1af48
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---


# Het detailhandelschema en de dataset maken

Deze zelfstudie biedt u de voorwaarden en elementen die vereist zijn voor alle andere onderdelen [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] zelfstudies. Na voltooiing, zullen het Retailschema en de datasets van de Verkoop voor u en leden van uw IMS Organisatie op [!DNL Experience Platform].

## Aan de slag

Voordat u deze zelfstudie kunt starten, moet u aan de volgende voorwaarden voldoen:
- Toegang tot [!DNL Adobe Experience Platform]. Als u geen toegang hebt tot een IMS-organisatie in [!DNL Experience Platform], spreek gelieve met uw systeembeheerder alvorens te werk te gaan.
- Toestemming om [!DNL Experience Platform] API-aanroepen. Voltooi de [Adobe Experience Platform API&#39;s verifiëren en openen](https://www.adobe.com/go/platform-api-authentication-en) zelfstudie voor het verkrijgen van de volgende waarden om deze zelfstudie te voltooien:
   - Autorisatie: `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{ORG_ID}`
   - Klantgeheim: `{CLIENT_SECRET}`
   - Clientcertificaat: `{PRIVATE_KEY}`
- Voorbeeldgegevens en bronbestanden voor de [Recipe detailhandel](../pre-built-recipes/retail-sales.md). Download de benodigde middelen voor dit en andere [!DNL Data Science Workspace] zelfstudies van de [Adobe openbare Git-opslagplaats](https://github.com/adobe/experience-platform-dsw-reference/).
- [Python >= 2,7](https://www.python.org/downloads/) en de volgende [!DNL Python] pakketten:
   - [pip](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [dictor](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- Een goed begrip van de volgende concepten die in deze zelfstudie worden gebruikt:
   - [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)
   - [Basisbeginselen van de schemacompositie](../../xdm/schema/field-dictionary.md)

## Handelsschema en gegevensset maken

Het schema en de datasets van de Verkoop van de detailhandel worden gecreeerd automatisch door het verstrekte laarzentrekkermanuscript te gebruiken. Voer onderstaande stappen uit in de volgorde:

### Bestanden configureren

1. Binnen de [!DNL Experience Platform] bronnenpakket van zelfstudie, navigeer naar de map `bootstrap`en open `config.yaml` een geschikte teksteditor gebruiken.
2. Onder de `Enterprise` in, voert u de volgende waarden in:

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {ORG_ID}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. Bewerk de waarden onder het dialoogvenster `Platform` sectie, Voorbeeld hieronder:

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
   - `ingest_data`: Voor deze zelfstudie stelt u deze waarde in als `"True"` om de detailhandelschema&#39;s en datasets van de Verkoop tot stand te brengen. Een waarde van `"False"` alleen de schema&#39;s maken.
   - `build_recipe_artifacts`: Voor deze zelfstudie stelt u deze waarde in als `"False"` om te voorkomen dat het script een Recipe-artefact genereert.
   - `kernel_type`: Het uitvoeringstype van het Recipe-artefact. Deze waarde behouden als `Python` indien `build_recipe_artifacts` is ingesteld als `"False"`, anders het correcte uitvoeringstype specificeren.

4. Onder de `Titles` de volgende informatie voor de voorbeeldgegevens van de detailhandel op de juiste wijze verstrekken, het bestand opslaan en sluiten nadat de bewerkingen zijn uitgevoerd. Voorbeeld hieronder:

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

1. Open de terminaltoepassing en navigeer naar de [!DNL Experience Platform] bronnenmap van de zelfstudie.
2. Stel de `bootstrap` als het huidige werkpad en voer het `bootstrap.py` [!DNL Python] door de volgende opdracht in te voeren:

   ```bash
   python bootstrap.py
   ```

   >[!NOTE]
   >
   >Het script kan enkele minuten duren.

## Volgende stappen

Op succesvolle voltooiing van het laarzentrekkerscript, kunnen de de input en outputschema&#39;s en datasets van de Verkoop de detailhandel worden bekeken [!DNL Experience Platform]. Zie de [voorbeeldschemagegevenszelfstudie](./preview-schema-data.md)
voor meer informatie .

Je hebt ook voorbeeldgegevens voor detailhandel opgenomen in [!DNL Experience Platform] het gebruiken van het verstrekte laarsmanuscript.

U kunt als volgt met de opgenomen gegevens blijven werken:
- [Uw gegevens analyseren met Jupyter-laptops](../jupyterlab/analyze-your-data.md)
   - Gebruik Jupyter-laptops in de Data Science Workspace voor toegang tot, verkenning, visualisatie en begrip van uw gegevens.
- [Bronbestanden in een pakket plaatsen in een ontvanger](./package-source-files-recipe.md)
   - Volg deze zelfstudie om te leren hoe u uw eigen model in kunt brengen [!DNL Data Science Workspace] door bronbestanden te verpakken in een importeerbaar Recipe-bestand.
