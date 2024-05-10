# autenticazione utilizzando Node.js, Express e un file JSON per memorizzare le credenziali degli utenti.

- admin.html: La pagina vuota riservata all'amministratore.
- index.html: I moduli di accesso e registrazione.
- user.html: La pagina vuota riservata all'utente.
- users.json: Il file JSON che contiene i dati dell'utente (prima di implementare SQLite).
- login.js: Il codice JavaScript frontend per gestire i submit dei moduli di accesso e registrazione.
- package.json: Contiene i metadati del tuo progetto, come le dipendenze.
- package-lock.json: File generato automaticamente che memorizza la versione esatta dei pacchetti installati.
- server.js: Il file principale che imposta e avvia il server Express.js. Contiene la logica dell'applicazione, le query del database e la gestione delle rotte.


 **Quindi, crea una nuova directory per il tuo progetto e inizializzala con un file package.json:**


- mkdir simple-auth
- cd simple-auth
- npm init -y


 **Installa le dipendenze:**


Avrai bisogno di Express per gestire le richieste del server e body-parser per analizzare i dati JSON:

- npm install express body-parser

Crea un file JSON per le credenziali degli utenti:
Crea un nuovo file chiamato users.json nella directory del tuo progetto:
```json
{
  "users": [
    {
      "username": "user1",
      "password": "password1"
    },
    {
      "username": "user2",
      "password": "password2"
    }
  ]
}
```


 **Crea un nuovo file chiamato server.js nella directory del tuo progetto:**

```javascript
const express = require('express');
const bodyParser = require('body-parser');
const users = require('./users.json');

const app = express();
app.use(bodyParser.json());

// Middleware to check authentication
function isAuthenticated(req, res, next) {
  const { username, password } = req.body;
  const user = users.users.find(
    (user) => user.username === username && user.password === password
  );

  if (user) {
    next();
  } else {
    res.status(401).json({ message: 'Unauthorized access' });
  }
}

// Authenticated route
app.post('/protected', isAuthenticated, (req, res) => {
  res.json({ message: 'You have accessed protected content' });
});

// Start the server
const port = process.env.PORT || 3000;
app.listen(port, () => console.log(`Server listening on port ${port}`));
```

 **Fai partire il tuo server eseguendo il seguente comando:**


- node server.js

Ora il tuo server sarà in esecuzione sulla porta 3000, e puoi accedere alla rotta protetta inviando una richiesta POST con le credenziali corrette:

- Apri un nuovo terminale e esegui il seguente comando:

>curl -X POST -H "Content-Type: application/json" -d '{"username": "user1", "password": "password1"}' http://localhost:3000/protected

- Se le credenziali sono corrette, il server risponderà con un messaggio JSON indicando che hai acceduto al contenuto protetto. Se le credenziali sono sbagliate, riceverai uno stato 401 Unauthorized con un messaggio JSON.

Tieni presente che questo approccio non è sicuro per gli ambienti di produzione o per i dati sensibili.
Per una maggiore sicurezza, considera l'utilizzo di un metodo di autenticazione adeguato, come JWT o OAuth, e un vero database per memorizzare le credenziali degli utenti.


# JWT


Per implementare l'autenticazione basata su JWT nella tua applicazione Node.js, devi installare la libreria jsonwebtoken:

- npm install jsonwebtoken


 **Dopo aver installato la libreria jsonwebtoken, modifica file server.js per includere l'autenticazione basata su JWT:**

