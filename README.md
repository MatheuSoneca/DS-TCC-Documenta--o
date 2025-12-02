**Sistema Web + PWA para Agendamentos**

## 1. Identificação do Projeto

### 1.1 Nome do Sistema – Corte em Dia

O sistema **Corte em Dia** foi idealizado para atender barbearias e salões de beleza que necessitam de um controle eficiente e moderno de agendamentos. O nome reforça a proposta de manter tanto o profissional quanto o cliente sempre “em dia” com seus horários, destacando organização, eficiência e praticidade.

É curto, fácil de lembrar e diretamente associado ao segmento de beleza e estética, facilitando sua identificação no mercado.

### 1.2 Integrantes do Grupo

| Integrante               | Função Principal                                              |
| ------------------------ | ------------------------------------------------------------- |
| Matheus Viana Dantas     | Desenvolvimento Front-end Web e apoio no PWA                 |
| Guilherme Soares Ferreira| Desenvolvimento Back-end (Node.js, PostgreSQL), API e integração geral |

---

## 2. Apresentação do Projeto

### 2.1 Objetivo do Sistema

O **Corte em Dia** tem como objetivo principal automatizar e organizar o processo de agendamentos para barbearias e salões de beleza, garantindo mais eficiência ao profissional e autonomia ao cliente.

#### Visão Administrativa (Profissional)

Criada para uso administrativo, permitindo ao barbeiro:

- Visualizar agenda diária
- Cadastrar, editar e remover serviços
- Organizar clientes
- Gerenciar horários livres e ocupados
- Evitar conflitos de agendamento
- Visualizar fluxo completo do dia
- Instalar o app na tela inicial como aplicativo nativo

#### Visão Pública (Cliente)

Voltada para clientes, com foco em praticidade:

- Listar serviços disponíveis
- Consultar horários compatíveis automaticamente
- Agendar dia e horário
- Ver futuros agendamentos
- Instalar o app na tela inicial como aplicativo nativo
  

### 2.2 Problema Identificado

Grande parte das barbearias de pequeno porte ainda utiliza métodos tradicionais para organizar seus horários:

- Agendas de papel
- Mensagens no WhatsApp
- Anotações desconexas
- Dependência de memória do profissional

Esse modelo traz problemas como:

- Horários duplicados
- Falta de controle sobre duração dos serviços
- Perda de clientes por desorganização
- Dificuldade em gerenciar dias cheios
- Comunicação lenta com clientes

**Público-alvo:**

- Barbeiros autônomos
- Barbearias de bairro
- Salões pequenos com fluxo constante

#### Soluções atuais e problemas

Ferramentas genéricas (Google Calendar, anotações, blocos) não atendem necessidades específicas como:

- Duração real de cada serviço
- Filtragem inteligente de horários compatíveis
- Comunicação direta com clientes integrada à agenda

#### Por que o Corte em Dia se destaca?

O sistema calcula automaticamente **quais horários realmente comportam o serviço escolhido**, evitando situações como:

> “Dá para colocar às 14h30?” mesmo que o serviço leve 1h30 e o barbeiro só tenha 1h livre.

#### Justificativa Web + PWA

- **Web (Cliente Profissional):** mais espaço, visão detalhada da agenda, foco em produtividade.
- **PWA (Cliente e Profissional):** uso natural via smartphone, instalação simples, experiência de app sem precisar de loja.

As versões funcionam juntas, formando um sistema completo e acessível.

### 2.3 Stack Tecnológica

A stack utilizada é baseada em tecnologias modernas e foi pensada para um sistema **single-tenant** (uma barbearia por instância).

#### 2.3.1 Front-end Web

- **React.js + Vite**
- **TailwindCSS**
- **React Router** (navegação SPA)
- **Axios** (requisições HTTP)

**Justificativa:** O combo **React + Vite** garante rapidez e modularidade. **Tailwind** permitem criar interfaces modernas e consistentes. As ferramentas escolhidas facilitam manutenção, escalabilidade e evolução do projeto.

#### 2.3.2 Versão Mobile (PWA)

Baseada na mesma estrutura da Web:

- React + Tailwind
- Vite Plugin PWA

**Service Worker:**

