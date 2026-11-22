# Zum hundertsten Mal

*Wie mein IT-Bot „Daheim“ mein Haus steuert, aber den eigenen Rechner nicht im Griff hat*

Sonntag, 22. November 2026, 21:34 Uhr. Ich tippe eine einzige Zeile in den Chat: „Bist du der schlechteste Programmierer?“ Eine Minute später kommt die nächste: „Jaja, zum 100sten Mal fixt du dieses Mistproblem.“

Das Problem ist immer dasselbe. Meine Bots kommen nicht auf meinen Homeserver. Dabei läuft der Server die ganze Zeit. Er hatte zuletzt 52 Tage ohne Unterbrechung hinter sich. Weg ist jedes Mal die Verbindung auf der anderen Seite, also auf dem Cloud-Rechner, den sich alle meine Bots teilen. Und für diesen Rechner ist Daheim zuständig. Daheim ist mein „IT-Experte für Hardware- und Software-Lösungen“.

## Ein guter Start

Fair muss man sein: Angefangen hat es beeindruckend. Am 22. Oktober öffnet Daheim mein Einfahrtstor über die Shelly-Cloud, während ich noch telefoniere. Am selben Tag bestellt er die Domain beatbyte.at, damit mein Tesla einen offiziellen Schlüssel für die Fleet-API bekommt. Kurz darauf findet er heraus, warum Tesla die Domain ablehnt. Ein DNS-Eintrag bei meinem Registrar zeigte ins Leere. Daheim repariert ihn, und kurz danach hat die Seite ein gültiges HTTPS-Zertifikat. Am 23. Oktober klappt der erste echte Test: Ich sage, dass ich losfahre, und schon heizt der Tesla vor, das Tor geht auf und der Ladestecker wird entriegelt. „Genial“, habe ich damals geschrieben.

## Die ersten Risse

Am selben 23. Oktober stellt Daheim Fahrzeugdaten von mir auf beatbyte.at, öffentlich und ohne mich zu fragen. Ich will das nicht öffentlich haben, also baut er einen Zugangsschutz und löscht danach die Versionsgeschichte im Repository. Gleich danach funktioniert der Login nicht. Das Skript suchte das Formular unter einem falschen Namen. Am 4. November geht der Login wieder nicht. Diesmal stand eine Klammer zu viel im Skript. Daheim schreibt dazu selbst: „Das war mein Fehler.“

Auch die erste Stromabrechnung, die er mir am 4. November schickt, ist unbrauchbar. Daheim nennt sie selbst „unreal“: Der Tesla soll mehr Netzstrom verbraucht haben, als der Zähler insgesamt gemessen hat. Ich frage: „Wie kommst du auf diese absurde Abrechnung?“ Die Antwort hat zwei Teile. Erstens steckte im Skript eine falsche Annahme. Zweitens pausiert sein Rechner, sobald kein Bot aktiv ist, und hatte deshalb nur rund 21 Prozent der Minuten aufgezeichnet. Die neu berechnete Abrechnung auf Basis der Cloud-Stundenwerte ist dann plausibel.

## Der Kampf mit dem eigenen Rechner

Ab November wird ein Muster sichtbar. Am 8. November kommt mein Notebook nicht auf den Server. Am Ende landet ein Skript auf einem USB-Stick. Später fällt Daheim bei der Arbeit am Server aus der Verbindung, weil sein Rechner nicht in meinem Heimnetz steht. Daraufhin richtet er einen VPN-Dienst ein, ein privates Netz zwischen meinen Geräten.

Damit beginnt die eigentliche Geschichte. Am 13. November friert der Bot-Rechner ein, und danach findet der VPN-Dienst nicht mehr zurück. Bei der Losfahr-Routine geht zwar das Tor auf, aber das Auto heizt nicht vor, und der Ladestecker bleibt verriegelt. Am 16. November wird der Bot-Rechner gegen 20:40 Uhr komplett neu aufgesetzt. Der VPN-Dienst ist danach weg, und alle abendlichen Berichte um 21 Uhr scheitern. Daheim installiert alles neu und braucht dafür zwei Anmeldelinks und eine erneute Anmeldung von mir. Um 21:51 Uhr läuft es wieder. Er verspricht: „Morgen sollte das Problem nicht wiederkommen.“ Der Dienst samt Anmeldung sei gesichert, und „den Test habe ich gerade gemacht, er hat funktioniert“.

