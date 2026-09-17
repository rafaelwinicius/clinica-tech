# Back-end e Segurança da Informação

## 1. Papel profissional
O desenvolvedor Back-end é responsável pela lógica central de processamento, regras de negócio, integrações, controle de concorrência e persistência confiável de dados da plataforma. No projeto Clínica-Tech, a camada de Segurança da Informação atua de forma transversal ao desenvolvimento, estabelecendo mecanismos de autenticação, autorização granular baseada em perfis, controle de privilégios mínimos, trilha de auditoria e proteção aos dados trafegados e armazenados.

* **Principais responsabilidades:** Implementar os fluxos transacionais de agendamento, consulta, bloqueio e cancelamento; aplicar rigorosamente as regras de concorrência e integridade; estruturar autenticação e autorização por perfis; registrar logs de operações críticas.
* **Competências centrais:** Arquitetura de APIs, modelagem relacional, gerenciamento de transações com controle de concorrência, princípios de segurança defensiva e privacidade por padrão.
* **Entregas nucleares:** Endpoints e serviços para consumo do chatbot e do portal web, validações de integridade da agenda, mecanismos de autenticação e política de auditoria.

## 2. Atuação no Clínica-Tech
No Clínica-Tech, a camada de back-end converte os requisitos funcionais e regras de negócio definidos pelo PO em serviços determinísticos. Requisitos como "impedir horários conflitantes para o mesmo profissional" ou "permitir agendamento tanto por WhatsApp quanto pela recepção" deixam de ser conceitos abstratos e tornam-se transações atômicas com validações imediatas no servidor, garantindo que o estado da agenda permaneça sempre íntegro e consistente para toda a rede.

## 3. Funcionamento geral
O processamento de qualquer requisição segue um fluxo unidirecional e controlado:

```
[Interface Web / Chatbot WhatsApp]
               │
               ▼  (1) Requisição com parâmetros (payload)
       [Camada de API]
               │
               ▼  (2) Autenticação e Verificação de Permissão (Perfil)
  [Regras de Negócio e Validações]
               │
               ▼  (3) Transação Atômica / Isolamento
      [Banco de Dados]
               │
               ▼  (4) Resposta padronizada (Sucesso ou Erro semântico)
```

1. **Recepção:** A interface administrativa ou a integração de webhook do WhatsApp envia os dados da operação.
2. **Autorização e Validação Prévia:** O back-end verifica se o autor possui permissão para executar a operação e se os dados obrigatórios foram informados.
3. **Aplicação de Regras:** Regras de negócio como verificação de conflitos de agenda, status de bloqueio e confirmação são avaliadas.
4. **Persistência / Consulta:** A operação é executada no banco sob garantia de isolamento.
5. **Retorno:** O sistema retorna uma resposta clara de confirmação ou o motivo específico pelo qual a operação não pôde ser concluída.

## 4. Principais operações

### 4.1 Consulta de Disponibilidade
* **Entrada:** Unidade, especialidade, profissional (opcional) e período de data.
* **Validação:** Validade dos identificadores de unidade/especialidade e coerência do intervalo de datas.
* **Regra Aplicada (RN02):** Apenas horários de agendas ativas, dentro do expediente, sem bloqueios aprovados e sem agendamento já confirmado são elegíveis.
* **Resultado:** Lista padronizada de janelas e horários livres disponíveis para reserva.

### 4.2 Realização de Agendamento
* **Entrada:** Identificação do paciente (Nome, CPF, data de nascimento, telefone), unidade, profissional, especialidade, data e horário selecionado.
* **Validação:** Consistência dos dados obrigatórios mínimos (Seção 12.1) e verificação do consentimento de privacidade antes da reserva.
* **Regras Aplicadas (RN01, RN03 e RNF03):** O profissional não pode ter outro agendamento no mesmo horário (mesmo em unidade diferente); a vaga só é ocupada após confirmação final explícita; o processo é protegido contra concorrência simultânea.
* **Resultado:** Registro do agendamento com status inicial `Agendada` e confirmação retornada ao canal de origem.

### 4.3 Confirmação e Lembrete
* **Entrada:** Resposta do paciente ao lembrete de 24h (`Confirmar`, `Remarcar` ou `Cancelar`).
* **Validação:** Identificador do agendamento e coerência do estado atual.
* **Regra Aplicada (RN06, RF12):** Se confirmado, o status de confirmação passa para `Confirmada`; se sem resposta, a consulta segue válida e não é liberada a terceiros.
* **Resultado:** Atualização do status de confirmação do agendamento.

