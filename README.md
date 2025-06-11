# momentus
**Precisão e reverência em cada detalhe.**

**Momentus** é a solução ideal para a organização dos cultos, oferecendo uma plataforma intuitiva para o planejamento detalhado de cada etapa da celebração. O app fortalece a união da comunidade e assegura que cada momento seja conduzido com excelência e reverência.

# 🎯 Projeto:

## 🧩 Categoria
App de Organização Colaborativa + Gestão de Eventos

---

## ✨ Funcionalidade Principal
Um app para planejar, montar e colaborar no cronograma de cultos, incluindo:

- Pregador
- Cantores ou Ministério de Louvor
- Leituras bíblicas
- Ordem dos elementos do culto
- Horário de cada parte
- Data do evento
- Observações adicionais

---

## 👥 Colaboração
- Múltiplos usuários podem acessar e editar o cronograma.
- Notificações ou e-mails para responsáveis (pregador, louvor etc.).
- Possibilidade de aprovação pelo líder antes de publicar o cronograma final.

---

## 🖼️ Exemplo de Telas

- **Dashboard dos Cultos**  
  Lista de eventos com status: "Rascunho", "Aguardando aprovação", "Publicado"

- **Editor de Cronograma**  
  Adicionar/remover partes do culto  
  Escolher horários e responsáveis

- **Lista de Participantes**  
  Ver quem está designado para cada papel

- **Perfil do Culto**  
  Resumo do evento (data, tema, pregador principal)

- **Modo Leitura**  
  Versão limpa do cronograma para usar durante o culto

---

## 🚀 Stack Recomendada
- Frontend mobile: React Native (com Expo)
- Backend/API: Node.js + Express
- Banco de dados: MongoDB (Mongoose)
- Autenticação: Firebase Auth ou JWT
- Sincronização em tempo real (opcional): Socket.IO ou Firebase
- Hospedagem: MongoDB Atlas + Railway ou Render para API

# 🗃️ 2. Modelo de Dados para MongoDB

Vamos definir coleções básicas com seus campos principais:

---

