# Fondamenti di HTML/CSS/JavaScript

I fondamenti di HTML, CSS e JavaScript sono alla base di quasi tutto ciò che vedi sul web. Ecco una breve descrizione di ciascuno:

HTML (HyperText Markup Language) è il linguaggio di markup utilizzato per strutturare e dare significato al contenuto web.

Ad esempio, il contenuto potrebbe essere strutturato in paragrafi, elenchi, intestazioni, link, immagini, tabelle e molti altri tipi di dati.

Ecco un esempio base di HTML

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Titolo della pagina</title>
  </head>
  <body>
    <h1>Il mio primo titolo</h1>
    <p>Il mio primo paragrafo.</p>
  </body>
</html>
```
CSS (Cascading Style Sheets) è il linguaggio utilizzato per descrivere l'aspetto e la formattazione di un documento scritto in HTML. 

Puoi utilizzare CSS per controllare aspetti come il colore del testo, la dimensione dei caratteri, lo spazio tra elementi, come vengono visualizzati gli elementi (in blocchi, inline, ecc.), il layout della pagina e molto altro.

Ecco un esempio base di CSS

```css
body {
  background-color: lightblue;
}

h1 {
  color: white;
  text-align: center;
}

p {
  font-family: verdana;
  font-size: 20px;
}
```
JavaScript è il linguaggio di programmazione del web.
Mentre HTML e CSS si occupano rispettivamente della struttura e dello stile, JavaScript consente di aggiungere comportamenti interattivi alle tue pagine web. Puoi utilizzare JavaScript per fare cose come:

- Modificare il contenuto HTML e gli attributi CSS
- Rispondere agli eventi dell'utente (ad esempio, clic del mouse, pressioni di tasti, caricamenti di pagine)
- Effettuare richieste HTTP per recuperare o inviare dati da o a un server
- Creare cookie
- E molto altro...

Ecco un esempio base di JavaScript

```javascript
document.getElementById("demo").innerHTML = "Hello world!";
Per diventare un buon sviluppatore web, è essenziale avere una solida comprensione di questi tre linguaggi. Dopo averli padroneggiati, puoi passare a tecnologie più avanzate come React, Angular, Vue, Node.js, e così via
```

> HTML

HTML struttura il contenuto del tuo sito web utilizzando elementi, che sono rappresentati da tag.

```html
Ogni tag HTML ha uno scopo specifico. Ad esempio, <h1> è un tag per un titolo principale, <p> è un tag per un paragrafo, <a> è un tag per un link, e così via. Alcuni tag, come <img> e <input>, possono richiedere attributi per funzionare correttamente (ad esempio, l'attributo "src" in <img src="url_to_image.jpg">)
```

> CSS

CSS definisce come gli elementi HTML vengono visualizzati sullo schermo. Puoi utilizzare i selettori CSS per targettizzare specifici elementi HTML e applicare stili a loro. Ad esempio, puoi targettizzare tutti i paragrafi sulla tua pagina e rendere il loro testo rosso con il seguente codice CSS:

```css
p {
  color: red;
}
```
Inoltre, CSS ha il concetto di "classi" e "id", che ti permettono di targettizzare specifici elementi HTML. Ad esempio, puoi dare a un elemento HTML la classe "testo-evidenziato" e poi utilizzare CSS per fare in modo che tutti gli elementi con quella classe abbiano il testo in grassetto:

```css
.testo-evidenziato {
  font-weight: bold;
}
```

> JavaScript

JavaScript aggiunge interattività al tuo sito web.

Puoi utilizzarlo per fare cose come cambiare il contenuto HTML o gli stili CSS sulla base degli input dell'utente, fare calcoli, manipolare dati, ecc.

Ecco un esempio in cui utilizziamo JavaScript per cambiare il testo di un elemento HTML quando l'utente clicca su un pulsante:

```html
<button onclick="cambiaTesto()">Clicca qui</button>
<p id="testo">Ciao, mondo!</p>

<script>
function cambiaTesto() {
  document.getElementById("testo").innerHTML = "Hai cliccato sul pulsante!";
}
</script>
```

In questo esempio, quando l'utente clicca sul pulsante, la funzione cambiaTesto() viene eseguita. Questa funzione cambia il contenuto dell'elemento con id "testo" in "Hai cliccato sul pulsante!".


> HTML

Attributi HTML
Gli attributi forniscono informazioni aggiuntive sugli elementi HTML. Ad esempio, l'attributo src indica la sorgente di un'immagine, l'attributo href indica l'URL di un link, e così via

Form HTML
I form HTML sono utilizzati per raccogliere input da parte degli utenti. Possono includere vari tipi di input come testo, password, checkbox, radio button, date, e-mail, e così via

Tag semantici HTML
I tag semantici
```html
<header>, <footer>, <article>, <section>, <nav>, <aside>
```
ecc. vengono utilizzati per dare un significato alla struttura del contenuto

> CSS

Pseudo-classi e pseudo-elementi
Le pseudo-classi come :hover, :active, :visited, :first-child, ecc. sono utilizzate per definire uno stile per uno stato speciale di un elemento. I pseudo-elementi come ::before, ::after, ::first-letter, ecc. sono utilizzati per stilizzare una specifica parte di un elemento.

Design responsivo
Il design responsive rende il tuo sito web visivamente efficace su diversi dispositivi, ridimensionando e riorganizzando il layout. Le media query sono uno strumento importante per il design responsive

CSS Preprocessors
I preprocessori CSS come Sass, Less ecc. consentono di utilizzare funzionalità che non esistono in CSS puro come variabili, nesting, mixin, ereditarietà, ecc.

> JavaScript

Oggetti
JavaScript è un linguaggio di programmazione basato sugli oggetti. Gli oggetti sono raccolte di proprietà, e una proprietà è un'associazione tra un nome (o una chiave) e un valore

Array
Un array è un tipo di dato speciale che può contenere più valori contemporaneamente

Controllo del flusso
Le istruzioni if, else, switch, i loop for, while, ecc. sono usati per controllare il flusso del programma

Promises e async/await
Sono utilizzati per gestire operazioni asincrone in JavaScript

Librerie e framework JavaScript
jQuery, React, Angular, Vue.js, ecc. sono librerie e framework JavaScript che aiutano a sviluppare applicazioni

Questi sono solo alcuni dei concetti chiave di HTML, CSS e JavaScript. Naturalmente, ci sono molti altri concetti e tecniche avanzate in ciascuno di questi domini

> HTML5

Multimedia: Gli elementi 
```html
<video>
<audio>
```
 
consentono di incorporare media direttamente nelle tue pagine web.

Accessibilità
L'accessibilità è un aspetto cruciale della progettazione web. L'utilizzo di attributi come alt per le immagini, una corretta struttura dei titoli (h1, h2, h3, ecc.) e l'uso di tag semantici migliorano l'accessibilità del tuo sito web.

> CSS

Animazioni CSS
Le animazioni e le transizioni CSS consentono di creare interfacce utente interattive e dinamiche. Puoi animare qualsiasi proprietà CSS nel tempo con le chiavi @keyframes, transition o animation

CSS Variables
Le variabili CSS consentono di riutilizzare valori specifici in tutto il tuo foglio di stile

CSS Frameworks
I framework CSS come Bootstrap, Foundation, TailwindCSS, ecc., offrono predefinite strutture di layout, componenti e temi per velocizzare lo sviluppo del frontend

> JavaScript

ES6 e oltre
Le nuove caratteristiche del JavaScript ES6 e oltre, come arrow functions, classi, moduli, template strings, spread operator, destructuring, ecc., rendono il codice più leggibile e facile da scrivere

Node.js
Node.js è un ambiente di runtime che consente di eseguire JavaScript sul lato server. Puoi creare applicazioni web complete (frontend e backend) utilizzando solo JavaScript

NPM
NPM è il gestore di pacchetti per Node.js e ti consente di installare e gestire librerie e dipendenze per il tuo progetto JavaScript

# Introduzione a React

React è una libreria JavaScript per la creazione di interfacce utente
È stato sviluppato da Facebook e ora è mantenuto da Facebook e una comunità di sviluppatori individuali e aziende
React ti permette di creare componenti UI riutilizzabili e gestire il rendering di questi componenti

Ecco alcuni concetti chiave che dovresti conoscere quando inizi a lavorare con React:

1. Componenti

In React, l'interfaccia utente di un'applicazione è costituita da componenti. Un componente è una unità indipendente di codice che restituisce un elemento React, che viene poi renderizzato come HTML nel browser. I componenti possono essere semplici o complessi e possono contenere altri componenti.

2. JSX

JSX è una sintassi di JavaScript che assomiglia a HTML. È utilizzato in React per descrivere l'aspetto dell'interfaccia utente. JSX ti permette di scrivere tag HTML in JavaScript, e React poi renderizza questi tag HTML nel DOM.

3. Stato e Props

Ogni componente in React ha un state e props. Lo state è un oggetto che contiene dati che possono cambiare nel tempo. I props (o proprietà) sono valori che vengono passati da un componente genitore a un componente figlio.

4. Ciclo di vita del componente

Ogni componente React ha diversi "momenti della vita". Questi includono il montaggio (quando un componente viene creato e inserito nel DOM), l'aggiornamento (quando un componente viene re-renderizzato a causa di cambiamenti nello state o nei props) e lo smontaggio (quando un componente viene rimosso dal DOM).

5. Hook

Gli Hook sono funzioni speciali che ti permettono di "agganciare" le funzionalità di React state e ciclo di vita all'interno dei componenti funzionali. Gli Hook sono una caratteristica introdotta in React 16.8, e offrono un modo alternativo per scrivere componenti rispetto alle classi di componenti basate sullo stato.

Ecco un esempio di un semplice componente React scritto in JSX:

```jsx
import React from 'react';

class Hello extends React.Component {
  render() {
    return <h1>Ciao, {this.props.name}</h1>;
  }
}

// Da utilizzare così:
// <Hello name="Mario" />
```
In questo esempio, Hello è un componente React

```jsx
Quando lo usi nella tua app (come <Hello name="Mario" />), React lo renderizza come <h1>Ciao, Mario</h1>
```

6. Gestione degli eventi

In React, gli eventi come il click del mouse, la pressione dei tasti, ecc., sono gestiti con sintassi molto simile a quella del DOM. Tuttavia, ci sono alcune differenze chiave come:

Gli eventi in React sono chiamati in camelCase piuttosto che in minuscolo.
Con JSX passi una funzione come gestore dell'evento invece di una stringa.
Ecco un esempio di gestione degli eventi in React:

```jsx
class MyButton extends React.Component {
  handleClick = () => {
    alert('Hai cliccato il bottone!');
  }

  render() {
    return <button onClick={this.handleClick}>Clicca qui</button>;
  }
}
```
7. Form

In HTML, i form mantengono il proprio stato e lo aggiornano in base all'input dell'utente. In React, lo stato mutabile è di solito mantenuto nei componenti dello stato. Si può combinare i due rendendo il componente React "controllato" su un form HTML.

```jsx
class NameForm extends React.Component {
  state = { value: '' };

  handleChange = (event) => {
    this.setState({value: event.target.value});
  }

  handleSubmit = (event) => {
    alert('Un nome è stato inviato: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Nome:
          <input type="text" value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="Invia" />
      </form>
    );
  }
}
```

8. Lifting State Up

In genere, diversi componenti possono aver bisogno di riflettere lo stesso cambiamento di dati

In React, si consiglia di sollevare lo stato condiviso ai loro antenati più vicini. Ciò significa che se più componenti hanno bisogno degli stessi dati, si dovrebbe far risiedere tale stato nel componente padre più vicino.

9. Composizione vs Ereditarietà

React ha un potente modello di composizione, e si consiglia di utilizzare la composizione invece dell'ereditarietà per riutilizzare il codice tra i componenti. In React, ciò può essere realizzato passando componenti come figli di altri componenti.

10. React sincronizza l'URL con lo stato

React Router è una libreria di routing per le applicazioni React che permette di aggiungere nuove schermate e flussi alla tua applicazione in modo molto efficiente, mantenendo l'URL sincronizzato con ciò che viene visualizzato sullo schermo.

11. Next.js

Next.js è un framework basato su React che offre funzionalità come il rendering lato server e la generazione di siti statici

12. React Hooks

Gli Hooks sono una funzionalità introdotta in React 16.8 che permette di utilizzare lo stato e altre funzionalità di React senza scrivere una classe. Alcuni degli Hooks forniti da React includono useState, useEffect, useContext, tra gli altri.

Ecco un esempio di come si utilizza l'hook useState:

```jsx
Copy code
import React, { useState } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Hai cliccato {count} volte</p>
      <button onClick={() => setCount(count + 1)}>
        Clicca me
      </button>
    </div>
  );
}
```
13. Redux

Redux è una libreria di gestione dello stato che è spesso utilizzata con React, ma può essere utilizzata con qualsiasi altra libreria o framework. Se stai costruendo un'applicazione di medie o grandi dimensioni con React, potresti voler considerare l'utilizzo di Redux.

14. React Testing Library e Jest

React Testing Library è una libreria molto popolare per testare i componenti React. Funziona molto bene con Jest, un framework di testing JavaScript, e offre un approccio più orientato all'utente per testare i componenti React.

15. Styled Components

Styled Components è una libreria che utilizza i tagged template literals (un tipo di stringhe in JavaScript) per stilizzare i tuoi componenti. Offre un modo per utilizzare il CSS direttamente nei tuoi componenti React, consentendo di gestire tutto il codice relativo a un componente in un unico posto.

16. React Dev Tools

React Dev Tools è un'estensione per Chrome e Firefox che ti aiuta a ispezionare la gerarchia dei componenti React nel browser, incluso lo stato e le props dei componenti.

17. Server-Side Rendering (SSR)

Il Server-Side Rendering, o SSR, è una tecnica per migliorare le prestazioni e l'ottimizzazione dei motori di ricerca delle applicazioni


# Creare applicazioni con Create React App


Create React App (CRA) è un tool molto popolare e ampiamente usato per creare nuove applicazioni React
È un ambiente che ti permette di avviare un nuovo progetto React senza dover configurare strumenti come Webpack o Babel, che sono già preconfigurati per te.

Ecco come creare una nuova applicazione React con Create React App:

Passo 1: Installare Node.js e npm

Prima di tutto, avrai bisogno di Node.js e npm (Node Package Manager) installati sul tuo computer. npm viene installato automaticamente con Node.js.

Puoi scaricare Node.js dal sito ufficiale

Passo 2: Installare Create React App

Apri la linea di comando e digita il seguente comando per installare globalmente Create React App sul tuo computer:


> npm install -g create-react-app

Passo 3: Creare una nuova applicazione React

Ora puoi creare una nuova applicazione React digitando il seguente comando (dove my-app è il nome della tua nuova applicazione):


> npx create-react-app my-app

Passo 4: Avviare l'applicazione

Vai nella cartella della tua nuova applicazione e avvia l'applicazione React digitando il seguente comando


>cd my-app
npm start

Dopo aver eseguito npm start, dovresti vedere il tuo nuovo sito React avviato in una nuova scheda del tuo browser predefinito

Ora hai una nuova applicazione React pronta per lo sviluppo! La struttura del progetto sarà simile a questa:

```
my-app/
  README.md
  node_modules/
  package.json
  .gitignore
  public/
    index.html
    favicon.ico
  src/
    App.css
    App.js
    App.test.js
    index.css
    index.js
    logo.svg
