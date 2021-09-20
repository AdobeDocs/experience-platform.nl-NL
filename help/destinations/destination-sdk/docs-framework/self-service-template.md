---
title: Zelfbedieningssjabloon voor documentatie // Vervangen door de naam van uw doel
description: Gebruik deze sjabloon om openbare documentatie voor uw bestemming in de Adobe Experience Platform-catalogus te maken. // Vervang door de alinea in de sectie Overzicht
exl-id: 99700474-8bf6-4176-acc1-38814e17c995
source-git-commit: 396b9a9ec1509abedba96797f68ad3e5aa2e5988
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 1%

---

# UW BESTEMMING {#your-destination}

*Terwijl u deze sjabloon doorloopt, vervangt of verwijdert u alle cursief gedrukte alinea&#39;s (te beginnen met deze alinea).*

*Begin door de meta-gegevens (titel en beschrijving) bij te werken bij de bovenkant van de pagina. Negeer alle exemplaren van UICONTROL op deze pagina. Dit is een label waarmee de pagina in de verschillende talen die wij ondersteunen correct wordt vertaald in onze computervertaalprocessen. Nadat u het document hebt verzonden, voegen wij codes toe aan de documentatie.*

## Overzicht {#overview}

*Geef een kort overzicht voor uw bedrijf, inclusief de waarde die het aan klanten biedt. Neem een koppeling op naar de startpagina van de productdocumentatie voor verdere lezing.*

>[!IMPORTANT]
>
>Deze documentatiepagina is gemaakt door het team *YOURDESTINATION*. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen via *Koppeling of e-mailadres invoegen waar u voor updates kunt komen*

## Vereisten {#prerequisites}

*Voeg informatie in deze sectie over om het even wat toe dat de klanten zich van bewust moeten zijn alvorens aan opstelling de bestemming in het gebruikersinterface van Adobe Experience Platform te beginnen. Dit kan over zijn:*

* *moet aan een lijst van gewenste personen worden toegevoegd*
* *vereisten voor e-mailhashing*
* *accountdetails aan je kant*
* *hoe u een API-sleutel kunt verkrijgen voor verbinding met uw platform*

*U kunt een koppeling maken naar uw relevante documentatie als dat nuttig zou zijn voor klanten.*

## Ondersteunde identiteiten {#supported-identities}

*Voeg in deze sectie informatie toe over de identiteiten die door uw bestemming worden gesteund. We hebben de tabel vooraf gevuld met enkele standaardwaarden. Schrap de waarden die niet op uw bestemming en om het even welke waarden van toepassing zijn die niet worden voorgevuld.*

** Uw DOELondersteunt de activering van de identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| GAID | Google-advertentie-id | Selecteer de GAID doelidentiteit wanneer uw bronidentiteit een GAID-naamruimte is. |
| IDFA | Apple ID for Advertisers | Selecteer de IDFA doelidentiteit wanneer uw bronidentiteit een IDFA namespace is. |
| ECID | Experience Cloud-id | Een naamruimte die ECID vertegenwoordigt. Naar deze naamruimte kan ook worden verwezen door de volgende aliassen: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Zie het volgende document op [ECID](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html) voor meer informatie. |
| phone_sha256 | Telefoonnummers die zijn hashed met het SHA256-algoritme | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-telefoonnummers. Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in om [!DNL Platform] de gegevens automatisch te laten hashen bij activering. |
| email_lc_sha256 | E-mailadressen die met het algoritme SHA256 worden gehasht | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-e-mailadressen met hashing. Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in om [!DNL Platform] de gegevens automatisch te laten hashen bij activering. |
| extern_id | Aangepaste gebruikers-id&#39;s | Selecteer deze doelidentiteit wanneer uw bronidentiteit een aangepaste naamruimte is. |

{style=&quot;table-layout:auto&quot;}

## Exporttype {#export-type}