```javascript
const express = require('express');
const bodyParser = require('body-parser');
const jwt = require('jsonwebtoken');
const users = require('./users.json');

const app = express();
app.use(bodyParser.json());

const SECRET_KEY = 'your-secret-key'; // Replace this with a more secure key in a production environment

// Login route
app.post('/login', (req, res) => {
  const { username, password } = req.body;
  const user = users.users.find(
    (user) => user.username === username && user.password === password
  );

  if (user) {
    // Generate and sign the JWT
    const token = jwt.sign({ username: user.username }, SECRET_KEY, {
      expiresIn: '1h',
    });

    res.json({ message: 'Authentication successful', token });
  } else {
    res.status(401).json({ message: 'Invalid credentials' });
  }
});

// Middleware to check authentication
function isAuthenticated(req, res, next) {
  const token = req.headers['authorization'];

  if (token) {
    jwt.verify(token, SECRET_KEY, (err, decoded) => {
      if (err) {
        return res.status(401).json({ message: 'Unauthorized access' });
      }
      req.decoded = decoded;
      next();
    });
  } else {
    res.status(401).json({ message: 'No token provided' });
  }
}

// Authenticated route
app.get('/protected', isAuthenticated, (req, res) => {
  res.json({ message: 'You have accessed protected content' });
});

// Start the server
const port = process.env.PORT || 3000;
app.listen(port, () => console.log(`Server listening on port ${port}`));
```

- Adesso, quando un utente effettua l'accesso con le credenziali corrette, il server risponderà con un token JWT. Il client deve includere questo token nell'intestazione Authorization delle richieste alle rotte protette.


 **Per testare l'autenticazione, puoi usare curl per simulare il processo di accesso:**


>curl -X POST -H "Content-Type: application/json" -d '{"username": "user1", "password": "password1"}' http://localhost:3000/login

- Bisogna ricordarsi di interrompere ed avviare il server con il comando: node server.js
- Se le credenziali sono corrette, riceverai una risposta JSON contenente il token JWT.


 **Per accedere alla rotta protetta, includi il token nell'intestazione Authorization:**


>curl -X GET -H "Authorization: your-jwt-token" http://localhost:3000/protected

>curl -X GET -H "Authorization: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxIiwiaWF0IjoxNjc5NjUxOTAxLCJleHAiOjE2Nzk2NTU1MDF9.y875_GQWYGKA5UiM1mO6MK6SBVnETx9lP-TdZypMDQk" http://localhost:3000/protected

Cambia your-jwt-token con il token ricevuto nella risposta di accesso.

Ricorda che memorizzare le password come testo semplice in un file JSON, come mostrato in questo esempio, non è sicuro. In un'applicazione reale, dovresti memorizzare le password hash in un database e utilizzare un metodo più sicuro per la gestione delle credenziali degli utenti.



 **Aggiungi un ruolo di amministratore**


Per aggiungere un ruolo di amministratore al tuo sistema di autenticazione, puoi modificare il file users.json per includere un campo ruolo per ogni utente. Poi, crea una nuova funzione middleware per controllare il ruolo di amministratore.


 **Prima di tutto, aggiorna il file users.json per includere le informazioni sul ruolo:**

```json
{
  "users": [
    {
      "username": "user1",
      "password": "password1",
      "role": "user"
    },
    {
      "username": "user2",
      "password": "password2",
      "role": "user"
    },
    {
      "username": "admin",
      "password": "adminpassword",
      "role": "admin"
    }
  ]
}
```

 **Poi, modifica il file server.js per includere il ruolo di amministratore nel payload JWT**


crea una funzione middleware per controllare il ruolo di amministratore:
```javascript
const express = require('express');
const bodyParser = require('body-parser');
const jwt = require('jsonwebtoken');
const users = require('./users.json');

const app = express();
app.use(bodyParser.json());

const SECRET_KEY = 'your-secret-key'; // Replace this with a more secure key in a production environment

// Login route
app.post('/login', (req, res) => {
  const { username, password } = req.body;
  const user = users.users.find(
    (user) => user.username === username && user.password === password
  );

  if (user) {
    // Generate and sign the JWT with the user role
    const token = jwt.sign({ username: user.username, role: user.role }, SECRET_KEY, {
      expiresIn: '1h',
    });

    res.json({ message: 'Authentication successful', token });
  } else {
    res.status(401).json({ message: 'Invalid credentials' });
  }
});

// Middleware to check authentication
function isAuthenticated(req, res, next) {
  const token = req.headers['authorization'];

  if (token) {
    jwt.verify(token, SECRET_KEY, (err, decoded) => {
      if (err) {
        return res.status(401).json({ message: 'Unauthorized access' });
      }
      req.decoded = decoded;
      next();
    });
  } else {
    res.status(401).json({ message: 'No token provided' });
  }
}

// Middleware to check for admin role
function isAdmin(req, res, next) {
  if (req.decoded && req.decoded.role === 'admin') {
    next();
  } else {
    res.status(403).json({ message: 'Access forbidden: not an administrator' });
  }
}

// Authenticated route
app.get('/protected', isAuthenticated, (req, res) => {
  res.json({ message: 'You have accessed protected content' });
});

// Admin route
app.get('/admin', isAuthenticated, isAdmin, (req, res) => {
  res.json({ message: 'Welcome to the admin area' });
});

// Start the server
const port = process.env.PORT || 3000;
app.listen(port, () => console.log(`Server listening on port ${port}`));
```

