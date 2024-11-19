---
keywords: Experience Platform;startpagina;populaire onderwerpen
solution: Experience Platform
title: Een gegevensset configureren voor het vastleggen van toestemmings- en voorkeursgegevens
description: Leer hoe u een XDM-schema (Experience Data Model) en een gegevensset configureert voor het vastleggen van toestemmings- en voorkeursgegevens in Adobe Experience Platform.
role: Developer
feature: Consent, Schemas, Datasets
exl-id: 61ceaa2a-c5ac-43f5-b118-502bdc432234
source-git-commit: bf651967714745a0b501dcb27373379fe014c9e1
workflow-type: tm+mt
source-wordcount: '1468'
ht-degree: 0%

---

# Een gegevensset configureren om toestemmings- en voorkeursgegevens vast te leggen

Adobe Experience Platform kan uw toestemming-/voorkeursgegevens van de klant alleen verwerken als die gegevens worden verzonden naar een gegevensset waarvan het schema velden bevat die betrekking hebben op toestemmingen en andere machtigingen. Specifiek, moet deze dataset op de [!DNL XDM Individual Profile] klasse worden gebaseerd, en voor gebruik in [!DNL Real-Time Customer Profile] worden toegelaten.

Dit document verstrekt stappen om een dataset te vormen om toestemmingsgegevens in Experience Platform te verwerken. Voor een overzicht van het volledige werkschema voor verwerkingstoestemming/voorkeur gegevens in Platform, verwijs naar het [ overzicht van de toestemmingsverwerking ](./overview.md).

>[!IMPORTANT]
>
>De voorbeelden in deze gids gebruiken een gestandaardiseerde reeks gebieden om de waarden van de klantentoestemming te vertegenwoordigen, zoals die door de [[!UICONTROL Consent and Preference Details] groep van het schemagebied ](../../../../xdm/field-groups/profile/consents.md) worden bepaald. De structuur van deze velden is bedoeld om een efficiënt gegevensmodel te bieden voor een groot aantal gemeenschappelijke gevallen waarin toestemming wordt gegeven.
>
>U kunt echter ook uw eigen veldgroepen definiëren om toestemming te vertegenwoordigen op basis van uw eigen gegevensmodellen. Vraag uw juridische team om goedkeuring voor een gegevensmodel voor toestemming dat past bij uw bedrijfsbehoeften, op basis van de volgende opties:
>
>* De standaardveldgroep voor toestemming
>* Een veldgroep voor aangepaste toestemming die door uw organisatie is gemaakt
>* Een combinatie van de standaardveldgroep voor toestemming en aanvullende velden die worden verstrekt door een veldgroep voor aangepaste toestemming