**De Uitvoer**  van het segment - u exporteert alle leden van een segment (publiek) met de herkenningstekens (naam, telefoonaantal, of anderen) die in de bestemming  ** YOURDESTINATION worden gebruikt.

## Gebruiksscenario’s

Om u beter te helpen begrijpen hoe en wanneer u *UURDESTINATION* bestemming zou moeten gebruiken, zijn hier voorbeelden van gebruiksgevallen die de klanten van Adobe Experience Platform door deze bestemming kunnen oplossen.

### Hoofdletters gebruiken #1

*Voor mobiele berichtenplatforms:*

*Een homepage- en verkoopplatform wil mobiele meldingen naar Android- en iOS-apparaten van klanten doorsturen om hen te laten weten dat er 100 bijgewerkte aanbiedingen zijn in het gebied waar ze eerder naar een verhuur hebben gezocht.*

### Hoofdletters gebruiken #2

*Voor sociale netwerkplatforms:*

*Een atletisch merk kledingartikelen wil bestaande klanten bereiken via hun sociale-mediakanalen. Het merkje van de kleding kan e-mailadressen van hun eigen CRM aan Adobe Experience Platform opnemen, segmenten van hun eigen off-line gegevens bouwen, en deze segmenten naar YOURDESTINATION verzenden, om advertenties in de sociale media van hun klanten te tonen feeds.*

## Verbinden met de bestemming {#connect}

Om met deze bestemming te verbinden, volg de stappen in [het leerprogramma van de bestemmingsconfiguratie](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html) worden beschreven.

### Verbindingsparameters {#parameters}

Terwijl [vestiging](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html) deze bestemming, u de volgende informatie moet verstrekken:

*Voeg de gebieden toe die de klanten moeten invullen wanneer het vormen van een nieuwe bestemming. Deze gebieden zijn bestemmings-specifiek en hangen van uw configuratie in Doel SDK af. De velden van uw bestemming zijn mogelijk niet gelijk aan de onderstaande velden.*

* **[!UICONTROL Name]**: Een naam waarmee u deze bestemming in de toekomst zult erkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Account ID]**: Uw  ** id van uw UPDINATIONAccount.


<!--

*Replace YOURDESTINATION with your destination name and TOBEFILLEDIN with the category that your destination belongs to.*

