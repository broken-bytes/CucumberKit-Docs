---
description: Dieses Dokument soll einen schnellen Einstieg in das Framework gewährleisten.
---

# Schnellstart

### Installation

Die Installation des Frameworks wird mittels Cocoapods realisiert. Cocoapods ist eine Software, welche die Verwaltung von Referenzen in iOS-Projekten vereinfacht.&#x20;

Dazu muss zunächst der folgende Befehl über die Konsole im Stammverzeichnis des Projekts ausgeführt werden.&#x20;

`pod install`&#x20;

Die nötigen Informationen, sowie einige Auswahlmöglichkeiten erhält der Nutzer über die Konsole. Nach Abschluss des Befehls ist das Projekt konfiguriert.

Nun muss der Nutzer die Datei „Podfile“ öffnen, welche im Zuge der Konfiguration automatisch angelegt wurde. Um das Framework einzubinden, muss der Pfad, in welchem sich das Framework befindet, nun eingetragen werden.

Eine beispielhafte Version des Podfiles entspricht minimal der folgenden Form:

```ruby
use_frameworks!

platform :ios, '13.0'

target 'CucumberKit_Example' do
  target 'CucumberKitExamplesUITests' do
    inherit! :search_paths
      pod 'CucumberKit', :path => '../' # Diese Zeile bindet das Framework ein
  end
end
```

Eine detaillierte Beschreibung des Erstellungsprozesses ist unter [https://cocoapods.org/](https://cocoapods.org) zu finden.

## Konfiguration

Um das Framework nutzen zu können muss XCode mitgeteilt werden, dass der Code des Frameworks zur Laufzeit von Tests als erstes gestartet werden soll. Andernfalls würde der Code zwar ausgeführt werden, die Testreihe würde allerdings ohne Berücksichtigung der automatisch erstellten Tests abgeschlossen werden. Dementsprechend muss der Entwickler eine Objective-C Datei erstellen, welche diesen Schritt ausführt.&#x20;

Die Nutzung von Objective-C ist an dieser Stelle nötig, weil Swift nicht die Möglichkeit bietet, die Ausführungsreihenfolge zu überladen.&#x20;

Die Datei sollte dem folgenden Code ähnlich sein:

```objectivec
#import <Foundation/Foundation.h>
#import "CucumberKitExamplesUITests-Swift.h" // Bridging Header des Frameworks. 

// Erzwingt die Ausführung dieses Codes vor Start der Testreihe
__attribute__((constructor)) 
void CucumberInit(){
// Hier sollte das Framework initialisert werden
    [CucumberKitInitializer setup]; 
}
```

## Testausführung

Um Tests auszuführen, importiert der Nutzer in seinem Code zunächst das Modul CucumberKit. Anschließend steht dem Nutzer die gleichnamige Klasse zur Verfügung, mit welcher der Testprozess gestartet werden kann.

Mittels der Methode `execute`wird die Testreihe gestartet. Dabei wird nach dem Ordner „Features“ im aktuellen Bundle gesucht, in welchem die Testdefinitionen in der Gherkin-Sprache vorhanden sind. Die Methode bietet eine Überladung, mit welcher sich die Menge an zu berücksichtigenden Tests beschränken lässt.

Alternativ kann der Nutzer mittels der Methode `addFeatureFolder`weitere Ordner in den Testlauf mit einbinden. Dabei ist zu beachten, dass der Standordner zu jedem Zeitpunkt, auch bei Angabe eigener Ordner, in die Testreihe miteinbezogen wird. Dieser kann dabei leer oder nicht vorhanden sein, ist also nicht zwingend benötigt.

## Schnittstellen

### Matcher

&#x20;Das Framework bietet dem Nutzer eine komfortable Weise Testausführungen zu implementieren. Mittels sogenannter „Matcher“ kann der Nutzer eine beliebige Menge an Testschritten mittels regulärer Ausdrücke abdecken. Möchte der Nutzer eine Reihe von dynamischen Argumenten seiner Testschritte abdecken, kann dies mithilfe von Teilausdrücken innerhalb des Ausdrucks realisiert werden. Dabei erhält der Nutzer die einzelnen Treffer der Teilausdrücke als Liste zurück.

### Hooks

&#x20;Dem Nutzer stehen diverse Schnittstellen zur Anpassung der Testumgebung zur Verfügung. Unter anderem verfügt das Framework über eine Vielzahl von Events, genannt „Hook“, mit welchen auf verschiedene Ereignisse im Testprozess eingegangen werden kann.

## Ausgabe

Die Ausgabe der Testergebnisse erfolgt über XCode. Über die Testübersicht innerhalb von XCode wird mitgeteilt, ob Testfälle sowie Schritte erfolgreich oder fehlerhaft durchgelaufen sind.

