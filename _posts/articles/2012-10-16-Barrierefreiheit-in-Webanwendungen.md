---
published: true
layout: article
title: Barrierefreiheit in Webanwendungen
abstract: Talk by Timm Bremus on the IPC12
author_twitter: Fabian_ikono
author: Fabian Blechschmidt
categories:
- articles
tags:
- IPC12
---

# Barrierefreiheit in Webanwendungen

> Zu kompliziert! nur für Blinde! zu teuer! müssen wir das machen?

> Barrierefreiheit bringt sauberen HTML und CSS Code.

> Man benutzt aktuelle Technik und bekommt SEO Optimierung gratis.

## Accessibility vs Useability

* `Accessibility` ist, wie gut man eine Seite erreichen kann
* `Useability` ist, wie gut man eine Seite benutzen kann

## Gesetze und Normen

* Behindertengleichstellungsgesetz BGG -> §11
* Barrierefreie Informationstechnik-Verordnung (BITV)
* Web Accessibility Initiative (WAI)
 * Alternative zu Videos und Audioinhalte
 * Struktus/Semantik nicht nur durch Farben darstellen
 * W3C Richtlinen einhalten
 * Klare Navigationsmechanismen
 * Einfach gehaltene Inhalts- und Satzstrukturen
 * Geräteunabhängiges Design

## Wer braucht's?
* Nutzer mit leerem Mausakku
* Gruppe der 50+
* Sehnenscheidentzündung
* Rot-Grüne-Schwäche
* moderne Mobiltechnik
* langsame Internetverbindung
* **6,7 Mio mit Schwerstbehinderung**
* **164.000 blinde und 1 Mio sehbehinderte Menschen**

## Farben & Kontraste
* Rot/Grün-Kombinationen vermeiden
* Grelle Farben vermeiden
* Genug Kontrast zwischen Text und Hintergrund

[Farbkontrast Analyzer von Web for all](http://www.webforall.info/index.php?option=com_content&view=article&id=84&Itemid=84)

## HTML
* Korrekte HTML Elemente nutzen (h1-h6, p, table, ul, ...)
* Suchfeld als erstes im Quelltext anlegen
* Verstecktes Menü
* Sprunglinks
 * &lt;a href&gt;, &lt;a id&gt;
 * nicht zuviele davon
 * hervorheben bei hover, focus, active
* Formatierungen und Darstellungen
 * sonnvolle Formatierungen
 * Unterstreichungen **nur** bei Links
 * Fettdruck in Maßen
 * nichr kursiv verwenden
 * sinnvolle alt-Attribute in Bildern &lt;img alt="Hier eine Beschreibung"&gt;
* Formulare
 * Pflichtfeldhinweis in &lt;label&gt; (Nicht nur ein Sternchen - für Blinde)
 * Captcha Frage innerhalb des Labels positionieren
 * Fehlermeldung vor Eingabefeldern ausgeben (im HTML!, nicht zwangsweise auch so sichtbar)
 * Seitentitel bei Fehlerausgabe abändern
 * aktives Feld hervorheben
* Navigation
 * aktiver Navigationspunkt mit &lt;strong&gt; einfaßen
 * Links "flächig" (display: block;) definieren, damit Benutzer mehr als den Text zum klicken haben
 * verstecktes Menü mit Sprunglinks
 
## Didaktik
* Fachbegriffe, Abkürzungen, Fremdwörter vermeiden
* Einfache Sätze und Sprache
* Links mit sinnvollen Bezeichnungen

> `Display: none;` wird vom Screenreader nicht vorgelesen, d.h. man darf Dinge, die Screenreader lesen sollen nicht mit display: none; belegen!

> Screenreder können JavaScript!

## Summary
Barrierefreiheit ist Win-Win-Situation für Benutzer, Entwickler und das Management.

Optimierungen sind nicht nur gut für das HTML, CSS sondern auch für [SEO](http://de.wikipedia.org/wiki/Suchmaschinenoptimierung).

