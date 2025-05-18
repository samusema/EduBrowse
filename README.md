# 🔐 EduBrowse - Browser scolastico con firewall integrato

EduBrowse è un browser personalizzato pensato per l'ambiente scolastico, con **firewall integrato**, **logging delle attività di navigazione**, e una **dashboard di amministrazione** per la gestione dei dispositivi e delle regole di accesso ai siti web.

## 🧠 Obiettivi principali

- Fornire un browser sicuro e controllato per gli studenti.
- Bloccare l'accesso a contenuti non autorizzati tramite **blacklist/whitelist**.
- Registrare tutti i siti visitati su **MongoDB**.
- Offrire agli amministratori uno strumento per gestire dispositivi e visualizzare log di navigazione.

---

## 🧱 Architettura del progetto

```
+------------------+
|     Browser      | <------ Studente
|  (Electron App)  |
+--------+---------+
         |
         ↓
+--------+---------+        +---------------------+
|  Proxy/Firewall  | <----> |   URL Filtering     |
| (Node.js/Go app) |        | (Blacklist/Rules DB)|
+--------+---------+        +----------+----------+
         |                             |
         ↓                             ↓
+--------+----------+     +--------------------------+
|     Logging        |     |  MongoDB (Visited URLs, |
|  (Event handler)   |     |  Dispositivi, Regole)   |
+--------------------+     +--------------------------+

+-------------------------+
| Admin Web Dashboard     |
| (Gestione dispositivi,  |
|  visualizzazione log)   |
+-------------------------+
```

---

## 🔧 Tecnologie utilizzate

| Componente        | Stack/Tool                |
|-------------------|---------------------------|
| Browser App       | [Electron](https://www.electronjs.org/) + HTML/CSS/JS |
| Proxy & Firewall  | Node.js (http-proxy) / Go (goproxy) |
| Database          | [MongoDB](https://www.mongodb.com/) |
| Backend API       | Express.js / Fastify       |
| Admin Dashboard   | React.js + Tailwind CSS    |
| Autenticazione    | JWT / Bcrypt               |
| Logging           | EventEmitter + MongoDB     |

---

## 📁 Struttura delle directory (proposta)

```
edubrowse/
│
├── browser-app/           # Browser Electron custom
├── proxy-firewall/        # Proxy con regole di filtro
├── admin-dashboard/       # Interfaccia web per gli admin
├── backend-api/           # API REST per MongoDB e autenticazione
├── database/              # Script di setup per MongoDB
└── README.md
```

---

## 📌 Funzionalità principali

### Studente
- Navigazione tramite browser controllato
- Accesso solo ai siti permessi
- Nessuna possibilità di cambiare impostazioni

### Amministratore
- Login sicuro nell'area admin
- Visualizzazione dei log per data/dispositivo
- Aggiunta/rimozione di dispositivi autorizzati
- Gestione di **blacklist** e **whitelist**
- Download dei log in CSV

---

## 🚀 Guida allo sviluppo

### 1. Clone del repository

```bash
git clone https://github.com/samusema/edubrowse.git
cd edubrowse
```

### 2. Installazione delle dipendenze

Installa i moduli necessari in ogni sottocartella (`browser-app/`, `proxy-firewall/`, `admin-dashboard/`, `backend-api/`).

```bash
cd proxy-firewall
npm install
# Ripeti per gli altri moduli
```

### 3. Avviare i servizi

Assicurati di avere MongoDB attivo, poi:

```bash
# Avvia il proxy
cd proxy-firewall
npm start

# Avvia il browser Electron
cd ../browser-app
npm start

# Avvia il backend API
cd ../backend-api
npm start

# Avvia la dashboard
cd ../admin-dashboard
npm run dev
```

---

## ✅ To-do (Roadmap)

- [ ] Proxy HTTPS con certificati auto-firmati
- [ ] Report settimanale delle attività
- [ ] Machine learning per rilevamento contenuti sospetti
- [ ] Supporto multi-scuola (tenant system)

---

## 📄 Licenza

Distribuito sotto licenza MIT. Vedi `LICENSE` per i dettagli.