Ora, solo gli utenti con il ruolo 'amministratore' possono accedere alla rotta /admin.


 **Per testare questo, effettua l'accesso come amministratore usando curl:**


>curl -X POST -H "Content-Type: application/json" -d '{"username": "admin", "password": "adminpassword"}' http://localhost:3000/login

Se le credenziali sono corrette verrà ricevuto il token admin


 **Per accedere alla rotta amministratore, includi il token nell'intestazione Authorization:**


>curl -X GET -H "Authorization: your-jwt-token" http://localhost:3000/admin

>curl -X GET -H "Authorization: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImFkbWluIiwicm9sZSI6ImFkbWluIiwiaWF0IjoxNjc5NjUyMjg2LCJleHAiOjE2Nzk2NTU4ODZ9.QELd1A72bowiul94iQ38Prh5AUfpHLiWAUvHPAEtagY" http://localhost:3000/admin


 **Crea un frontend per il tuo sistema di autenticazion**


Per creare un frontend semplice con una pagina di accesso accessibile a tutti gli utenti e pagine riservate separate per amministratori e utenti, puoi seguire i seguenti passaggi:


 **Installa il middleware express-static per servire i file statici:**


- npm install serve-static


 **Crea una cartella pubblica nella directory del progetto**


all'interno di quella cartella 'public', crea tre file HTML: index.html, admin.html e user.html.

Crea la pagina di accesso per gli utenti

In questo esempio, la pagina di accesso è index.html. Includi un modulo di accesso con un campo di testo per l'username e un campo di password. Includi anche un pulsante di invio per inviare il modulo di accesso.
In questo esempio, il modulo di accesso è inviato tramite una richiesta POST a /login.

index.html (Login Page):
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Login</title>
</head>
<body>
  <h1>Login</h1>
  <form id="login-form">
    <label for="username">Username:</label>
    <input type="text" id="username" name="username" required>
    <br>
    <label for="password">Password:</label>
    <input type="password" id="password" name="password" required>
    <br>
    <input type="submit" value="Login">
  </form>
  <p id="message"></p>
  <script src="login.js"></script>
</body>
</html>
```
admin.html (Admin Page):
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Admin Page</title>
</head>
<body>
  <h1>Welcome to the Admin Page</h1>
  <script src="auth.js"></script>
</body>
</html>
```
user.html (User Page):
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>User Page</title>
</head>
<body>
  <h1>Welcome to the User Page</h1>
  <script src="auth.js"></script>
