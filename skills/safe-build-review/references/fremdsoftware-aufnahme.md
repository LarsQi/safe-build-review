# Fremdsoftware aufnehmen

Lies diese Referenz bei einer beauftragten Sicherheitsprüfung fremder Software
oder vor ihrer Einführung. Sie ergänzt safe-build-review; sie verlangt weder
bei jedem Build ein Audit noch eine VM für jede harmlose Dateiänderung.

## Auftrag und Prüfablage

Bestimme Ziel, konkrete Software/Version, Bezugsquelle, Zielsystem und geplanten
Betriebsumfang. Unterscheide Dokumentationsrecherche, Download, statische
Prüfung, isolierte Ausführung und Zielinstallation. Führe nur die beauftragten
Phasen aus; bestehende Freigaben gelten innerhalb ihres Umfangs weiter.

Wähle eine für diesen Auftrag bestätigte Prüfablage:
`<PFAD_EINFUEGEN>/<SOFTWARE>/<VERSION>/`.
Diesen Platzhalter vor Benutzung durch einen konkreten Pfad ersetzen;
solange keine Ablage vereinbart ist, keine Downloads ausführen. Eine ausdrücklich benannte andere Ablage oder
ein führender Projekt-Prüfstand hat Vorrang. Schreibrechte für den gewählten
Ort prüfen; die Pfadvereinbarung erweitert keine technischen Rechte. Frage
nur bei einer relevanten offenen Ablageentscheidung. Lege Software und Version
getrennt ab. Ein Downloadauftrag
ist keine Installationsfreigabe und erlaubt keine Ablage in fremden persönlichen
Bereichen. Schreibsperren konkret melden, nicht still in einen unpassenden
Projektordner ausweichen. Vorhandene Dateien erhalten, neue Stände getrennt
ablegen und Schreibvorgänge durch erneutes Lesen prüfen.

Erstelle in der Prüfablage eine kurze README zum vereinbarten Vorgehen, Umfang,
aktuellen Prüfstatus und Berichtspfad. Halte im vorhandenen Prüfbericht die
Befunde und Entscheidungen nach; eröffne keine konkurrierenden Aufgabenlisten.
Ein Ordner namens Quarantäne ist keine Isolation.

## Download und statische Erstprüfung

- Exakte Paketversion, ursprüngliche Bezugs-URL, Downloadzeitpunkt und
  SHA-256 festhalten. Originalpakete unverändert bewahren. Hashes mit der
  veröffentlichten Quelle vergleichen; Signaturen oder Attestationen bei
  Verfügbarkeit prüfen und angeben, ob nur eingesehen oder tatsächlich
  kryptographisch verifiziert. Ein Hash der heruntergeladenen Datei allein
  authentifiziert keinen Herausgeber. Bei einer Prüfsummenabweichung das
  betroffene Artefakt bis zur Klärung weder ausführen noch installieren.
  Sollwerte nicht ungeprüft ersetzen; sichere statische Prüfungen fortsetzen.
- Das tatsächlich vorgesehene Installationsartefakt untersuchen. README,
  main-Zweig, Release-Tag und veröffentlichtes Paket können auseinanderliegen.
  Sicherheitsrelevante Dateien bei Bedarf mit dem zugeordneten Commit
  vergleichen; Umfang und Grenzen des Vergleichs benennen.
- Archive zunächst als Daten lesen. Pfade, Links, Spezialdateien und Größen
  vor einem nötigen Entpacken kontrollieren; nicht außerhalb der Prüfablage
  schreiben und vorhandene Dateien nicht überschreiben. Keinen Paketcode
  importieren und keine fremden Build-, Installations- oder Hilfsskripte allein
  zur Inspektion ausführen. Auch dynamische Metadatenabfragen, Paketmanager,
  Source-Builds und erstmaliges Starten über npx/uvx können Code nachladen und
  ausführen; das gehört nicht zur rein statischen Prüfung.
- Einstiegspunkte, Installations-/Build-Hooks, native Bibliotheken und
  nachgeladene ausführbare Artefakte im betroffenen Umfang untersuchen.
  Syntax- oder interne Archivhashprüfung ist kein Verhaltenstest und kein
  Nachweis der Schadlosigkeit.

