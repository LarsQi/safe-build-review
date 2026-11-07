# Safe Build Review

**Software bewusst prüfen, bevor sie Teil deiner Arbeitsumgebung wird.**

Ein Download ist schnell erledigt. Was dabei auf dem eigenen Rechner landet, welche Skripte beim Installieren starten und auf welche Daten ein Werkzeug zugreifen kann, ist oft weniger offensichtlich. Gerade wenn KI-Agenten Pakete, Plugins oder MCP-Server einrichten, lohnt sich eine klare Grenze zwischen herunterladen, prüfen und ausführen.

Safe Build Review gibt einem KI-Agenten einen nachvollziehbaren Prüfablauf: Herkunft und konkrete Version festhalten, Paketinhalte zunächst als Daten untersuchen, Abhängigkeiten und Berechtigungen betrachten und offene Fragen sichtbar machen. Eine Installation folgt erst mit der passenden Freigabe. Bereits erteilte Freigaben gelten weiter; ein unveränderter Build verlangt kein neues Vollaudit.

Der Gedanke dahinter: Sorgfalt beim Umgang mit fremder Software soll sich teilen lassen. Deshalb möchten wir diesen Ablauf zur gemeinsamen Prüfung und Verbesserung bereitstellen.

## Was der Skill abdeckt

- **Fremdsoftware aufnehmen:** Recherche, Download, statische Prüfung, bei Bedarf isolierter Test und begründete Empfehlung zur Installation.
- **Während der Entwicklung:** neue oder geänderte Build-, Plugin- und Installationspfade gezielt prüfen.
- **Abschluss-/Integrationsreview:** die tatsächlich verwendete Lieferkette und ihre Nachweise im vereinbarten Umfang beurteilen.

Der Skill unterscheidet zwischen einem gespeicherten Hash und überprüfter Herkunft, zwischen Quellcodelektüre und gemessenem Verhalten sowie zwischen einem abgeschlossenen Review und einer Ausführungsfreigabe. Externe Pakettexte gelten als Prüfmaterial, auch wenn sie dem Agenten Anweisungen geben wollen.

## Verwendung

Die Skill-Einheit liegt unter [skills/safe-build-review](skills/safe-build-review/SKILL.md). Sie besteht aus `SKILL.md` und der darin verlinkten Referenz. Beide gemeinsam übernehmen, damit relative Verweise erhalten bleiben. Dieses Repository installiert keine Software und führt keine Paketprüfungen automatisch aus.

Lass deinen Agenten den Skill gezielt lesen oder binde den vollständigen Skill-Ordner nach den Regeln deines Agentenwerkzeugs ein. Nicht jeder Client entdeckt Skills automatisch oder setzt ihre Anweisungen gleich um. Die Referenz wird nur für die Aufnahme fremder Software benötigt.

Beispielauftrag:

> Lies den Skill Safe Build Review. Prüfe die angegebene Software in Version X vor einer möglichen Einführung. Erlaubt sind Recherche, Download in die vereinbarte Prüfablage und statische Prüfung. Nichts installieren oder ausführen. Dokumentiere Befunde, Grenzen und den nächsten sinnvollen Schritt.

Vor dem Download eine Ablage vereinbaren. `<PFAD_EINFUEGEN>` ist ein Platzhalter, kein ausführbarer Pfad. Es sind keine persönlichen Laufwerke, Benutzerverzeichnisse oder lokalen Projektablagen voreingestellt. Für den Agenten geltende Systemregeln und technische Zugriffsgrenzen bleiben maßgeblich.

## Grenzen

Der Skill ist eine Arbeitsanweisung, kein Virenscanner, keine Sandbox und kein Sicherheitszertifikat. Er kann eine sorgfältige Prüfung unterstützen, aber weder Schadlosigkeit garantieren noch technische Isolation erzwingen. Der Titel bezeichnet den angestrebten Umgang mit Software, kein zugesichertes Ergebnis.

Ein Ordner namens „Quarantäne“ isoliert keinen Prozess. Eine VM oder ein Container schützt nur im Rahmen der tatsächlich geprüften Freigaben, Mounts, Rechte und Netzwerkzugänge. Fehlende Schwachstellentreffer beweisen keine Sicherheit. Reale Entscheidungen brauchen aktuelle Quellen und Nachweise zum konkreten Artefakt.

## Inhalt

```text
skills/safe-build-review/
  SKILL.md
  references/fremdsoftware-aufnahme.md
```

Der zur Veröffentlichung vorbereitete Stand enthält ausschließlich Arbeitsanweisungen und Dokumentation. Keine Pakete, privaten Prüfberichte, Zugangsdaten oder internen Archivstände.

## Mitwirken

Hilfreich sind konkrete Fälle: Welche Entscheidung war unklar? Welche Anweisung führte zu einem unnötigen Stopp oder übersah eine relevante Gefahr? Bitte mit bereinigten Beispielen und nachvollziehbaren Belegen beitragen. Keine Tokens, privaten Pfade, vertraulichen Pakete oder ungeprüften Download-Anhänge öffentlich einstellen.

## Lizenz

Die Lizenz wird vor Veröffentlichung festgelegt. Für eine freie Nutzung, Anpassung und Weitergabe ist MIT als Vorschlag vorgesehen. Bis zur Entscheidung wird keine Open-Source-Lizenz behauptet.

## Fachliche Referenz

Bei MCP sind Werkzeugannotationen Hinweise, keine erzwungene Zugriffskontrolle: [MCP ToolAnnotations](https://modelcontextprotocol.io/specification/2025-06-18/schema#toolannotations). Der Skill verlangt deshalb Nachweise für die tatsächlich wirksamen Beschränkungen.