- Cache básico
- Fallback offline

**Web App Manifest:**

- Instalação como app nativo
- Ícone, nome e tema configurados


**Justificativa:** PWA é ideal para sistemas que não dependem de câmera, GPS ou sensores avançados. Além disso:

- Menor custo
- Mesma base de código da Web
- Fácil distribuição
  

#### 2.3.3 Back-end

- **Node.js + Express**
- **API REST**
- **PostgreSQL**
- **Supabase Auth** para autenticação

Hospedagem do servidor em ambiente Node (Hostinger, Railway etc.).

**Justificativa:** A arquitetura permite:

- Desenvolvimento rápido
- Boa escalabilidade
- Segurança com autenticação moderna (JWT + Bcrypt)
- Padronização entre Web e PWA por meio de API REST


## 3. Arquitetura e Fluxo do Sistema

### 3.1 Mapa de Telas

**Tela 1 — Login**

- **Objetivo:** Autenticar usuários (profissional ou cliente).
- **Componentes:**
  - Campo de e-mail
  - Campo de senha
  - Botão **Entrar**
  - Link **"Esqueci minha senha"**
  - Link **"Criar conta"** (somente cliente)

**Tela 2 — Agenda do Dia (Profissional)**

- **Objetivo:** Gerenciar toda a agenda diária.
- **Recursos:**
  - Lista de horários ocupados/livres
  - Ação para criar agendamento
  - Editar/cancelar agendamentos
  - Navegar entre dias

**Tela 3 — Gestão de Serviços (Profissional)**

- **Recursos:**
  - Nome do serviço
  - Duração estimada
  - Preço (opcional)
  - Criar/editar/excluir serviços

**Tela 4 — Gestão de Clientes / Cadastro**

- **Recursos:**
  - Lista de clientes (Web)
  - Formulário com nome, telefone, e-mail

**Tela 5 — Escolha de Serviço (Cliente)**

- **Recursos:**
  - Catálogo de serviços
  - Botões para seleção

**Tela 6 — Seleção de Data e Horário (Cliente)**

- **Recursos:**
  - Calendário
  - Horários disponíveis filtrados automaticamente
  - Confirmação de agendamento

**Tela 7 — Meus Agendamentos (Cliente)**

- **Recursos:**
  - Lista de agendamentos futuros
  - Cancelamento (com regras)
  - Iniciar novo agendamento



## 3.2 Fluxograma de Navegação

A navegação do sistema é organizada em fluxos principais separados por tipo de usuário.

### 3.2.1 Fluxo – Profissional 

- **Login (Tela 1)**  
  → Usuário cabeleireiro se autentica  
  → Redirecionamento para **Agenda do Dia (Tela 2)**  

- **Agenda do Dia (Tela 2)**  
  → Visualiza agendamentos e horários livres  
  → Pode:
  - Criar novo agendamento manual em um horário livre  
  - Acessar detalhes/edição de um agendamento existente  
  - Navegar para:
    - **Gestão de Serviços (Tela 3)**  

- **Gestão de Serviços (Tela 3)**  
  → Cadastrar/editar/excluir serviços  
  → Retornar para **Agenda do Dia (Tela 2)**   

Em qualquer momento, o profissional poderá sair do sistema e voltar à **Tela 1 (Login)**.

---

### 3.2.2 Fluxo – Cliente

- **Login (Tela 1)**  
  → Cliente se autentica (ou acessa fluxo de cadastro, quando disponível)  
  → Redirecionamento para **Escolha de Serviço (Tela 5)**  

- **Escolha de Serviço (Tela 5)**  
  → Cliente seleciona o serviço desejado  
  → Avança para **Seleção de Data e Horário (Tela 6)**  

- **Seleção de Data e Horário (Tela 6)**  
  → Cliente escolhe a data  
  → Sistema exibe apenas horários compatíveis com a duração do serviço  
  → Cliente escolhe um horário disponível  
  → Confirma → criação do agendamento no sistema  
  → Redirecionamento para **Meus Agendamentos (Tela 7)**  

- **Meus Agendamentos (Tela 7)**  
  → Cliente visualiza seus agendamentos futuros  
  → Pode, conforme regras definidas, cancelar algum agendamento  
  → Pode iniciar um novo agendamento, retornando para **Tela 5 (Escolha de Serviço)**