## Abhängigkeiten und Sicherheitsmeldungen

Erfasse direkte und für den geplanten Betrieb relevante transitive Versionen,
Extras, Plattformmarker und Buildabhängigkeiten. Trenne den tatsächlich
aufgelösten/installierten Stand von einem nur aus einem Upstream-Lock
abgeleiteten Kandidaten. Ein Paket-Pin fixiert keine offenen transitiven
Versionen; ein Repository-Lock gilt nicht automatisch für die Paketinstallation.

Prüfe Betriebssystem, Edition, Architektur, Interpreter, vorhandene Werkzeugpfade
und geeignete Binärpakete vor der Installationsplanung. Ein fehlendes Wheel ist
kein Schadsoftwarebeleg und erlaubt weder automatischen Source-Build noch
Compiler-, Interpreter- oder Paketmanagerinstallation. Behauptete
Nichtverfügbarkeit nur auf die tatsächlich geprüften Quellen/Versionen beziehen.

Gleiche relevante konkrete Versionen mit aktuellen Herausgebermeldungen und
geeigneten Schwachstellendatenbanken ab. Halte Zeitpunkt, IDs, betroffene und
reparierte Versionen fest. Unterscheide Versionsbetroffenheit und Erreichbarkeit
der problematischen Funktion im vorgesehenen Betrieb. Aliase nicht als
unabhängige Lücken zählen. Fehlende Treffer oder eine leere Datenbankantwort
beweisen keine Sicherheit. Bei Widersprüchen zwischen Advisory und Paketcode
beide Belege dokumentieren und die betroffene Funktion bis zur Klärung nicht
zur Nutzung empfehlen; keine Versionsentwarnung allein aus einem unvollständigen
Bereich ableiten. Eine Installation mit ausgeschlossener Problemfunktion nur
für einen konkret begrenzten Betrieb empfehlen, wenn die wirksame Beschränkung
nachgewiesen ist. Ohne diesen Nachweis keine solche Installationsempfehlung.
Keine pauschalen Updates als automatische Reparatur.

Im statischen Prüfschritt keine Scanner nachinstallieren und keinen fremden Code
starten. Pakete oder private Inhalte nicht ohne passenden Auftrag an externe
Dienste senden.
Öffentliche Paketnamen/Versionen dürfen zur beauftragten Schwachstellenrecherche
abgefragt werden; private Abhängigkeitslisten sind keine automatisch öffentlichen
Daten. Zugriff auf Quellen und technische Grenzen offen benennen.

## Rechte, Daten und Netzwerk

Erfasse Benutzerrechte, erreichbare Dateien/Secrets, Programmstarts, Telemetrie,
Fehlerberichte, Autostart, Dienste, Ports und konfigurierte Netzwerkziele.
Unterscheide gelesene Konfiguration von gemessenem Laufzeitverhalten.
Beschränkungen des Clients oder der Codex-Shell gelten nicht nachweislos für
separat laufende MCP-Server, Plugins oder deren Kindprozesse.

Bei Werkzeugservern die kleinste zweckmäßige positive Werkzeugliste planen.
Nicht allein gefährlich klingende Werkzeuge ausschließen: App-Start mit
Argumenten, Dateifunktionen und GUI-Eingaben können dieselben Auswirkungen wie
eine Shell haben. UI-Hinweise wie readOnlyHint sind keine Durchsetzung.
Zwischenablage- und Dateinebenwirkungen der erlaubten Funktionen berücksichtigen.

Prüfe bei lokaler Integration, ob stdio den Zweck ohne Netzwerklistener erfüllt.
Ein lokaler Transport verhindert keine ausgehende Telemetrie. Abschalten laut
Konfiguration nicht als nachgewiesene Netzwerkfreiheit ausgeben. Bildschirm-
und UI-Daten, die an den Modellclient gehen, bleiben nicht automatisch lokal,
auch wenn der Werkzeugserver selbst keine Screenshots an seinen Hersteller
sendet. Sichtbare Geheimnisse und angemeldete Apps im nötigen Umfang begrenzen.

## Entscheidung vor Ausführung und isolierter Test

