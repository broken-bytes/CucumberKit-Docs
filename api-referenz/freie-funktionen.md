---
description: >-
  Das Framework stellt eine Reihe von freien Funktionen bereit, mit denen
  Testausführungen möglichst vielseitig konfiguriert werden können.
---

# Freie Funktionen

### <mark style="color:green;">**Matcher**</mark>

### Match

Diese Funktion wird genutzt um Testschritte zu implementieren.&#x20;

Mittels regulärer Ausdrücke können einzelne Parameter in Teilausdrücken ausgedrückt werden, um eine Vielzahl von Schritten abzudecken und über Parameter auf diese einzugehen.

Diese Funktion deckt alle Step Keywords (WHEN, THEN, AND,  GIVEN, \*) ab, soll nur auf bestimmte Keywords reagiert werden, muss die Überladung der Funktion genutzt werden, bei der ein zusätzliches Parameter an erster Stelle erwartet wird. Mit diesem lässt sich die Menge an Keywords definieren.&#x20;

#### Beispiel

```swift
Match("I eat \(RegexValue.numbers.rawValue) cucumbers") { args, step, test in }
```

#### Parameter

| Name        | Typ             | Beschreibung                                                                                                                              |
| ----------- | --------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| instruction | String          | Regulärer Ausdruck, gegen welchen jede Zeile der Gherkin-Dateien geprüft wird. Bei Treffer werden entsprechende Parameter weitergeleitet. |
| matcher     | MatcherCallback | Das Callback, welches bei einem Treffer ausgeführt wird.                                                                                  |

### Match

Diese Funktion wird genutzt um Testschritte zu implementieren.&#x20;

Mittels regulärer Ausdrücke können einzelne Parameter in Teilausdrücken ausgedrückt werden, um eine Vielzahl von Schritten abzudecken und über Parameter auf diese einzugehen.

Diese Funktion deckt nur die Keywords ab, welche im Argument keywords angegeben werden.

#### Beispiel

```swift
Match("And", "I eat \(RegexValue.numbers.rawValue) cucumbers") { args, step, test in }sws
```

#### Parameter

| Name        | Typ             | Beschreibung                                                                                                                              |
| ----------- | --------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| keywords    | String Array    | Liste der Keywords, welche dieses Match inkludieren soll.                                                                                 |
| instruction | String          | Regulärer Ausdruck, gegen welchen jede Zeile der Gherkin-Dateien geprüft wird. Bei Treffer werden entsprechende Parameter weitergeleitet. |
| matcher     | MatcherCallback | Das Callback, welches bei einem Treffer ausgeführt wird.                                                                                  |

### <mark style="color:green;">Hooks</mark>

### Before

Die Before Hook wird verwendet, wenn bestimmter Code vor dem Durchlauf jedes Szenarios ausgeführt werden soll.&#x20;

Möchte man die Reihenfolge angeben oder filtern, sollten die anderen Überladungen genutzt werden.

#### Beispiel

```swift
Before { args, step, test in }
```

| Name | Typ          | Beschreibung                                 |
| ---- | ------------ | -------------------------------------------- |
| hook | ScenarioHook | Das Callback welches ausgeführt werden soll. |

### Before

Die Before Hook wird verwendet, wenn bestimmter Code vor dem Durchlauf jedes Szenarios ausgeführt werden soll.&#x20;

Diese Überladung bietet die Angabe einer Reihenfolge, in welcher diese Hook ausgeführt werden soll.

#### Beispiel

```swift
Before(order: 2) { args, step, test in }  
```

#### Parameter

| Name  | Typ          | Beschreibung                                                               |
| ----- | ------------ | -------------------------------------------------------------------------- |
| order | Int          | Die Reihenfolge der Ausführung. Bei Dopplung der Nummer nach LIFO Prinzip. |
| hook  | ScenarioHook | Das Callback welches ausgeführt werden soll.                               |

### Before

Die Before Hook wird verwendet, wenn bestimmter Code vor dem Durchlauf jedes Szenarios ausgeführt werden soll.&#x20;

Diese Überladung bietet die Angabe eines Filters, mit welchem nur bestimmte Szenarien einbezogen werden sollen.

#### Beispiel

```swift
Before(filter: "Hello and World") { scenario in }
Before(filter: "Hello or World") { scenario in }
Before(filter: "Hello and not World") { scenario in }
```

#### Parameter

| Name   | Typ          | Beschreibung                                 |
| ------ | ------------ | -------------------------------------------- |
| filter | String       | Infix Filter auf Tags.                       |
| hook   | ScenarioHook | Das Callback welches ausgeführt werden soll. |

### Before

Die Before Hook wird verwendet, wenn bestimmter Code vor dem Durchlauf jedes Szenarios ausgeführt werden soll.&#x20;

Diese Überladung bietet die Angabe einer Reihenfolge in welcher diese Hook ausgeführt werden soll sowie einen Filter für Tags mittels infix.

Tags werden mittels des Infix-Operators behandelt.

#### Beispiel

```swift
Before(filter: "Hello and World", order: 1) { scenario in }
Before(filter: "Hello or World", order: 2) { scenario in }
Before(filter: "Hello and not World", order: 3) { scenario in }
```

#### Parameter

| Name   | Typ          | Beschreibung                                                               |
| ------ | ------------ | -------------------------------------------------------------------------- |
| filter | String       | Infix Filter auf Tags.                                                     |
| order  | Int          | Die Reihenfolge der Ausführung. Bei Dopplung der Nummer nach LIFO Prinzip. |
| hook   | ScenarioHook | Das Callback welches ausgeführt werden soll.                               |