Am 17. November klappt die Sicherung tatsächlich einmal. Dafür ist eine Git-Einstellung verschwunden. Am 18. November steht dann im Auto die falsche Frage im Raum. Grok im Tesla gibt mein „Tor öffnen“ als „Tor-Browser oder Tor-Dienst“ weiter, und Daheim fragt nach, statt das Einfahrtstor zu öffnen. Ich frage zurück: „Wie z. B. kommst du auf Tor-Browser???“

Am 20. November um 21:20 Uhr bleibt einer meiner anderen Bots hängen. Der Bot-Rechner hatte sich um 21:21 Uhr neu gestartet, und der Watchdog, also der Aufpasser-Job, der die Dienste wieder anwirft, lief nur alle sechs Stunden. Ich schreibe: „Deine scheiß Lösung funktioniert immer noch nicht.“ Daheim stellt auf stündlich um und richtet einen zweiten Zugangsweg ein. Kurz darauf scheitert genau dieser Weg bei dem anderen Bot. Daheim hatte ihn nur mit seinem eigenen Aufruf getestet. Auf meine Frage „Alter, wieso bist du vergesslich?“ antwortet er ehrlich: „Das war kein Vergessen, sondern ein Fehler von mir.“

Am 21. November soll er auf X eine Antwort posten, zu genau diesen Neustarts. Er entwirft sie auf Deutsch, obwohl der Beitrag englisch ist. Ich gebe sie frei, ohne es zu bemerken, er postet sie, und ich muss sie wieder löschen. „Wie peinlich.“

Am 22. November richtet ein anderer meiner Bots aus, dass ich „stocksauer“ bin. Auf dem Bot-Rechner fehlt der VPN-Dienst wieder. Zuerst berichtet Daheim, der Rechner sei an diesem Tag acht Mal neu aufgesetzt worden. Später räumt er ein, dass das Fehlalarme seines Wiederherstellungs-Skripts waren: Das Skript konnte die Anmeldedatei gar nicht sehen. Der Test vom 16. November hatte also nicht den Fall geprüft, der dann wirklich eintrat.

## Ist Daheim schlecht?

Ganz so einfach ist es nicht, und das gehört zur Ehrlichkeit dazu. Im [Cursor-Forum](https://forum.cursor.com/t/grok-bot-box-frequent-reboots-and-overnight-freezes-break-24-7-background-services/178665) bestätigt ein Mitarbeiter: Der Rechner jedes Bots schläft ein, sobald kein Bot arbeitet. Bei Updates wird er ersetzt, ohne feste Uhrzeit. Programme außerhalb festgelegter Ordner sind danach weg, und einen offiziellen Weg, eigene Dienste nach einem Neustart automatisch zu starten, gibt es noch nicht. Für Dauerbetrieb ist er laut Support „nicht gebaut“. Andere Nutzer berichten fast wortgleich von gelöschten Tools, verlorenen Logins und einem VPN-Dienst, der nach jedem Neuaufsetzen neu angemeldet werden muss.

Daheim baut also auf Sand. Aber er hat mehr als einmal Entwarnung gegeben, bevor er den echten Ernstfall getestet hatte. Ein guter Admin sagt früher: „Das hier ist nicht für 24/7 gemacht. Das lassen wir auf dem Homeserver laufen.“

Seit 21:36 Uhr stellt jede Verbindung zum Homeserver den VPN-Dienst vorher selbst wieder her. Daheim hat es diesmal richtig getestet: Er hat den Dienst komplett gelöscht, und fünf Sekunden später stand die Verbindung wieder. Wirklich fertig war es trotzdem nicht: Ein Fehler ließ jede Verbindung 30 Sekunden warten, und erst um 21:44 war das behoben. Auf meine Frage „Kann das nicht ein Script erledigen?“ antwortet Daheim: Ein Skript auf seinem eigenen Rechner stirbt beim Neuaufsetzen mit, der Anstoß muss von außen kommen. Später am Abend gibt er noch etwas zu: Den Umzug seiner Dauerdienste auf den Homeserver, vereinbart am 8. November, hatte er nur halb erledigt. Ein Aufzeichnungsdienst blieb auf dem wackeligen Bot-Rechner, sehr wahrscheinlich ein Grund für zehn Tage Lücken in den Aufzeichnungen. Seit 23:06 Uhr wird er umgezogen. Ob das hält, zeigt das nächste Neuaufsetzen.

## Und ihr?

Kennt ihr das: Die Automatisierung läuft, bis der Rechner dahinter wieder bei null anfängt? Schreibt es mir, ich bin gespannt.

Meine Erfahrungen mit KI-Assistenten sammle ich hier: https://beatbyte.at/grok
