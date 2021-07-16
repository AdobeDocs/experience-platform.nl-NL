---
title: SFTP-hosts
description: Leer hoe u tags in Adobe Experience Platform configureert om bibliotheekbuilds te leveren aan een beveiligde, zelfgehoste SFTP-server.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 1%

---

# SFTP-hosts

>[!NOTE]
>
>Adobe Experience Platform Launch wordt omgedoopt tot een reeks technologieën voor gegevensverzameling in Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Als u niet wilt dat Adobe uw gehoste bibliotheken beheert, kunt u er ook voor kiezen dat Adobe Experience Platform builds levert aan een beveiligde SFTP-server die u host.

Platform maakt verbinding met uw SFTP-site met behulp van een gecodeerde sleutel. Er zijn een paar stappen om dit correct in te stellen:

1. Er moet een combinatie van openbare/persoonlijke sleutels op uw SFTP-server zijn geïnstalleerd. U kunt deze sleutels op uw server produceren of hen ergens anders produceren en hen installeren op uw server. Zie de documentatie GitHub betreffende [hoe te SSH sleutels](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/#generating-a-new-ssh-key) voor meer informatie te produceren.
1. De persoonlijke sleutel wordt gebruikt om de openbare sleutel van GPG te coderen. U moet uw persoonlijke sleutel opgeven tijdens het maken van de SFTP-host. Zie de sectie [Waarden versleutelen](https://developer.adobelaunch.com/api/guides/encrypting_values/) in de Reactor API-documentatie voor instructies over het versleutelen van openbare GPG-sleutels. Gebruik de GPG-sleutel van de productieomgeving, tenzij u weet dat u een specifieke sleutel nodig hebt. Tot slot kunt u uw persoonlijke sleutel van om het even welke machine coderen, zodat te hoeven u geen GPG op uw server te installeren om deze stap te voltooien.
1. Mogelijk moet u de IP-adressen goedkeuren die worden gebruikt met de firewall van uw bedrijf om Platform toe te staan uw SFTP-server te bereiken en er verbinding mee te maken. Die IP Adressen zijn:
   * `184.72.239.68`
   * `23.20.85.113`
   * `54.226.193.184`

>[!NOTE]
>
>De structuur van builds van tags is in de loop der tijd gewijzigd. Zij gebruiken symbolische verbindingen (symbolische verbindingen) intern om achterwaartse verenigbaarheid te handhaven zodat de vorige inbedcodes met de recentste bouwstijlstructuur zullen blijven werken. Uw SFTP-server moet het gebruik van symlinks ondersteunen om als geldige bestemming voor het maken van tags te kunnen fungeren.

Raadpleeg voor meer gedetailleerde informatie het volgende Medium-artikel op [hoe u SFTP-servers kunt instellen om een build](https://medium.com/launch-by-adobe/configuring-an-sftp-server-for-use-with-adobe-launch-bc626027e5a6) te leveren.

## Een SFTP-host maken

1. Open het tabblad [!UICONTROL Hosts].
1. Maak de nieuwe host.
1. Geef de host een naam.
1. Selecteer **[!UICONTROL SFTP]** als hosttype.
1. Voer de host, het pad, de poort, de gebruikersnaam en de gecodeerde persoonlijke sleutel in.

   De poort moet een van de volgende zijn:

   * 21
   * 22
   * 80
   * 200-299
   * 443
   * 2000-2999
   * 4343
   * 8080
   * 8888

   >[!NOTE]
   >
   >Als veiligheid beste praktijken, beperkt Adobe het aantal havens die voor uitgaand verkeer kunnen worden gebruikt. De geselecteerde havens worden algemeen toegestaan door collectieve firewalls, plus zij omvatten sommige waaiers voor flexibiliteit.

1. Selecteer **[!UICONTROL Save]**.

Wanneer u **[!UICONTROL Save]** selecteert, worden de verbinding en de mogelijkheid om de bestanden naar uw SFTP-server te leveren getest. Met Platform maakt u een map, schrijft u een bestand in die map, controleert u of het bestand aanwezig is en wist u het daarna weer. Als de gebruikersaccount op uw SFTP-server (die is gekoppeld aan het beveiligde certificaat dat u aan het Platform hebt verstrekt) niet de benodigde machtigingen heeft om deze handeling uit te voeren, gaat de host naar de status &quot;Mislukt&quot;.
