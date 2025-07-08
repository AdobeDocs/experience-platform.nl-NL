---
title: Referentie van CMK-waarschuwingsresolutie
description: Identificeer, los problemen op, en los gemeenschappelijke alarm op die door Klant Beheerde Zeer belangrijke (CMK) misconfiguraties in Adobe Experience Platform worden teweeggebracht. Gebruik deze handleiding om duidelijke, stapsgewijze instructies te volgen en veilige toetstoegang te herstellen.
exl-id: ffe2eadc-dfb5-418b-a201-2c20dcc9cfe4
source-git-commit: e8cfed9ebd50cf50f03e232755eddef1cb8c0d3b
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 0%

---

# CMK-waarschuwingsresolutieverwijzing

Met deze handleiding kunt u problemen oplossen en waarschuwingen oplossen die worden veroorzaakt door verkeerd geconfigureerde CMK-instellingen (Customer Managed Key) in Adobe Experience Platform. Het helpt systeembeheerders en implementatiespecialisten oorzaken identificeren en resoluties toepassen om veilige toegang te herstellen.

## Waarschuwingscategorieën {#categories}

In de volgende secties worden de typen waarschuwingen beschreven die kunnen worden geactiveerd door CMK-problemen (Customer Managed Key) in Adobe Experience Platform:

