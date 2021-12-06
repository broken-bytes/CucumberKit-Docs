---
description: >-
  Das Framework stellt eine Reihe von öffentlichen Typen bereit, welche der
  Nutzer einsetzen kann
---

# Typen

### **CucumberKit**

#### Attribute

| Name    | Typ         | Beschreibung                 |
| ------- | ----------- | ---------------------------- |
| default | CucumberKit | Singleton-Instanz der Klasse |

#### Beispiel

```swift
let framework = CucumberKit.default
```



### <mark style="color:green;">**Methoden**</mark>

### execute

#### Beispiel

```swift
framework.execute()
```

#### Parameter

Keine

### execute

#### Beispiel

```swift
framework.execute(filter: "Hello and World")
framework.execute(filter: "Hello or World")
framework.execute(filter: "Hello and not World")
```

#### Parameter

| Name   | Typ    | Beschreibung                                                                                                                                                          |
| ------ | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| filter | String | Erlaubt es dem Nutzer Tests auszuführen, die einem bestimmten FIlter entsprechen. Dabei werden einzelne Tags mittels infix kombiniert, um so den FIlter zu erstellen. |

### addFeatureFolder

#### Beispiel

```swift
framework.addFeatureFolder(folder: "Tests", bundle: Bundle.main)
```

#### Parameter

| Name   | Typ    | Beschreibung                                     |
| ------ | ------ | ------------------------------------------------ |
| folder | String | Der Name des des Ordners, welcher Tests enthält. |
| bundle | Bundle | Das iOS-Bundle, welches genutzt werden soll.     |

### CucumberScenario

CucumberScenario beschreibt ein einzelnes Testszenario einer Gherkin-Testdefinition.

#### Attribute

| Name  | Typ                | Beschreibung                                               |
| ----- | ------------------ | ---------------------------------------------------------- |
| file  | String             | Die Datei, in welcher das Szenario angelgt wurde.          |
| name  | String             | Der Name des Szenarios.                                    |
| steps | CucumberStep Array | Die Schritte dieses Szenarios, nach Zeilennummer sortiert. |
| tags  | String Array       | Die Tags dieses Szenarios.                                 |

### CucumberStep

CucumberStep bschreibt einen einzelnen Schritt in einer Testdefinition

#### Attribute

| Name        | Typ    | Beschreibung                                                     |
| ----------- | ------ | ---------------------------------------------------------------- |
| keyword     | String | Das Gherkin-Keyword, mit welchem der Testschritt beginnt.        |
| instruction | String | Der auszuführende Schritt. Ist im wesentlichen die Zeile selbst. |
|             |        |                                                                  |

### MatcherCallback

MatcherCallback ist die Typdefinition einer Callbackfunktion für Matcher

#### Parameter

| Name | Typ          | Beschreibung                                                               |
| ---- | ------------ | -------------------------------------------------------------------------- |
| args | String Array | Eine Array von Strings, welches durch den Aufruf von Match populiert wird. |
| step | CucumberStep | Der Schritt, welcher im aktuellen Match behandelt wird.                    |
| test | XCTestCase   | Der aktuelle native Test, welcher für die Ausführung genutzt wird.         |

### ScenarioHook

ScenarioHook ist die Typdefinition einer Callbackfunktion für Hooks, welche auf Szenarien ausgeführt werden können.

#### Parameter

| Name     | Typ              | Beschreibung                          |
| -------- | ---------------- | ------------------------------------- |
| scenario | CucumberScenario | Das Szenario welches ausgeführt wird. |

### StepHook

StepHook ist die Typdefinition einer Callbackfunktion für Hooks, welche auf Steps ausgeführt werden können.

#### Parameter

| Name     | Typ              | Beschreibung                          |
| -------- | ---------------- | ------------------------------------- |
| scenario | CucumberScenario | Das Szenario welches ausgeführt wird. |
| step     | CucumberStep     | Der Schritt, welcher ausgeführt wird. |

