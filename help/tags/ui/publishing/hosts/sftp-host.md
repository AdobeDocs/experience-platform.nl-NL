---
title: SFTP-hosts
description: Leer hoe u tags in Adobe Experience Platform configureert om bibliotheekbuilds te leveren aan een beveiligde, zelfgehoste SFTP-server.
exl-id: 3c1dc43b-291c-4df4-94f7-a03b25dbb44c
source-git-commit: a077d3a1b14d9b7786d3181a556c49e940a42c2f
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 5%

---

# SFTP-hosts

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor dataverzameling in Adobe Experience Platform.  Als gevolg hiervan zijn er verschillende terminologiewijzigingen in de productdocumentatie doorgevoerd. Raadpleeg het volgende [&#x200B; document &#x200B;](../../../term-updates.md) voor een geconsolideerde referentie van de terminologiewijzigingen.

Met Experience Platform kunt u bouwen van tagbibliotheken leveren aan een beveiligde SFTP-server die u host, zodat u meer controle hebt over de manier waarop uw builds worden opgeslagen en beheerd. In deze handleiding wordt uitgelegd hoe u een SFTP-host instelt voor een tag-eigenschap in de gebruikersinterface van Experience Platform of de gebruikersinterface voor gegevensverzameling.

>[!NOTE]
>
>U kunt er ook voor kiezen om een host te gebruiken die door Adobe wordt beheerd. Zie de gids op [&#x200B; Adobe-Beheerde gastheren &#x200B;](./managed-by-adobe-host.md) voor meer informatie.
>
>Voor informatie over de voordelen en de beperkingen van zelf-ontvangende bibliotheken, zie de [&#x200B; zelf-ontvangende gids &#x200B;](./self-hosting-libraries.md).

## Een toegangstoets voor uw server instellen {#access-key}

Experience Platform maakt verbinding met uw SFTP-site met behulp van een gecodeerde sleutel. Er zijn een paar stappen om dit correct in te stellen:

### Een combinatie van openbare/persoonlijke sleutels maken

Er moet een combinatie van openbare/persoonlijke sleutels op uw SFTP-server zijn geïnstalleerd. U kunt deze sleutels op uw server produceren of hen ergens anders produceren en hen installeren op uw server. Zie de documentatie GitHub betreffende [&#x200B; hoe te om sleutels van SSH &#x200B;](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/#generating-a-new-ssh-key) voor meer informatie te produceren.

### De sleutels versleutelen

De persoonlijke sleutel wordt gebruikt om de openbare sleutel te coderen. U moet uw persoonlijke sleutel opgeven tijdens het maken van de SFTP-host. Zie de sectie over [&#x200B; het coderen van waarden &#x200B;](../../../api/guides/encrypting-values.md) in de Reactor API gids voor instructies bij het coderen van openbare sleutels. Gebruik de GPG-sleutel van de productieomgeving, tenzij u weet dat u een specifieke sleutel nodig hebt. Tot slot kunt u uw persoonlijke sleutel van om het even welke machine coderen, zodat te hoeven u niet om GPG op uw server te installeren om deze stap te voltooien.

### Experience Platform IP-adressen voor Lijst van gewenste personen

Mogelijk moet u een set IP-adressen goedkeuren die binnen uw bedrijfsfirewall moet worden gebruikt, zodat Experience Platform uw SFTP-server kan bereiken en er verbinding mee kan maken. Deze IP Adressen zijn:

* `34.227.138.75`
* `44.194.43.191`
* `3.215.163.18`

>[!NOTE]
>
>De structuur van builds van tags is in de loop der tijd gewijzigd. Zij gebruiken symbolische verbindingen (symbolische verbindingen) intern om achterwaartse verenigbaarheid te handhaven zodat de vorige inbedcodes met de recentste bouwstijlstructuur zullen blijven werken. Uw SFTP-server moet het gebruik van symlinks ondersteunen om als geldige bestemming voor het maken van tags te kunnen fungeren.

Voor meer gedetailleerde informatie, verwijs naar het volgende artikel van Medium op [&#x200B; hoe te opstellingsSFTP servers om een bouwstijl &#x200B;](https://medium.com/launch-by-adobe/configuring-an-sftp-server-for-use-with-adobe-launch-bc626027e5a6) te leveren.

## Een SFTP-host maken {#create}

Selecteer **[!UICONTROL Hosts]** in de linkernavigatie, gevolgd door **[!UICONTROL Add Host]** .

![&#x200B; Beeld dat de Add knoop toont van de Gastheer die in UI wordt geselecteerd &#x200B;](../../../images/ui/publishing/sftp-hosts/add-host-button.png)

Het dialoogvenster voor het maken van de host wordt weergegeven. Geef een naam op voor de host en selecteer **[!UICONTROL Type]** onder **[!UICONTROL SFTP]** .

![&#x200B; Beeld dat SFTP toont die optie wordt geselecteerd &#x200B;](../../../images/ui/publishing/sftp-hosts/select-sftp.png)

### De SFTP-host configureren {#configure}

Het dialoogvenster wordt uitgebreid en bevat aanvullende configuratieopties voor de SFTP-host. Deze worden hieronder toegelicht.

![&#x200B; Beeld die de vereiste details voor een de gastheerverbinding van SFTP tonen &#x200B;](../../../images/ui/publishing/sftp-hosts/host-details.png)

| Configuratieveld | Beschrijving |
| --- | --- |
| [!UICONTROL Don't Use Symlinks] | Door gebrek, gebruiken alle gastheren SFTP symbolische verbindingen (symbolische verbindingen) om bibliotheek [&#x200B; van verwijzingen te voorzien bouwt &#x200B;](../builds.md) die aan de server worden bewaard. Niet alle servers ondersteunen echter het gebruik van symlinks. Als deze optie is geselecteerd, gebruikt de gastheer een kopieerbewerking om de build-elementen rechtstreeks bij te werken in plaats van gebruik te maken van symlinks. |
| [!UICONTROL SFTP Server URL] | Het URL-basispad voor uw server. |
| [!UICONTROL Path] | Het pad dat moet worden toegevoegd aan de URL van de basisserver voor deze host. |
| [!UICONTROL Port] | De poort moet een van de volgende zijn:<ul><li>`21`</li><li>`22`</li><li>`201`</li><li>`200`</li><li>`2002`</li><li>`2018`</li><li>`2022`</li><li>`2200`</li><li>`2222`</li><li>`2333`</li><li>`2939`</li><li>`443`</li><li>`4343`</li><li>`80`</li><li>`8080`</li><li>`8888`</li></ul>Als veiligheid beste praktijken, beperkt Adobe het aantal havens die voor uitgaand verkeer kunnen worden gebruikt. De geselecteerde havens worden algemeen toegestaan door collectieve firewalls en omvatten sommige waaiers voor flexibiliteit. |
| [!UICONTROL Username] | De gebruikersnaam die moet worden gebruikt wanneer de server wordt geopend. |
| [!UICONTROL Encrypted Private Key] | De gecodeerde privé sleutel die u in a [&#x200B; vorige stap &#x200B;](#access-key) creeerde. |

Selecteer **[!UICONTROL Save]** om de host te maken met de geselecteerde configuratie.

![&#x200B; Beeld dat de gastheer toont SFTP die wordt bewaard &#x200B;](../../../images/ui/publishing/sftp-hosts/save-host.png)

Wanneer u **[!UICONTROL Save]** selecteert, worden de verbinding en de mogelijkheid om de bestanden naar uw SFTP-server te leveren getest. Experience Platform maakt een map, schrijft een bestand in die map, controleert of het bestand aanwezig is en wist het vervolgens zelf. Als de gebruikersaccount op uw SFTP-server (die is gekoppeld aan het beveiligde certificaat dat u aan Experience Platform hebt verstrekt) niet de benodigde machtigingen heeft om deze handeling uit te voeren, gaat de host naar de status &quot;Mislukt&quot;.

## Volgende stappen

In deze handleiding wordt beschreven hoe u een zelfgehoste SFTP-server instelt voor gebruik in tags. Zodra de gastheer is gevestigd, kunt u het met één of meerdere van uw [&#x200B; milieu&#39;s &#x200B;](../environments.md) voor het publiceren van markeringsbibliotheken associëren. Voor meer informatie over het proces op hoog niveau om markeringsfuncties op uw Web of mobiele eigenschappen te activeren, zie het [&#x200B; het publiceren overzicht &#x200B;](../overview.md).
