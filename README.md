

# TRADER

## Estrutura do Projeto

TRADER/
├── backend/
│   ├── app.js
│   ├── config/
│   │   └── db.js
│   ├── controllers/
│   │   ├── authController.js
│   │   ├── cursoController.js
│   │   ├── simulacaoController.js
│   │   └── userController.js
│   ├── models/
│   │   ├── Curso.js
│   │   ├── Simulacao.js
│   │   └── User.js
│   ├── package.json
│   └── routes/
│       ├── authRoutes.js
│       ├── cursoRoutes.js
│       ├── simulacaoRoutes.js
│       └── userRoutes.js
├── frontend/
│   ├── public/
│   │   ├── favicon.ico
│   │   └── index.html
│   ├── src/
│   │   ├── components/
│   │   │   ├── Cursos.js
│   │   │   ├── Dashboard.js
│   │   │   ├── Header.js
│   │   │   ├── Login.js
│   │   │   ├── Simulacoes.js
│   │   │   └── UserProfile.js
│   │   ├── App.js
│   │   ├── api.js
│   │   ├── index.js
│   │   └── utils.js
│   ├── package.json
│   └── vercel.json
├── .gitignore
├── package.json
└── README.md


## backend/app.js
js
const express = require('express');
const app = express();
const mongoose = require('mongoose');
const authRoutes = require('./routes/authRoutes');
const cursoRoutes = require('./routes/cursoRoutes');
const simulacaoRoutes = require('./routes/simulacaoRoutes');
const userRoutes = require('./routes/userRoutes');

mongoose.connect('mongodb://localhost/trader', { useNewUrlParser: true, useUnifiedTopology: true });

app.use(express.json());
app.use('/api/auth', authRoutes);
app.use('/api/cursos', cursoRoutes);
app.use('/api/simulacoes', simulacaoRoutes);
app.use('/api/users', userRoutes);

app.listen(3001, () => {
  console.log('Backend rodando na porta 3001');
});


## frontend/src/App.js

jsx
import React from 'react';
import { BrowserRouter, Route, Routes } from 'react-router-dom';
import Cursos from './components/Cursos';
import Dashboard from './components/Dashboard';
import Header from './components/Header';
import Login from './components/Login';
import Simulacoes from './components/Simulacoes';
import UserProfile from './components/UserProfile';

function App() {
  return (
    <BrowserRouter>
      <Header />
      <Routes>
        <Route path="/" element={<Login />} />
        <Route path="/cursos" element={<Cursos />} />
        <Route path="/dashboard" element={<Dashboard />} />
        <Route path="/simulacoes" element={<Simulacoes />} />
        <Route path="/perfil" element={<UserProfile />} />
      </Routes>
    </BrowserRouter>
  );
}

export default App;


## frontend/vercel.json

{
  "rewrites": [
    {
      "source": "/(.*)",
      "destination": "/index.html"
    }
  ]
}