</body>
</html>
```

 **Crea un file login.js nella cartella pubblica per gestire l'invio del modulo di accesso:**

```javascript
document.getElementById('login-form').addEventListener('submit', async (e) => {
  e.preventDefault();

  const username = document.getElementById('username').value;
  const password = document.getElementById('password').value;

  try {
    const response = await fetch('/login', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify({ username, password }),
    });

    if (response.status === 200) {
      const data = await response.json();
      localStorage.setItem('token', data.token);
      if (data.token) {
        const decoded = atob(data.token.split('.')[1]);
        const payload = JSON.parse(decoded);
        if (payload.role === 'admin') {
          window.location.href = '/admin.html';
        } else {
          window.location.href = '/user.html';
        }
      }
    } else {
      document.getElementById('message').innerText = 'Invalid credentials';
    }
  } catch (error) {
    console.error('Error:', error);
  }
});
```

 **Crea un file auth.js nella cartella pubblica per gestire l'autenticazione per le pagine utente e ammin**

```javascript
document.addEventListener('DOMContentLoaded', async () => {
  const token = localStorage.getItem('token');

  if (!token) {
    window.location.href = '/index.html';
    return;
  }

  try {
    const response = await fetch('/protected', {
      method: 'GET',
      headers: {
        'Authorization': token,
      },
    });

    if (response.status !== 200) {
      localStorage.removeItem('token');
      window.location.href = '/index.html';
      return;
    }

    const decoded = atob(token.split('.')[1]);
    const payload = JSON.parse(decoded);
    if (payload.role === 'admin' && window.location.pathname !== '/admin.html') {
      window.location.href = '/admin.html';
    } else if (payload.role === 'user' && window.location.pathname !== '/user.html') {
      window.location.href = '/user.html';
    }
  } catch (error) {
    console.error('Error:', error);
  }
});
```

 **Aggiorna il file server.js per servire i file statici nella cartella pubblica e aggiungi la rotta /logout:**

```javascript
const express = require('express');
const bodyParser = require('body-parser');
const jwt = require('jsonwebtoken');
const users = require('./users.json');
const serveStatic = require('serve-static');

const app = express();
app.use(bodyParser.json());
app.use(serveStatic('public'));

// ... (rest of your code)

// Logout route
app.get('/logout', (req, res) => {
  res.clearCookie('token');
  res.redirect('/index.html');
});

// Start the server
const port = process.env.PORT || 3000;
app.listen(port, () => console.log(`Server listening on port ${port}`));
```
Adesso, dovresti avere una pagina di accesso accessibile a tutti gli utenti in /index.html. Dopo un accesso riuscito, gli utenti saranno reindirizzati alla pagina amministrativa in /admin.html o alla pagina utente in /user.html, a seconda del loro ruolo. L'accesso non autorizzato alla pagina amministrativa o utente reindirizzerà l'utente alla pagina di accesso.


 **Test dell'applicazione.**


Per testare l'applicazione esegui il server con node server.js e apri il browser a http://localhost:3000/index.html

Inserisci le credenziali di amministratore (username: admin, password: adminpassword) e premi il pulsante Login.
# SQLITE

 **Crea il ‘CreateDb’ JAVASCRIPT per creare il db SQLite**


Per creare un database SQLite utilizzando JavaScript in un ambiente Node.js, avrai bisogno del pacchetto sqlite3.


 **Prima, installa il pacchetto utilizzando npm:**


>npm install sqlite3


 **Poi, crea un file denominato createDb.js**


aggiungi il seguente codice per creare un database SQLite e una tabella denominata users:
```javascript
const sqlite3 = require('sqlite3').verbose();

const createDb = () => {
  const db = new sqlite3.Database('./myDatabase.db', (err) => {
    if (err) {
      console.error(err.message);
    }
    console.log('Connected to the myDatabase SQLite database.');
  });

  db.serialize(() => {
    db.run(`CREATE TABLE IF NOT EXISTS users (
              id INTEGER PRIMARY KEY,
              username TEXT NOT NULL UNIQUE,
              password TEXT NOT NULL,
              role TEXT NOT NULL
            )`, (err) => {
      if (err) {
        console.error(err.message);
      } else {
        console.log("Users table created successfully.");
      }
    });
  });

  db.close((err) => {
    if (err) {
      console.error(err.message);
    }
    console.log('Closed the database connection.');
  });
};

createDb();
```
Questo script crea un nuovo file di database SQLite denominato myDatabase.db se non esiste e una tabella utenti con colonne per id, username, password e ruolo. La tabella verrà creata solo se non esiste già.


 **Per eseguire lo script createDb, esegui il seguente comando nel terminale:**


>node createDb.js

Dopo l'esecuzione dello script, dovresti vedere un nuovo file myDatabase.db nella directory del progetto. Ora puoi utilizzare questo database SQLite per memorizzare i dati utente e gestire l'autenticazione utente.



 **Crea lo script ‘AddUsers’ JAVASCRIPT per inserire 3 utenti**


 crea un file denominato addUsers.js
```javascript
const sqlite3 = require('sqlite3').verbose();