### 4.4 Cancelamento
* **Entrada:** Identificador do agendamento e identificador do solicitante (paciente via WhatsApp ou usuário administrativo).
* **Validação:** Existência da consulta e permissão para cancelamento.
* **Regra Aplicada (RN04):** O cancelamento atualiza o resultado do agendamento para `Cancelada` e libera imediatamente o horário na agenda ativa do profissional.
* **Resultado:** Horário liberado para novas consultas e log de auditoria gerado.

### 4.5 Remarcação
* **Entrada:** Identificador do agendamento atual e nova data/horário/unidade desejada.
* **Validação:** Disponibilidade em tempo real do novo horário e permissão do solicitante.
* **Regra Aplicada (RN05):** O horário antigo é liberado e a nova vaga é reservada na mesma operação transacional.
* **Resultado:** Registro de reagendamento salvo com preservação do histórico.

### 4.6 Acompanhamento do Atendimento
* **Entrada:** ID da consulta e atualização de desfecho (`Realizada` ou `Não compareceu`) informada pela secretaria/unidade.
* **Validação:** Consulta deve estar no status `Agendada` e ter data/horário compatível com a execução.
* **Regra Aplicada (RF13, RF14):** Registro definitivo do desfecho do atendimento e consolidação no histórico do paciente.
* **Resultado:** Histórico atualizado para fins operacionais da clínica.

### 4.7 Solicitação e Aprovação de Bloqueio de Agenda
* **Entrada:** Identificador do profissional, intervalo de data/horário e justificativa.
* **Validação:** Verificação se o usuário logado é o próprio profissional solicitante ou o gerente da unidade responsável.
* **Regras Aplicadas (RN08, RN10):** Solicitações feitas por profissionais ficam em estado pendente até aprovação formal do gerente de sua respectiva unidade; gerentes só podem aprovar bloqueios da sua própria unidade.
* **Resultado:** Período marcado como bloqueado na agenda do profissional, indisponibilizando novos horários no período.

## 5. Aplicação das regras de negócio
O sistema impede situações inválidas diretamente na camada de domínio da aplicação:

* **Conflito de locais para o mesmo profissional (RN01):** Antes de confirmar qualquer vaga, o back-end valida se o profissional já possui agendamento no mesmo instante em qualquer unidade da rede, rejeitando a operação caso haja sobreposição de horários.
* **Tentativas concorrentes de reserva (RNF03):** Se dois pacientes (ou paciente e secretária) tentam reservar o mesmo horário ao mesmo tempo, o back-end utiliza controle de concorrência no banco; a primeira solicitação confirmada garante o espaço e a segunda recebe aviso de indisponibilidade.
* **Encaixes indevidos (RN07):** O chatbot é desprovido de lógica ou permissão para cadastrar encaixes; no painel administrativo, o back-end só aceita encaixe se houver flag de autorização do profissional e perfil com permissão adequada.
* **Alterações cruzadas entre unidades (RN09, RN10):** Secretárias podem consultar e marcar consultas em outras unidades, mas o back-end barra qualquer tentativa de secretárias ou gerentes de alterar parâmetros de agendas pertencentes a outras unidades.

## 6. Perfis e permissões
Matriz de permissões estritamente alinhada às definições do Product Owner (Seção 8 do documento oficial):

| Ação | Paciente | Secretária | Profissional | Gerente | Adm. Rede | Adm. Técnico |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **Consultar informações públicas** | Sim | Sim | Sim | Sim | Sim | Sim |
| **Agendar consulta** | WhatsApp | Sim | Não | Sim | Sim | Excepcional |
| **Cancelar/remarcar** | WhatsApp | Sim | Não | Sim | Sim | Excepcional |
| **Cadastrar/alterar paciente** | Não | Sim | Não | Sim | Sim | Excepcional |
| **Consultar própria agenda** | - | - | Sim | - | - | - |
| **Consultar agendas para agendamento** | - | Sim | Própria | Sim | Sim | Excepcional |
| **Configurar agenda** | - | Não | Solicita bloqueio | Sim | Sim | Excepcional |
| **Cadastrar profissional** | - | Não | Não | Sim | Sim | Excepcional |
| **Cadastrar secretária** | - | Não | Não | Sim | Sim | Excepcional |
| **Cadastrar unidade** | - | Não | Não | Não | Sim | Excepcional |
| **Indicadores gerenciais** | - | Não | Próprios (se aplicável) | Unidade | Rede | Não é função de negócio |

