
# 💬 Uatizap - Sistema de Autenticação e Chat

O **Uatizap** é uma aplicação web simples inspirada no WhatsApp, composta por um backend em Node.js (Express) e um frontend em HTML, CSS e JavaScript Vanilla. O sistema permite o **registro de novos utilizadores**, **autenticação (login)** e a **troca de mensagens em tempo real** gravadas numa base de dados MySQL.

---

## 📁 Estrutura do Projeto

```text
WPP/
├── db/
│   └── connection.js      # Configuração da conexão com a base de dados MySQL
├── front-end/
│   ├── css/
│   │   └── style.css      # Estilização das páginas
│   ├── img/
│   │   └── phone-call.png # Ícone da aplicação
│   ├── js/
│   │   └── script.js     # Lógica do frontend (requisições de login, cadastro e chat)
│   ├── chat.html          # Interface da sala de chat
│   ├── index.html         # Interface de login/autenticação
│   └── register.html      # Interface de registo de novos utilizadores
├── routes/
│   └── auth.route.js      # Rotas da API (/auth, /signin, /chat)
├── main.js                # Servidor principal Express
├── package.json           # Dependências e scripts Node.js
└── README.md              # Documentação do projeto

```

---

## 🛠️ Tecnologias Utilizadas

* **Backend:** Node.js, Express, Cors, Mysql2
* **Frontend:** HTML5, CSS3, JavaScript (Fetch API)
* **Base de Dados:** MySQL / MariaDB (gerido via XAMPP e HeidiSQL)

---

## 🗄️ Configuração da Base de Dados (XAMPP + HeidiSQL)

Siga os passos abaixo para criar a base de dados `whatsapp` e as respetivas tabelas.

### 1. Iniciar o Servidor MySQL no XAMPP

1. Abra o **XAMPP Control Panel**.
2. Clique no botão **Start** ao lado do módulo **MySQL** (e Apache, se necessário).

### 2. Conectar ao HeidiSQL

1. Abra o **HeidiSQL**.
2. Crie uma nova conexão com as seguintes credenciais padrão:
* **Hostname / IP:** `localhost` ou `127.0.0.1`
* **Utilizador / User:** `root`
* **Palavra-passe / Password:** *(deixar em branco)*
* **Porta:** `3306`


3. Clique em **Abrir**.

### 3. Criar a Base de Dados e Tabelas (Comandos SQL)

No HeidiSQL, vá até ao separador **Consulta / Query** (ou clique em `F9` para executar) e execute o seguinte script SQL:

```sql
-- 1. Criar a base de dados se não existir
CREATE DATABASE IF NOT EXISTS `whatsapp` 
DEFAULT CHARACTER SET utf8mb4 
COLLATE utf8mb4_general_ci;

USE `whatsapp`;

-- 2. Criar a tabela de utilizadores
CREATE TABLE IF NOT EXISTS `utilizadores` (
  `Id` INT(11) NOT NULL AUTO_INCREMENT,
  `Apelido` VARCHAR(100) NOT NULL,
  `Telefone` VARCHAR(20) NOT NULL,
  `Senha` VARCHAR(255) NOT NULL,
  `Criado_em` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP(),
  PRIMARY KEY (`Id`),
  UNIQUE KEY `Telefone` (`Telefone`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

-- 3. Criar a tabela de mensagens
CREATE TABLE IF NOT EXISTS `mensagens` (
  `Id` INT(11) NOT NULL AUTO_INCREMENT,
  `telefone_remetente` VARCHAR(20) NOT NULL,
  `telefone_destinatario` VARCHAR(20) NOT NULL,
  `mensagem` TEXT NOT NULL,
  `data_envio` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP(),
  PRIMARY KEY (`Id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

```

---

## 🚀 Como Executar o Projeto

1. **Clonar o Repositório / Aceder à pasta do projeto:**
```bash
cd caminho/para/o/projeto/WPP

```


2. **Instalar as dependências:**
```bash
npm install

```


3. **Iniciar o servidor:**
```bash
node main.js

```


4. **Aceder à aplicação no navegador:**
* **Login / Autenticação:** `http://localhost:3000/` ou `http://localhost:3000/auth`
* **Criar Conta:** `http://localhost:3000/register`
* **Chat:** `http://localhost:3000/chat-page`



---

## ⚙️ Rotas da API

| Método | Rota | Descrição |
| --- | --- | --- |
| `POST` | `/auth` | Autentica um utilizador com `telefone` e `senha`. |
| `POST` | `/signin` | Regista um novo utilizador (`apelido`, `telefone`, `senha`). |
| `GET` | `/chat` | Procura as mensagens associadas a um número de telefone (`?telefone=...`). |
| `POST` | `/chat` | Envia e guarda uma nova mensagem na base de dados. |

```

```