const db = new sqlite3.Database('./myDatabase.db', (err) => {
  if (err) {
    console.error(err.message);
  }
  console.log('Connected to the myDatabase SQLite database.');
});

const addUsers = () => {
  const users = [
    { username: 'user1', password: 'password1', role: 'user' },
    { username: 'user2', password: 'password2', role: 'user' },
    { username: 'admin', password: 'adminpassword', role: 'admin' },
  ];

  const insertUser = db.prepare('INSERT INTO users (username, password, role) VALUES (?, ?, ?)');

  users.forEach((user) => {
    insertUser.run(user.username, user.password, user.role, (err) => {
      if (err) {
        console.error(err.message);
      } else {
        console.log(`User ${user.username} added successfully`);
      }
    });
  });

  insertUser.finalize();
};

addUsers();

db.close((err) => {
  if (err) {
    console.error(err.message);
  }
  console.log('Closed the database connection.');
});
```

 **Per eseguire lo script addUsers e inserire gli 3 utenti nel database, esegui il seguente comando nel terminale:**


>node addUsers.js

Quando esegui lo script, gli utenti verranno aggiunti alla tabella utenti nel database SQLite myDatabase.db e puoi testare la funzionalità di accesso utilizzando queste credenziali.






 **Adesso, modificare server.js per utilizzare il database SQLite per autenticazione utente invece del file users.json**


Aggiungeremo anche una rotta di registrazione per consentire agli utenti di registrarsi.

Aggiorna il file server.js con le seguenti modifiche:

Importa il pacchetto sqlite3 richiesto:

>const sqlite3 = require('sqlite3').verbose();

Sosituisci la seguente riga:

>const users = require('./users.json');

Con il seguente codice per creare una nuova connessione al database:

>const db = new sqlite3.Database('./myDatabase.db', (err) => {
  if (err) {
    console.error(err.message);
  }
  console.log('Connected to the myDatabase SQLite database.');
});

Aggiorna /login per interrogare il database SQLite:
```javascript
// Login route
app.post('/login', (req, res) => {
  const { username, password } = req.body;

  db.get('SELECT * FROM users WHERE username = ?', [username], (err, user) => {
    if (err) {
      console.error(err.message);
      return res.status(500).json({ message: 'Internal server error' });
    }

    if (user && user.password === password) {
      const token = jwt.sign({ username: user.username, role: user.role }, SECRET_KEY, {
        expiresIn: '1h',
      });

      res.json({ message: 'Authentication successful', token });
    } else {
      res.status(401).json({ message: 'Invalid credentials' });
    }
  });
});
```
Aggiungi /register per inserire nuovi utenti nel database SQLite:
```javascript
// Register route
app.post('/register', (req, res) => {
  const { username, password, role } = req.body;

  db.run('INSERT INTO users (username, password, role) VALUES (?, ?, ?)', [username, password, role], (err) => {
    if (err) {
      console.error(err.message);
      return res.status(500).json({ message: 'Internal server error' });
    }

    res.status(201).json({ message: 'User created successfully' });
  });
});
```
Chiudi la connessione al database quando il server si ferma:
```javascript
process.on('SIGINT', () => {
  db.close((err) => {
    if (err) {
      console.error(err.message);
    }
    console.log('Closed the database connection.');
  });

  process.exit(0);
});
```

 **Aggiungi un modulo di registrazione al frontend**


invia i dati utente alla rotta /register per creare nuovi account utente

Prima di tutto, crea il file register.html per includere il modulo di registrazione:
```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Login</title>
</head>
<body>
<h1>Register</h1>
<form id="register-form">
  <label for="reg-username">Username:</label>
  <input type="text" id="reg-username" name="reg-username" required>
  <br>
  <label for="reg-password">Password:</label>
  <input type="password" id="reg-password" name="reg-password" required>
  <br>
  <label for="reg-role">Role:</label>
  <select id="reg-role" name="reg-role" required>
    <option value="user">User</option>
    <option value="admin">Admin</option>
  </select>
  <br>
  <input type="submit" value="Register">
