# Postagem para LinkedIn — Front-end

**Empresa:** Clínica-Tech
**Papel:** Desenvolvimento Front-end

## Texto da publicação

Interface não é só o que aparece na tela. É a forma como uma regra do negócio chega até a pessoa que vai usá-la.

Na Clínica-Tech, atuo no **Front-end** da plataforma web integrada ao WhatsApp que estamos concebendo para apoiar o agendamento e o acompanhamento dos atendimentos de uma rede de clínicas populares.

Nesta etapa do projeto, meu trabalho foi transformar os requisitos definidos pelo Product Owner e os fluxos aprovados por UX/UI em uma estrutura de telas: o que cada perfil vê, quais informações aparecem e quais ações ficam disponíveis. O resultado foi a separação clara entre o **site público**, informativo e sem login, e o **ambiente administrativo**, autenticado e sensível ao perfil de quem acessa.

Uma decisão que considero importante foi começar pela **estrutura semântica** das páginas. Usar `header`, `nav`, `main`, `section`, `form` e `table` com `label` e `caption` não é detalhe de código: é o que permite navegação por teclado, leitura por tecnologias assistivas e títulos que fazem sentido para quem não enxerga a tela. Como parte do público da rede é composta por pessoas idosas e com pouca familiaridade digital, a acessibilidade entrou no início do desenho da interface, e não como ajuste final.

Outro cuidado foi com os formulários, que concentram o maior risco de erro: rótulo visível em todo campo, obrigatoriedade indicada por texto e não apenas por cor, mensagens que explicam como corrigir o problema e confirmação explícita antes de ações como cancelar uma consulta.

Registro também um ponto que aprendi na prática: esconder um botão na interface **não é** controle de acesso. A tela reflete a permissão do usuário, mas quem autoriza de fato é o back-end. Esse alinhamento com as áreas de back-end e segurança evita uma falsa sensação de proteção.

O sistema ainda está em fase de definição e documentação. O que temos hoje é uma base estruturada o suficiente para que a implementação comece sem improviso.

#FrontEnd #HTML #Acessibilidade #DesenvolvimentoWeb #UXUI #Tecnologia #Saude