## Vereisten

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Model van de Gegevens van de Ervaring (XDM) ](../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM.
* [ Real-Time Profiel van de Klant ](../../../../profile/home.md): consolideert klantengegevens van verschillende bronnen in een volledige, verenigde mening terwijl het aanbieden van een actionable, timestamped rekening van elke klanteninteractie.

>[!IMPORTANT]
>
>In deze zelfstudie wordt ervan uitgegaan dat u het [!DNL Profile] -schema in Platform kent dat u wilt gebruiken om klantkenmerkinformatie vast te leggen. Ongeacht de methode u gebruikt om toestemmingsgegevens te verzamelen, moet dit schema [ voor het Profiel van de Klant in real time ](../../../../xdm/ui/resources/schemas.md#profile) worden toegelaten. Bovendien kan de primaire identiteit van het schema geen direct identificeerbaar veld zijn dat niet mag worden gebruikt in op rente gebaseerde reclame, zoals een e-mailadres. Raadpleeg uw juridische adviseur als u niet zeker weet welke velden beperkt zijn.

## [!UICONTROL Consent and Preference Details] veldgroepstructuur {#structure}

De veldgroep [!UICONTROL Consent and Preference Details] verschaft gestandaardiseerde toestemmingsvelden voor een schema. Deze veldgroep is momenteel alleen compatibel met schema&#39;s die zijn gebaseerd op de klasse [!DNL XDM Individual Profile] .

De veldgroep biedt één objecttype veld, `consents`, waarvan de subeigenschappen een set gestandaardiseerde toestemmingsvelden vastleggen. De volgende JSON is een voorbeeld van het type gegevens dat `consents` verwacht bij het invoeren van gegevens:

```json
{
  "consents": {
    "collect": {
      "val": "y",
    },
    "share": {
      "val": "y",
    },
    "personalize": {
      "content": {
        "val": "y"
      }
    },
    "marketing": {
      "preferred": "email",
      "any": {
        "val": "y"
      },
      "push": {
        "val": "n",
        "reason": "Too Frequent",
        "time": "2019-01-01T15:52:25+00:00"
      }
    },
    "idSpecific": {
      "email": {
        "jdoe@example.com": {
          "marketing": {
            "email": {
              "val": "n"
            }
          }
        }
      }
    }
  },
  "metadata": {
    "time": "2019-01-01T15:52:25+00:00"
  }
}
```

>[!NOTE]
>
>Zie het overzicht over de [[!UICONTROL Consent and Preference Details] veldgroep ](../../../../xdm/field-groups/profile/consents.md) voor meer informatie over de structuur en betekenis van de subeigenschappen in `consents` .

## Vereiste veldgroepen toevoegen aan uw [!DNL Profile] -schema {#add-field-group}

Als u gegevens met toestemming wilt verzamelen met de standaard Adobe, moet u een schema met profiel hebben dat de volgende twee veldgroepen bevat:

* [[!UICONTROL Consent and Preference Details]](../../../../xdm/field-groups/profile/consents.md)
* [[!UICONTROL IdentityMap]](../../../../xdm/field-groups/profile/identitymap.md) (vereist als het gebruiken van het Web van het Platform of Mobiele SDK om toestemmingssignalen te verzenden)

Selecteer in de gebruikersinterface van het platform **[!UICONTROL Schemas]** in de linkernavigatie en selecteer vervolgens het tabblad **[!UICONTROL Browse]** om een lijst met bestaande schema&#39;s weer te geven. Van hier, selecteer de naam van [!DNL Profile] - toegelaten schema dat u toestemmingsgebieden aan wilt toevoegen. De schermafbeeldingen in deze sectie gebruiken het schema &quot;van de Leden van de Loyalty&quot;dat in het [ schemaverwezenlijking leerprogramma ](../../../../xdm/tutorials/create-schema-ui.md) als voorbeeld wordt gebouwd.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/select-schema.png)

>[!TIP]
>
>U kunt de zoek- en filtermogelijkheden van de werkruimte gebruiken om uw schema gemakkelijker te vinden. Zie de gids bij [ het onderzoeken van middelen XDM ](../../../../xdm/ui/explore.md) voor meer informatie.

De [!DNL Schema Editor] wordt weergegeven en geeft de structuur van het schema in het canvas weer. Selecteer links op het canvas de optie **[!UICONTROL Add]** onder de sectie **[!UICONTROL Field groups]** .

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-field-group.png)

Het dialoogvenster **[!UICONTROL Add field group]** wordt weergegeven. Selecteer **[!UICONTROL Consent and Preference Details]** in de lijst. U kunt de zoekbalk desgewenst gebruiken om de resultaten te beperken en zo de veldgroep gemakkelijker te vinden.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-group-dialog.png)

Zoek vervolgens de veldgroep **[!UICONTROL IdentityMap]** in de lijst en selecteer deze ook. Selecteer **[!UICONTROL Add field groups]** als beide veldgroepen in de rechtertrack worden weergegeven.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/identitymap.png)

