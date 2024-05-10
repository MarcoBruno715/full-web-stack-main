# esempio di come creare un'applicazione web MVC

- Aprire Visual Studio Code e creare una nuova cartella di progetto.
- Aprire il terminale integrato di Visual Studio Code e digitare il comando npm init per inizializzare un nuovo progetto Node.js.
- Digitare npm install express per installare il framework Express per Node.js.
Creare un nuovo file app.js nella cartella di progetto.
Aggiungere il seguente codice per creare una applicazione web con Express:
```javascript
const express = require('express');
const app = express();

app.set('view engine', 'ejs');
app.use(express.static('public'));

app.get('/', (req, res) => {
  res.render('index');
});

app.listen(3000, () => {
  console.log('Server avviato sulla porta 3000');
});
```
- Salvare il file app.js.
- Creare una nuova cartella views nella cartella di progetto.
- Creare un nuovo file index.ejs nella cartella views.
Aggiungere il seguente codice HTML per creare la pagina principale dell'applicazione:
```php
<!DOCTYPE html>
<html>
  <head>
    <title>Applicazione web MVC</title>
  </head>con un layout comune condiviso tra 3 viste e un menu di navigazione
  <body>
    <h1>Benvenuti nell'applicazione web MVC</h1>
    <p>Questa è la pagina principale dell'applicazione.</p>
  </body>
</html>
```
- Salvare il file index.ejs.
- Creare una nuova cartella public nella cartella di progetto.
- Creare un nuovo file style.css nella cartella public.
Aggiungere il seguente codice CSS per personalizzare lo stile della pagina principale:
```css
body {
  font-family: Arial, sans-serif;
  background-color: #eee;
  text-align: center;
  padding-top: 50px;
}

h1 {
  font-size: 36px;
  color: #333;
}

p {
  font-size: 18px;
  color: #666;
}
```

- Salvare il file style.css.
Aprire il terminale integrato di Visual Studio Code e digitare node app.js per avviare il server web.
Aprire un browser web e digitare http://localhost:3000 per accedere alla pagina principale dell'applicazione.
In questo esempio, il framework Express viene utilizzato per creare una applicazione web MVC. Il pacchetto ejs viene utilizzato per rendere la pagina HTML dinamica, mentre la cartella public viene utilizzata per ospitare file statici come fogli di stile CSS e immagini.

L'applicazione web è composta da un unico controller che gestisce la richiesta di base all'URL '/', e restituisce la vista corrispondente. La vista è creata utilizzando il motore di rendering ejs e viene visualizzata nella pagina HTML. Il risultato è una semplice applicazione web MVC senza database.

Questo esercizio è solo un esempio di base di come creare un'applicazione web MVC senza database utilizzando Node.js in Visual Studio Code. È possibile personalizzare ulteriormente il codice in base all'esigenzi

# con un layout comune condiviso tra 3 viste e un menu di navigazione

Ecco un esempio di come creare un'applicazione web MVC senza database utilizzando Node.js in Visual Studio Code per principianti, con un layout comune condiviso tra 3 viste e un menu di navigazione:

- Aprire Visual Studio Code e aprire la cartella di progetto in cui si desidera creare l'applicazione web.
- Digitare il comando npm init nel terminale integrato di Visual Studio Code per inizializzare un nuovo progetto Node.js.
- Digitare npm install express ejs per installare il framework Express e il motore di rendering EJS.
Creare una nuova cartella views nella cartella di progetto.
Creare un nuovo file layout.ejs nella cartella views.
Aggiungere il seguente codice HTML per creare il layout comune dell'applicazione:
```php
<!DOCTYPE html>
<html>
  <head>
    <title><%= title %></title>
  </head>
  <body>
    <header>
      <nav>
        <ul>
          <li><a href="/">Home</a></li>
          <li><a href="/page1">Pagina 1</a></li>
          <li><a href="/page2">Pagina 2</a></li>
        </ul>
      </nav>
    </header>
    <main>
      <%= content %>
    </main>
  </body>
</html>
```
- Salvare il file layout.ejs.
- Creare un nuovo file home.ejs nella cartella views.
Aggiungere il seguente codice HTML per creare la vista della pagina principale dell'applicazione:
```html
<h1>Benvenuti nell'applicazione web MVC</h1>
<p>Questa è la pagina principale dell'applicazione.</p>
```
- Salvare il file home.ejs.
Creare un nuovo file page1.ejs nella cartella views.
Aggiungere il seguente codice HTML per creare la vista della prima pagina dell'applicazione:
```css
<h1>Pagina 1</h1>
<p>Questa è la pagina 1 dell'applicazione.</p>
```
- Salvare il file page1.ejs.
Creare un nuovo file page2.ejs nella cartella views.
Aggiungere il seguente codice HTML per creare la vista della seconda pagina dell'applicazione:
```css
<h1>Pagina 2</h1>
<p>Questa è la pagina 2 dell'applicazione.</p>
```
- Salvare il file page2.ejs.
Creare un nuovo file app.js nella cartella di progetto.
Aggiungere il seguente codice per creare una applicazione web con Express che utilizza il layout comune e le viste specifiche:
```javascript
const express = require('express');
const app = express();

app.set('view engine', 'ejs');
app.use(express.static('public'));

app.get('/', (req, res) => {
  res.render('layout', { title: 'Home', content: 'home' });
});

app.get('/page1', (req, res) => {
  res.render('layout', { title: 'Pagina 1', content: 'page1' });
});

app.get('/page2', (req, res) => {
  res.render('layout', { title: 'Pagina 2', content: 'page2' });
});

app.listen(3000, () => {
console.log('Server avviato sulla porta 3000');
});
```