## 📦 Coleção: usuarios
```json
{
  "_id": "ObjectId",
  "nome": "João Silva",
  "email": "joao@email.com",
  "role": "pastor" // ou cantor, líder, membro
}

## 📦 Coleção: cultos (ou eventos)
{
  "_id": "ObjectId",
  "titulo": "Culto de Gratidão",
  "data": "2025-06-15T19:30:00Z",
  "descricao": "Celebração com a comunidade",
  "status": "rascunho", // ou "publicado"
  "responsavel": "ObjectId", // ID do usuário
  "etapas": ["ObjectId"], // lista de IDs da programação
  "participantes": [
    { "usuarioId": "aaa111", "permissao": "editor" },
    { "usuarioId": "bbb222", "permissao": "visualizador" }
  ]
}

## 📦 Coleção: etapas
{
  "_id": "ObjectId",
  "cultoId": "ObjectId",
  "ordem": 1,
  "titulo": "Louvor",
  "horario": "19:30",
  "observacoes": "3 músicas do repertório atual",
  "responsaveis": [
    {
      "tipo": "líder de louvor", // ou "pregador", "leitora", etc.
      "usuarioId": "ObjectId"
    },
    {
      "tipo": "cantor",
      "usuarioId": "ObjectId"
    },
    {
      "tipo": "cantor",
      "usuarioId": "ObjectId"
    }
  ]
}

## 📦 (Opcional) Coleção: notificacoes
{
  "_id": "ObjectId",
  "usuarioId": "ObjectId",
  "cultoId": "ObjectId",
  "mensagem": "Você foi adicionado como responsável pelo louvor",
  "lido": false,
  "data": "ISODate(...)"
}

## 🚧 3. Roadmap de Desenvolvimento
Aqui está um plano prático e escalável para seu MVP:

- Fase 1: Planejamento e Setup
Criar estrutura do projeto com React Native (via Expo)

Criar API com Express + MongoDB (usando Mongoose)

Configurar banco na MongoDB Atlas

- Fase 2: Funcionalidades Básicas
Tela de login e autenticação (Firebase Auth ou JWT simples)

CRUD de Cultos

CRUD de Etapas

Atribuir responsáveis

Visualizar cronograma no modo leitura

- Fase 3: Compartilhamento e Colaboração
Permitir convite via link/código

Controle de permissões (quem pode editar)

Feedback em tempo real (opcional: WebSocket)

- Fase 4: Extras
Notificações

Histórico de alterações

Exportar cronograma em PDF

Tema escuro (modo noite do culto 😄)

---

## ✅ MVP (Mínimo Produto Viável)
- Criar evento (culto)
- Adicionar partes ao cronograma (com título, horário e pessoa responsável)
- Compartilhar com os membros da equipe (via link ou código)
- Modo leitura para exibir o cronograma final

# ✅ 1. Wireframe (Esboço de Telas)

## 📱 Tela 1: Lista de Cultos (Eventos)
- Mostrar data, título, status
- Botão “+ Criar Novo Culto”

---

## 📱 Tela 2: Criar/Editar Culto
Campos:
- Data do culto
- Tema/título
- Observações gerais
- Responsável principal
- Botão: “Adicionar Etapa”

---

## 📱 Tela 3: Etapas do Culto (Cronograma)
Lista ordenada de:
- Tipo de etapa (Louvor, Palavra, Oração, etc.)
- Responsável (ex: Pr. João)
- Horário (ex: 19:30)

Botões:
- Adicionar etapa
- 🖊️ Editar etapa
- 🗑️ Remover etapa

---

## 📱 Tela 4: Compartilhamento
- Link ou código para compartilhar com os envolvidos
- Opção para definir permissões (visualizar / editar)

---

## 📱 Tela 5: Visualização (Modo Culto)
- Exibição limpa do cronograma por ordem de execução
- Indicação de horário atual (opcional com destaque)

# 🧱 Conceito Base de Permissões no App de Cronograma de Culto

## 🎭 Papéis de Usuários por Evento (Culto)
Cada usuário dentro de um culto pode ter um papel específico, que define o nível de acesso às funcionalidades. Exemplo de papéis:

| Papel             | Permissões                                           |
|-------------------|-----------------------------------------------------|
| Editor            | Criar/editar etapas, alterar dados do culto, convidar outros usuários |
| Visualizador      | Ver o cronograma e informações do culto, sem editar |
| Responsável geral | Igual ao editor, mas com autoridade final (opcional) |

> ⚠️ **Importante:** o papel é por culto, não global. Ou seja, um mesmo usuário pode ser editor em um culto e apenas visualizador em outro.

---

## 🧭 Níveis de Permissão (o que cada um pode fazer)

| Ação                            | Editor | Visualizador |
|--------------------------------|--------|--------------|
| Ver cronograma                 | ✅     | ✅           |
| Editar cronograma             | ✅     | ❌           |
| Adicionar etapas              | ✅     | ❌           |
| Atribuir responsáveis às etapas | ✅     | ❌           |
| Convidar participantes        | ✅     | ❌ (visualizadores só entram por convite) |
| Ver quem está envolvido       | ✅     | ✅           |

---

## 🔐 Permissões extras (a serem consideradas futuramente)
Você pode, se quiser, evoluir esse sistema com:

- Confirmação de presença: cada participante confirma se vai cumprir seu papel.
- Permissão granular por etapa: exemplo — alguém pode editar só o "Louvor", mas não o resto.
- Permissão de publicação: só um líder pode "publicar" ou "finalizar" o cronograma.
- Histórico de edição: registra quem alterou o quê e quando.

---

## 🧩 Relacionamentos entre permissões e dados
- Culto tem vários participantes, cada um com um papel.
- Cada etapa tem responsáveis específicos (não necessariamente com permissão de edição do culto inteiro).
- Você pode permitir que visualizadores vejam apenas etapas em que estão envolvidos — ou todas, dependendo da sua escolha.

---

## 📝 Exemplo prático

Culto de Domingo (15/06/2025)

| Nome    | Papel no Culto | Papel na Etapa    |
|---------|----------------|-------------------|
| Pr. João| Editor         | Pregador          |
| Maria   | Visualizador   | Cantora no Louvor |
| Pedro   | Editor         | Líder de Louvor   |
| Ana     | Visualizador   | Não atribuída a etapas |

---

Essa estrutura permite escalar seu sistema com segurança e clareza. Quando for implementar, basta traduzir esses conceitos em código com roles, permissions e lógica de acesso nos endpoints/telas.
