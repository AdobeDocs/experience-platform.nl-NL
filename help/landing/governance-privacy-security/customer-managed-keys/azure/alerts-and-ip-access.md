---
title: Alarm en IP lijst van gewenste personen voor Azure CMK vormen
description: Leer hoe u het statische IP-adres van Adobe voegt op lijst van gewenste personen in Azure Key Vault en begrijpt hoe waarschuwingen van Experience Platform helpen problemen met sleuteltoegang door klanten op te sporen en op te lossen.
source-git-commit: 719273798954b70460c77711ef5eda5f9d22cdb0
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 0%

---

# Waarschuwingen en IP-lijst van gewenste personen configureren voor [!DNL Azure] CMK

Om transparantie te verbeteren, verleent Adobe de dienst van de a [&#x200B; controle &#x200B;](../../../../observability/alerts/ui.md){target="_blank"} die de toegangsstatus van uw zeer belangrijke kluis controleert en alarm in werking stelt als de kwesties voorkomen. Met deze waarschuwingen kunt u snel reageren en onderbreking van de service voorkomen. Om deze dienst toe te laten, lijst van gewenste personen Adobe het statische IP adres.

>[!IMPORTANT]
>
>Als u de toegang tot openbare netwerken hebt uitgeschakeld of als u de Key Vault van [!DNL Azure] hebt geconfigureerd om alleen geselecteerde netwerken toe te staan, moet u het statische IP-adres van Adobe aan uw lijst van gewenste personen toevoegen. Zonder deze functie kun je niet op de hoogte worden gesteld van toegangsproblemen die van invloed kunnen zijn op je Experience Platform-exemplaar.

## Lijst van gewenste personen Adobe statische IP in [!DNL Azure] Key Vault {#add-adobe-static-ip}

Navigeer naar uw **[!DNL Azure Key Vault]** > **[!DNL Networking settings]** om deze waarschuwingen in te schakelen terwijl de netwerkbeperkingen behouden blijven. Selecteer op het tabblad **[!DNL Firewalls and virtual networks]** de optie **[!DNL Allow public access from specific virtual networks and IP addresses]** .

![[!DNL Azure] Het scherm van de montages van het Voorzien van een netwerk van de Zeer belangrijke kluis die waar te om Adobe toe te voegen statisch IP adres en met de Allow toegang van optie benadrukt.](../../../images/governance-privacy-security/customer-managed-keys/key-vault-networking-settings.png)

### Adobe statisch IP-adres

>[!IMPORTANT]
>
>Het door Adobe opgegeven statische IP-adres is: `20.88.123.53` .

Selecteer vervolgens in de sectie **[!DNL Firewall]** de optie **[!DNL Add your current IP address]** en vervang deze door het statische IP-adres van Adobe. Alle uitgaande verbindingen worden behandeld als de milieu&#39;s van de Productie, zodat moet dit statische IP adres worden gevoegd op lijst van gewenste personen om ononderbroken toegang tot uw zeer belangrijke kluis in beperkte netwerkconfiguraties te verzekeren.

>[!NOTE]
>
>Nadat u het statische IP-adres hebt toegevoegd of bijgewerkt in uw [!DNL Azure] Key Vault-instellingen, kunt u de wijziging tot 10 minuten laten gelden. Nadat het IP-bestand is toegevoegd, opent de CMK-toepassing de sleutelkluis om de machtigingen te controleren.

Na het voegend op lijst van gewenste personen statische IP van Adobe, kan Experience Platform toegang tot uw zeer belangrijke kluis controleren en alarm teweegbrengen als de kwesties zich voordoen. Deze waarschuwingen geven vroegtijdige waarschuwingen, zodat u kunt reageren voordat de service wordt beïnvloed. In de volgende sectie worden de typen waarschuwingen beschreven die u kunt ontvangen en hoe u kunt reageren.

## Monitorwaarschuwingen {#monitor-alerts}

Platformwaarschuwingen geven u een melding van problemen die sleuteltoegang kunnen onderbreken, zoals **[!UICONTROL Key access failure]** of **[!UICONTROL Key disablement]** . Deze waarschuwingen helpen u snel problemen zoals verwijderde statische IP of een misconfigured firewall identificeren. Als u de toegang wilt herstellen, controleert u de firewallinstellingen van [!DNL Azure] en voegt u het vereiste IP-adres opnieuw toe.

<!-- For a complete list of alert types and recommended resolutions, see the [CMK alert resolution reference](../alert-resolution-reference.md). -->

Meld u aan voor Adobe I/O-gebeurtenismeldingen om real-time waarschuwingen te ontvangen in uw controleprogramma&#39;s. Voor opstellingsinstructies, zie [&#x200B; aan de berichten van de Gebeurtenis van Adobe I/O &#x200B;](../../../../observability/alerts/subscribe.md) intekenen. U kunt ook naar de [&#x200B; gids van het alarm UI &#x200B;](../../../../observability/alerts/ui.md) verwijzen om te leren hoe te om alarm binnen Experience Platform te bekijken en te beheren.

## Volgende stappen

U hebt nu IP voegende op lijst van gewenste personen en waakzame controle voor uw [!DNL Azure] Zeer belangrijke vault gevormd. Volg deze configuratiehandleidingen om de installatie van door de klant beheerde sleutels in [!DNL Azure] te voltooien.

- [&#x200B; vorm een  [!DNL Azure]  Zeer belangrijke Uitvault &#x200B;](./azure-key-vault-config.md)
- [&#x200B; Gebruik API aan opstelling CMK &#x200B;](./api-set-up.md)
- [De gebruikersinterface gebruiken om CMK in te stellen](./ui-set-up.md)