---

### 3.2.3 Fluxo de Cadastro de Cliente

- **Login (Tela 1)**  
  → Clique em “Criar conta”   
  → Após o cadastro bem-sucedido, o cliente é redirecionado para o fluxo principal de agendamento, iniciando em **Escolha de Serviço (Tela 5)**.

---

# 4. Funcionalidades Detalhadas

As funcionalidades do sistema **Corte em Dia** foram organizadas em três níveis de prioridade:

- **Essenciais (MVP):** necessárias para o funcionamento básico.  
- **Importantes:** agregam valor e melhoram a experiência.  
- **Desejáveis:** podem ser implementadas se houver tempo (melhorias futuras).

---

## 4.1 Funcionalidades Essenciais (MVP)

1. **Login de Usuário (Profissional e Cliente)**  
   - **Descrição:** Autenticação de usuários (cabeleireiros e clientes), garantindo acesso aos fluxos adequados.  
   - **Telas envolvidas:** Tela 1 – Login  
   - **Versões:** Web e Mobile (PWA)

2. **Cadastro e Gestão de Serviços**  
   - **Descrição:** Cadastro, edição e exclusão de serviços oferecidos (ex.: corte, progressiva, luzes), incluindo duração estimada.  
   - **Telas envolvidas:** Tela 3 – Gestão de Serviços  

3. **Agendamento de Serviço com Cálculo Automático de Horário (Cliente)**  
   - **Descrição:** Permite ao cliente agendar um serviço, exibindo apenas horários compatíveis com a duração do serviço escolhido.  
   - **Telas envolvidas:** Tela 5 – Escolha de Serviço; Tela 6 – Seleção de Data e Horário  

4. **Criação de Agendamento no Banco de Dados**  
   - **Descrição:** Registro do agendamento (cliente, serviço, data, horário de início e término) no Supabase após confirmação.  
   - **Telas envolvidas:** Fluxo de confirmação dentro da Seleção de Data e Horário  

5. **Visualização da Agenda do Dia (Profissional)**  
   - **Descrição:** Exibição dos agendamentos do dia e horários livres para o cabeleireiro.  
   - **Telas envolvidas:** Tela 2 – Agenda do Dia  

6. **Meus Agendamentos (Cliente)**  
   - **Descrição:** Lista de agendamentos futuros do cliente, com informações de serviço, data e horário.  
   - **Telas envolvidas:** Tela 7 – Meus Agendamentos  

---

## 4.2 Funcionalidades Importantes

7. **Edição e Cancelamento de Agendamentos (Profissional)**  
   - **Descrição:** Permite ao cabeleireiro ajustar ou cancelar agendamentos já criados, liberando o horário quando necessário.  
   - **Telas envolvidas:** Tela 2 – Agenda do Dia (e/ou tela de detalhes de agendamento)  

8. **Cancelamento de Agendamento pelo Cliente (com regras de antecedência)**  
   - **Descrição:** Permite que o cliente cancele seus agendamentos, respeitando regras de antecedência definidas.  
   - **Telas envolvidas:** Tela 7 – Meus Agendamentos  

9. **Recuperação de Senha**  
    - **Descrição:** Recuperação de acesso ao sistema por meio de link de redefinição de senha via e-mail (Supabase Auth).  
    - **Telas envolvidas:** Tela 1 – Login (fluxo “Esqueci minha senha”)  

10. **Filtros e Navegação por Data na Agenda (Profissional)**  
    - **Descrição:** Navegação entre dias (anterior/próximo) e filtros simples na agenda, facilitando a visualização da carga de trabalho.  
    - **Telas envolvidas:** Tela 2 – Agenda do Dia  

---

## 4.3 Funcionalidades Desejáveis

- **Notificações por e-mail ou mensagem como lembrete de agendamento**  
- **Notificações push (PWA)**  
- **Relatórios simples para o profissional (serviços mais realizados, volume por período)**  
- **Suporte a múltiplos profissionais (multi-cabeleireiro) no mesmo salão**

---

# 5. Considerações de UX/UI