*Nota:* O Administrador Técnico atua exclusivamente para manutenção/suporte de forma controlada e auditável.

## 7. Segurança da Informação
A segurança do sistema é fundamentada em mecanismos de defesa em profundidade:

* **Autenticação Individual:** Acesso ao ambiente administrativo exclusivo por credenciais individuais (sem logins genéricos ou compartilhados), com hash de senhas forte.
* **Autorização RBAC (Role-Based Access Control):** Cada endpoint valida o token do usuário e checa a matriz de papéis antes de executar qualquer ação.
* **Princípio do Menor Privilégio:** Secretárias operam apenas agendamentos; gerentes administram somente sua unidade; pacientes não possuem acesso administrativo.
* **Comunicação Segura:** Todas as trocas de mensagens e requisições ocorrem sob tráfego criptografado (HTTPS/TLS).
* **Auditoria e Rastreabilidade (RNF10, RF15):** Logs registram o autor, o timestamp, o endereço IP e a natureza de alterações críticas (ex: cancelamentos, remarcações, bloqueios de agenda e acessos excepcionais).
* **Backup e Recuperação (RNF05):** Estratégia de rotinas automáticas de backup para salvaguarda dos dados da rede de clínicas.

## 8. Privacidade e proteção de dados
A arquitetura adota as diretrizes da Lei Geral de Proteção de Dados (LGPD) com foco operacional:
* **Minimização de Dados (Privacy by Default):** São solicitados apenas os dados estritamente indispensáveis para o agendamento (Nome completo, CPF, data de nascimento e WhatsApp). Endereço, e-mail e gênero foram excluídos do MVP.
* **Transparência e Consentimento:** O chatbot apresenta aviso de privacidade informando a finalidade do uso dos dados antes do início do cadastro.
* **Isolamento de Dados Sensíveis:** O escopo do MVP não armazena prontuários, anotações médicas, exames ou dados clínicos, o que reduz substancialmente a superfície de risco.

## 9. Entregas desta área
* Especificação da arquitetura lógica de serviços e endpoints.
* Definição dos validadores das regras de negócio e prevenção de concorrência.
* Estruturação do modelo de autenticação, autorização por perfis e trilha de auditoria.
* Postagem de divulgação técnica profissional para LinkedIn.
* Apresentação executiva em slides cobrindo o fluxo transacional e a segurança da solução.

## 10. Integração com os demais papéis
* **Com Front-end:** Fornece contratos de dados (APIs) para autenticação, listagem de disponibilidades e submissão de ações administrativas.
* **Com UX/UI:** Alinha os tempos de resposta, mensagens de validação e feedback semântico de indisponibilidade ou conflito.
* **Com Banco de Dados e QA:** Valida as restrições de integridade relacional, chaves de unicidade, planos de contingência/backup e casos de testes de carga e concorrência.
* **Com o Product Owner:** Valida a conformidade de regras e reporta restrições operacionais do MVP.

## 11. Impacto da ausência desta função
A ausência de uma modelagem técnica de back-end e segurança resultaria em sobreposição de horários (dois pacientes agendados para o mesmo médico no mesmo minuto), brechas de escalada de privilégios (como secretárias configurando permissões ou profissionais alterando dados de outras unidades), exposição inadequada de dados pessoais e inconsistência na comunicação com a API do WhatsApp.

## 12. Riscos, limitações e cuidados
* **Dependência Externa:** Instabilidades no serviço integrado do WhatsApp podem reter requisições; a solução mitiga isso orientando o canal telefônico alternativo.
* **Concorrência em Horários de Pico:** Múltiplos acessos exigem controle transacional seguro no banco de dados para evitar reservas duplicadas simultâneas.
* **Falhas de Operação:** Imputação de dados incorretos ou esquecimento de cancelamentos manuais são mitigados por validações no payload e logs de rastreabilidade.

## 13. Pontos a validar com o Product Owner
1. **Janela de retenção do horário durante o fluxo do WhatsApp:** Caso o paciente selecione um horário no chatbot, quanto tempo esse horário permanece em retenção temporária antes de ser liberado novamente para outros usuários, caso a confirmação final não ocorra imediatamente?
2. **Tratamento de faltas reincidentes:** Na evolução do histórico de faltas (`Não compareceu`), haverá bloqueio automático temporário ou regras de alerta para novos agendamentos via chatbot?
3. **Comportamento da agenda frente a bloqueios retroativos:** Se o gerente aprovar um bloqueio de agenda em um período onde já existiam consultas agendadas, qual fluxo de notificação ao paciente o back-end deve disparar?
