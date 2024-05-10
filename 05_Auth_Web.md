# creare un'interfaccia web per inserire dati in un database SQLit

Per creare un'interfaccia web per inserire dati in un database SQLite utilizzando JavaScript, puoi fare uso di framework come Node.js e Express.js per gestire il lato server e HTML, CSS e JavaScript per la parte client.

Installa le dipendenze necessarie:

Express.js: **npm install express**
sqlite3: **npm install sqlite3**

Crea un file **index.js** e incolla il seguente codice:
```javascript
const express = require('express');
const sqlite3 = require('sqlite3').verbose();

const app = express();
const db = new sqlite3.Database('mydb.db');

// Crea la tabella se non esiste
db.serialize(() => {
  db.run('CREATE TABLE IF NOT EXISTS mytable (name TEXT, age INTEGER, city TEXT)');
});

app.use(express.urlencoded({ extended: true }));
app.use(express.static('public'));

// Route per la pagina principale
app.get('/', (req, res) => {
  res.sendFile(__dirname + '/public/index.html');
});

// Route per gestire il submit del form
app.post('/submit', (req, res) => {
  const { name, age, city } = req.body;
  const stmt = db.prepare('INSERT INTO mytable VALUES (?, ?, ?)');
  stmt.run(name, age, city);
  stmt.finalize();
  res.send('Dati inseriti correttamente!');
});

// Avvia il server
app.listen(3000, () => {
  console.log('Server avviato sulla porta 3000');
});
```

Crea una cartella public nella stessa directory del file index.js e al suo interno crea un file **index.html** con il seguente contenuto
```xml
<!DOCTYPE html>
<html>
<head>
  <title>Inserimento dati nel database</title>
  <style>
    body {
      font-family: Arial, sans-serif;
    }
    form {
      margin-bottom: 10px;
    }
  </style>
</head>
<body>
  <h1>Inserimento dati nel database</h1>
  <form action="/submit" method="POST">
    <label for="name">Nome:</label>
    <input type="text" id="name" name="name" required><br>

    <label for="age">Età:</label>
    <input type="number" id="age" name="age" required><br>

    <label for="city">Città:</label>
    <input type="text" id="city" name="city" required><br>

    <button type="submit">Inserisci</button>
  </form>
</body>
</html>
```

# aggiugere una pagina per la visualizzazione degli inserimenti con ejs

Per aggiungere una pagina per visualizzare i dati inseriti nel database SQLite, puoi seguire i seguenti passaggi:

>Aggiungi una nuova route nel file index.js per gestire la visualizzazione dei dati:
```javascript
// Route per visualizzare i dati
app.get('/data', (req, res) => {
  db.all('SELECT * FROM mytable', (err, rows) => {
    if (err) {
      res.status(500).send('Errore nel recupero dei dati dal database');
    } else {
      res.render('data', { rows });
    }
  });
});
```
>Crea una cartella views nella stessa directory del file index.js e al suo interno crea un file data.ejs con il seguente contenuto
```html
<!DOCTYPE html>
<html>
<head>
  <title>Dati inseriti</title>
  <style>
    body {
      font-family: Arial, sans-serif;
    }
    table {
      border-collapse: collapse;
      width: 100%;
    }
    th, td {
      border: 1px solid #ddd;
      padding: 8px;
    }
    th {
      background-color: #f2f2f2;
    }
  </style>
</head>
<body>
  <h1>Dati inseriti</h1>
  <table>
    <tr>
      <th>Nome</th>
      <th>Età</th>
      <th>Città</th>
    </tr>
    <% rows.forEach(row => { %>
    <tr>
      <td><%= row.name %></td>
      <td><%= row.age %></td>
      <td><%= row.city %></td>
    </tr>
    <% }); %>
  </table>
</body>
</html>
```
Installa il modulo ejs eseguendo il comando **npm install ejs**.

>Modifica il file index.js per utilizzare il motore di visualizzazione EJS:

```javascript
const express = require('express');
const sqlite3 = require('sqlite3').verbose();
const ejs = require('ejs');

const app = express();
const db = new sqlite3.Database('mydb.db');

// Crea la tabella se non esiste
db.serialize(() => {
  db.run('CREATE TABLE IF NOT EXISTS mytable (name TEXT, age INTEGER, city TEXT)');
});

app.use(express.urlencoded({ extended: true }));
app.use(express.static('public'));
app.set('view engine', 'ejs'); // Imposta EJS come motore di visualizzazione

// ... Resto del codice ...

// Avvia il server
app.listen(3000, () => {
  console.log('Server avviato sulla porta 3000');
});
```
Avvia l'applicazione eseguendo il comando **node index.js**.

