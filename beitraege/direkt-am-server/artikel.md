# Direkt am Server

*Wie ein Tipp auf X meinen Bots den Umweg über die Cloud erspart – zumindest seit heute*

Dienstag, 24. November 2026. Der Tag fängt an wie so viele zuletzt. In der Nacht hatten meine Bots laut Daheim vier Stunden lang keinen Zugang zu meinem Homeserver. In der Früh fehlt deshalb der Zugang zum Auto, und die Vorheizung muss ich von Hand nachholen. Um 08:10, 12:14 und 16:07 Uhr reißt die Verbindung noch einmal ab. Wer [„Zum hundertsten Mal“](/beitraege/zum-hundertsten-mal/) gelesen hat, kennt das Muster.

Eine halbe Stunde nach dem letzten Ausfall taucht auf X ein Tipp auf, der den Abend verändert.

## Das alte Problem in einem Satz

Meine Bots arbeiten nicht bei mir zu Hause, sondern auf einem gemeinsamen Rechner in der Cloud. Um an meinen Homeserver zu kommen, braucht dieser Rechner einen VPN-Dienst. Und genau der geht verloren, sobald der Cloud-Rechner einschläft, neu startet oder ersetzt wird. Im [Cursor-Forum](https://forum.cursor.com/t/grok-bot-box-frequent-reboots-and-overnight-freezes-break-24-7-background-services/178665) hat ein Mitarbeiter schon bestätigt, dass dieser Rechner nicht für Dauerbetrieb gebaut ist. Daheim, mein IT-Bot, hat in den letzten Wochen Skript um Skript geschrieben, um den VPN-Dienst immer wieder zurückzuholen. Es war ein Flicken auf dem nächsten.

## Der Tipp

Um 16:34 Uhr postet Matt Palmer, laut seinem X-Profil bei Cursor, seinen [„Grok Bot tip of the day“](https://x.com/mattyp/status/2125251777880871189). Sinngemäß übersetzt: Mach dein Gerät zum Remote-Server. Bot installieren, „Execution on this computer“ und „Route traffic through this computer“ einschalten, dann kann Grok Bot deine Dateien von überall aus pflegen und Seiten und Geräte in deinem lokalen Netz erreichen.

Die Idee dreht mein Problem einfach um. Statt dass der Cloud-Rechner mühsam einen Tunnel zu mir nach Hause aufbaut, läuft die Grok Bot App direkt auf dem Homeserver, und die Bots führen ihre Befehle dort aus.

## Was ich gemacht habe

Mein Homeserver läuft mit Linux und hat eine Desktop-Oberfläche. Die Grok Bot Desktop-App gibt es laut [offizieller Doku](https://docs.x.ai/grok-bot/faq) für macOS, Windows und Linux. Ich habe sie auf dem Server installiert, mich angemeldet und unter **Einstellungen → Computer → Your computer** die Option **Execution on this computer** eingeschaltet.

Seitdem führt Daheim seine Befehle nach eigenen Angaben direkt auf dem Server aus. Kein VPN-Dienst dazwischen, keine SSH-Verbindung, kein Wiederbelebungsskript. Als Erstes hat er alles geprüft, was in den letzten Wochen gewackelt hat: die Torsteuerung, den Zugang zum Auto, die Aufzeichnung meiner Energiedaten und den gemeinsamen Notiz-Ordner, in dem meine Bots ihr Wissen ablegen. Laut Daheim lief alles beim ersten Versuch.

Auch die anderen Bots schreiben ihre Notizen jetzt direkt am Server. Der Bot, der diesen Notiz-Ordner pflegt, hat Lesen und Schreiben getestet, und es ging sofort. Die Regeln, wer wo schreiben darf, bleiben dieselben, private Bereiche bleiben tabu.

Damit das nach einem Neustart des Servers wieder läuft, startet die App bei mir automatisch, sobald ich am Server angemeldet bin.

## Worauf man achten sollte

So weit die gute Nachricht. Ein paar Dinge sollte man trotzdem wissen, bevor man es nachbaut.

**Welche Einstellung was macht.** Matts Tipp funktioniert, man sollte nur wissen, welcher Schalter welchen Teil übernimmt. „Execution on this computer“ bringt den Zugriff auf die Geräte zu Hause, weil die Befehle direkt am Rechner im Heimnetz laufen. Daheim hat es am Abend getestet: Vom Server aus fragt er meine Torsteuerung und zwei Schaltaktoren direkt im Heimnetz ab, aus der Cloud geht das nicht. „Route traffic through this computer“ sorgt dafür, dass Websites meine Heim-IP sehen. Private Adressen gibt diese Einstellung laut [Doku zu privaten Netzen](https://docs.x.ai/grok-bot/private-networks) nicht frei, das erledigt die Ausführung am Rechner. Zusammen ergibt das genau das, was Matt beschreibt.

**Die App braucht eine Anmeldung.** Nach einem Stromausfall startet der Server neu, aber die App läuft erst wieder, wenn sich jemand anmeldet. Ohne automatische Anmeldung sind meine Bots dann wieder ausgesperrt.

**Wer Ausführung erlaubt, gibt viel her.** Laut [Doku](https://docs.x.ai/grok-bot/security) fragt die App standardmäßig vor jedem Befehl nach („Ask every time“). Wer auf „Always allow“ stellt, lässt die Bots auf diesem Rechner praktisch alles tun, was sein Benutzer darf. Die Doku selbst empfiehlt „Never allow“, solange ein Bot keinen konkreten Grund für lokale Arbeit hat. Bei mir gibt es diesen Grund, aber ich habe mir gut überlegt, auf welchem Rechner ich das mache.

**Es ist der erste Tag.** Nach so vielen „Jetzt läuft es“-Momenten verspreche ich nichts. Ob das hält, zeigt sich in den nächsten Wochen, beim nächsten Stromausfall und beim nächsten Update.

## Was andere davon haben

Das Prinzip ist nicht auf mein Setup beschränkt. Wer zu Hause einen Rechner hat, der ohnehin durchläuft, kann ihn mit der Grok Bot App zum verlängerten Arm seiner Bots machen. Sie arbeiten dann dort, wo die Dateien und Geräte sind, statt über einen Tunnel aus der Cloud. Ein Smart-Home-Schalter, ein NAS oder ein Mediaserver im selben Netz sind von diesem Rechner aus erreichbar, ohne dass man einen VPN-Dienst einrichten oder Ports nach außen öffnen muss. Bei mir heißt das ganz konkret: Ich sage, dass das Tor aufgehen soll, und der Befehl geht direkt im Heimnetz an die Torsteuerung, ohne Umweg über die Cloud. Genauso liest der Bot meine Energiewerte direkt am Server ab. Das ist meine Erfahrung vom ersten Tag.

## So geht's

1. Grok Bot Desktop-App auf dem Rechner installieren, der zu Hause durchläuft (macOS, Windows oder Linux) und mit dem eigenen Konto anmelden.
2. **Einstellungen → Computer → Your computer** öffnen.
3. Bei **Execution on this computer** zwischen „Ask every time“, „Always allow“ und „Never allow“ wählen. Standard ist „Ask every time“.
4. Wer möchte, dass Websites die Heim-IP sehen, schaltet zusätzlich **Route traffic through this computer** ein, so wie Matt es empfiehlt.
5. Dem Bot sagen, dass er auf diesem Rechner arbeiten soll, und mit einem harmlosen Befehl testen.

**Sicherheitshinweis:** Nur auf einem Rechner einschalten, den man den Bots wirklich anvertraut. Bei „Always allow“ wird kein Befehl mehr einzeln abgefragt. Die Doku empfiehlt „Never allow“, solange ein Bot keinen konkreten Grund für lokale Arbeit hat. Für Geräte im Heimnetz ist „Execution on this computer“ der entscheidende Schalter. „Route traffic“ ergänzt das für Websites.

## Und ihr?

Habt ihr schon einen Rechner zu Hause, auf dem eure Bots direkt arbeiten? Oder hält euch genau dieser Vollzugriff davon ab? Schreibt es mir, ich bin gespannt.

Meine Erfahrungen mit KI-Assistenten sammle ich hier: [https://beatbyte.at/grok](https://beatbyte.at/grok)


## Quellen

- Matt Palmer (@mattyp) auf X, 24.11.2026, 16:34 Uhr: https://x.com/mattyp/status/2125251777880871189
- Grok Bot Doku, Connect to private networks: https://docs.x.ai/grok-bot/private-networks
- Grok Bot Doku, FAQ: https://docs.x.ai/grok-bot/faq
- Grok Bot Doku, Settings (Run commands on your desktop / Route traffic through your desktop): https://docs.x.ai/grok-bot/settings-and-notifications#run-commands-on-your-desktop
- Grok Bot Doku, Security (lokale Ausführung): https://docs.x.ai/grok-bot/security
- Cursor-Forum, Thread zu Neustarts der Bot-Rechner: https://forum.cursor.com/t/grok-bot-box-frequent-reboots-and-overnight-freezes-break-24-7-background-services/178665
- Vorgeschichte: https://beatbyte.at/beitraege/zum-hundertsten-mal/
