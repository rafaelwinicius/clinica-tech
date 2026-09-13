# Clínica-Tech — Produto e Requisitos

## 1. Empresa

**Nome:** Clínica-Tech  
**Área de atuação:** Soluções de Tecnologia da Informação para a área da saúde.  
**Proposta:** desenvolver soluções digitais para clínicas e redes de atendimento que organizem processos, integrem informações e contribuam para uma experiência mais eficiente para pacientes e equipes.

A solução deste projeto será desenvolvida especificamente para uma rede de clínicas populares com cinco unidades: **Valentina, Mangabeira, Bancários, Expedicionários e Manaíra**.

---

## 2. Problema

A rede possui informações de agendamento e atendimento distribuídas entre telefone, mensagens e controles não integrados. Isso pode gerar:

- desorganização dos agendamentos;
- conflitos de horários;
- dificuldade no envio de lembretes;
- falhas de comunicação;
- perda ou dispersão de informações;
- dificuldade de acompanhamento dos atendimentos;
- pouca visão gerencial da rede.

**Problema central:** ausência de um sistema integrado para apoiar o agendamento de consultas e o acompanhamento dos atendimentos.

---

## 3. Objetivo do produto

Centralizar o gerenciamento das agendas da rede, permitindo que pacientes, secretárias, profissionais e gestores utilizem a mesma base de informações, respeitando seus níveis de acesso.

---

## 4. Formato e proposta da solução

### 4.1 Formato

Plataforma **web**, com:

- site público voltado ao paciente;
- ambiente administrativo acessado pelo navegador;
- integração com **WhatsApp**, por meio de chatbot para agendamento;
- base centralizada de profissionais, unidades, agendas, pacientes e agendamentos.

### 4.2 Site público

O site apresentará, de forma objetiva:

- unidades e localizações;
- profissionais;
- especialidades e áreas de atuação;
- informações gerais da rede;
- acesso ao WhatsApp para agendamento;
- telefone como canal alternativo de atendimento.

O paciente **não precisará criar login e senha**.

### 4.3 Proposta de valor

Oferecer à rede uma visão centralizada de profissionais, pacientes e agendas, reduzindo controles dispersos e facilitando o agendamento, a comunicação e o acompanhamento dos atendimentos.

---

## 5. Usuários e perfis

| Perfil | Escopo geral |
|---|---|
| **Paciente** | Consulta informações no site e agenda, cancela ou remarca pelo WhatsApp. |
| **Secretária** | Cadastra pacientes, consulta agendas e realiza agendamentos, cancelamentos e remarcações. |
| **Profissional** | Consulta a própria agenda, acompanha seus pacientes e solicita bloqueios de agenda. |
| **Gerente** | Gerencia sua unidade, profissionais, secretárias e agendas vinculadas à unidade. |
| **Administrador da Rede / Proprietário** | Visualiza e administra a rede de forma global. |
| **Administrador Técnico Clínica-Tech** | Acesso técnico excepcional para manutenção e suporte, com ações controladas e auditáveis. |

---

## 6. Funcionamento geral

### 6.1 Agendamento pelo WhatsApp

Fluxo definido:

**Site → WhatsApp → aviso de privacidade → CPF → identificação/cadastro → especialidade → profissional ou qualquer disponível → unidade → data → horário → confirmação.**

Regras principais:

- o chatbot consulta a mesma agenda utilizada pela secretaria;
- somente horários disponíveis são apresentados;
- o horário só é reservado após a confirmação final;
- ao concluir, o paciente recebe profissional, unidade, data, horário e orientação para chegar com antecedência;
- cancelamento e remarcação podem ser feitos pelo WhatsApp;
- atendimento humano pelo WhatsApp fica como evolução futura.

### 6.2 Agendamento pela secretaria

A secretária utiliza o ambiente administrativo para:

1. localizar ou cadastrar o paciente;
2. selecionar especialidade/profissional;
3. consultar agendas disponíveis;
4. realizar, cancelar ou remarcar agendamentos;
5. consultar histórico de agendamentos e faltas.

