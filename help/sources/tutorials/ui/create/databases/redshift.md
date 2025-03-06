---
title: Opnieuw overschakelen naar Experience Platform via de gebruikersinterface van Connect AWS
description: Leer hoe u een AWS Redshift-account koppelt aan Experience Platform met behulp van de interface voor bronnen.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 4faf3200-673b-4a20-8f94-d049e800444b
source-git-commit: dd9aee1ac887637d4761188d6dbcf55ad5bde407
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 1%

---

# Verbinding maken [!DNL AWS Redshift] met Experience Platform via de gebruikersinterface

>[!IMPORTANT]
>
>De [!DNL AWS Redshift] -bron is in de broncatalogus beschikbaar voor gebruikers die Real-Time Customer Data Platform Ultimate hebben aangeschaft.

Lees deze handleiding voor informatie over hoe u uw [!DNL AWS Redshift] -account kunt verbinden met Adobe Experience Platform via de gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Experience Platform:

- [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor Experience Platform gegevens van de klantenervaring organiseert.
   - [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u reeds een geldige [!DNL AWS Redshift] verbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [ vormend een dataflow ](../../dataflow/databases.md).

## Navigeren door de catalogus met bronnen

Selecteer in de gebruikersinterface van het platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van [!UICONTROL Sources] . U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer **[!DNL AWS Redshift]** onder de categorie *[!UICONTROL Databases]* en selecteer vervolgens **[!UICONTROL Set up]** .

>[!TIP]
>
>Bronnen in de catalogus met bronnen geven de optie **[!UICONTROL Set up]** weer wanneer een bepaalde bron nog geen geverifieerde account heeft. Zodra een geverifieerd account bestaat, verandert deze optie in **[!UICONTROL Add data]** .

![ de broncatalogus van bronnen met de AWS Redshift geselecteerde bronkaart.](../../../../images/tutorials/create/redshift/catalog.png)

## Een bestaande account gebruiken {#existing}

Vervolgens gaat u naar de verificatiestap van de workflow voor bronnen. Hier kunt u een bestaand account gebruiken of een nieuw account maken.

Als u een bestaande account wilt gebruiken, selecteert u de [!DNL AWS Redshift] -account in de accountmap en selecteert u **[!UICONTROL Next]** om door te gaan.

![ de rekeningenfolder in het bronwerkschema hier zijn de bestaande rekeningen vermeld.](../../../../images/tutorials/create/redshift/existing.png)

## Een nieuwe account maken {#create}

Als u geen bestaand account hebt, moet u een nieuw account maken door de vereiste verificatiereferenties op te geven die overeenkomen met uw bron.

Als u een nieuwe account wilt maken, selecteert u **[!UICONTROL New account]** en geeft u een naam op en voegt u desgewenst een beschrijving voor uw account toe.

### Verbinding maken met Experience Platform on Azure {#azure}

Als u uw [!DNL AWS Redshift] -account op Azure aan Experience Platform wilt koppelen, geeft u uw verificatiereferenties op in het invoerformulier en selecteert u vervolgens **([!UICONTROL Connect to source])** .

![ de nieuwe rekeningsinterface om AWS opnieuw te verbinden aan Experience Platform op Azure.](../../../../images/tutorials/create/redshift/new.png)

| Credentials | Beschrijving |
| --- | --- |
| Server | De servernaam van de instantie [!DNL AWS Redshift] . |
| Poort | De TCP-poort die een [!DNL AWS Redshift] -server gebruikt om te luisteren naar clientverbindingen. |
| Gebruikersnaam | De gebruikersnaam van de account waartoe u toegang wilt geven. |
| Wachtwoord | Het wachtwoord dat overeenkomt met de gebruikersaccount. |
| Database | De [!DNL AWS Redshift] -database waaruit gegevens moeten worden opgehaald. |

Voor meer informatie over begonnen worden, verwijs naar [ dit  [!DNL AWS Redshift]  document ](https://docs.aws.amazon.com/redshift/latest/gsg/new-user-serverless.html).

### Verbinding maken met Experience Platform op AWS {#aws}

>[!AVAILABILITY]
>
>Deze sectie is op implementaties van Experience Platform van toepassing die op de Diensten van het Web van AWS (AWS) lopen. Experience Platform die op AWS wordt uitgevoerd, is momenteel beschikbaar voor een beperkt aantal klanten. Meer over de gesteunde infrastructuur van Experience Platform leren, zie het [ multi-wolkenoverzicht van Experience Platform ](../../../../../landing/multi-cloud.md).

Als u een nieuwe [!DNL AWS Redshift] -account wilt maken en verbinding wilt maken met Experience Platform op AWS, controleert u of u zich in een VA6-sandbox bevindt, geeft u de vereiste verificatiegegevens op en selecteert u **[!UICONTROL Connect to source]** .

![ de nieuwe rekeningsinterface om AWS opnieuw te verbinden aan Experience Platform op AWS.](../../../../images/tutorials/create/redshift/aws-auth.png)

| Credentials | Beschrijving |
| --- | --- |
| Server | De servernaam van de instantie [!DNL AWS Redshift] . |
| Poort | De TCP-poort die een [!DNL AWS Redshift] -server gebruikt om te luisteren naar clientverbindingen. |
| Gebruikersnaam | De gebruikersnaam van de account waartoe u toegang wilt geven. |
| Wachtwoord | Het wachtwoord dat overeenkomt met de gebruikersaccount. |
| Database | De [!DNL AWS Redshift] -database waaruit gegevens moeten worden opgehaald. |
| Schema | De naam van het schema dat aan uw [!DNL AWS Redshift] database is gekoppeld. U moet ervoor zorgen dat de gebruiker u gegevensbestandtoegang tot wilt geven, ook toegang tot dit schema heeft. |

Voor meer informatie over begonnen worden, verwijs naar [ dit  [!DNL AWS Redshift]  document ](https://docs.aws.amazon.com/redshift/latest/gsg/new-user-serverless.html).

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht tussen uw [!DNL AWS Redshift] -database en Experience Platform. U kunt nu aan het volgende leerprogramma verdergaan en [ een dataflow tot stand brengen om gegevens van uw gegevensbestand aan Experience Platform ](../../dataflow/databases.md) in te voeren.