Het canvas verschijnt weer en geeft aan dat de velden `consents` en `identityMap` zijn toegevoegd aan de schemastructuur. Als u extra toestemming en voorkeursgebieden niet vereist die door de standaardgebiedsgroep worden gevangen, zie de bijlage sectie op [ toevoegend de gebieden van de douanetoestemming en voorkeur aan het schema ](#custom-consent). Anders selecteert u **[!UICONTROL Save]** om de wijzigingen in het schema te voltooien.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/save-schema.png)

>[!IMPORTANT]
>
>Als u een nieuw schema creeert, of een bestaand schema uitgeeft dat niet voor Profiel is toegelaten, moet u [ het schema voor Profiel ](../../../../xdm/ui/resources/schemas.md#profile) toelaten alvorens op te slaan.

Als het schema u uitgeeft door [!UICONTROL Profile Dataset] wordt gebruikt die in uw gegevensstroom van SDK van het Web van het Platform wordt gespecificeerd, zal die dataset nu de nieuwe toestemmingsgebieden omvatten. U kunt nu aan de [ gids van de toestemmingsverwerking ](./overview.md#merge-policies) terugkeren om het proces voort te zetten om Experience Platform te vormen om toestemmingsgegevens te verwerken. Als u geen dataset voor dit schema hebt gecreeerd, volg de stappen in de volgende sectie.

## Een gegevensset maken op basis van uw toestemmingsschema {#dataset}

Zodra u een schema met toestemmingsgebieden hebt gecreeerd, moet u een dataset tot stand brengen die uiteindelijk de gegevens van de klantentoestemming zal opnemen. Deze gegevensset moet zijn ingeschakeld voor [!DNL Real-Time Customer Profile] .

Selecteer eerst **[!UICONTROL Datasets]** in de linkernavigatie en selecteer vervolgens **[!UICONTROL Create dataset]** in de rechterbovenhoek.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/create-dataset.png)

Selecteer op de volgende pagina **[!UICONTROL Create dataset from schema]** .

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/from-schema.png)

De **[!UICONTROL Create dataset from schema]** -workflow wordt weergegeven, te beginnen bij de **[!UICONTROL Select schema]** -stap. Zoek in de opgegeven lijst een van de toestemmingsschema&#39;s die u eerder hebt gemaakt. U kunt de zoekbalk desgewenst gebruiken om de resultaten te beperken en het schema gemakkelijker te vinden. Selecteer het keuzerondje naast het gewenste schema en selecteer vervolgens **[!UICONTROL Next]** om door te gaan.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/select-dataset-schema.png)

De stap **[!UICONTROL Configure dataset]** wordt weergegeven. Geef een unieke, gemakkelijk herkenbare naam en beschrijving voor de gegevensset op voordat u **[!UICONTROL Finish]** selecteert.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/dataset-details.png)

De detailspagina voor de pas gecreëerde dataset verschijnt. Als de dataset op uw tijd-reeksen schema gebaseerd is, dan is het proces volledig. Als de dataset op uw verslagschema gebaseerd is, is de definitieve stap in het proces om de dataset voor gebruik in [!DNL Real-Time Customer Profile] toe te laten.

Selecteer in de rechtertrack de **[!UICONTROL Profile]** -schakeloptie.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/profile-toggle.png)

Selecteer ten slotte **[!UICONTROL Enable]** in de bevestigingspop-up om het schema in te schakelen voor [!DNL Profile] .

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/enable-dataset.png)

De gegevensset wordt nu opgeslagen en ingeschakeld voor gebruik in [!DNL Profile] . Als u van plan bent gebruikend het Web SDK van het Platform om toestemmingsgegevens naar Profiel te verzenden, moet u deze dataset als [!UICONTROL Profile Dataset] selecteren wanneer vestiging uw [ datastream ](../../../../datastreams/overview.md).

## Volgende stappen

Door deze zelfstudie te volgen, hebt u toestemmingsgebieden aan een [!DNL Profile] toegelaten schema toegevoegd, waarvan dataset zal worden gebruikt om toestemmingsgegevens in te voeren gebruikend het Web SDK van het Platform of directe opname XDM.