A secretária pertence a uma unidade, mas pode **consultar disponibilidade e criar/cancelar/remarcar agendamentos em outras unidades**. O gerenciamento operacional da unidade continua restrito à unidade à qual está vinculada.

### 6.3 Agenda dos profissionais

Cada agenda considera:

- profissional;
- especialidade;
- unidade;
- dias de atendimento;
- horário inicial e final;
- duração padrão do atendimento por especialidade;
- bloqueios aprovados;
- horários já ocupados.

Exemplos iniciais de duração: médico 20 min, psicólogo 40 min e odontólogo 50 min. A duração pode ser ajustada mediante necessidade aprovada.

O limite diário decorre dos horários disponíveis. Encaixes são permitidos somente quando autorizados pelo profissional e realizados por funcionário autorizado.

### 6.4 Lembretes e confirmação

- um lembrete é enviado pelo WhatsApp **24 horas antes**;
- opções: **Confirmar / Remarcar / Cancelar**;
- sem resposta, a consulta continua válida;
- consulta sem confirmação não é oferecida a outro paciente.

### 6.5 Acompanhamento dos atendimentos realizados

O MVP deverá permitir acompanhar o resultado dos agendamentos, com registro mínimo de:

- **Agendada**;
- **Cancelada**;
- **Realizada**;
- **Não compareceu**.

A confirmação será tratada separadamente como **Pendente / Confirmada / Sem resposta**.

Fila eletrônica, totem e monitor de chamadas ficam para evolução futura.

---

## 7. Escopo

### 7.1 MVP — primeira versão

O MVP deverá contemplar:

1. site público com informações da rede e acesso ao WhatsApp;
2. cadastro básico de unidades, profissionais, especialidades e pacientes;
3. configuração e consulta das agendas;
4. agendamento pelo chatbot do WhatsApp;
5. agendamento diretamente pela secretaria;
6. cancelamento e remarcação;
7. lembrete e confirmação 24 horas antes;
8. consulta de agenda pelo profissional;
9. prevenção de conflitos e duplicidade de horários;
10. acompanhamento dos atendimentos realizados e faltas;
11. autenticação e controle de acesso no ambiente administrativo;
12. histórico básico e registro de alterações relevantes.

### 7.2 Evoluções futuras

- fila presencial com priorização automática;
- totem e monitor/telão de chamadas;
- atendimento humano integrado ao fluxo do WhatsApp;
- dashboard e relatórios gerenciais avançados;
- informações clínicas, diagnósticos, prescrições e prontuário eletrônico;
- exames e módulos adicionais.

### 7.3 Fora do escopo atual

- faturamento;
- financeiro;
- contabilidade;
- módulo específico de exames;
- prontuário médico;
- telemedicina.

Procedimentos realizados como parte natural da consulta podem ser tratados dentro do atendimento, sem módulo próprio nesta versão.

---

## 8. Perfis e permissões — visão de produto

| Ação | Paciente | Secretária | Profissional | Gerente | Adm. Rede | Adm. Técnico |
|---|---:|---:|---:|---:|---:|---:|
| Consultar informações públicas | Sim | Sim | Sim | Sim | Sim | Sim |
| Agendar consulta | WhatsApp | Sim | Não | Sim | Sim | Excepcional |
| Cancelar/remarcar | WhatsApp | Sim | Não | Sim | Sim | Excepcional |
| Cadastrar/alterar paciente | Não | Sim | Não | Sim | Sim | Excepcional |
| Consultar própria agenda | — | — | Sim | — | — | — |
| Consultar agendas para agendamento | — | Sim | Própria | Sim | Sim | Excepcional |
| Configurar agenda | — | Não | Solicita bloqueio | Sim | Sim | Excepcional |
| Cadastrar profissional | — | Não | Não | Sim | Sim | Excepcional |
| Cadastrar secretária | — | Não | Não | Sim | Sim | Excepcional |
| Cadastrar unidade | — | Não | Não | Não | Sim | Excepcional |
| Indicadores gerenciais | — | Não | Próprios, se aplicável | Unidade | Rede | Não é função de negócio |