</form>
<p id="register-message"></p>
</body>
</html>
```

 **Dopo, aggiungi il codice di gestione della presentazione del modulo di registrazione al file login.js:**

```javascript
// Aggiungi questo codice dopo l'ascoltatore di eventi del modulo di accesso

document.getElementById('register-form').addEventListener('submit', async (e) => {
  e.preventDefault();

  const username = document.getElementById('reg-username').value;
  const password = document.getElementById('reg-password').value;
  const role = document.getElementById('reg-role').value;

  try {
    const response = await fetch('/register', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify({ username, password, role }),
    });

    if (response.status === 201) {
      document.getElementById('register-message').innerText = 'User registered successfully';
    } else {
      document.getElementById('register-message').innerText = 'Registration failed';
    }
  } catch (error) {
    console.error('Error:', error);
  }
});
```
Adesso, hai un modulo di registrazione  sul frontend che invia i dati utente alla rotta /register per creare nuovi account utente. Dopo aver registrato con successo, gli utenti possono accedere con le loro nuove credenziali.

Adesso, la tua applicazione utilizza il database SQLite per l'autenticazione e la registrazione degli utenti. Puoi aggiungere un modulo di registrazione al frontend e inviare i dati utente alla rotta /register per creare nuovi account utente.
 **cURL**


un tool e una libreria per la trasmissione di dati con URL. È utilizzato per effettuare richieste HTTP, scaricare file e interagire con API RESTful. cURL supporta una vasta gamma di protocolli, tra cui HTTP, HTTPS, FTP, SCP e molti altri.

Qui di seguito alcuni comandi cURL utili per il sistema di gestione degli utenti che abbiamo lavorato:

Registra un nuovo utente:

>curl -X POST -H "Content-Type: application/json" -d '{"username": "newuser", "password": "newpassword", "role": "user"}' http://localhost:3000/register

Log in con le credenziali di un utente:

>curl -X POST -H "Content-Type: application/json" -d '{"username": "user1", "password": "password1"}' http://localhost:3000/login
Dopo un log in riuscito, riceverai un JSON Web Token (JWT) nella risposta. Copia il token e utilizzalo per i seguenti comandi cURL per accedere alle rotte protette.

Accedi alla rotta protetta come utente loggato:

>curl -H "Authorization: Bearer <your_jwt_token>" http://localhost:3000/protected
Cambia <your_jwt_token> con il JWT che hai ricevuto dopo il login.

Log out

>curl -X GET http://localhost:3000/logout

Questi sono alcuni comandi cURL utili per testare il sistema di gestione degli utenti senza utilizzare un browser web. Possono essere utili per la risoluzione dei problemi, il test degli endpoint API e l'automazione delle attività.
# MVC


 **autenticazione utilizzando Node.js, Express e un file JSON per memorizzare le credenziali degli utenti.**
 
 implement MVC

Seguendo il pattern MVC, la struttura della cartella del progetto dovrebbe avere la seguente struttura:

>your_project/
|-- controllers/
|   |-- userController.js
|
|-- models/
|   |-- userModel.js
|
|-- views/
|   |-- admin.html
|   |-- index.html
|   |-- user.html
|
|-- .gitignore
|-- addUsers.js
|-- createDb.js
|-- login.js
|-- package.json
|-- package-lock.json
|-- server.js
|-- myDatabase.db

Questi files e cartelle separano i diversi componenti della tua applicazione:

controllers:
contiene la logica dell'applicazione e gestisce l'input dell'utente (la parte Controller del pattern MVC).

userController.js:
contiene la logica per gestire l'accesso e la registrazione degli utenti.

models:
contiene la logica correlata ai dati e comunica con il database (la parte Model del pattern MVC).

userModel.js:
contiene la logica per interrogare e inserire gli utenti nel database SQLite.

views:
contiene i file HTML per la visualizzazione dell'interfaccia utente (la parte View del pattern MVC).

admin.html:
la pagina vuota riservata all'amministratore.

index.html:
i moduli di accesso e registrazione.

user.html:
la pagina vuota riservata all'utente.

Gli altri file nella directory del progetto sono:

.gitignore:
contiene un elenco di file e cartelle da ignorare da Git.

addUsers.js:
uno script per inserire 3 utenti nel database SQLite.

createDb.js:
uno script per creare il database SQLite e la tabella degli utenti.

login.js:
il codice JavaScript frontend per gestire le sottomissioni dei moduli di accesso e registrazione.

package.json:
contiene i metadati del tuo progetto, come le dipendenze.

package-lock.json:
file generato automaticamente che memorizza la versione esatta dei pacchetti installati.

server.js:
il file principale che imposta e avvia Express.js


 **Per implementare il Model-View-Controller (MVC) pattern**


nella tua applicazione, devi ristrutturare il codice e organizzarlo in file separati per i modelli, le viste e i controller. Ecco un elenco dei passaggi necessari per ristrutturare la tua applicazione esistente:

Crea le nuone cartelle models, controllers e views nella directory del progetto.

Sposta i file HTML nella cartella views.
```html
<!-- Aggiorna i tag script alla fine dei files html -->
<script src="/auth.js"></script>
<script src="/login.js"></script>
```

 **Aggiorna il file server.js per servire i file statici dalla cartella view**
```javascript
app.use(serveStatic('views'));
```

 **Crea un nuovo file denominato userModel.js all'interno della cartella models e aggiungi il seguente codice:**
```javascript
const sqlite3 = require('sqlite3').verbose();