```
La directory public contiene il file HTML che serve come template per l'applicazione, mentre la directory src contiene tutti i file JavaScript e CSS per la tua applicazione React

> Puoi ora iniziare a sviluppare la tua applicazione modificando i file nella directory src

> Ogni volta che salvi i file, l'applicazione verrà ricaricata in automatico

Una volta creato il tuo progetto con Create React App (CRA), avrai a disposizione diversi script npm che ti aiuteranno nello sviluppo:

> npm start

Avvia l'applicazione in modalità sviluppo. Verrà aperta una finestra del browser che punta a http://localhost:3000
L'applicazione verrà ricaricata automaticamente se modifichi file nel progetto

> npm test

Avvia il test runner in modalità watch. CRA usa Jest come test runner. Questo comando eseguirà tutti i test che trova nei tuoi file .test.js o .spec.js

> npm run build

Crea una versione di produzione della tua app nella cartella build. Questa versione è ottimizzata per le prestazioni e pronta per essere implementata

> npm run eject

Questo è un comando one-way. Una volta che "ejecti", non puoi tornare indietro! Se non sei soddisfatto della configurazione di build e delle scelte di strumenti, puoi "eject" in qualsiasi momento. Questo comando rimuoverà la dipendenza da CRA dal tuo progetto

Nella cartella src/ troverai i seguenti file:

index.js
Questo è il punto di ingresso della tua app. Qui è dove React viene effettivamente renderizzato nel DOM con ReactDOM.render()

App.js
Questo è il componente principale della tua app. Di solito, avrai i tuoi componenti di routing e layout principali qui

index.css e App.css
Questi file contengono gli stili globali e gli stili specifici dell'app, rispettivamente

serviceWorker.js
Questo è un web worker che esegue JavaScript in background del tuo browser. Puoi utilizzarlo per funzioni avanzate come la capacità di far funzionare la tua app offline, ma di solito non ne avrai bisogno per i progetti più semplici


# Aggiunta di Componenti e Gestione dello Stato

La tua app React sarà composta da componenti. I componenti sono come i blocchi di costruzione della tua app. Ogni componente rappresenta una parte dell'interfaccia utente (UI), e può avere il proprio stato e le proprie props.

Ad esempio, potresti avere un componente Header che mostra il titolo della tua app, un componente Footer per mostrare alcune informazioni sul copyright, e un componente Main per il contenuto principale della tua app.

Un componente in React può essere una classe o una funzione. Con l'introduzione degli Hooks in React 16.8, i componenti funzionali possono ora avere uno stato, rendendoli molto più potenti e facili da usare rispetto ai componenti di classe.

Ecco un esempio di un semplice componente funzionale in React:

```jsx
import React from 'react';