**Observação:** o Administrador Técnico possui acesso apenas quando necessário para suporte/manutenção e suas ações devem ser auditáveis.

---

## 9. Requisitos funcionais

| Código | Requisito |
|---|---|
| **RF01** | O sistema deverá disponibilizar um site público com informações das unidades, profissionais, especialidades e canais de contato. |
| **RF02** | O site deverá disponibilizar acesso ao WhatsApp para início do fluxo de agendamento. |
| **RF03** | O chatbot deverá identificar/cadastrar o paciente e consultar a agenda centralizada. |
| **RF04** | O chatbot deverá permitir seleção de especialidade, profissional, unidade, data e horário disponível. |
| **RF05** | O sistema deverá efetivar o agendamento somente após confirmação final do paciente. |
| **RF06** | A secretária deverá poder cadastrar e atualizar pacientes. |
| **RF07** | A secretária deverá poder consultar disponibilidade e realizar agendamentos nas unidades da rede. |
| **RF08** | O sistema deverá permitir cancelamento e remarcação, liberando o horário anterior quando aplicável. |
| **RF09** | O sistema deverá permitir cadastrar profissionais, especialidades, unidades e agendas conforme as permissões definidas. |
| **RF10** | O profissional deverá poder consultar sua própria agenda. |
| **RF11** | O profissional deverá poder solicitar bloqueio de agenda, sujeito à aprovação do gerente. |
| **RF12** | O sistema deverá enviar lembrete 24 horas antes da consulta com opções de confirmação, remarcação ou cancelamento. |
| **RF13** | O sistema deverá registrar o resultado do agendamento como agendado, cancelado, realizado ou não compareceu. |
| **RF14** | O sistema deverá manter histórico básico de agendamentos, cancelamentos, remarcações e faltas. |
| **RF15** | O sistema deverá registrar alterações relevantes e o usuário responsável. |
| **RF16** | O sistema deverá permitir autenticação dos usuários do ambiente administrativo. |
| **RF17** | O sistema deverá aplicar permissões conforme o perfil do usuário. |
| **RF18** | O sistema deverá permitir consulta de indicadores gerenciais em evolução posterior ao MVP. |

---

## 10. Requisitos não funcionais

| Código | Requisito |
|---|---|
| **RNF01 — Segurança** | O ambiente administrativo deverá exigir autenticação individual e autorização por perfil. |
| **RNF02 — Privacidade** | O sistema deverá coletar apenas dados necessários e informar ao paciente a finalidade de uso. |
| **RNF03 — Integridade** | O sistema deverá impedir duplicidade de agendamento para o mesmo profissional, unidade, data e horário, inclusive em acessos simultâneos. |
| **RNF04 — Disponibilidade** | A solução deverá estar disponível pela internet, ressalvadas indisponibilidades técnicas. |
| **RNF05 — Backup** | Os dados relevantes deverão possuir mecanismo de backup e recuperação. |
| **RNF06 — Acessibilidade** | A interface deverá considerar linguagem clara, contraste adequado, navegação compreensível, uso por teclado e compatibilidade conceitual com tecnologias assistivas. |
| **RNF07 — Responsividade** | A solução deverá ser projetada para uso em computador e dispositivos móveis. |
| **RNF08 — Usabilidade** | Formulários e mensagens deverão utilizar instruções claras e não depender exclusivamente de cores. |
| **RNF09 — Desempenho** | Consultas de disponibilidade e operações de agendamento deverão responder em tempo adequado ao uso cotidiano. |
| **RNF10 — Auditoria** | Operações relevantes deverão ser registradas para rastreabilidade. |

---

## 11. Regras de negócio