## 5.1 Identidade Visual

A identidade visual do **Corte em Dia** será simples, moderna e alinhada ao contexto de salões de beleza. Inicialmente, pretende-se utilizar uma paleta com tons claros e um destaque principal em azul ou roxo suave, combinados com branco e cinza para garantir boa legibilidade. As cores poderão ser ajustadas posteriormente de acordo com a preferência do salão que utilizar o sistema.

Para tipografia, a ideia é utilizar fontes sem serifa, como **Roboto** ou similar, por apresentarem boa leitura em telas pequenas e grandes. Títulos e elementos de destaque utilizarão pesos mais fortes, enquanto textos de apoio terão peso regular.

O uso do **Tailwind** auxiliará a manter consistência visual entre componentes (botões, campos de formulário, diálogos, navegação), com foco na clareza das informações de horário, serviço e status dos agendamentos.

---

## 5.2 Responsividade

A versão web do **Corte em Dia** será desenvolvida com foco em layout responsivo, adaptando-se a diferentes resoluções de tela:

- **Desktop:** prioriza a visualização da agenda do dia em maior área.  
- **Tablets e telas intermediárias:** mantém as mesmas funcionalidades com reorganização de layout (colunas reduzidas, menus recolhidos etc.).  
- **Mobile:** embora exista o PWA como versão principal para o cliente, a aplicação web também será utilizável em telas menores, com ajustes de espaçamento, tamanho de fonte e componentes amigáveis ao toque.

---

## 5.3 Diferenças de Experiência entre Web e Mobile/PWA

- **Versão Web (Administrador):**
  - Focada na gestão da agenda, serviços e clientes.  
  - Aproveita o espaço de tela maior para exibir mais informações simultaneamente (agenda do dia, menus laterais/superiores).  
  - Interações pensadas para uso com teclado e mouse, otimizando a produtividade no dia a dia do salão.

- **Versão Mobile/PWA (Cliente):**
  - Focada em consulta de horários, agendamento e visualização de “Meus Agendamentos”.  
  - Interface simplificada, com passos em sequência (escolher serviço → escolher data/horário → confirmar).  
  - Navegação otimizada para toque, com botões maiores e menos elementos por tela.  
  - Possibilidade de instalação do PWA na tela inicial do celular, com comportamento semelhante a um aplicativo nativo.

O objetivo é que ambas as versões compartilhem a mesma identidade visual, adaptando apenas os fluxos às necessidades de cada tipo de usuário.

---

# 6. Cronograma de Desenvolvimento

O cronograma abaixo apresenta uma previsão geral para a **Etapa 2 (desenvolvimento)** do sistema **Corte em Dia**, podendo sofrer ajustes conforme o andamento do projeto.

| Período                   | Atividade                                                                                  | Responsável                                  |
|---------------------------|--------------------------------------------------------------------------------------------|----------------------------------------------|
| 02/12/2025 - 15/12/2025   | Definição detalhada de requisitos, ajustes na documentação e criação de wireframes/protótipos | Dupla                                        |
| 16/12/2025 - 05/01/2026   | Configuração do ambiente, criação do projeto React, integração inicial com Supabase (auth e banco) | Dupla (com foco em back-end/configuração)    |
| 06/01/2026 - 20/01/2026   | Desenvolvimento das principais telas e funcionalidades da versão Web (login, agenda, serviços, clientes) | Principalmente Matheus, com apoio de Guilherme |
| 06/01/2026 - 20/01/2026   | Adaptação para PWA e implementação dos fluxos principais do cliente (escolha de serviço, horários, meus agendamentos) | Principalmente Guilherme, com apoio de Matheus |
| 21/01/2026 - 28/01/2026   | Integração completa, testes básicos dos fluxos de agendamento, ajustes de UX/UI e correção de bugs | Dupla                                        |
| 29/01/2026 - 01/02/2026   | Refinos finais, preparação da apresentação e atualização da documentação com o sistema implementado | Dupla                                        |

O cronograma reserva tempo para:

- Configuração técnica inicial;  
- Desenvolvimento das funcionalidades essenciais;  
- Integração entre Web e PWA;  
- Testes e ajustes finais antes da apresentação.
