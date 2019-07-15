# starter
Der WDR-Data Starter ermöglicht es JournalistInnen, unsere Design-Patterns und die Komponentenbibliothek für datengesteuerte Journalismusprojekte zu nutzen.

Ziele:
- Einen abgenommenen Rahmen haben, in dem Datenprojekte schneller stattfinden können
- Neue Visualisierungsformen mobile first und accessible erproben
- Entwicklungen wiederverwendbar machen (Als Datengeschichte auf data.wdr.de und als Grafik-iFrame im CMS)

## Für JournalistInnen

### Wie nehme ich ein Datenprojekt ab?
- Ersteller*in schickt Link zu: 
    - Preview bei Netlify - z.B.:  `http://data-wdr.netlify.com/oper-in-nrw`
    - Markdown-File dazu in Github - z.B.: `https://github.com/wdr-data/starter/pages/index.md`

- Zum Bearbeiten:
    - Auf Stift-Icon oben rechts: Edit this File
    - Änderungen vornehmen / Preview ansehen
    - Zum Abschluss unten unter 'Commit changes' die Änderung dokumentieren
    - Auf 'commit changes' klicken

- Commit löst aus: 
    - Änderungen werden dokumentiert (und sind rückgängig zu machen)
    - Änderungen werden im Slack gepostet
    - Automatische Veröffentlichung der Änderung bei Netlify 

### Wie lege ich ein neues Datenprojekt an?

:globe_with_meridians: https://github.com/wdr-data/starter/
- Für den Zugang ist ein Github Account nötig 

Schritte:
- Für eine neue Story 
1. Ein neues, leeres Repo unter data.wdr.de anlegen
- Projekte können wahlweise von Anfang an 'öffentlich' sein oder erst später veröffentlicht werden 
2. `git clone <new repository>.git` des neuen Repos auf dem eigenen Rechner
3. In das neue Verzeichnis wechseln: `cd <new repository>`
4. Die Referenz zum starter Verzeichnis hinzufügen `git remote add upstream git@github.com:wdr-data/starter.git`
5. Alle Inhalte aus dem Starter ins neue Verzeichnis ziehen: `git pull upstream master`
6. Alle Inhalte zum neuen Verzeichnis pushen: `git push origin master`
 
### Meine Story bearbeiten 
Unter /pages die index.md mit eigenen Inhalten überschreiben:

#### Metadatenfelder

```title: "Opern-Spielpläne in NRW: tot und männlich"
description: WDR 3 Datenanalyse der Opern-Spielzeit 2018/2019
author: Niklas Rudolph, Patricia Ennenbach
pub_date: "2019-07-15"
heroImage: "richard-wagner-und-freunde.jpg"
heroAlt: "Richard Wagner und seine Freunde"
heroCredit: "Richard Wagner und seine Freunde"
sharingImageFacebook: "richard-wagner-und-freunde_facebook.jpg"
sharingImageTwitter: "richard-wagner-und-freunde_twitter.jpg"
``` 

- `title` - **Überschrift**
- `description` - **Beschreibung**
    - für das Google-Suchergebnis
    - ca. 160 Zeichen
- `author` - **Liste der AutorInnen**
    - als Liste (Spiegelstriche, eingerückt)
- `pub_date` - **Veröffentlichungsdatum**
    - z.B. `2019-06-27`
- `heroImage` - **Titelbild**
- `heroAlt` - **Alt-Attribut für Titelbild**
- `heroCredit` - **Credit für Titelbild**
- sharingImageFacebook: - **Bild für Faceook open graph**
- sharingImageTwitter: - **Bild für Twitter card** 

### Texte in Markdown

Die eigentliche Geschichte wird in **Markdown** geschrieben, das ist eine vereinfachte Auszeichnungssprache fürs Web.

:bulb: [Markdown Cheat Sheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)


#### Bilder 
- Unter /static werden die Bilddateien für das Projekt abgelegt (HeroImage, weitere Bilder)

heroImage: 1920x1080 Sophora / Full HD
Twitter: 2:1 - mindestens 300 x 157
Facebook: 1200 x 630 

Weitere Bilder: 
- 1920x1080 Sophora / Full HD

