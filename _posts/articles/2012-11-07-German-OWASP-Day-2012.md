---
published: false
layout: article
title: German OWASP Day 2012
abstract: Summary of the talks I heard
author_twitter: Fabian_ikono
author: Fabian Blechschmidt
categories: [articles]
tags: [owasp, owasp2012]
---

Ich war gestern auf dem German OWASP Day 2012. Die [OWASP](http://www.owasp.org) ist das ["Open Web Application Security Project"](http://www.owasp.org). Eine offene, kostenlose Organisation, die

# Keynote: Volkmar Lotz (SAP)

## Part 1: Build Knowledge

Auch mit Frameworks kann man Sicherheit nicht ohne den Entwickler garantieren -> Entwickler sind die Basis alles Sicherheit!

Warum jetzt?
Entwicklung der technologie brauch mehr sicherheit: mobile, cloud, business ecosystems.
Systeme werden komplexer und heterogener -> Outsourcing (Partner schreiben Software, nicht alles inhouse!)

Sicherheitskonferenzen berichten über SAP und SAP-Software. SAP rückt in den Focus von hackern.

awarness and responibility by every developer is important!

Target Audience: all, Entwkcleru und Architekten 3 Tage, alle anderen (Manager, product owner, technical writer, tester, quality manager, ...) 1 tag

Nicht nur schwachstellen vermeiden, sondern auch die reaktion und der umgang mit gefunden bugs wird gelehrt.

1,5 Tage secure programming: buffer overflow, etc.

Übungen, demonstrationen

Identity and Access management 1 tag

> Macht' s nicht selber, benutzt was da ist und benutzt es richtig!

Bookshop (Lab):
> Von XSS bis Code Injection funktioniert da alles.

###Lessons learned
#### "One size fits all" does not work

Verschiedene Formen von Training, Übungen, LAbore, Ausprobieren

Trennen zwischen Programmiersprachen!

Trennen zwischen Frameworks, damit der Entwickler weiß, was er in der täglichen arbeit beachten muss

Deal with contradicting feedback (nicht gleich beim ersten schlechten feedback inhalte oder art des trainings ändern)

#### Trainer role is critical

> Training steht und fällt mit dem engagement des TRainiers

Trainer müssen sich austauschen

#### Provide interactive content and different media

Videos, Bilder, Übungen, Demos, ...

Secure Coding: geschätzt 2/3 ist diskussion und coding

#### Run pilots (more than one!)

Because of the contradicting feedback

#### Cultural specifics need to be considered

#### Put business units in charge

Trainer mitnehmen, mit entwicklern reden, was sie wollen - nicht von außen aufdrücken!

## Part 2: Retain Knowledge

### Weiterführen in einzelnen modulen

* frontend security (HTML 5)
* databse security
* mobile security
* threat modelling
* ...

Integration in die allgemeinen trainnigs einbetten, z.B. HTML5 in das training für webentwickler

> Keep Motivation High and Costs Low

Virtual, Interactive, self-controlled, entertaining, rewarding

-> Gamification (not Serious Gaming)

> 1st Your need, your choice

Lernen wie man will, aber alles muss gelernt werden

> 2nd Raise the exitement

anschließend zusätzliche Möglichkeiten, Hack Me, Penetration Test Challenge, etc.

> 3rd your progress is the KEY

Profilseite: Awards, Achievments, Punkte sammeln, historie, ...

Lessons Learned
Gamificatin funktioniert sehr gut
-> über alle Kulturen hinweg

Nicht jeder mag es, nicht jeder möchte sein profil öffentlich, jeder hat die wahl

Enge Absprache mit den Betriebsräten weltweit umgesetzt

#  XSS von 1999 bis 2013 - Die Doctrine Classique der Websicherheit (Mario Heiderich)

Ecommerce: Pizza hut online shop

Brendan Eich erfindet SOP (Same Origin Policy), LiveScript (JavaScript) und damit auch XSS.

Browserkriege kommen 1999
HTML4 + DOM -> JS kann DOM manipulieren

Security nightmare, weil Browser Features brauchten.

2001 500 Mio. Internetnutzer

HTML stagniert

AJAX und Web 2.0 (Facebook wird geboren)

Browser bauen eigene Features XML, WML, E4X, VBS, XDR, LiveConnect, Drag & Drop, Clipboard, WBXML, Behaviours, WD-XSL, CSS, Expressions, SSE, SVG, HTML+TIME, SMIL, SAMI, ASX, ActiveX, XDR

2005

1 Mrd Internet benutzer

hoch komplexe Webanwendungen: GMail

HTML 5 entsteht, WHATWG vs. W3C

Erste XSS Würmer (Sammy Wurm)

Wieder Browserkriege -> Feature die nicht rein gehören

2009
1,6 Mrd User

Über-Browser: Cloud, Mobile, Social Networks, Venture Capital

XSS ist Allgegenwertig!

> Wenn wir eine Million Hühner haben und eine Million Tastaturen und da einfach Körner reinstreuen, exploiten die auf irgendeiner Internetseite XSS.


# Lost in Translation: Missverständnisse zwischen Mensch/Mensch und Mensch/Maschine und deren Auswirkungen auf Web-Security (Sebastian Schinzel)

 > Das ist ein Awarness talk

wir brauchen demut vor der technik und die nötige offenheit um sichere anwendungen zu bauen

> Post-Penetrationstest-Phase oft frustrierend
> - Report fängt Staub
> - Gegenmaßnahmen nur, wenn Explot gezeigt wurde
> - Beratungsresistenz bei den Entwicklern

> PHP Quellcode ist missverständlich.

Hintertür im Linux Kernel

Zuweisung auf der rechten Seite





> "MEinen Stundenten würde ich abraten, mit PHP coden zu lernen"