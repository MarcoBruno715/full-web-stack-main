# creare un database con una tabella e tre campi utilizzando Node.js e SQLite

>Questo codice utilizza il modulo **sqlite3** per creare un **database SQLite** e inserire alcuni dati nella tabella **mytable**.
La prima riga del codice richiede il modulo sqlite3 e utilizza il metodo verbose() per abilitare i messaggi di debug.
La seconda riga istanzia un nuovo oggetto Database che rappresenta il database SQLite denominato **mydb.db**.
La funzione serialize() viene utilizzata per **garantire che tutte le query vengano eseguite in sequenza, una dopo l'altra**.
All'interno della funzione serialize(), viene eseguita una query SQL per creare una nuova tabella denominata mytable, con tre colonne: name di tipo **TEXT**, age di tipo **INTEGER** e city di tipo **TEXT**.
Successivamente, viene preparata una **query SQL** che inserisce tre righe nella tabella mytable, con i valori 'Mario', 30 e 'Roma' per la prima riga, 'Luigi', 25 e 'Napoli' per la seconda riga, e 'Giovanni', 35 e 'Milano' per la terza riga.
viene chiamato il metodo finalize() per completare l'inserimento dei dati nella tabella e viene stampato **un messaggio di conferma sull'inserimento dei dati**.
Infine, il metodo close() viene utilizzato per **chiudere la connessione al database**