Bild einfügen: 
``` 
<figure role="group">
<img src="berthold-schneider-credit-jens-grossmann.jpg" alt="Der Wuppertaler Opernintendant Berthold Schneider, fotografiert von Jens Grossmann" />
<figcaption style="text-align: end;">Berthold Schneider</figcaption>
</figure>
```

### Weitere Komponenten in Markdown einbinden

Es können Komponenten aus der Bibliothek unter wdr-data.netlify.com/components eingebunden werden. Dazu wird die Markdown-Erweiterung [MDX](https://mdxjs.com/) verwendet. 

Um Komponeneten nutzen zu können, müssen sie in der index.md importiert werden. Laut Konvention oben unter den Metadaten. 

``` 
import DataWrapper from '../components/datawrapper/datawrapper.jsx'
import Quote from '../components/quote/quote.jsx'
import Accordion from '../components/accordion/accordion.jsx'
import Webtrekk from '../components/webtrekk/webtrekk.jsx'
import Sharing from '../components/sharing/sharing.jsx'
``` 

### Datawrapper

#### Beim Grafiken bauen beachten
- Design: Datawrapper
- Titel ausblenden, Subtitle weglassen (passiert im Markdown des Projekts)
- Datenquelle, Link zur Datenquelle und Verfasserzeile ausfüllen
- Social Media Sharing aus 
- Farbskala anpassen: Für unterschiedliche Graphentypen stehen Möglichkeiten der farblichen Modifizierbarkeit zur Verfügung. Beispielhaft folgen zwei Optionen.
 
1. Farben > importieren `#dadfdf,#b6cad1,#5bb1c0,#365886,#1d2124`
![](https://i.imgur.com/VhffYRF.png)

2. Farbwerte ersetzen:
#1D2124 (WDR Dunkelblau)
#00345E (WDR Blau)
#007381 (WDR Petrol)
#B37500 (WDR Honiggelb)

Fertige Grafik veröffentlichen und Datawrapper-Pfad kopieren: 
`//datawrapper.dwcdn.net/6D2bM/4/`


#### Maps und Charts einbinden

Um eine im Datawrapper erstellte Grafik einzubinden, wird in den Fließtext folgendes eingebaut: 

``` 
### Jeder dritte Komponist lebt - wird aber kaum aufgeführt

<figure role="group">
    <figcaption> Bei Klick auf 'KomponistInnen' ist zu sehen, wie das Verhältnis von verstorbenen zu lebenden KomponistInnen ist.</ figcaption>
    <DataWrapper
        alt="Fast jede dritte KomponistIn lebt, aber nur 9 % der Aufführung stammen von ihnen."
        title="Nur 9 % der Aufführungen stammen von lebenden KomponistInnen."
        src="//datawrapper.dwcdn.net/6D2bM/4/"
    />

</figure>
```

- H3-Überschrift der Grafik - möglichst sprechend: So what? Was ist die Erkenntnis?
- Figcaption: Erklärung der Grafik, was ist zu sehen? Was kann wie angeklickt werden?
- alt: Alternativ-Text: Textlichte Beschreibung des Inhalts 
- title: Wird aus der H3-Überschrift der Grafik übernommen
- scr: Datawrapper-Pfad einfügen 



### Quote

Zitat mit Nennung des Urhebers, Verlinkung möglich. 

Ohne Link: 
```
<Quote author="Berthold Schneider, Intendant Oper Wuppertal">Die Oper ist stark genug, dass sie sich immer wieder verändern wird.</Quote>
```

Mit Link: 
``` 
<Quote author={
<a href="https://blogs.nmz.de/badblog/2018/04/10/die-ernuechternde-opernstatistik-der-spielzeit-2017-2018/" target="_blank" rel="noopener noreferrer">Moritz Eggert</a>
}>Überlebenschance der Gattung Oper, wenn sich nicht grundlegend etwas ändert: 0%</Quote>
```


### Sharing 
Die Komponente ist gut so, wie sie ist. Einfach importiert und eingebunden lassen.

``` <Sharing twitter facebook mail whatsapp telegram reddit xing linkedin /> ```


### Accordion
Inhalte austauschen. 
Das Accordion ist ev. etwas fummelig. Alle schließenden und öffnenden Tags müssen vorhanden sein. Ggf. vom Datenteam helfen lassen. 

```
<Accordion authors={
    <ul>
        <li><a href="https://twitter.com/TheOrganicer" target="_blank" rel="noopener noreferrer">Niklas Rudolph</a></li>
        <li><a href="https://twitter.com/pen1710" target="_blank" rel="noopener noreferrer">Patricia Ennenbach</a></li>
    </ul>
} sources={
<React.Fragment>
    <h3>Daten</h3>
        <ul>
            <li>- WDR Umfrage und eigene Recherchen - Daten zum Download: <a href='https://raw.githubusercontent.com/wdr-data/starter/main/data/opern_nrw_18_19.csv' target="_blank" rel="noopener noreferrer">opern_nrw_18_19.csv</a>
            </li>
            <li>- Per <a href='https://query.wikidata.org/' target="_blank" rel="noopener noreferrer">Wikidata Query Service </a>abgerufene Lebensdaten - Daten zum Download: <a href='https://raw.githubusercontent.com/wdr-data/starter/main/data/komponisten_wikidata.csv' target="_blank" rel="noopener noreferrer">Komponistinnen_wikidata.csv</a>
            </li>
            <li>- Die Vorgehensweise bei der Datenanalyse können Sie hier nachlesen: <a href='https://github.com/wdr-data/starter/blob/main/data/Daten-Analyse_Opern_in_NRW.ipynb' target="_blank" rel="noopener noreferrer">Daten-Analyse Opern in NRW</a>
            </li>
        </ul>
    <h3>Code</h3>
        <ul>
            <li>- 'Oper in NRW' ist das erste WDR Data Projekt, das mit unserem Data Starter umgesetzt wurde. Der Code steht OpenSource zur Verfügung: <a href='https://github.com/wdr-data/starter/' target="_blank" rel="noopener noreferrer">WDR Data Starter</a>
            </li>
        </ul>
</React.Fragment>
} credits={
<React.Fragment>
    <h3>Bildrechte:</h3>
        <ul>
        <li>Aufmacher-Bild: Richard Wagner und seine Freunde, Foto von Joseph Albert (picture alliance / akg-images)</li>
        <li>Bild 2: Der Wuppertaler Opernintendant Berthold Schneider, fotografiert von Jens Grossmann</li>
        </ul>
    <h3>Credits:</h3>
        <ul>
            <li><b>Redaktion</b>: Niklas Rudolph, Urs Zietan, Jutta Starke</li>
            <li><b>Design</b>: Chrissi Holderbaum, Dilek Wache</li>
            <li><b>Programmierung</b>: Christine Gotthardt, Marcus Weiner, Jakob Holderbaum, Patricia Ennenbach</li>
            <li><b>Accessability, UX</b>: Dilek Wache, Stephanie Juranek</li>
            <li><b>Datenrecherche</b>: Felix Buczek, Hannah Schmidt, Anne Glaser, Robert Haase, Greta Hey, Inge Akyaa, Katharina Riethmüller</li>
            <li><b>Besondere Unterstützung:</b> Dr. Olaf Roth, Musiktheater im Revier</li>
        </ul>
</React.Fragment>
} hints={
<React.Fragment>
<h3>Analytics</h3>
    <p>Diese Seite verwendet Webtrekk, um Daten über das Interaktions- und Nutzungsverhalten zu sammeln. Diese Daten werden auf Seiten des WDR ausschliesslich in anonymisierter Form gespeichert und ausgewertet.</p>
<h3>Fehler melden</h3>
    <p>Für Hinweise und die Meldung von Fehlern schreiben Sie uns an data@wdr.de.</p>
</React.Fragment>}
/>

```

### Webtrekk
- Veröffentlichungsdatum anpassen
- Entsprechend der Absprache mit der Medienforschung die Content-Groups (CG1 bis CG4) anpassen: 
CG1 = WDR 
CG2 = Data
CG3 = Partnerredaktion
CG4 = H1 (Hauptüberschrift) des Stücks

``` <Webtrekk publishedAt='2019-07-15' cg1='WDR' cg2="Data" cg3="WDR 3" cg4="Opern-Spielpläne in NRW: tot und männlich"/> ```

#### Data
- unter /data werden Daten (.csv, .json etc.)  und Datenanalyse-Notebook abgelegt

## Für DesignerInnen

### Typografie

Im Design greifen wir auf die u.g. Schriften zurück:

- Google Font [Merriweather](https://fonts.google.com/specimen/Merriweather?selection.family=Merriweather) in Regular 400
- Google Font [Open Sans](https://fonts.google.com/specimen/Open+Sans) in Light 300 und Semibold 600

Eine Übersicht zur Typografie befindet sich hier: https://wdr-data.netlify.com/components/?path=/story/typography--default

### Farben

Die Farbkontraste für das gesamte Design sind im [Kontrast Checker](https://contrast-ratio.com/) überprüft worden. 

- Schriftfarbe: #1D2124 (WDR Dunkelblau)
- Flächenfarbe: #00345E (WDR Blau)
- Highlightfarbe für Links: #007381 (WDR Petrol)
- Akzentfarbe: #B37500 (WDR Honiggelb)

### Logo & Header

Im oberen Bereich einer jeden Dataseite befindet sich lediglich das WDR Logo, mithilfe dessen man aus der Datawelt zurück in die WDR Welt navigieren kann.

- Falls ein Hero Image vorhanden ist: Weißes WDR Logo im Rechteck auf Blau
- Falls kein Hero Image vorhanden ist: Blaues WDR Logo auf weiß

### Iconography

https://icomoon.io/#preview-free

### Designprinzipien

- Arbeite mit einfach erkennbaren visuellen Hierachien
- Nutze ein klar strukturiertes Layout ohne Ablenkungen mit Fokus auf Inhalten
- Erschaffe ein konsistentes Design mit modular einsetzbaren und wiederkehrenden Elementen
- Gestalte ein leichtes, modernes und ansprechendes Design mit Mut zu Weißraum

### Sketch files

> ToDo: Sketch Datei hinterlegen

## Für EntwicklerInnen

- Pull-Request stellen oder per Mail / bei Github darum bitten, Teil des Teams zu werden: [wdr-data@hacking.studio](mailto:wdr-data@hacking.studio)

Repository: https://github.com/wdr-data/starter

### Wie baue ich eine neue Komponente?

Komponenten liegen im Git Repo unter `src/components`. Jede Komponente hat einen eigenen Unterordner mit folgenden Dateien: 

- JSX-Datei - React-Code der Komponente
- CSS-Datei - Styling
- `.stories.jsx` - Enthält die Stories für das Storybook

### Wie integriere ich React Komponenten?

Am Beispiel [Semiotic](https://semiotic.nteract.io/)
- Neuen Branch anlegen feature/semiotic
- yarn add xy
- Unterordner für die Komponente anlegen
- JSX, CSS und `stories.jsx` Datei anlegen

### Guides / Manuals für React

- https://reacttraining.com/blog/javascript-the-react-parts/
- https://reactjs.org/tutorial/tutorial.html
- https://leanpub.com/the-road-to-learn-react/
- https://reactpatterns.com/
- https://www.learnstorybook.com/react/en/simple-component/
- https://reactjs.org/docs/faq-styling.html
- https://github.com/css-modules/css-modules/blob/master/README.md

#### Storybook

:bulb: [Storybook Dokumentation](https://storybook.js.org/)

Eine lebende Dokumentation der Komponentenbibliothek. Hier kann jede Komponente in ihren Ausprägungen angesehen und ausprobiert werden.

:arrow_right: [Starter-Komponenten](https:/wdr-data.netlify.com/components) (unser Storybook)

Das Ziel ist die Funktion der Komponente greifbar zu machen. Dazu können entweder mehrere Stories pro Komponente erstellt oder [Knobs](https://github.com/storybookjs/storybook/blob/master/addons/knobs/README.md#available-knobs) benutzt werden.

> ToDo: Screenshot hinzufügen

### Gatsby: Publishing-Umgebung

Der Starter nutzt [Gatsby](https://www.gatsbyjs.org/) zum Generieren von statischen HTML-Seiten aus unserem Basis-Layout und Markdown-Inhalten.

Das Gatsby-Setup wurde auf Basis des [Schnellstart-Tutorial](https://www.gatsbyjs.org/docs/quick-start) aufgebaut.

Ein Großteil der Konfiguration von Gatsby befindet sich in `gatsby-config.js`.

#### Relevante Ordner für Gatsby

- `src/pages`
    - Ablage für statische Inhaltsseiten
    - :bulb: [Gatsby: Mit Seiten arbeiten](https://www.gatsbyjs.org/tutorial/part-one/#familiarizing-with-gatsby-pages)
    - aus jeder JS(X)-Datei wird eine statische Seite generiert
    - der Dateiname dient als URL
    - `index.md` wird zur Startseite
- `src/templates`
    - Ablage für Seitenvorlagen
    - :bulb: [Gatsby: Seiten generieren](https://www.gatsbyjs.org/tutorial/part-seven/#creating-pages)
    - enthält `default.jsx` - bestimmt Grundlayout und Metadaten

#### Wie wird Markdown zu HTML?

:bulb: *Tipp: GraphQL-Playground unter http://localhost:8000/__graphql benutzen*

Wenn ich `yarn start` oder `yarn gatsby build` ausführe werden folgende Schritte ausgeführt:

1. Einlesen der Markdown-Dateien als Gatsby-Nodes
    - via [`gatsby-source-filesystem`](https://www.gatsbyjs.org/packages/gatsby-source-filesystem/)
    - Das Plugin `gatsby-source-filesystem` liest alle Dateien im Ordner `content` ein
    - Erstellt werden Nodes vom Typ `File`
    - *Beispiel-Query:*
      ```graphql
      query MyQuery {
        allFile {
          edges {
            node {
              name
              extension
            }
          }
        }
      }
      ```
2. Parsen der Dateien in MDX-Nodes
    - via [`gatsby-plugin-mdx`](https://www.gatsbyjs.org/packages/gatsby-plugin-mdx/)
    - Nimmt alle File-Nodes mit Extension `md` oder `mdx`
    - Wandelt Markdown zu JSX
    - Macht Frontmatter in Gatsby verfügbar
    - Erstellt Nodes vom Typ `MDX`
    - *Beispiel-Query:*
      ```graphql
      query MyQuery {
        allMdx {
          nodes {
            frontmatter {
              title
              author
              description
              pub_date
              slug
            }
            rawBody
          }
        }
      }
      ```
3. Erstellen von Gatsby Pages
    - Custom Code in `gatsby-node.js`
    - Weist eine URL aus `slug` zu oder macht `title` URL-fähig (TODO)
    - Weist der Seite ein [Template](#%C3%9Cber-Seiten-Templates) zu
4. Generieren der statischen Seiten aus Inhalt und Template
    - Ausführen der GraphQL-Query im zugewiesenen Template-File
      - Query in Named Export `pageQuery`
      - `context` aus `createPage` dient als Parameter der Query (z.B. `$id`)
    - Rendern der Template-Komponente
      - Komponente als Default Export
      - Ergebnis der GraphQL wird als `data` Property gesetzt


##### Inhalte als Markdown

- `pages/index.md`
    - Ablage für Datengeschichten
    - pro Geschichte ein repo mit einer eine Markdown-Datei
    - Die [MDX-Erweiterung](https://mdxjs.com/) wird genutzt um inline Komponenten einsetzen zu können
    - :bulb: [Gatsby and MDX](https://www.gatsbyjs.org/docs/mdx/)

#### Über Seiten-Templates

:bulb: [Gatsby: Templates für MDX-Seiten](https://www.gatsbyjs.org/docs/mdx/programmatically-creating-pages/#make-a-template-for-your-posts)

Was ein Template machen sollte:

- Header einbinden
- Markdown-Inhalt einheitlich stylen
- Meta-Tags für die Seite setzen
- Breadcrumb erstellen
- Footer einbinden

#### Plugins

Genutzte Plugins:

- [Source Filesystem](https://www.gatsbyjs.org/packages/gatsby-source-filesystem/)
    - Einlesen der Inhalte als Gatsby-Nodes zur Weiterverarbeitung
- [MDX Plugin](https://www.gatsbyjs.org/packages/gatsby-plugin-mdx/)
    - Parsing von MDX-Dateien zu Gatsby Pages
    - Genutzte Extensions: `md` & `mdx`
    - Ziel: Verarbeiten von Seiten aus dem Filesystem-Plugin
- [Remark Images](https://www.gatsbyjs.org/packages/gatsby-remark-images/)
    - Extrahiert Bilder, die in Markdown referenziert werden
    - **Wichtig:** Es können nur Bilder aus dem gleichen Ordner referenziert werden
- [Sharp](https://www.gatsbyjs.org/packages/gatsby-plugin-sharp/)
    - Skaliert verwendete Bilder in verschiedene Größen
- [React Helmet Plugin](https://www.gatsbyjs.org/packages/gatsby-plugin-react-helmet/)
    - fügt Metadaten dem `<head>` hinzu
    - [React Helmet](https://github.com/nfl/react-helmet) kann aus jeder Komponente zum Setzen von Metadaten genutzt werden
    - Globale Metadaten werden in der Komponente `SEO` verwaltet
- [Manifest Plugin](https://www.gatsbyjs.org/packages/gatsby-plugin-manifest/)
    - Erzeugt ein PWA-Manifest

*TODO: Erklären*
- CSS Modules
- [SEO](https://www.gatsbyjs.org/docs/seo/)
- [Google Analytics](https://www.gatsbyjs.org/packages/gatsby-plugin-google-analytics/) 


### Code-Style

TODO

### Deployment

Der DDJ-Editor wird bei [Netlify](https://www.netlify.com/docs/) gebaut & gehostet.
(PBI-Kreditkarte hinterlegt.)

*Was passiert?*

- Push ins Git-Repository
- Netlify CI baut das Projekt automatisiert
- Bereitstellung des Build-Outputs auf dem Netlify CDN (bei erfolgreichem Build)

*Warum?*

- Nachvollziehbarer Output basierend auf einer automatisierten Umgebung
- Klare Verknüpfung zwischen Git-Commit und veröffentlichtem Ergebnis

#### CI & Hosting

Konfiguration ist definiert in [`netlify.toml`](https://github.com/wdr-data/starter/tree/main/netlify.toml). Sie überschreibt die Einstellungen, die man im Netlify-UI vornimmt.

:arrow_right: [netlify.toml Docs](https://www.netlify.com/docs/netlify-toml-reference/)

Die Netlify Build-Umgebung geht so vor:
- Installieren der Dependencies (yarn)
- Ausführen des Build-Kommandos
- Hochladen des Ergebnis ins CDN

Automatisch von der CI-Umgebung gebaut werden Main-Branch und alle Pull-Requests. Netlify stellt für Pull Requests sog. "Preview Builds" bereit, die eine LIVE-Vorschau von Änderungen unter einer URL ermöglicht.

`/public` dient als Deployment-Ordner und wird von Netlify nach erfolgreichem Build aus der CI im CDN veröffentlicht.

Das zentrale Build-Kommando (`yarn build`) baut 3 Teile:

#### Storybook

- Befehl: `yarn build-storybook`
    - Build-Tooling: npm-Modul `storybook`
    - Konfiguriert in `.storybook`
- Ergebnis liegt in: `public/components`
- Ergebnis URL-Pfad `/components`


#### Publikation

- im URL-Pfad: `/`
- Befehl: `yarn build-gatsby`
    - Build-Tooling: Gatsby
- Ergebnis liegt in: `public`

#### Auf data.wdr.de 
Per Mail an Dittmann um neuen Ordner auf data.wdr.de bitten. Mit den Zugangsdaten Daten aus dem Build-Ordner auf den Server hochladen.  


### Tests

*TODO*

#### Visual Regression Testing

- Snapshot: https://www.npmjs.com/package/@storybook/addon-storyshots-puppeteer
- Compare: https://github.com/reg-viz/reg-cli


#### Accessability testing

- https://github.com/dequelabs/axe-core
- https://github.com/dequelabs/react-axe
- https://developers.google.com/web/tools/lighthouse/


#### Content checks

- Dead links
- Missing URLs



## License

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons Lizenzvertrag" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a>
<br /><span xmlns:dct="http://purl.org/dc/terms/" href="http://purl.org/dc/dcmitype/Dataset" property="dct:title" rel="dct:type">WDR Data Starter</span> by <a xmlns:cc="http://creativecommons.org/ns#" href="https://github.com/wdr-data/starter" property="cc:attributionName" rel="cc:attributionURL">WDR Data</a> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.
