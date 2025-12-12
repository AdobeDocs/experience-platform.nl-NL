---
title: Compatibiliteitsnorm met achterwaartse compatibiliteit
description: Leer meer over de standaard voor achterwaartse compatibiliteit in Adobe Experience Platform die ervoor zorgt dat bijgewerkte versies van tagextensies compatibel zijn met eerdere versies.
exl-id: 325390f1-88c7-4b9e-a484-5442ca649bdf
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 0%

---

# Achterwaartse compatibiliteitsnorm

Updates van een tagextensie in Adobe Experience Platform moeten compatibel zijn met eerdere versies van de extensie. Dit betekent dat:

* Wijzigingen in de primaire componenten van de extensies moeten compatibel zijn met eerdere versies.  Dit omvat extensieconfiguratie, gebeurtenistypen, gebeurtenistypen, gegevenselemetypen en gedeelde modules.
* Componenten die een gebruiker met de oudere extensieversie heeft gemaakt, moeten validatie kunnen doorstaan voor de schema&#39;s die door de nieuwere versie worden geleverd.
* Een Adobe Experience Platform-gebruiker moet een bijgewerkte versie van uw extensie kunnen installeren en alles wat hij of zij heeft gedaan, precies zo laten werken totdat hij of zij opzettelijk wijzigingen aanbrengt.

## Toegestane wijzigingen

De volgende typen wijzigingen in uw extensie zijn toegestaan:

1. U kunt nieuwe componenten toevoegen (gebeurtenistypen, gebeurtenistypen, enz.).
1. U kunt nieuwe optionele velden toevoegen aan de configuratie-instellingen voor extensies.
1. U kunt vereiste velden wijzigen in optionele velden.

## Verboden wijzigingen

De volgende typen wijzigingen in uw extensie zijn niet toegestaan:

1. U kunt de naam van een component niet wijzigen.
1. U kunt een component niet verwijderen.
1. U kunt een veld niet uit een component verwijderen.
1. U kunt optionele velden niet wijzigen in vereiste velden.
1. U kunt geen nieuwe vereiste velden toevoegen.
1. U kunt de API van bestaande gedeelde modules niet wijzigen.

Als u een van deze wijzigingen aanbrengt, krijgt iedereen die de extensie in zijn eigenschap heeft geïnstalleerd, direct problemen zoals:

* Regels worden niet meer correct gerenderd omdat een van de regelcomponenten naar een component zoekt die niet bestaat
* Alle builds mislukken omdat de bibliotheek een upstream-bron bevat die niet meer bestaat in de extensie
* Alle builds mislukken omdat de Bibliotheek een middel met montages omvat die bevestiging tegen het nieuwe schema ontbreken

Met name in dit tweede geval kunnen gebruikers zonder een oplossing worden gelaten en kunnen ze hun eigenschap niet repareren zodat ze deze opnieuw kunnen publiceren.

## Functies verwijderen

Er kunnen scenario&#39;s zijn wanneer u een geldige bedrijfsreden hebt en u denkt u echt een verboden verandering (hierboven vermeld) moet maken.  Je kunt het nog steeds niet doen, maar dit is wat je kunt doen:

1. Ik wil een component verwijderen => Maak een nieuwe component en vervang oude
1. Ik wil een veld uit een component verwijderen => Maak een nieuwe component met dat veld verwijderd en vervang het oude veld
1. Ik wil een optioneel veld dat vereist is, wijzigen => Maak een nieuw onderdeel waarvoor het gewenste veld is vereist en verwijder het oude veld
1. Ik wil de API van een gedeelde module wijzigen => Maak een nieuwe gedeelde module en vervang de oude

Je neemt misschien op een gewone thread.  Dat is goed.  Wanneer u een oude component vervangt, wilt u gebruikers van uw extensie op de hoogte stellen van het feit dat de extensie is vervangen en dat ze naar een nieuwe moeten overschakelen.  Enkele suggesties voor het communiceren met gebruikers:

* Werk de weergavenaam van de oude component bij en voeg &quot;(Afgekeurd)&quot; toe.
* Werk de mening voor de oude component bij om grote rode waarschuwingstekst te hebben dat deze component is afgekeurd en dat de gebruiker op de nieuwe component zou moeten schakelen.
* Werk uw modulecode bij om de berichten van de logboekveroudering in de console te registreren.  Houd in mening dat deze aan eindgebruikers zullen tonen, zodat houd het schoon en enigszins generisch.
* Verzend vriendelijke e-mailberichten van uw CRM-systeem.

In gevallen waar de oude functionaliteit niet alleen ongewenste is, maar eigenlijk niet meer in uw oplossing bestaat, is er één extra stap u kunt nemen - maar zou slechts moeten doen nadat u uw gebruikers hebt bericht en hen tijd gegeven om bij te werken.

* Werk de inhoud van uw module bij zodat het niets doet.  Hierdoor wordt de functionaliteit verwijderd uit de geïmplementeerde bibliotheek van de gebruiker in de volgende build, maar worden de regels of builds niet verbroken.

### Verwijderde functies herstellen

Als u reeds functionaliteit hebt verwijderd en van gebruikers horen dat de dingen als resultaat breken, moet u een nieuwe versie van uw uitbreiding vrijgeven die de componenten herstelt u verwijderde.

Het is prima om ze in een vervangen toestand te herstellen, zoals hierboven beschreven, maar ze moeten wel bestaan.

Als voorbeeld, laten wij zeggen u een v1.0 hebt die Component XYZ heeft die de mensen gebruiken.  Vervolgens geeft u een versie 1.1 vrij die geen Component XYZ meer heeft.  U hoort van uw gebruikers dat uw extensie de eigenschappen heeft verbroken en dat u deze moet herstellen.  U moet v1.2 vrijgeven die Component XYZ (misschien in verouderde staat-dat tot u) terugbrengt en uw gebruikers hebben verbetering aan v1.2 om dingen te maken opnieuw werken.
