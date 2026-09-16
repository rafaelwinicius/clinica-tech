# Front-end

**Projeto:** Clínica-Tech — plataforma web integrada ao WhatsApp para uma rede de clínicas populares (Valentina, Mangabeira, Bancários, Expedicionários e Manaíra).

**Fonte oficial das decisões de produto:** `01-produto-requisitos/produto-e-requisitos.md`. Este documento descreve apenas a atuação da área de Front-end e não altera escopo, MVP, perfis ou regras de negócio.

---

## 1. Papel profissional

### 1.1 O que faz

A pessoa desenvolvedora **Front-end** é responsável pela camada da aplicação com a qual o usuário interage diretamente no navegador. Ela recebe os requisitos definidos pelo Product Owner e os fluxos e telas definidos por UX/UI e transforma esse material em páginas reais: estrutura das informações, formulários, navegação, estados de tela e exibição das informações fornecidas pelo Back-end.

### 1.2 Principais responsabilidades

- estruturar as páginas com HTML semântico, organizando cabeçalho, navegação, conteúdo principal, seções e rodapé;
- transformar os fluxos aprovados de UX/UI em telas navegáveis;
- construir os formulários do sistema (login, busca e cadastro de paciente, agendamento), com rótulos, campos e mensagens claras;
- exibir as informações vindas do Back-end (agendas, horários disponíveis, agendamentos, status) e enviar as ações do usuário;
- garantir que cada perfil visualize apenas as opções compatíveis com suas permissões;
- aplicar os requisitos de acessibilidade, responsividade e usabilidade (RNF06, RNF07 e RNF08) na interface;
- tratar os estados da interface: carregando, vazio, erro, sucesso e sem permissão;
- manter a consistência visual e de linguagem entre todas as telas.

### 1.3 Conhecimentos e competências

**Técnicos:** HTML semântico, elementos de multimídia, noções de CSS e de layout responsivo, noções de JavaScript para interação, leitura de protótipos, consumo de dados fornecidos por uma API, boas práticas de acessibilidade (uso de teclado, contraste, leitores de tela) e versionamento com Git/GitHub.

**Comportamentais:** atenção a detalhes, leitura cuidadosa de requisitos, comunicação com UX/UI e Back-end, capacidade de perguntar antes de assumir uma regra e empatia com usuários de baixa familiaridade digital.

### 1.4 Entregas típicas da função

Estrutura das páginas, componentes reutilizáveis de interface, formulários, telas do ambiente administrativo, páginas públicas, checklist de acessibilidade aplicado à interface e documentação da estrutura das telas.

---

## 2. Atuação no Clínica-Tech

O ponto de partida do Front-end é sempre um requisito. O caminho de trabalho adotado é:

```text
Requisito (PO) → Fluxo e tela (UX/UI) → Estrutura HTML e formulários (Front-end) → Dados e regras (Back-end)
```

Exemplo prático, a partir do **RF07** ("a secretária deverá poder consultar disponibilidade e realizar agendamentos nas unidades da rede"):

1. o requisito define **o que** precisa existir;
2. o UX/UI define **como** o fluxo será percorrido: buscar paciente → escolher especialidade → ver horários → confirmar;
3. o Front-end define **a estrutura da página**: um `main` com a seção de busca, uma seção com os horários disponíveis e um formulário de confirmação;
4. o Back-end fornece os horários realmente livres e efetiva a reserva, aplicando a **RN03** (o horário só é ocupado após a confirmação final).

Duas decisões de produto orientam toda a estrutura do Front-end:

- **o paciente não tem login** (RN13): as páginas públicas são apenas informativas e conduzem ao WhatsApp e ao telefone;
- **o ambiente administrativo exige autenticação** (RF16) e **respeita perfis** (RF17): a interface muda conforme o usuário conectado.

Por isso o Front-end é dividido em dois conjuntos de páginas com finalidades distintas: **site público** e **ambiente administrativo**.

---

## 3. Principais interfaces

### 3.1 Site público (sem login)

| Tela | Usuário | Finalidade | Informações exibidas | Ações possíveis |
|---|---|---|---|---|
| **Página inicial** | Paciente / público geral | Apresentar a rede e conduzir ao agendamento | Nome da rede, resumo dos serviços, destaque das especialidades, botão de WhatsApp e telefone | Ir para o WhatsApp, ligar, navegar para as demais páginas |
| **Unidades** | Paciente | Localizar a unidade mais próxima | As cinco unidades com endereço, horário de funcionamento e telefone | Ver detalhe da unidade, abrir a localização, ligar |
| **Profissionais e especialidades** | Paciente | Saber quem atende e em quais unidades | Especialidades, profissionais e unidades onde atendem | Filtrar por especialidade ou unidade, seguir para o WhatsApp |
| **Como agendar** | Paciente | Explicar o fluxo do agendamento | Passo a passo do atendimento pelo WhatsApp e aviso de que o telefone continua disponível | Iniciar conversa no WhatsApp, ligar para a clínica |