### After

Die After Hook wird verwendet, wenn bestimmter Code nach dem Durchlauf jedes Szenarios ausgeführt werden soll.&#x20;

Möchte man die Reihenfolge angeben oder filtern, sollten die anderen Überladungen genutzt werden.

#### Beispiel

```swift
After { scenario in }
```

#### Parameter

| Name | Typ          | Beschreibung                                 |
| ---- | ------------ | -------------------------------------------- |
| hook | ScenarioHook | Das Callback welches ausgeführt werden soll. |

### After

Die After Hook wird verwendet, wenn bestimmter Code vor dem Durchlauf jedes Szenarios ausgeführt werden soll.&#x20;

Diese Überladung bietet die Angabe einer Reihenfolge, in welcher diese Hook ausgeführt werden soll.

#### Beispiel

```swift
After(order: 2) { scenario in }  
```

#### Parameter

| Name  | Typ          | Beschreibung                                                               |
| ----- | ------------ | -------------------------------------------------------------------------- |
| order | Int          | Die Reihenfolge der Ausführung. Bei Dopplung der Nummer nach LIFO Prinzip. |
| hook  | ScenarioHook | Das Callback welches ausgeführt werden soll.                               |

### After

Die After Hook wird verwendet, wenn bestimmter Code vor dem Durchlauf jedes Szenarios ausgeführt werden soll.&#x20;

Diese Überladung bietet die Angabe eines Filters, mit welchem nur bestimmte Szenarien einbezogen werden sollen.

#### Beispiel

```swift
After(filter: "Hello and World") { scenario in }
After(filter: "Hello or World") { scenario in }
After(filter: "Hello and not World") { scenario in }
```

#### Parameter

| Name   | Typ          | Beschreibung                                 |
| ------ | ------------ | -------------------------------------------- |
| filter | String       | Infix Filter auf Tags.                       |
| hook   | ScenarioHook | Das Callback welches ausgeführt werden soll. |

### After

Die After Hook wird verwendet, wenn bestimmter Code vor dem Durchlauf jedes Szenarios ausgeführt werden soll.&#x20;

Diese Überladung bietet die Angabe einer Reihenfolge in welcher diese Hook ausgeführt werden soll sowie einen Filter für Tags mittels infix.

Tags werden mittels des Infix-Operators behandelt.

#### Beispiel

```swift
After(filter: "Hello and World", order: 1) { scenario in }
After(filter: "Hello or World", order: 2) { scenario in }
```

#### Parameter

| Name   | Typ          | Beschreibung                                                               |
| ------ | ------------ | -------------------------------------------------------------------------- |
| filter | String       | Infix Filter auf Tags.                                                     |
| order  | Int          | Die Reihenfolge der Ausführung. Bei Dopplung der Nummer nach LIFO Prinzip. |
| hook   | ScenarioHook | Das Callback welches ausgeführt werden soll.                               |

### BeforeStep

Die BeforeStep Hook wird verwendet, wenn bestimmter Code vor dem Durchlauf jedes TestSteps ausgeführt werden soll.&#x20;

Sollen nur bestimmte Steps abgedeckt werden, wird eine Überladung dieser Funktion genutzt.

#### Beispiel

```swift
BeforeStep { scenario, step in }
```

#### Parameter

| Name | Typ      | Beschreibung                                 |
| ---- | -------- | -------------------------------------------- |
| hook | StepHook | Das Callback welches ausgeführt werden soll. |

### BeforeStep

Die BeforeStep Hook wird verwendet, wenn bestimmter Code vor dem Durchlauf jedes TestSteps ausgeführt werden soll. &#x20;

Mit dem Parameter filter wird die Menge der abgedeckten Steps gefiltert.&#x20;

#### Beispiel

```swift
BeforeStep(filter: "Hello and World") { scenario, step in }
BeforeStep(filter: "Hello or World") { scenario, step in }
BeforeStep(filter: "Hello and not World") { scenario, step in }
```

#### Parameter

| Name   | Typ      | Beschreibung                                 |
| ------ | -------- | -------------------------------------------- |
| filter | String   | Infix-Filter auf die Tags des Steps.         |
| hook   | StepHook | Das Callback welches ausgeführt werden soll. |

### AfterStep

Die AfterStep Hook wird verwendet, wenn bestimmter Code nach dem Durchlauf jedes TestSteps ausgeführt werden soll.&#x20;

Sollen nur bestimmte Steps abgedeckt werden, wird eine Überladung dieser Funktion genutzt.

#### Beispiel

```swift
AfterStep { scenario, step in }
```

#### Parameter

| Name | Typ      | Beschreibung                                 |
| ---- | -------- | -------------------------------------------- |
| hook | StepHook | Das Callback welches ausgeführt werden soll. |

### AfterStep

Die AfterStep Hook wird verwendet, wenn bestimmter Code nach dem Durchlauf jedes TestSteps ausgeführt werden soll. &#x20;

Mit dem Parameter filter wird die Menge der abgedeckten Steps gefiltert.&#x20;

#### Parameter

#### Beispiel

```swift
AfterStep(filter: "Hello and World") { scenario, step in }
AfterStep(filter: "Hello or World") { scenario, step in }
AfterStep(filter: "Hello and not World") { scenario, step in }
```

| Name   | Typ      | Beschreibung                                 |
| ------ | -------- | -------------------------------------------- |
| filter | String   | Infix-Filter auf die Tags des Steps.         |
| hook   | StepHook | Das Callback welches ausgeführt werden soll. |

