---
layout: page
tags:
  - Programmieren
title: "Debugging ist toll"
---

<link rel="stylesheet" href="{{ "/assets/css/style.css" | absolute_url }}">

Beim Programmieren ist das Debuggen von Funktionen enorm wichtig. Kürzlich ist mir in meinem `siegmund_gb` Projekt
aufgefallen, dass ich Debuggen liebe.

Ich hatte das Problem, dass bei einer bestimmten Stelle auf der Map random ein Gegner direkt vor dem Spieler gespawnt
ist. Eigentlich sollte das natürlich nicht auftreten. Da ich erst das Problem beim Placement der Sprites vermutete,
habe ich *vergebens* danach gesucht. Ich probierte für locker ne Stunde rum, bis ich die grandiose Idee bekam, einfach
mal Stück für Stück Funktionen und States aus dem Code für den Spieler entfernte. Plötzlich war das Problem mit dem
merkwürdigen Gegner Spawnen weg :)

So konnte ich also rausfinden, dass in einem State, in dem der Attack Sprite vom Spieler abgefragt wurde, bei
Nicht-Existenz des Attack Sprites einfach der nächstbeste wie der Attack Sprite vor den Spieler gepackt wird :)