Nenhuma dessas páginas exibe dados pessoais de pacientes ou a agenda interna. O agendamento do paciente acontece **fora do site**, no WhatsApp (RF02).

### 3.2 Ambiente administrativo (com login)

| Tela | Usuário | Finalidade | Informações exibidas | Ações possíveis |
|---|---|---|---|---|
| **Login** | Secretária, profissional, gerente, administrador | Autenticar o usuário (RF16) | Campos de identificação e senha, mensagem de erro genérica | Entrar |
| **Agenda do dia (painel)** | Secretária, gerente | Visão operacional imediata | Data, unidade, profissionais, horários, paciente, status de confirmação e resultado | Filtrar por data, profissional ou unidade; abrir um agendamento |
| **Busca e cadastro de paciente** | Secretária, gerente | Localizar ou cadastrar o paciente (RF06) | Resultado da busca por CPF ou nome; formulário com nome, CPF, nascimento e telefone | Buscar, cadastrar, atualizar dados |
| **Disponibilidade e novo agendamento** | Secretária, gerente | Agendar nas unidades da rede (RF07, RN09) | Especialidade, profissional, unidade, data e apenas horários livres | Selecionar horário, confirmar agendamento |
| **Detalhe do agendamento** | Secretária, gerente | Acompanhar o agendamento até seu desfecho (RF08, RF13) | Dados da consulta, status de confirmação e histórico | Cancelar, remarcar, registrar "realizada" ou "não compareceu" |
| **Minha agenda** | Profissional | Consultar a própria agenda (RF10) | Consultas do dia e da semana, unidade, horário e paciente | Visualizar, solicitar bloqueio de agenda (RF11) |
| **Solicitação de bloqueio** | Profissional | Informar indisponibilidade (RN08) | Período solicitado e situação da solicitação | Enviar solicitação, acompanhar aprovação |
| **Cadastros (unidades, profissionais, agendas)** | Gerente, administrador da rede | Manter a base da operação (RF09) | Listas e formulários de cadastro conforme permissão | Cadastrar, editar, configurar agenda |

**Regra de interface ligada a permissões (RF17):** cada tela apresenta apenas as ações permitidas ao perfil conectado. O profissional visualiza a própria agenda, mas não vê botões de agendar ou cancelar; a secretária consulta agendas de outras unidades, mas não acessa as telas de configuração dessas unidades (RN09).

> Cuidado importante: esconder um botão **não é** controle de acesso. A interface reflete a permissão, mas a autorização é sempre validada pelo Back-end (RNF01).

---

## 4. Estrutura semântica

As páginas são estruturadas com elementos HTML semânticos, de modo que o conteúdo faça sentido tanto visualmente quanto para leitores de tela.

| Elemento | Uso no Clínica-Tech |
|---|---|
| `header` | Identificação da rede no site público; identificação do usuário e da unidade no ambiente administrativo |
| `nav` | Menu do site (Início, Unidades, Profissionais, Como agendar) e menu do ambiente administrativo |
| `main` | Conteúdo principal e único de cada página |
| `section` | Blocos temáticos: lista de unidades, horários disponíveis, dados do paciente |
| `article` | Item independente, como o cartão de uma unidade ou de um profissional |
| `h1` a `h3` | Hierarquia de títulos, sem pular níveis |
| `form`, `label`, `input`, `select`, `button` | Todos os formulários do sistema |
| `table`, `caption`, `th`, `td` | Agenda do dia e listagens de agendamentos |
| `footer` | Contato, telefone e aviso de privacidade |

Exemplo reduzido — lista de unidades no site público:

```html
<main>
  <h1>Nossas unidades</h1>
  <section>
    <article>
      <h2>Unidade Mangabeira</h2>
      <p>Endereço e horário de funcionamento</p>
      <a href="tel:...">Telefone da unidade</a>
    </article>
  </section>
</main>
```

Exemplo reduzido — agenda do dia no ambiente administrativo:

```html
<table>
  <caption>Agenda de 17/09 — Unidade Bancários</caption>
  <thead>
    <tr><th>Horário</th><th>Profissional</th><th>Paciente</th><th>Status</th></tr>
  </thead>
  <tbody>
    <tr><td>08:00</td><td>Profissional exemplo</td><td>Paciente exemplo</td><td>Confirmada</td></tr>
  </tbody>
</table>
```

O uso de `table` aqui é intencional: a agenda é um dado tabular real, com relação entre linha e coluna. Com `th` e `caption`, a leitura assistiva consegue anunciar a que coluna cada informação pertence.

---

## 5. Formulários e interação

Os formulários são o ponto mais sensível da interface, porque concentram entrada de dados e risco de erro — risco já registrado no item 14 do documento de produto ("risco de preenchimento incorreto de dados").

**Formulários previstos:** login, busca de paciente, cadastro e atualização de paciente, novo agendamento, cancelamento, remarcação, registro do resultado do atendimento e solicitação de bloqueio de agenda.

**Critérios de construção adotados:**

- todo campo tem um `label` visível e associado ao campo (`for` / `id`); o rótulo não é substituído por texto dentro do campo;
- o tipo do campo acompanha o dado: texto para nome, data para nascimento, telefone para WhatsApp, campo numérico com máscara para CPF, seleção para especialidade, profissional e unidade;
- campos obrigatórios são indicados por texto, e não apenas por cor (RNF08);
- mensagens de erro ficam próximas ao campo, explicam o problema e como corrigir — "Informe o CPF com 11 dígitos", em vez de "Dado inválido";
- o formulário mantém os dados já preenchidos quando ocorre um erro;
- a validação no navegador serve apenas para ajudar o usuário; **a validação que vale é a do Back-end**;
- ações destrutivas, como cancelar uma consulta, exigem confirmação explícita e informam a consequência (RN04: o horário será liberado).

Exemplo reduzido — bloco do formulário de busca/cadastro de paciente:

```html
<form>
  <label for="cpf">CPF (obrigatório)</label>
  <input id="cpf" name="cpf" type="text" inputmode="numeric" required>
  <p id="ajuda-cpf">Digite apenas números.</p>
  <button type="submit">Buscar paciente</button>
</form>
```

**Interação no agendamento:** a tela exibe **somente horários livres** (RN02) e, ao selecionar um horário, mostra um resumo com profissional, unidade, data e hora antes da confirmação final. A reserva só é enviada quando o usuário confirma (RN03). Se o horário for ocupado por outro usuário nesse intervalo (RNF03), a interface precisa exibir mensagem clara e recarregar a lista de horários, em vez de falhar em silêncio.

---

## 6. Acessibilidade no Front-end

A acessibilidade é requisito do produto (RNF06 e RNF08) e diretriz de UX/UI. No Front-end, ela se traduz em decisões de estrutura:

- **navegação por teclado:** todas as ações usam elementos nativos (`button`, `a`, `input`), garantindo foco e acionamento por Tab e Enter, com indicador de foco visível;
- **leitores de tela:** hierarquia correta de títulos, uso de `label`, `caption` em tabelas e texto alternativo em imagens informativas;
- **contraste e legibilidade:** contraste adequado entre texto e fundo e tamanho de fonte confortável, considerando o público idoso atendido pela rede;
- **não depender de cor:** o status de uma consulta é indicado por texto somado à cor — por exemplo "Cancelada" —, nunca apenas pela cor;
- **linguagem simples:** rótulos e mensagens sem jargão técnico ("Horário disponível", "Consulta cancelada");
- **responsividade (RNF07):** a mesma estrutura semântica serve para computador e celular, com alvos de toque adequados — importante para a secretaria, que usa o sistema o dia inteiro, e para a gestão, que pode acessar pelo celular;
- **conteúdo multimídia:** se o site público usar vídeo ou áudio explicando como agendar, é necessário prever legenda e texto equivalente, sem reprodução automática.

---

## 7. Entregas desta área

1. **Mapa de telas** do site público e do ambiente administrativo, com usuário, finalidade e ações de cada tela (seção 3).
2. **Estrutura semântica de referência** das páginas, indicando os elementos HTML de cada região (seção 4).
3. **Padrão de formulários**: rótulos, tipos de campo, obrigatoriedade, mensagens de erro e confirmação (seção 5).
4. **Checklist de acessibilidade aplicada à interface** (seção 6).
5. **Regras de exibição por perfil**, indicando o que cada usuário vê em cada tela (seção 3.2).
6. **Lista das informações que a interface precisa receber do Back-end** e das ações que precisa enviar.
7. Documentação da área, postagem individual para o LinkedIn e apresentação da contribuição.