Bei konkreter ungeklärter Gefahr nur den betroffenen Ausführungsschritt
zurückhalten. Sinnvolle statische Prüfungen fortsetzen. Für risikoreiche oder
noch nicht ausreichend einschätzbare Ausführung eine geeignete isolierte
Testumgebung vorbereiten; aus einem Reviewauftrag keine Einrichtung ableiten.
Wenn sie nötig, aber nicht verfügbar ist, die Grenze und den nächsten benötigten
Schritt nennen. Keine ungeprüfte Ausführung auf dem Hauptsystem als Ersatz.

Vorhandene VM/Sandbox und ihre Eignung für Edition, Architektur und Anwendung
prüfen. Mounts, gemeinsam genutzte Ordner, Zwischenablage, Geräte, Benutzerrechte,
Zugangsdaten und Netzwerk ausdrücklich kontrollieren. Nur benötigte Ressourcen
durchreichen; keine produktiven Daten oder Schlüssel als Testmaterial. Ein
Server im Gast bedient dessen Desktop; eine Freigabe des Hostdesktops kann den
gewünschten Isolationsschutz aufheben. Kein pauschaler Container-Nachweis.

Liegt die konkrete Ausführungs-/Installationsfreigabe bereits vor, nutze sie;
frage nur nach noch nicht autorisierten Änderungen. Bei nötiger Entscheidung
einen konkreten Plan mit betroffenen Pfaden, Versionen, Rechten und Auswirkungen
vorlegen. Keine erneute Bestätigung jedes bereits genehmigten Schritts verlangen.

Teste nur die vereinbarten Funktionen. Bei Werkzeugfiltern tatsächliches
Werkzeugangebot und Ablehnung ausgeschlossener direkter Aufrufe prüfen;
Fehlkonfiguration oder inkompatible Abhängigkeiten dürfen keinen unbemerkten
Vollzugriff ergeben. Dazu relevante Nebenwirkungen, Daten-/Netzwerkverhalten
sowie Übernahme und Abbruch prüfen. Ergebnisse und Testgrenzen festhalten;
bloße Quellcodelektüre oder ein erfolgreicher Start ersetzt diese Nachweise nicht.

## Bericht, Zielinstallation und Abschluss

Weise für jede relevante Phase den Stand, das Ergebnis und die Grenzen aus:
Download, statische Prüfung, isolierter Test und Empfehlung zur Zielinstallation.
Dies ist keine zwingende lineare Statusfolge. „Statisch geprüft“ kann einen
negativen Befund bedeuten; nicht ausgeführte Phasen und Gründe kenntlich machen.
„Prüfung abgeschlossen“ ist keine pauschale Aussage „sicher“ und keine
Installationsfreigabe durch die auftraggebende Person.

Der Bericht enthält, soweit für den Auftrag relevant:

- Gegenstand/Version, Herkunft, Hashes, Datum und verwendete Nachweise.
- Geprüfte Phasen, Befunde mit Auswirkungen, Ungewissheiten und nicht geprüfte
  Teile; Beobachtung, Vermutung und Empfehlung getrennt.
- Entscheidung zum nächsten Schritt und die hierfür noch nötigen Nachweise.
- Vor einer empfohlenen Zielinstallation: konkrete Paket-/Abhängigkeitsversionen,
  Zielpfade, erlaubte Funktionen, Telemetrie/Netzwerk/Rechte, Änderungen an
  bestehender Konfiguration, Funktionstest und Weg zur Rücknahme/Deinstallation.
  Vor Änderungen nötige vorhandene Zustände sichern; mögliche Datenverluste
  oder verbleibende Zustände bei einer Rücknahme benennen.

Eine Übernahme an den vereinbarten Zielort erfolgt erst nach den für diesen
Umfang nötigen Nachweisen und bei vorhandener konkreter Freigabe; sie ist keine
automatische Folge eines positiven Berichts. Originaldownload und Prüfnachweise
bleiben nachvollziehbar erhalten. Wenn der Stand nicht empfohlen wird, keine
scheinbar fertige Installationsanleitung oder versteckte Einrichtung erzeugen.

Nach relevanten Versions-, Paket-, Konfigurations- oder Rechteänderungen die
betroffenen Nachweise erneuern. Nicht jeden unveränderten Build neu auditieren.