| Código | Regra |
|---|---|
| **RN01** | Um profissional não poderá possuir dois atendimentos no mesmo horário, ainda que em unidades diferentes. |
| **RN02** | Somente horários pertencentes à agenda ativa e não bloqueada poderão ser disponibilizados. |
| **RN03** | O horário somente será ocupado após a confirmação final do agendamento. |
| **RN04** | Um cancelamento deverá liberar o horário correspondente. |
| **RN05** | Uma remarcação deverá liberar o horário anterior e reservar o novo horário. |
| **RN06** | Uma consulta sem resposta ao lembrete continuará válida e não poderá ser oferecida a outra pessoa. |
| **RN07** | Encaixes não serão oferecidos pelo chatbot e dependerão de autorização do profissional. |
| **RN08** | Bloqueios de agenda solicitados pelo profissional dependerão de aprovação do gerente. |
| **RN09** | A secretária poderá consultar e realizar agendamentos em outras unidades, mas não administrar configurações operacionais dessas unidades. |
| **RN10** | O gerente administrará apenas sua unidade. |
| **RN11** | O Administrador da Rede terá visão global e poderá cadastrar novas unidades e gerentes. |
| **RN12** | O Administrador Técnico utilizará acesso excepcional apenas para suporte/manutenção, com registro das ações. |
| **RN13** | O paciente não precisará de login para utilizar o site e o fluxo de WhatsApp. |
| **RN14** | O atendimento prioritário não altera a disponibilidade da agenda e será tratado em evolução futura da organização presencial. |

---

## 12. Dados principais

### 12.1 Paciente — dados mínimos previstos

**Obrigatórios:**

- nome completo;
- CPF;
- data de nascimento;
- telefone/WhatsApp.

**Opcional quando necessário:**

- condição de atendimento prioritário ou necessidade de acessibilidade.

E-mail, endereço e sexo/gênero não fazem parte dos dados mínimos do MVP, salvo necessidade posterior devidamente justificada.

### 12.2 Demais informações necessárias ao produto

- unidades e endereços;
- profissionais e especialidades;
- vínculo do profissional com uma ou mais unidades;
- agendas, horários e bloqueios;
- agendamentos;
- status de confirmação;
- resultado do atendimento;
- histórico de alterações e usuário responsável.

---

## 13. Benefícios esperados

- **Paciente:** maior facilidade e celeridade para localizar disponibilidade e agendar.
- **Secretária:** menor dependência de controles dispersos e maior facilidade de gerenciamento das agendas.
- **Profissional:** visualização organizada da própria agenda.
- **Gerente:** visão estruturada da operação da unidade.
- **Proprietário:** visão centralizada da rede.

A solução pode contribuir para reduzir conflitos de horário, retrabalho, falhas de comunicação e faltas por meio de lembretes e confirmações, sem prometer eliminação total desses problemas.

---

## 14. Limitações, riscos e cuidados

- dependência de internet e da disponibilidade dos serviços integrados ao WhatsApp;
- possibilidade de indisponibilidade temporária do sistema;
- risco de preenchimento incorreto de dados;
- tentativas simultâneas de reserva do mesmo horário;
- risco de acesso indevido ou compartilhamento de credenciais;
- necessidade de backup e recuperação;
- necessidade de linguagem simples para usuários com baixa familiaridade digital;
- situações excepcionais podem exigir atendimento por telefone ou presencial.

Quando a integração com WhatsApp estiver indisponível, o site continuará exibindo o telefone da clínica e o atendimento poderá ocorrer por telefone ou presencialmente.

---

## 15. Privacidade e responsabilidade no uso dos dados

- coletar somente os dados necessários ao serviço;
- apresentar aviso de privacidade antes da coleta de dados pelo chatbot;
- restringir visualização e alteração conforme a função do usuário;
- utilizar credenciais individuais;
- registrar operações relevantes;
- evitar exposição pública de informações pessoais;
- transmitir informações de forma segura;
- ampliar controles caso futuramente sejam incorporados dados clínicos ou prontuários.