> Conforme o escopo da atividade, não há implementação funcional: a entrega é a definição estruturada da interface.

---

## 8. Integração com os demais papéis

| Papel | O que o Front-end recebe | O que o Front-end devolve |
|---|---|---|
| **PO / Análise de Requisitos** | Requisitos, MVP, perfis, permissões e regras de negócio | Dúvidas de interface, pontos não previstos e impacto das decisões nas telas |
| **UX/UI + Acessibilidade** | Fluxos, protótipo, hierarquia da informação e diretrizes de acessibilidade | Viabilidade da estrutura, ajustes de conteúdo por tela e estados não previstos (vazio, erro, sem permissão) |
| **Back-end + Segurança** | Dados de agendas, horários disponíveis, agendamentos, perfil do usuário e mensagens de erro | Ações do usuário, informações necessárias por tela e comportamento esperado nos erros |
| **Banco de Dados + QA** | Estrutura e comportamento dos dados; cenários de teste | Telas e fluxos a serem testados, principalmente conflito de horário, cancelamento, remarcação e permissões |

O Front-end é um ponto de encontro do projeto: sem UX/UI não há definição de fluxo; sem Back-end não há dado real; sem PO não há certeza sobre a regra.

---

## 9. Impacto da ausência desta função

Sem alguém responsável pelo Front-end:

- o protótipo de UX/UI permaneceria como imagem, sem se tornar uma interface utilizável no navegador;
- as regras e os dados do Back-end não teriam por onde ser acessados pela secretária, pelo profissional e pela gestão;
- cada tela seria construída de forma improvisada por quem estivesse disponível, gerando inconsistência de navegação, de linguagem e de estrutura;
- acessibilidade e responsividade ficariam sem responsável técnico e tenderiam a ser tratadas apenas no fim do projeto, quando o custo de correção é maior;
- os requisitos de permissão (RF17) poderiam chegar à tela de forma confusa, exibindo opções que o usuário não pode executar;
- na prática, a rede continuaria dependendo de planilhas, telefone e mensagens — exatamente o problema que a solução pretende resolver.

---

## 10. Riscos, limitações e cuidados

| Risco / limitação | Cuidado adotado |
|---|---|
| Esconder um botão ser confundido com controle de acesso | A interface apenas reflete a permissão; a autorização é sempre validada pelo Back-end (RNF01) |
| Dois usuários tentarem o mesmo horário (RNF03) | Mensagem clara de horário indisponível e atualização imediata da lista de horários |
| Exposição indevida de dados pessoais na tela | O site público não exibe dados de paciente; no ambiente administrativo, exibir apenas o necessário à tarefa (RNF02) |
| Formulário longo e cansativo | Solicitar apenas os dados mínimos definidos no produto: nome, CPF, data de nascimento e telefone |
| Usuários com baixa familiaridade digital | Linguagem simples, poucas ações por tela e confirmação antes de ações irreversíveis |
| Indisponibilidade do sistema ou da integração com o WhatsApp | Telefone sempre visível no site público, conforme o item 14 do documento de produto |
| Equipe ainda em formação, com estudo concentrado em HTML semântico e multimídia | A entrega é conceitual e estrutural; CSS, JavaScript e frameworks serão detalhados em etapa posterior |
| Tela pensada apenas para computador | Estrutura definida considerando também o uso em celular (RNF07) |

---

## 11. Pontos a validar com o Product Owner

1. O site público deverá exibir **horários livres** dos profissionais ou apenas informações institucionais com encaminhamento ao WhatsApp? (entendimento atual: apenas informativo)
2. Na agenda do dia, a visão padrão da secretária deve ser **por unidade** ou **por profissional**?
3. O registro do resultado do atendimento ("realizada" / "não compareceu") será feito pela **secretária** ou pelo **profissional**, e em qual tela?
4. A solicitação de bloqueio de agenda (RF11) precisa de tela própria ou pode ser uma ação dentro de "Minha agenda"?
5. Quando a secretária agendar em **outra unidade** (RN09), a interface deve exibir aviso explícito de que a operação ocorre fora de sua unidade?
6. O site público terá conteúdo **multimídia** (por exemplo, vídeo explicando o agendamento pelo WhatsApp)? Em caso positivo, será necessário prever legenda e texto equivalente.

> Conforme a regra de governança do projeto, nenhum desses pontos foi incorporado como requisito: todos permanecem registrados para decisão do PO.