Ora puoi accedere alla pagina dei dati inseriti aprendo il tuo browser e visitando l'indirizzo http://localhost:3000/data.

Vedrai una tabella che mostra i dati inseriti nel database SQLite.

Assicurati di avere il file mydb.db nella stessa directory del file index.js e che il modulo SQLite3 e EJS siano installati correttamente

# creare un'interfaccia web per modificare i dati in un database SQLite utilizzando JavaScript

Aggiungi ad index.js la route per la modifica
```javascript
// Route per la pagina di modifica
app.get('/edit', (req, res) => {
  res.sendFile(__dirname + '/public/edit.html');
});

// Route per gestire la modifica dei dati
app.post('/edit', (req, res) => {
  const { id, newAge } = req.body;
  const stmt = db.prepare('UPDATE mytable SET age = ? WHERE rowid = ?');
  stmt.run(newAge, id, err => {
    if (err) {
      res.status(500).send('Errore nella modifica dei dati');
    } else {
      res.send(`Dato con id ${id} aggiornato correttamente!`);
    }
  });
  stmt.finalize();
});
```

Crea il file edit.html nella cartella 'public' inserendo il seguente contenuto:
```html
<!DOCTYPE html>
<html>
<head>
<title>Inserimento dati nel database</title>
<style>
    body {
    font-family: Arial, sans-serif;
    }
    form {
    margin-bottom: 10px;
    }
</style>
</head>
<body>
<h1>Inserimento dati nel database</h1>
<form action="/edit" method="POST">
  <label for="id">ID:</label>
  <input type="number" id="id" name="id" required><br>

  <label for="newAge">Nuova età:</label>
  <input type="number" id="newAge" name="newAge" required><br>

  <button type="submit">Modifica</button>
</form>
</body>
</html>
```
Avvia l'applicazione eseguendo il comando **node index.js**.

Ora puoi aprire il tuo browser e accedere all'indirizzo http://localhost:3000 per visualizzare il modulo di inserimento dei dati e http://localhost:3000/edit per visualizzare il modulo di modifica dei dati.

Quando invii il modulo di modifica, il dato corrispondente verrà aggiornato nel database SQLite e riceverai una conferma di successo nella pagina

# aggiungere un'interfaccia web per gestire l'eliminazione di un dato nel database SQLite

Aggiungi una nuova route nel file index.js per gestire l'eliminazione del dato:
```javascript
// Route per la pagina di eliminazione
app.get('/delete', (req, res) => {
  res.sendFile(__dirname + '/public/delete.html');
});

// Route per gestire l'eliminazione dei dati
app.post('/delete', (req, res) => {
  const { id } = req.body;
  const stmt = db.prepare('DELETE FROM mytable WHERE rowid = ?');
  stmt.run(id, err => {
    if (err) {
      res.status(500).send('Errore nell\'eliminazione del dato');
    } else {
      res.send(`Dato con id ${id} eliminato correttamente!`);
    }
  });
  stmt.finalize();
});
```
Crea un file delete.html nella cartella public con il seguente contenuto:
```html
<!DOCTYPE html>
<html>
<head>
  <title>Eliminazione dato dal database</title>
  <style>
    body {
      font-family: Arial, sans-serif;
    }
    form {
      margin-bottom: 10px;
    }
  </style>
</head>
<body>
  <h1>Eliminazione dato dal database</h1>
  <form action="/delete" method="POST">
    <label for="id">ID:</label>
    <input type="number" id="id" name="id" required><br>

    <button type="submit">Elimina</button>
  </form>
</body>
</html>
```
Avvia l'applicazione eseguendo il comando **node index.js**.

Ora puoi accedere alla pagina di eliminazione aprendo il tuo browser e visitando l'indirizzo http://localhost:3000/delete.
Vedrai un modulo per inserire l'ID del dato che desideri eliminare.
Quando invii il modulo, il dato corrispondente verrà eliminato dal database SQLite e riceverai una conferma di successo nella pagina
# aggiungere un'interfaccia web per il login degli utenti