- Aprire Visual Studio Code e creare una nuova cartella di progetto.
- Aprire il terminale integrato di Visual Studio Code (Ctrl + Shift + `).
- Inserire il comando **npm init** e seguire le istruzioni per creare un file package.json, che descrive il progetto e le sue dipendenze.
- Installare il pacchetto sqlite3 utilizzando il comando **npm install sqlite3**.
Creare un nuovo file app.js nella cartella di progetto.
Aggiungere il seguente codice per creare un database con una tabella e tre campi:
```javascript
const sqlite3 = require('sqlite3').verbose();

const db = new sqlite3.Database('mydb.db');

db.serialize(() => {
  db.run('CREATE TABLE mytable (name TEXT, age INTEGER, city TEXT)');

  const stmt = db.prepare('INSERT INTO mytable VALUES (?, ?, ?)');
  stmt.run('Mario', 30, 'Roma');
  stmt.run('Luigi', 25, 'Napoli');
  stmt.run('Giovanni', 35, 'Milano');
  stmt.finalize();

  console.log('Dati inseriti correttamente!');
});

db.close();
```
- Salvare il file app.js.
- Aprire il terminale integrato di Visual Studio Code e digitare **node app.js** per eseguire il codice.
- Controllare la console per verificare che i dati siano stati inseriti correttamente nel database.
e

# leggere i dati da un database SQLite utilizzando Node.js

- Aprire Visual Studio Code e aprire la cartella di progetto in cui è stato creato il database SQLite nel precedente esercizio.
- Creare un nuovo file **app_read.js** nella cartella di progetto.
Aggiungere il seguente codice per connettersi al database SQLite e leggere i dati dalla tabella:
```javascript
const sqlite3 = require('sqlite3').verbose();

const db = new sqlite3.Database('mydb.db');

db.all('SELECT * FROM mytable', (err, rows) => {
  if (err) {
    console.error(err.message);
  }

  rows.forEach(row => {
    console.log(row.name, row.age, row.city);
  });
});

db.close();
```
- Salvare il file **app_read.js**.
- Aprire il terminale integrato di Visual Studio Code e digitare node **app_read.js** per eseguire il codice.
- Controllare la console per verificare che i dati siano stati letti correttamente dalla tabella.
In questo esempio, il metodo all() viene utilizzato per eseguire una **query SQL** che seleziona tutti i dati nella tabella. La funzione di callback viene eseguita una volta che la query è stata completata, e i risultati vengono passati come parametro rows. Il metodo forEach() viene utilizzato per iterare sui risultati e visualizzarli nella console.

È possibile modificare la query SQL per selezionare solo i dati specifici necessari, ad esempio utilizzando filtri o ordinamenti

# come aggiornare i dati in un database SQLite utilizzando Node.js

- Aprire Visual Studio Code e aprire la cartella di progetto in cui è stato creato il database SQLite nel precedente esercizio.
- Creare un nuovo file **app_update.js** nella cartella di progetto.
Aggiungere il seguente codice per connettersi al database **SQLite** e aggiornare i dati nella tabella:
```javascript
const sqlite3 = require('sqlite3').verbose();

const db = new sqlite3.Database('mydb.db');

const id = 1;
const newAge = 40;

db.run(`UPDATE mytable SET age = ${newAge} WHERE rowid = ${id}`, err => {
  if (err) {
    console.error(err.message);
  }

  console.log(`Dato con id ${id} aggiornato correttamente!`);
});

db.close();
```
- Salvare il file **app_update.js**.
- Aprire il terminale integrato di Visual Studio Code e digitare node **app_update.js** per eseguire il codice.
- Controllare la console per verificare che i dati siano stati aggiornati correttamente nella tabella.
In questo esempio, il metodo run() viene utilizzato per eseguire una **query SQL che aggiorna un singolo dato nella tabella**. La query utilizza il valore di id per selezionare il dato da aggiornare e il valore di newAge per impostare il nuovo valore dell'età. La funzione di callback viene eseguita una volta che la query è stata completata, e viene visualizzato un messaggio nella console.

È possibile utilizzare altri metodi per aggiornare più dati contemporaneamente o per eliminare dati.

# esempio di come eliminare i dati da un database SQLite

- Aprire Visual Studio Code e aprire la cartella di progetto in cui è stato creato il database SQLite nel precedente esercizio.
- Creare un nuovo file **app_delete.js** nella cartella di progetto.
- Aggiungere il seguente codice per connettersi al database SQLite e eliminare i dati dalla tabella:
```javascript
const sqlite3 = require('sqlite3').verbose();

const db = new sqlite3.Database('mydb.db');

const id = 1;

db.run(`DELETE FROM mytable WHERE rowid = ${id}`, err => {
  if (err) {
    console.error(err.message);
  }

  console.log(`Dato con id ${id} eliminato correttamente!`);
});

db.close();
```
- Salvare il file **app_delete.js**.
- Aprire il terminale integrato di Visual Studio Code e digitare node **app_delete.js** per eseguire il codice.
- Controllare la console per verificare che i dati siano stati eliminati correttamente dalla tabella.
In questo esempio, il metodo run() viene utilizzato per eseguire una query SQL che **elimina un singolo dato dalla tabella**. La query utilizza il valore di id per selezionare il dato da eliminare. La funzione di callback viene eseguita una volta che la query è stata completata, e viene visualizzato un messaggio nella console.

# creare un database con una tabella e tre campi utilizzando Node.js e SQL Server

- Aprire Visual Studio Code e creare una nuova cartella di progetto.
- Aprire il terminale integrato di Visual Studio Code (Ctrl + Shift + `).
- Inserire il comando npm init e seguire le istruzioni per creare un file package.json, che descrive il progetto e le sue dipendenze.
- Installare il pacchetto mssql utilizzando il comando npm install mssql.
Creare un nuovo file **app.js** nella cartella di progetto.
Aggiungere il seguente codice per creare una connessione al database SQL Server e creare una tabella con tre campi:
```javascript
const sql = require('mssql');

const config = {
  user: 'username',
  password: 'password',
  server: 'localhost',
  database: 'mydb',
  options: {
    trustServerCertificate: true,
  },
};

const pool = new sql.ConnectionPool(config);

pool.connect(err => {
  if (err) {
    console.error(err);
  } else {
    const request = new sql.Request(pool);

    request.query(`
      CREATE TABLE mytable (
        id INT PRIMARY KEY,
        name VARCHAR(50),
        age INT
      )
    `, (err, result) => {
      if (err) {
        console.error(err);
      } else {
        console.log('Tabella creata correttamente!');
      }

      pool.close();
    });
  }
});
```
- Salvare il file **app.js**.
- Aprire il terminale integrato di Visual Studio Code e digitare **node app.js** per eseguire il codice.
- Controllare la console per verificare che la tabella sia stata creata

# come leggere i dati da un database SQL

- Aprire Visual Studio Code e aprire la cartella di progetto in cui è stato creato il database SQL Server nel precedente esercizio.
- Creare un nuovo file **app_read.js** nella cartella di progetto.
Aggiungere il seguente codice per connettersi al database SQL Server e leggere i dati dalla tabella:
```javascript
const sql = require('mssql');

const config = {
  user: 'username',
  password: 'password',
  server: 'localhost',
  database: 'mydb',
  options: {
    trustServerCertificate: true,
  },
};

const pool = new sql.ConnectionPool(config);

pool.connect(err => {
  if (err) {
    console.error(err);
  } else {
    const request = new sql.Request(pool);

    request.query('SELECT * FROM mytable', (err, result) => {
      if (err) {
        console.error(err);
      } else {
        console.log(result.recordset);
      }

      pool.close();
    });
  }
});
```
- Salvare il file **app_read.js**.
- Aprire il terminale integrato di Visual Studio Code e digitare node app.js per eseguire il codice.
Controllare la console per verificare che i dati siano stati letti correttamente dalla tabella.
In questo esempio, il pacchetto mssql viene utilizzato per creare una connessione al database SQL Server e eseguire una query che seleziona tutti i dati nella tabella. La funzione di callback viene eseguita una volta che la query è stata completata, e i risultati vengono passati