---

## 16. Modelo de contratação

A solução será oferecida como **serviço**, com:

- taxa inicial de implantação;
- mensalidade proporcional à quantidade de profissionais;
- hospedagem, manutenção, suporte e atualizações incluídos;
- custos previstos da integração com WhatsApp incluídos.

Não serão apresentados valores monetários no pitch.

---

## 17. Papel profissional — Product Owner + Analista de Requisitos

### 17.1 O que faz

O **Product Owner** representa as necessidades do negócio e dos usuários, define prioridades e mantém clareza sobre o valor e o escopo do produto. O **Analista de Requisitos** investiga, organiza e documenta necessidades, regras e restrições para que a equipe possa trabalhar sobre uma definição comum.

### 17.2 Responsabilidades neste projeto

- compreender o problema apresentado pela cliente;
- definir objetivo e proposta da solução;
- identificar usuários e necessidades;
- definir escopo, MVP e evoluções futuras;
- consolidar requisitos funcionais, não funcionais e regras de negócio;
- priorizar funcionalidades;
- registrar decisões de produto;
- fornecer insumos comuns aos integrantes;
- revisar PRs quanto à coerência com produto, escopo e requisitos;
- validar mudanças que alterem requisitos ou regras de negócio.

### 17.3 Competências importantes

- visão sistêmica;
- comunicação;
- organização;
- capacidade analítica;
- priorização;
- entendimento do problema do cliente;
- negociação e tomada de decisão;
- documentação objetiva.

### 17.4 Entregas do PO/Requisitos no Clínica-Tech

- alinhamento inicial da equipe;
- definição da estrutura de trabalho no GitHub;
- documento oficial de produto e requisitos;
- definição do MVP;
- requisitos e regras de negócio;
- critérios comuns para revisão das entregas;
- apresentação da visão do produto;
- validação das contribuições submetidas por Pull Request.

### 17.5 Limites do papel

O PO não define detalhes técnicos que pertencem à especialidade de quem executará a solução, como ferramenta de prototipação, tecnologia visual, linguagem de programação, arquitetura específica ou plataforma de banco de dados. Essas escolhas devem respeitar os requisitos e o escopo definidos, mas permanecem sob responsabilidade técnica de quem as propõe.

### 17.6 Risco da ausência do papel

Sem uma referência comum de produto e requisitos, cada participante poderia interpretar o problema de forma diferente, criar funcionalidades incompatíveis ou produzir artefatos que não se conectam entre si.

---

# 18. Bloco comum de insumos para as demais entregas

Este documento é a **fonte oficial de produto**. Qualquer entrega técnica deverá respeitar, no mínimo:

1. **Problema e objetivo:** seções 2 e 3;
2. **Formato da solução:** seção 4;
3. **Usuários:** seção 5;
4. **Fluxos e funcionamento:** seção 6;
5. **MVP, evolução e fora do escopo:** seção 7;
6. **Permissões:** seção 8;
7. **Requisitos funcionais:** seção 9;
8. **Requisitos não funcionais:** seção 10;
9. **Regras de negócio:** seção 11;
10. **Dados:** seção 12;
11. **Benefícios, riscos, privacidade e acessibilidade:** seções 13 a 15.

**Regra de governança:** funcionalidades, regras ou perfis não previstos neste documento não devem ser incorporados como decisão definitiva sem validação do PO.

## 18.1 Títulos-padrão para os documentos individuais

No que couber a cada papel, recomenda-se utilizar esta estrutura para facilitar a leitura e a comparação das entregas:

1. **Papel profissional**
2. **Principais responsabilidades**
3. **Conhecimentos e competências**
4. **Aplicação no Clínica-Tech**
5. **Decisões e entregas da área**
6. **Integração com o projeto**
7. **Riscos, limitações e cuidados**
8. **Pontos a validar com o PO**

---

# 19. Insumos específicos por integrante

## 19.1 UX/UI + Acessibilidade

Utilizar especialmente:

- **4.2 Site público**;
- **5. Usuários e perfis**;
- **6.1 Agendamento pelo WhatsApp**;
- **6.2 Agendamento pela secretaria**;
- **6.4 Lembretes e confirmação**;
- **7.1 MVP**;
- **10. RNF06, RNF07 e RNF08**;
- **12. Dados mínimos do paciente**;
- **13. Benefícios esperados**;
- **14. Limitações e riscos**.

Decisões já fixadas para servir de base:

- paciente sem login;
- linguagem simples;
- público inclui idosos e pessoas com baixa familiaridade digital;
- boa legibilidade e contraste;
- não depender exclusivamente de cores;
- solução projetada para computador e dispositivos móveis;
- fluxo principal do paciente ocorre pelo WhatsApp;
- ambiente administrativo precisa facilitar consulta de agenda e agendamento pela secretária.

## 19.2 Front-end

Utilizar especialmente:

- **4. Formato e proposta da solução**;
- **5. Usuários e perfis**;
- **6. Funcionamento geral**;
- **7.1 MVP**;
- **8. Perfis e permissões**;
- **9. RF01, RF02, RF06, RF07, RF08, RF10, RF13, RF16 e RF17**;
- **10. Requisitos não funcionais**, principalmente acessibilidade, responsividade e usabilidade.

Decisões já fixadas para servir de base:

- site público e ambiente administrativo separados por finalidade;
- páginas públicas devem apresentar unidades, profissionais, especialidades, localização e contato;
- o ambiente administrativo deve exigir autenticação;
- as telas devem respeitar os diferentes perfis e permissões;
- o documento não exige aplicação funcional completa, podendo trabalhar com estrutura semântica e representação das telas.

## 19.3 Back-end + Segurança

Utilizar especialmente:

- **5. Usuários e perfis**;
- **6. Funcionamento geral**;
- **7.1 MVP**;
- **8. Perfis e permissões**;
- **9. Requisitos funcionais**;
- **10. RNF01, RNF02, RNF03, RNF04, RNF05, RNF09 e RNF10**;
- **11. Regras de negócio**;
- **12. Dados principais**;
- **14 e 15. Riscos, privacidade e responsabilidade**.

Decisões já fixadas para servir de base:

- chatbot e secretaria consultam a mesma agenda;
- reserva somente após confirmação final;
- prevenção obrigatória de duplicidade;
- autorização por perfil;
- ações técnicas excepcionais devem ser auditáveis;
- cancelamento libera horário;
- remarcação troca a reserva do horário;
- lembrete 24h antes;
- histórico e rastreabilidade de alterações.

## 19.4 Banco de Dados + QA/Testes

Utilizar especialmente:

- **5. Usuários e perfis**;
- **6. Funcionamento geral**;
- **7.1 MVP**;
- **8. Perfis e permissões**;
- **9. Requisitos funcionais**;
- **10. RNF03, RNF05 e RNF10**;
- **11. Regras de negócio**;
- **12. Dados principais**;
- **14. Limitações e riscos**.

Decisões já fixadas para servir de base:

- unidades, profissionais, especialidades, pacientes, agendas e agendamentos precisam se relacionar;
- um profissional pode atender em mais de uma unidade;
- um profissional não pode ocupar dois locais no mesmo horário;
- histórico de cancelamentos, remarcações, faltas e alterações deve ser preservado;
- CPF identifica o paciente no fluxo proposto;
- operações críticas devem ser testadas também em cenários negativos, especialmente conflito de horário, permissões, cancelamento, remarcação e duplicidade.

---

## 20. Controle de mudanças

Este documento deverá ser atualizado sempre que uma decisão aprovada alterar:

- escopo;
- MVP;
- requisitos;
- regras de negócio;
- perfis ou permissões;
- dados obrigatórios;
- funcionamento dos fluxos principais.

Mudanças propostas pelos integrantes devem ser submetidas ao PO antes de serem tratadas como requisito definitivo.