function Welcome(props) {
  return <h1>Ciao, {props.name}</h1>;
}

export default Welcome;
```

Puoi quindi utilizzare questo componente in un altro componente, passando i dati tramite props:

```jsx
import React from 'react';
import Welcome from './Welcome';

function App() {
  return <Welcome name="Mario" />;
}

export default App;
```
Gestione dello Stato con Hooks

Gli Hooks sono una funzionalità aggiunta in React 16.8 che permette ai componenti funzionali di avere uno stato e altri poteri che prima erano disponibili solo nei componenti di classe. useState e useEffect sono due degli Hooks più comunemente utilizzati.

Ecco un esempio di come si può utilizzare l'Hook useState per aggiungere uno stato a un componente funzionale:

```jsx
import React, { useState } from 'react';

function Contatore() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Hai cliccato {count} volte</p>
      <button onClick={() => setCount(count + 1)}>
        Clicca qui
      </button>
    </div>
  );
}

export default Contatore;
```
Nell'esempio sopra, useState(0) inizializza lo stato del contatore a 0. setCount è la funzione che useremo per aggiornare lo stato. Quando il pulsante viene cliccato, chiamiamo setCount(count + 1) per incrementare il contatore.

Una volta che hai una buona comprensione dei componenti e dello stato in React, puoi iniziare a esplorare concetti più avanzati come l'uso di Redux o Context per la gestione dello stato globale, o l'uso di React Router per aggiungere il routing alla tua app
