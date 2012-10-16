---
published: true
layout: article
title: Mythen und Fakten über Behaviour Driven Development
abstract: Einführung in BDD, Behat und Mink von Sebastian Bauer und Dominik Jungowski
author_twitter: Fabian_ikono
author: Fabian Blechschmidt
categories:
- articles
tags:
- IPC12
---

# Mythen und Fakten über Developer Driven Development

## Von TDD zu BDD

TDD schreibt technische Tests, die dafür sorgen, dass die Komponenten tun, was der Entwickler von Ihnen möchte. Das ist ein Problem, wenn die Anwendung hinterher nicht tut, wofür sie eigentlich gedacht ist. BDD setzt früher an, nämlich beim späteren Benutzer, mit dem man zusammen das Verhalten beschreibt um dann anschließend Tests zu generieren, die sicherstellen, dass die Anwendung tut, wofür sie gedacht ist.

## Warum verhaltensgetrieben?

Die Sicht von technischer Seite soll zur Kunden und Benutzersicht wechseln.

##Gherkin (Domain Specific Language)

War ein Teil von Cucumber. Ist normale Sprache, d.h. nicht nur Techniker, sondern auch Kunden und Projektleiter können sie lesen.

### Wie funktioniert Gherkin:

* Annahme/Umwelt: Wie ist die Welt gerade? -> Voraussetzungen
 * Schlüsselwort: Given
* Aktion: Was tut man dann? Aktion, die der Benutzer/... unternimmt.
 * Schlüsselwort: When
* Erwartetes Ergebnis: Wie ist der Status am Ende? Was erwarten wir?
 * Schlüsselwort: Then
 
Man sollte einen Negativ und einen Positivtest geben. Wenn man etwas sucht beschreibt man z.B. das Ergebnis, wenn es ein Suchergebnis gibt und wenn es keines gibt.

> Live-Demo mit Behat

## Behat

Wenn man Tests in Behat implementiert und probiert auszuführen, bekommt man eine Übersicht von PHP-Code, den es zu implementieren gilt um die Tests auszuführen.

## Mink

Mink ist ein Browseremulator, der bei Symfony dabei ist. Mit Mink erhält man CSS-Selektoren, XQuery, man kann Formulare ausfüllen, Buttons drücken, etc.

## andere Treiber

Chrome, Selenium, Headless

> [Cucumber](http://cukes.info/) ist das bessere Tool.

## BDD als agile Dokumentation

Wenn ein neuer Entwickler an unbekanntem Code sitzt, stellt er sich immer die Frage, welches Verhalten wird an dieser Stelle erwartet. Diese Stelle kann man dank Tests beantworten.

## Warum in agilen Teams? Wo macht es Sinn?

Der große Vorteil ist, dadurch das der Product Owner die Tests lese und vorher abnehmen kann. Dadurch bekommt er - vorausgesetzt er macht sich vorher ausreichend Gedanken, genau das, was er will.

## Wo macht BDD keinen Sinn?

Auf Seiten die "content getrieben" sind, macht es keinen Sinn, z.B. [heise.de](http://heise.de) oder [spon.de](http://www.spon.de).

Verhalten wie "Klick auf Link öffnet diesen und man landet hinterher auf dem Artikel" ist zu simpel, als dass sich der Aufwand lohnt.