- Salvare il file `app.js`.
Creare una nuova cartella `public` nella cartella di progetto.
Creare un nuovo file `style.css` nella cartella `public`.
Aggiungere il seguente codice CSS per personalizzare lo stile della pagina principale:

```
body {
font-family: Arial, sans-serif;
background-color: #eee;
text-align: center;
padding-top: 50px;
}

h1 {
font-size: 36px;
color: #333;
}

p {
font-size: 18px;
color: #666;
}

header {
background-color: #333;
color: #fff;
padding: 10px;
}

nav ul {
margin: 0;
padding: 0;
list-style: none;
}

nav li {
display: inline-block;
}

nav a {
color: #fff;
text-decoration: none;
padding: 10px;
}

nav a:hover {
background-color: #fff;
color: #333;
}
```

- Salvare il file `style.css`.
Aprire il terminale integrato di Visual Studio Code e digitare `node app.js` per avviare il server web.
Aprire un browser web e digitare `http://localhost:3000` per accedere alla pagina principale dell'applicazione.

In questo esempio, il layout comune viene definito nel file `layout.ejs`, mentre le specifiche viste della pagina sono definite nei file `home.ejs`, `page1.ejs` e `page2.ejs`. Il pacchetto `ejs` viene utilizzato per rendere le pagine HTML dinamiche, mentre la cartella `public` viene utilizzata per ospitare file statici come fogli di stile CSS e immagini

# 3 NODE JS MVC con SQLITE in VISUAL STUDIO CODE per principianti layout con 3 viste di cui 1 vista che verifica se c’è il database altrimenti fa creare il database se non c’è già, 1 vista per amministrare i dati, 1 vista per eliminare il database, ed un unico menu condivisi

- Aprire Visual Studio Code e aprire la cartella di progetto in cui si desidera creare l'applicazione web.
- Digitare il comando npm init nel terminale integrato di Visual Studio Code per inizializzare un nuovo progetto Node.js.
- Digitare npm install express ejs sqlite3 per installare il framework Express, il motore di rendering EJS e il driver per SQLite.
Creare una nuova cartella views nella cartella di progetto.
Creare un nuovo file layout.ejs nella cartella views.
Aggiungere il seguente codice HTML per creare il layout comune dell'applicazione:
```php
<!DOCTYPE html>
<html>
  <head>
    <title><%= title %></title>
  </head>
  <body>
    <header>
      <nav>
        <ul>
          <li><a href="/">Home</a></li>
          <li><a href="/admin">Amministra Dati</a></li>
          <li><a href="/delete">Elimina Database</a></li>
        </ul>
      </nav>
    </header>
    <main>
      <%= content %>
    </main>
  </body>
</html>
```
- Salvare il file layout.ejs.
Creare un nuovo file home.ejs nella cartella views.
Aggiungere il seguente codice HTML per creare la vista della pagina principale dell'applicazione, che verifica la presenza del database:
```php
<h1>Benvenuti nell'applicazione web MVC con SQLite</h1>
<% if (dbExists) { %>
  <p>Il database esiste già.</p>
<% } else { %>
  <p>Il database non esiste ancora. <a href="/create">Crea Database</a></p>
<% } %>
```
- Salvare il file home.ejs.
Creare un nuovo file admin.ejs nella cartella views.
Aggiungere il seguente codice HTML per creare la vista della pagina di amministrazione dei dati dell'applicazione, che permette di visualizzare i dati presenti nel database:
```css
<h1>Amministra Dati</h1>
<table>
  <thead>
    <tr>
      <th>ID</th>
      <th>Nome</th>
      <th>Cognome</th>
    </tr>
  </thead>
  <tbody>
    <% for (let i = 0; i < rows.length; i++) { %>
      <tr>
        <td><%= rows[i].id %></td>
        <td><%= rows[i].name %></td>
        <td><%= rows[i].surname %></td>
      </tr>
    <% } %>
  </tbody>
</table>
```
- Salvare il file admin.ejs.
Creare un nuovo file create.ejs nella cartella views.
Aggiungere il seguente codice HTML per creare la vista della pagina di creazione del database dell'applicazione:

```php
<h1>Crea Database</h1>
<p>Sei sicuro di voler creare il database?</p>
<form method="POST" action="/create">
  <button type="submit">Crea Database</button>
</form>
```
- Salvare il file create.ejs.
Creare un nuovo file delete.ejs nella cartella views.
Aggiungere il seguente codice HTML per creare la vista della pagina di eliminazione del database dell'applicazione:
```php
<h1>Elimina Database</h1>
<p>Sei sicuro di voler eliminare il database?</p>
<form method="POST" action="/delete">
  <button type="submit">Elimina Database</button>
</form>
```
- Salvare il file delete.ejs.
Creare un nuovo file app.js nella cartella di progetto.
Aggiungere il seguente codice per creare il server web, le rotte per le viste e la connessione al database SQLite:
```javascript
const express = require('express');
const ejs = require('ejs');
const sqlite3 = require('sqlite3');

const app = express();

app.set('view engine', 'ejs');

app.use(express.urlencoded({ extended: true }));
app.use(express.static('public'));

const db = new sqlite3.Database('data.db', (err) => {
  if (err) {
    console.error(err.message);
  }
  console.log('Connesso al database SQLite.');
});

app.get('/', (req, res) => {
  db.get('SELECT name FROM sqlite_master WHERE type="table" AND name="users"', (err, row) => {
    if (row) {
      res.render('home', { title: 'Home', dbExists: true });
    } else {
      res.render('home', { title: 'Home', dbExists: false });
    }
  });
});

app.get('/admin', (req, res) => {
  db.all('SELECT * FROM users', [], (err, rows) => {
    if (err) {
      console.error(err.message);
    }
    res.render('admin', { title: 'Amministra Dati', rows: rows });
  });
});

app.get('/create', (req, res) => {
  res.render('create', { title: 'Crea Database' });
});

app.post('/create', (req, res) => {
  db.run('CREATE TABLE IF NOT EXISTS users (id INTEGER PRIMARY KEY AUTOINCREMENT, name TEXT, surname TEXT)', (err) => {
    if (err) {
      console.error(err.message);
    }
    console.log('Tabella utenti creata.');
  });
  res.redirect('/');
});

app.get('/delete', (req, res) => {
  res.render('delete', { title: 'Elimina Database' });
});

app.post('/delete', (req, res) => {
  db.run('DROP TABLE IF EXISTS users', (err) => {
    if (err) {
      console.error(err.message);
    }
    console.log('Tabella utenti eliminata.');
  });
  res.redirect('/');
});

app.listen(3000, () => {
  console.log('Server avviato sulla porta 3000');
});
```
- Salvare il file app.js.
- Aprire il terminale integrato di Visual Studio Code e digitare node app.js per avviare il server web.
- Aprire un browser web e digitare http://localhost:3000 per accedere alla pagina principale dell'applicazione
- Verificare se il database esiste già. Se non esiste, cliccare sul link "Crea Database" per creare il database.
- Cliccare sul link "Amministra Dati" per visualizzare i dati presenti nel database.
- Cliccare sul link "Elimina Database" per eliminare il database.
- Verificare che il database sia stato eliminato. Se non è stato eliminato, chiudere il server web nel terminale integrato di Visual Studio Code e cancellare il file data.db dalla cartella di progetto.
- Modificare i file delle viste e del layout secondo le proprie esigenze, aggiungere ulteriori rotte e funzionalità all'applicazione web MVC con SQLite in Node.js