- [Sleuteltoegang uitgeschakeld](#key-access-disabled)
- [Sleuteltoegangsfout](#key-access-failure)
- [Waarschuwingsmelding](#alert-notification)

## Sleuteltoegang uitgeschakeld {#key-access-disabled}

Deze waarschuwing geeft aan dat Adobe Experience Platform geen toegang heeft tot de geconfigureerde CMK omdat de toets wegens de configuratie is uitgeschakeld of niet toegankelijk. In dergelijke gevallen behandelt het systeem de voorwaarde als een opzettelijke verwijdering van sleuteltoegang.

### Wanneer dit gebeurt

Deze waarschuwing wordt geactiveerd wanneer de coderingssleutel in Azure Key Vault zich in een uitgeschakelde toestand bevindt, verwijderd of op een andere manier onjuist geconfigureerd is, zodat toegang tijdens platformbewerkingen niet mogelijk is.

### Mogelijke oorzaken

Deze waarschuwing kan om de volgende redenen voorkomen:

- De toets was handmatig uitgeschakeld.
- Keybewerkingen (wrapKey/unwrapKey) zijn verwijderd.
- De belangrijkste activeringsdatum wordt geplaatst in de toekomst.
- De belangrijkste vervaldatum is in het verleden.
- De sleutel is verwijderd.
- De MultiTenant App-machtigingen zijn verwijderd of gewijzigd.
- De MultiTenant-app is verwijderd.
- De eigenschappen van de MultiTenant-app zijn gewijzigd.
- De Key Vault is verwijderd of is niet meer toegankelijk.

### Resolutie

+++Als de toets is uitgeschakeld

1. Navigeer aan de [ Azure Zeer belangrijke vault ](https://portal.azure.com/) die CMK bevat.
2. Selecteer de sleutel die aan Adobe Experience Platform is gekoppeld.
3. Verifieer dat de status van de sleutel aan **Toegelaten** wordt geplaatst.
4. Als de sleutel gehandicapt is, laat het toe gebruikend het Azure portaal of het CLI bevel `az keyvault key enable`.

>[!NOTE]
>
>Pas deze opdracht aan voor uw Azure-omgeving.

+++

+++Als de belangrijkste verrichtingen zijn veranderd

1. Voeg de machtigingen `wrapKey` en `unwrapKey` opnieuw toe aan de sleutel.

>[!NOTE]
>
>De toets werkt alleen als alle instellingen van de toets, inclusief de activerings- en vervaldatums, geldig zijn.

+++

+++Als de activerings- of vervaldatum onjuist is geconfigureerd

1. Stel de activeringsdatum in op het verleden of heden.
2. Stel de vervaldatum in op een toekomstige datum.

+++

+++Als de toets is verwijderd

1. Zorg ervoor dat soft-delete is ingeschakeld in Azure Key Vault.
2. Navigeer naar &quot;verwijderde sleutels beheren&quot; in de Azure-portal of CLI.
3. Selecteer de verwijderde toets in de lijst met items die zijn verwijderd met de optie soft.
4. Klik **Herstellen** om de sleutel te herstellen.

+++

+++Als de MultiTenant App-machtigingen zijn verwijderd of gewijzigd

1. Herstel de juiste machtigingen voor de MultiTenant-app.
2. Controleer of de volgende machtigingen zijn verleend: `Key Vault Crypto Service Encryption User`

+++

+++ als de MultiTenant-app is verwijderd

Dit is een baanbrekende verandering. U moet contact opnemen met Adobe om de MultiTenant-app te herstellen of opnieuw te genereren.

+++

+++ als de instellingen voor de MultiTenant-app zijn gewijzigd

1. Hiermee worden de wijzigingen in de eigenschappen van de MultiTenant-app hersteld.

+++

+++Als de Key Vault is verwijderd

1. Bevestig dat soft-delete in Azure wordt toegelaten.
2. Navigeer naar &quot;verwijderde vaults beheren&quot; in de portal of CLI.
3. Herstel de verwijderde vault binnen de retentieperiode (7-90 dagen).
4. Als de afvalbeveiliging is uitgeschakeld, kunt u de vault mogelijk nog herstellen.

>[!NOTE]
>
>Als soft-delete of purge bescherming niet correct wordt gevormd, kan de sleutel of de kluis niet terugwinbaar zijn.

+++

## Sleuteltoegangsfout {#key-access-failure}

Deze waarschuwing geeft aan dat Adobe Experience Platform geen toegang heeft tot de CMK vanwege een weigering van toegang op netwerkniveau of op configuratie gebaseerd.

>[!IMPORTANT]
>
>Dit wordt beschouwd als een herstelbare fout. Gegevens worden **niet** gezuiverd onder SLA in dit geval.

### Wanneer dit gebeurt

Deze waarschuwing wordt doorgaans geactiveerd wanneer de sleutelvafirewall niet is geconfigureerd om toegang tot Adobe CMK toe te staan of wanneer toegang op basis van identiteit mislukt.

### Mogelijke oorzaken

- Key Vault firewall blokkeert statische IP van Adobe (`20.88.123.53`)
- De sleutel bestaat niet meer op de verwachte locatie
- Machtigingen voor de Adobe MultiTenant-app ontbreken
- De Key Vault is verwijderd of onjuist geconfigureerd
- De object-id van de MultiTenant-app is gewijzigd

### Resolutie

+++ als de Key Vault of Key niet meer bestaat

1. Controleer of de Key Vault en de coderingssleutel nog steeds bestaan.
2. Als de sleutel is verwijderd, volgt u de herstelstappen voor soft-delete onder &#39;Toetstoegang uitgeschakeld&#39;.

+++

+++ als de MultiTenant App-machtigingen ontbreken of zijn gewijzigd

1. Controleer of de MultiTenant-app van Adobe de volgende machtigingen heeft:
   - `get` , `wrapKey` en `unwrapKey` op de toets.
2. Controleer of de object-id voor de MultiTenant-app juist is. Als deze is gewijzigd, past u de machtigingen opnieuw toe.

+++

+++Als de firewall Adobe blokkeert

1. Controleer de firewallregels in Azure Key Vault.
2. Zorg ervoor dat ze toegang bieden vanaf statische IP van Adobe: `20.88.123.53` .

>[!NOTE]
>
>Zelfs met correcte toestemmingen, zal geblokkeerde IP zeer belangrijke toegang verhinderen.

+++

## Waarschuwingsmelding {#alert-notification}

Dit alarm dient als algemeen bericht voor configuratie CMK of toegangsanomalieën die geen bekend mislukkingstype aanpassen.

>[!NOTE]
>
>Deze waarschuwing kan een interne fout, een nieuwe verkeerde configuratie of een onverwachte voorwaarde weerspiegelen.

### Wanneer dit gebeurt

Deze waarschuwing wordt weergegeven wanneer Adobe CMK een onbekend, niet-ondersteund of nieuw probleem detecteert tijdens sleuteltoegang of controle.

### Mogelijke oorzaken

- Onverwachte firewall-/netwerkvoorwaarden
- Wijzigingen in sleutel of vault die niet door vooraf gedefinieerde typen waarschuwingen worden gedekt
- Interne Adobe-netwerkverstoringen
- Misconfiguration Adobe is nog niet eerder gezien

### Resolutie

+++Als de oorzaak onbekend of dubbelzinnig is

1. Controleer het waarschuwingsbericht voor eventuele contextafhankelijke details.
2. Controleer de firewall-, vault- en sleutelinstellingen voor recente wijzigingen.
3. Als er geen duidelijke oorzaak wordt gevonden, neemt u contact op met de ondersteuning van Adobe.
4. Logboeken van de monitor en systeemgedrag om patronen te identificeren.

+++

## Volgende stappen

Om te begrijpen hoe het alarm wordt teweeggebracht en hoe te om IP voegend op lijst van gewenste personen voor [!DNL Azure] CMK te vormen, zie [ alarm en IP lijst van gewenste personen voor Azure CMK ](./azure/alerts-and-ip-access.md) gids vormen.
