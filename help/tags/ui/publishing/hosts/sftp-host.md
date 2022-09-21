---
title: SFTP-hosts
description: Leer hoe u tags in Adobe Experience Platform configureert om bibliotheekbuilds te leveren aan een beveiligde, zelfgehoste SFTP-server.
exl-id: 3c1dc43b-291c-4df4-94f7-a03b25dbb44c
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 0%

---

# SFTP-hosts

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Met Adobe Experience Platform kunt u bouwen van tagbibliotheken leveren aan een beveiligde SFTP-server die u host, zodat u meer controle hebt over de manier waarop uw builds worden opgeslagen en beheerd. Deze gids behandelt hoe te opstelling een gastheer SFTP voor een markeringsbezit in de UI van het Experience Platform of UI van de Inzameling van Gegevens.

>[!NOTE]
>
>U kunt er ook voor kiezen om een host te gebruiken die door Adobe wordt beheerd. Zie de handleiding op [Door Adobe beheerde hosts](./managed-by-adobe-host.md) voor meer informatie .
>
>Voor informatie over de voordelen en beperkingen van bibliotheken die zichzelf hosten raadpleegt u de [zelfhostinghandleiding](./self-hosting-libraries.md).

## Een toegangstoets voor uw server instellen {#access-key}

Platform maakt verbinding met uw SFTP-site met behulp van een gecodeerde sleutel. Er zijn een paar stappen om dit correct in te stellen:

### Een combinatie van openbare/persoonlijke sleutels maken

Er moet een combinatie van openbare/persoonlijke sleutels op uw SFTP-server zijn geïnstalleerd. U kunt deze sleutels op uw server produceren of hen ergens anders produceren en hen installeren op uw server. Zie de documentatie van GitHub betreffende [SSH-toetsen genereren](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/#generating-a-new-ssh-key) voor meer informatie .

### De sleutels versleutelen

De persoonlijke sleutel wordt gebruikt om de openbare sleutel te coderen. U moet uw persoonlijke sleutel opgeven tijdens het maken van de SFTP-host. Zie de sectie over [versleutelen, waarden](../../../api/guides/encrypting-values.md) in de Reactor API-handleiding voor instructies voor het versleutelen van openbare sleutels. Gebruik de GPG-sleutel van de productieomgeving, tenzij u weet dat u een specifieke sleutel nodig hebt. Tot slot kunt u uw persoonlijke sleutel van om het even welke machine coderen, zodat te hoeven u geen GPG op uw server te installeren om deze stap te voltooien.

### IP van het Platform van de Lijst van gewenste personen adressen

Mogelijk moet u een set IP-adressen goedkeuren die binnen uw bedrijfsfirewall moet worden gebruikt, zodat Platform uw SFTP-server kan bereiken en er verbinding mee kan maken. Deze IP Adressen zijn:

* `184.72.239.68`
* `23.20.85.113`
* `54.226.193.184`

>[!NOTE]
>
>De structuur van builds van tags is in de loop der tijd gewijzigd. Zij gebruiken symbolische verbindingen (symbolische verbindingen) intern om achterwaartse verenigbaarheid te handhaven zodat de vorige inbedcodes met de recentste bouwstijlstructuur zullen blijven werken. Uw SFTP-server moet het gebruik van symlinks ondersteunen om als geldige bestemming voor het maken van tags te kunnen fungeren.

Raadpleeg voor meer informatie het volgende Medium artikel over [hoe u SFTP-servers kunt instellen om een build te leveren](https://medium.com/launch-by-adobe/configuring-an-sftp-server-for-use-with-adobe-launch-bc626027e5a6).

## Een SFTP-host maken {#create}

Selecteren **[!UICONTROL Hosts]** in de linkernavigatie, gevolgd door **[!UICONTROL Add Host]**.

![Afbeelding waarin de knop Host toevoegen wordt weergegeven die in de gebruikersinterface is geselecteerd](../../../images/ui/publishing/sftp-hosts/add-host-button.png)

Het dialoogvenster voor het maken van de host wordt weergegeven. Geef een naam op voor de host en onder **[!UICONTROL Type]**, selecteert u **[!UICONTROL SFTP]**.

![Afbeelding waarin de SFTP-hostingoptie wordt geselecteerd](../../../images/ui/publishing/sftp-hosts/select-sftp.png)

### De SFTP-host configureren {#configure}

Het dialoogvenster wordt uitgebreid en bevat aanvullende configuratieopties voor de SFTP-host. Deze worden hieronder toegelicht.

![Afbeelding met de vereiste gegevens voor een SFTP-hostverbinding](../../../images/ui/publishing/sftp-hosts/host-details.png)

| Configuratieveld | Beschrijving |
| --- | --- |
| [!UICONTROL Don't Use Symlinks] | Standaard gebruiken alle SFTP-hosts symbolische koppelingen (symbolische koppelingen) om naar de bibliotheek te verwijzen [builds](../builds.md) die op de server worden opgeslagen. Niet alle servers ondersteunen echter het gebruik van symlinks. Als deze optie is geselecteerd, gebruikt de gastheer een kopieerbewerking om de build-elementen rechtstreeks bij te werken in plaats van gebruik te maken van symlinks. |
| [!UICONTROL SFTP Server URL] | Het URL-basispad voor uw server. |
| [!UICONTROL Path] | Het pad dat moet worden toegevoegd aan de URL van de basisserver voor deze host. |
| [!UICONTROL Port] | De poort moet een van de volgende zijn:<ul><li>`21`</li><li>`22`</li><li>`80`</li><li>`200-299`</li><li>`443`</li><li>`2000-2999`</li><li>`4343`</li><li>`8080`</li><li>`8888`</li></ul>Als veiligheid beste praktijken, beperkt Adobe het aantal havens die voor uitgaand verkeer kunnen worden gebruikt. De geselecteerde havens worden algemeen toegestaan door collectieve firewalls en omvatten sommige waaiers voor flexibiliteit. |
| [!UICONTROL Username] | De gebruikersnaam die moet worden gebruikt wanneer de server wordt geopend. |
| [!UICONTROL Encrypted Private Key] | De gecodeerde persoonlijke sleutel die u in een [vorige stap](#access-key). |

Selecteren **[!UICONTROL Save]** om de gastheer met de geselecteerde configuratie tot stand te brengen.

![Afbeelding die de SFTP-host weergeeft die wordt opgeslagen](../../../images/ui/publishing/sftp-hosts/save-host.png)

Wanneer u **[!UICONTROL Save]**, worden de verbinding en de mogelijkheid om de bestanden naar uw SFTP-server te leveren getest. Met Platform maakt u een map, schrijft u een bestand in die map, controleert u of het bestand aanwezig is en wist u het daarna opnieuw. Als de gebruikersaccount op uw SFTP-server (die is gekoppeld aan het beveiligde certificaat dat u aan het Platform hebt verstrekt) niet de benodigde machtigingen heeft om deze handeling uit te voeren, gaat de host naar de status &quot;Mislukt&quot;.

## Volgende stappen

In deze handleiding wordt beschreven hoe u een zelfgehoste SFTP-server instelt voor gebruik in tags. Zodra de gastheer is gevestigd, kunt u het met één of meerdere van uw associëren [omgevingen](../environments.md) voor het publiceren van tagbibliotheken. Raadpleeg voor meer informatie over het proces op hoog niveau voor het activeren van tagfuncties op uw web of mobiele eigenschappen de [publicatieoverzicht](../overview.md).
