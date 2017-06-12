# Einleitung

In diesem Repository findet man zwei Vorlagen für Abschlussprojekte. Die Vorlagen sind für
das Textsatzsytem Latex vorbereitet. Die Vorlagen und diese Anleitung ist für Anfänger gedacht, die bisher mit
Latex noch keine Berührung hatten. Profis mögen über die Warnungen im Output hinwegsehen. Es funktioniert.

Die Singleuser Vorlage ist für Einzelpersonen gedacht und zeigt prinizipiell die Verteilung der Inhalte auf mehrere Dokument.

Die Multiuser Vorlage ist etwas komplexer, da sie aufzeigt, wie man die Inhalte mehrerer Personen auf diverse Ordner verteilen kann.

Selbstverständlich sind beide Vorlagen nur als Grundgerüst gedacht. Anpassungen sind also in jedem Fall nötig.

## Wegweiser durch die Dateien

Datei  | Beschreibung
-------|--------------
`make_pdf.sh` | Kurzes Skript, um die PDF-Datei zu erstellen. Alle erstellten Dateien landen im Ordner `output`
`Dokumentation_main.tex` | Hauptdokument, in dem alle weiteren Dokumente einbunden werden.
`preinput.tex` | Formatierungssteuerung. Hier werden die Formatierungen definiert und eigene `commands`
`res`-Ordner | In diesem Ordner werden alle Bilder/Datei (resources), die benutzt werden. 

Alle weiteren Dokumente sind durch den Dateinamen selbsterklärend. 

## Eigene Kommandos

Es wurden einige neue Befehl in die Datei `preinput.tex` als Beispiele integriert. Die Logik ist relativ einfach.

```
\newcommand{\code}[1]{\texttt{#1}}
```

Das Code-Wort `\newcommand` startet die Definition eines neuen Befehls. In der ersten gescheiften ersten Klammer (`\code`) wird dann der neue Befehl, der später im Dokument verwendet werden soll definiert. Die Zahl in den eckigen Klammern (`[1]`) gibt an, wieviele Parameter an den Befehl übergeben werden sollen. Dies ist optional.

In der zweiten gescheiften Klammer werden dann die eigentlich auszuführenden Befehl angegeben (`\texttt{#1}`).
Mit `#1`, `#2` usw. werden die einzelnen Parameter angesprochen.

Der hier gezeigte Befehl ersetzt den Standard-Befehl `\texttt` durch `\code` und formatiert den übergebenen Text in Courier (Sourcecode-Schriftart).

**Im Latex-Dokument**

`\code{Dieser Text soll anders aussehen.}`

**Ergebnis im PDF-Dokument**

`Dieser Text soll anders aussehen.`

Etwas komplexer kann dies so aussehen:

```
\newcommand{\picinsert}[3] {
% Beispiel: 
% \picinsert{Breite in Prozent der Seitenbreite}{Dateiname (ohne png)}{Abbildungbeschriftung}
  \begin{figure}[h]
    \centering
    \includegraphics[width=#1\textwidth]{./res/#2.png}
    % Bildtitel zur Referenzierung
    \caption{#3\label{fig:#2}}
  \end{figure}
}
```

Es werden drei Parameter übergeben:
- Breite in Prozent
- Dateiname (ohne png)
- Abbildungsbeschriftung

Der Dateiname wird später noch als Label verwendet, um das Bild zu referenzieren. Dabei wird davon ausgegangen, dass die Bilddatei die Endung `png` hat und im Ordner `res` abgelegt wurde.

**Beispiel**

`\picinsert{0.5}{hyperbel_kreis_ellipse}{Hyperbel mit Kreis}`