# come aggiornare i dati in un database SQL

- Aprire Visual Studio Code e aprire la cartella di progetto in cui è stato creato il database SQL Server nel primo esercizio.
- Creare un nuovo file **app_update.js** nella cartella di progetto.
Aggiungere il seguente codice per connettersi al database SQL Server e aggiornare i dati nella tabella:
```javascript
const sql = require('mssql');

const config = {
  user: 'username',
  password: 'password',
  server: 'localhost',
  database: 'mydb',
  options: {
    trustServerCertificate: true,
  },
};

const pool = new sql.ConnectionPool(config);

pool.connect(err => {
  if (err) {
    console.error(err);
  } else {
    const request = new sql.Request(pool);

    request.query(`
      UPDATE mytable
      SET age = 30
      WHERE id = 1
    `, (err, result) => {
      if (err) {
        console.error(err);
      } else {
        console.log('Dati aggiornati correttamente!');
      }

      pool.close();
    });
  }
});
```
- Salvare il file **app_update.js**.
- Aprire il terminale integrato di Visual Studio Code e digitare node app.js per eseguire il codice.
Controllare la console per verificare che i dati siano stati aggiornati correttamente nella tabella.
In questo esempio, il pacchetto mssql viene utilizzato per creare una connessione al database SQL Server e eseguire una query che aggiorna il valore di un campo nella tabella. La query utilizza la clausola WHERE per selezionare il dato specifico da aggiornare, in questo caso utilizzando l'id = 1. La funzione di callback viene eseguita una volta che la query è stata completata, e viene visualizzato un messaggio nella console.

È possibile utilizzare altri metodi per aggiornare più dati contemporaneamente o per aggiornare dati basati su altri filtri.

Questo esercizio è solo un esempio di base per aggiornare i dati in un database SQL Server utilizzando Node.js in Visual Studio Code. È possibile personalizzare ulteriormente il codice in base alle esigenze del progetto, ad esempio utilizzando filtri più complessi o aggiungendo altre funzionalità di aggiornamento dei dati

# come eliminare i dati da un database SQL Server utilizzando Node.js

- Aprire Visual Studio Code e aprire la cartella di progetto in cui è stato creato il database SQL Server nel primo esercizio.
Creare un nuovo file **app_delete.js** nella cartella di progetto.
- Aggiungere il seguente codice per connettersi al database SQL Server ed eliminare i dati nella tabella:
```javascript
const sql = require('mssql');

const config = {
  user: 'username',
  password: 'password',
  server: 'localhost',
  database: 'mydb',
  options: {
    trustServerCertificate: true,
  },
};

const pool = new sql.ConnectionPool(config);

pool.connect(err => {
  if (err) {
    console.error(err);
  } else {
    const request = new sql.Request(pool);

    request.query(`
      DELETE FROM mytable
      WHERE id = 1
    `, (err, result) => {
      if (err) {
        console.error(err);
      } else {
        console.log('Dati eliminati correttamente!');
      }

      pool.close();
    });
  }
});
```
- Salvare il file **app_delete.js**.
- Aprire il terminale integrato di Visual Studio Code e digitare node app.js per eseguire il codice.
- Controllare la console per verificare che i dati siano stati eliminati correttamente dalla tabella.
In questo esempio, il pacchetto mssql viene utilizzato per creare una connessione al database SQL Server e eseguire una query che elimina un dato specifico dalla tabella. La query utilizza la clausola WHERE per selezionare il dato da eliminare, in questo caso utilizzando l'id = 1. La funzione di callback viene eseguita una volta che la query è stata completata, e viene visualizzato un messaggio nella console.

È possibile utilizzare altri metodi per eliminare più dati contemporaneamente o per eliminare dati basati su altri filtri.

Questo esercizio è solo un esempio di base per eliminare i dati da un database SQL Server utilizzando Node.js in Visual Studio Code. È possibile personalizzare ulteriormente il codice in base alle esigenze del progetto, ad esempio utilizzando filtri più complessi o aggiungendo altre funzionalità di eliminazione dei dati