U kunt nu aan het [ overzicht van de toestemmingsverwerking ](./overview.md#merge-policies) terugkeren om Experience Platform te blijven vormen om toestemmingsgegevens te verwerken.

## Bijlage

De volgende sectie bevat extra informatie over het creëren van een dataset om klantentoestemming en voorkeursgegevens in te gaan.

### Aangepaste toestemmings- en voorkeursvelden toevoegen aan het schema {#custom-consent}

Als u extra toestemmingssignalen buiten die moet vangen die door de standaard [!UICONTROL Consent and Preference Details] gebiedsgroep worden vertegenwoordigd, kunt u douaneXDM componenten gebruiken om uw toestemmingsschema te verbeteren om uw bijzondere bedrijfsbehoeften aan te passen. In deze sectie worden de basisbeginselen beschreven voor het aanpassen van uw toestemmingsschema om deze signalen in Profiel in te voeren.

>[!IMPORTANT]
>
>Het Web van het Platform en Mobiele SDKs steunt geen douanegebieden in hun toestemming-verandering bevelen. Momenteel is de enige manier om de gebieden van de douanetoestemming in Profiel in te nemen door [ partij ingeslikt ](../../../../ingestion/batch-ingestion/overview.md) of a [ bronverbinding ](../../../../sources/home.md).

U wordt ten zeerste aangeraden de veldgroep [!UICONTROL Consent and Preference Details] te gebruiken als basislijn voor de structuur van uw gegevens voor toestemming en zo nodig extra velden toe te voegen in plaats van de volledige structuur helemaal zelf te maken.

Als u aangepaste velden wilt toevoegen aan de structuur van een standaardveldgroep, moet u eerst een aangepaste veldgroep maken. Na het toevoegen van de [!UICONTROL Consent and Preference Details] gebiedsgroep aan het schema, selecteer **plus (+)** pictogram in de **[!UICONTROL Field groups]** sectie, en selecteer dan **[!UICONTROL Create new field group]**. Geef een naam en een optionele beschrijving voor de veldgroep op en selecteer vervolgens **[!UICONTROL Add field group]** .

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-custom-field-group.png)

De [!DNL Schema Editor] wordt weer weergegeven als de nieuwe aangepaste veldgroep in de linkertrack is geselecteerd. Op het canvas worden besturingselementen weergegeven waarmee u aangepaste velden kunt toevoegen aan de schemastructuur. Om een nieuw toestemmings of voorkeurgebied toe te voegen, selecteer **plus (+)** pictogram naast het `consents` voorwerp.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-custom-field.png)

Er wordt een nieuw veld weergegeven in het object `consents` . Aangezien u een aangepast veld toevoegt aan een standaard XDM-object, wordt het nieuwe veld gemaakt onder een object dat een naam krijgt toegewezen aan uw huurder-id.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/nested-tenantId.png)

Geef in de rechtertrack onder **[!UICONTROL Field properties]** een naam en een beschrijving voor het veld op. Wanneer u het veld **[!UICONTROL Type]** selecteert, moet u het juiste standaardgegevenstype gebruiken voor een veld met aangepaste toestemming of voorkeur:

* [[!UICONTROL Generic Consent Field]](../../../../xdm/data-types/consent-field.md)
* [[!UICONTROL Generic Marketing Preference Field]](../../../../xdm/data-types/marketing-field.md)
* [[!UICONTROL Generic Marketing Preference Field with Subscriptions]](../../../../xdm/data-types/marketing-field-subscriptions.md)
* [[!UICONTROL Generic Personalization Preference Field]](../../../../xdm/data-types/personalization-field.md)

Selecteer **[!UICONTROL Apply]** als u klaar bent.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-properties.png)

Het toestemmings- of voorkeursveld wordt toegevoegd aan de schemastructuur. De naamruimte [!UICONTROL Path] die in de rechtertrack wordt weergegeven, bevat de naamruimte `_tenantId` . Deze naamruimte moet worden opgenomen wanneer u in de gegevensbewerkingen naar dit veld verwijst.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-added.png)

Voer de bovenstaande stappen uit om door te gaan met het toevoegen van de toestemmings- en voorkeurvelden die u nodig hebt. Als u klaar bent, selecteert u **[!UICONTROL Save]** om uw wijzigingen te bevestigen.

Als u geen dataset voor dit schema hebt gecreeerd, ga aan de sectie over [ voort creërend een dataset ](#dataset).