const db = new sqlite3.Database('./myDatabase.db', (err) => {
  if (err) {
    console.error(err.message);
  }
  console.log('Connected to the myDatabase SQLite database.');
});

module.exports = {
  getUserByUsername: (username, callback) => {
    db.get('SELECT * FROM users WHERE username = ?', [username], callback);
  },

  createUser: (username, password, role, callback) => {
    db.run('INSERT INTO users (username, password, role) VALUES (?, ?, ?)', [username, password, role], callback);
  },
};
```

 **Crea un nuovo file denominato userController.js all'interno della cartella controllers e aggiungi il seguente codice:**
```javascript
const jwt = require('jsonwebtoken');
const userModel = require('../models/userModel');
const SECRET_KEY = 'your-secret-key';

module.exports = {
  login: (req, res) => {
    const { username, password } = req.body;

    userModel.getUserByUsername(username, (err, user) => {
      if (err) {
        console.error(err.message);
        return res.status(500).json({ message: 'Internal server error' });
      }

      if (user && user.password === password) {
        const token = jwt.sign({ username: user.username, role: user.role }, SECRET_KEY, {
          expiresIn: '1h',
        });

        res.json({ message: 'Authentication successful', token });
      } else {
        res.status(401).json({ message: 'Invalid credentials' });
      }
    });
  },

  register: (req, res) => {
    const { username, password, role } = req.body;

    userModel.createUser(username, password, role, (err) => {
      if (err) {
        console.error(err.message);
        return res.status(500).json({ message: 'Internal server error' });
      }

      res.status(201).json({ message: 'User created successfully' });
    });
  },
};

const userController = require('./controllers/userController');

// ...

// Login route
app.post('/login', userController.login);

// Register route
app.post('/register', userController.register);
```

 **Aggiorna il file server.js per utilizzare il userController:**
```javascript
 
const userController = require('./controllers/userController');

// ...

// Login route
app.post('/login', userController.login);

// Register route
app.post('/register', userController.register);
```

Adesso la tua applicazione è strutturata secondo il pattern MVC. Il file userModel.js contiene la logica correlata al database (Model), i files HTML nella cartella views rappresentano l'interfaccia utente (View) e il file userController.js gestisce l'input dell'utente e interagisce con il modello e la vista (Controller)