1. In **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**, scroll to the ***TOBEFILLEDIN*** category. Select ***YOURDESTINATION***, then select **[!UICONTROL Configure]**.


    >[!NOTE]
    >
    >If a connection with this destination already exists, you can see an **[!UICONTROL Activate]** button on the destination card. For more information about the difference between **[!UICONTROL Activate]** and **[!UICONTROL Configure]**, refer to the [Catalog](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/destinations-workspace.html#catalog) section of the destination workspace documentation.  

    ![Connect to YOURDESTINATION](./assets/yourdestination1.png)

2. In the **Account** step, if you had previously set up a connection to your *YOURDESTINATION* destination, select **[!UICONTROL Existing Account]** and select your existing connection. Or, you can select **[!UICONTROL New Account]** to set up a new connection to *YOURDESTINATION*. Select **[!UICONTROL Connect to destination]** to log in and connect Adobe Experience Cloud to your *YOURDESTINATION* account.

    >[!NOTE]
    >
    >Adobe Experience Platform supports credentials validation in the authentication process and displays an error message if you input incorrect credentials to your ***YOURDESTINATION*** account. This ensures that you don't complete the workflow with incorrect credentials.

3. Once your credentials are confirmed and Adobe Experience Cloud is connected to your ***YOURDESTINATION*** account, you can select **[!UICONTROL Next]** to proceed to the **[!UICONTROL Setup]** step.

4. In the **[!UICONTROL Authentication]** step, enter a **[!UICONTROL Name]** and a **[!UICONTROL Description]** for your activation flow and fill your account ID. <br> Also in this step, you can select any marketing action that should apply to this destination. Marketing actions indicate the intent for which data will be exported to the destination. You can select from Adobe-defined marketing actions or you can create your own marketing action. For more information about marketing actions, see the [Data usage policies overview](https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/overview.html).

    ![Connect to YOURDESTINATION](./assets/yourdestination2.png)

5. Your destination is now created. You can select **[!UICONTROL Save & Exit]** if you want to activate segments later on or you can select **[!UICONTROL Next]** to continue the workflow and select segments to activate. In either case, see the next section, [Activate segments](#activate-segments), for the rest of the workflow.

-->

## Segmenten naar dit doel activeren {#activate}

Lees [Activate profielen en segmenten aan het stromen segment de uitvoerbestemmingen ](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en) voor instructies op het activeren van publiekssegmenten aan deze bestemming.

<!--

To activate segments to *YOURDESTINATION*, follow the steps below: 

1. In **[!UICONTROL Destinations > Browse]**, select the *YOURDESTINATION* destination where you want to activate your segments.

2. Click the name of the destination. This takes you to the Activate flow.
    ![activate-flow](./assets/yourdestination3.png)
    Note that if an activation flow already exists for a destination, you can see the segments that are currently being sent to the destination. Select **[!UICONTROL Edit activation]** in the right rail and follow the steps below to modify the activation details.
3. Select **[!UICONTROL Activate]**;
4. In the **[!UICONTROL Activate destination]** workflow, on the **[!UICONTROL Select Segments]** page, select which segments to send to *YOURDESTINATION*.
    ![segments-to-destination](./assets/activate-segments-google-customer-match.png)
5.  In the **[!UICONTROL Mapping]** step, select which attributes and identities from the source XDM schema to map to the target schema. Select **[!UICONTROL Add new mapping]** and browse your schema, select identity namespaces and map them to the corresponding target identity.  
![identity mapping initial screen](./assets/gcm-identity-mapping.png) <br>&nbsp;
   *Plain text email address as primary identity*: If you have plain text (unhashed) email addresses as primary identity in your schema, select the email field in your **[!UICONTROL Source Attributes]** and map to the Email field in the right column under **[!UICONTROL Target Identities]**, as shown below. Set up a mapping between any other attributes you plan to use.
   ![identity mapping step](./assets/ssd-template-identity.png) <br>&nbsp;
6. On the **[!UICONTROL Segment schedule]** page, you can set the start date for sending data to the destination.
7. On the **[!UICONTROL Review]** page, you can see a summary of your selection. Select **[!UICONTROL Cancel]** to break up the flow, **[!UICONTROL Back]** to modify your settings, or **[!UICONTROL Finish]** to confirm your selection and start sending data to the destination.

>[!IMPORTANT]
>
>In this step, Adobe Experience Platform checks for data usage policy violations. Shown below is an example where a policy is violated. You cannot complete the segment activation workflow until you have resolved the violation. For information on how to resolve policy violations, see [Policy enforcement](https://experienceleague.adobe.com/docs/experience-platform/data-governance/enforcement/auto-enforcement.html#enforcement) in the data governance documentation section.
 
![confirm-selection](./assets/data-policy-violation.png)

If no policy violations have been detected, select **[!UICONTROL Finish]** to confirm your selection and start sending data to the destination.

![confirm-selection](./assets/gcm-review.png)

-->

## Geëxporteerde gegevens {#exported-data}

*Voeg een opmerking toe over de manier waarop gegevens naar uw bestemming worden geëxporteerd. Dit zou de klant helpen ervoor zorgen dat zij correct met uw bestemming geïntegreerd hebben. U kunt bijvoorbeeld een voorbeeld-JSON opgeven zoals hieronder.*

```
{
  "person": {
    "email": "yourstruly@adobe.con"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "existing"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Lees voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt het [Overzicht gegevensbeheer](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Aanvullende bronnen {#additional-resources}

*U kunt verdere verbindingen aan uw productdocumentatie of om het even welke andere middelen verstrekken u belangrijk voor de klant om succesvol te zijn.*