Aggiungi una nuova route nel file index.js per gestire il login degli utenti:
```javascript
// Route per la pagina di login
app.get('/login', (req, res) => {
  res.sendFile(__dirname + '/public/login.html');
});

// Route per gestire il login degli utenti
app.post('/login', (req, res) => {
  const { name, age } = req.body;
  const stmt = db.prepare('SELECT COUNT(*) AS count FROM mytable WHERE name = ? AND age = ?');
  stmt.get(name, age, (err, row) => {
    if (err) {
      res.status(500).send('Errore nel login');
    } else {
      if (row.count > 0) {
        res.send('Accesso riuscito!');
      } else {
        res.send('Credenziali non valide');
      }
    }
  });
  stmt.finalize();
});
```
Crea un file login.html nella cartella public con il seguente contenuto:
```html
<!DOCTYPE html>
<html>
<head>
  <title>Login</title>
  <style>
    body {
      font-family: Arial, sans-serif;
    }
    form {
      margin-bottom: 10px;
    }
  </style>
</head>
<body>
  <h1>Login</h1>
  <form action="/login" method="POST">
    <label for="name">Nome:</label>
    <input type="text" id="name" name="name" required><br>

    <label for="age">Età:</label>
    <input type="number" id="age" name="age" required><br>

    <button type="submit">Login</button>
  </form>
</body>
</html>
```
Avvia l'applicazione eseguendo il comando **node index.js**.



Ora puoi accedere alla pagina di login aprendo il tuo browser e visitando l'indirizzo http://localhost:3000/login.

# reindirizzare l'utente su diverse pagine HTML dopo il login

Per reindirizzare l'utente su diverse pagine HTML dopo il login, puoi seguire questi passaggi:

Aggiorna la route di gestione del login nel file index.js (sostituisci) per effettuare il reindirizzamento:
```javascript
// Route per gestire il login degli utenti
app.post('/login', (req, res) => {
  const { name, age } = req.body;
  const stmt = db.prepare('SELECT COUNT(*) AS count FROM mytable WHERE name = ? AND age = ?');
  stmt.get(name, age, (err, row) => {
    if (err) {
      res.status(500).send('Errore nel login');
    } else {
      if (row.count > 0) {
        // Reindirizza l'utente a diverse pagine in base alle condizioni
        if (name === 'admin') {
          res.redirect('/admin-page.html');
        } else if (age > 18) {
          res.redirect('/premium-page.html');
        } else {
          res.redirect('/user-page.html');
        }
      } else {
        res.send('Credenziali non valide');
      }
    }
  });
  stmt.finalize();
});
```
Avvia l'applicazione eseguendo il comando **node index.js**.

Ora, quando un utente effettua il login, verrà reindirizzato a diverse pagine HTML in base alle condizioni specificate.

Se il nome inserito è "admin", l'utente sarà reindirizzato a **admin-page.html**.

Se l'età è superiore a 18, l'utente sarà reindirizzato a **premium-page.html**.

In caso contrario, l'utente sarà reindirizzato a **user-page.html**

# impedire l'accesso alla pagina admin-page.htm

impedire l'accesso alla pagina admin-page.html per gli utenti non amministratori, puoi utilizzare middleware per verificare l'autenticazione e i privilegi dell'utente.

Aggiorna il file index.js per includere il middleware di autenticazione:
```javascript
// Funzione middleware per verificare l'autenticazione
const authenticate = (req, res, next) => {
  const { name, age } = req.body;
  const stmt = db.prepare('SELECT COUNT(*) AS count FROM mytable WHERE name = ? AND age = ?');
  stmt.get(name, age, (err, row) => {
    if (err) {
      res.status(500).send('Errore nel login');
    } else {
      if (row.count > 0) {
        // Utente autenticato, passa al prossimo middleware
        req.user = { name, age };
        next();
      } else {
        res.send('Credenziali non valide');
      }
    }
  });
  stmt.finalize();
};

// Middleware per verificare se l'utente è un amministratore
const isAdmin = (req, res, next) => {
  const { name } = req.user;
  if (name === 'admin') {
    // L'utente è un amministratore, passa al prossimo middleware
    next();
  } else {
    res.status(403).send('Accesso negato');
  }
};

// Route per la pagina di amministrazione
app.get('/admin-page.html', isAdmin, (req, res) => {
  res.sendFile(__dirname + '/public/admin-page.html');
});
```


Avvia l'applicazione eseguendo il comando **node index.js**.