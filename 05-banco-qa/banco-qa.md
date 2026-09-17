# Banco de Dados e QA/Testes

## 1. Papel profissional

O profissional de Banco de Dados é responsável por organizar, armazenar, proteger e disponibilizar as informações utilizadas pelo sistema. Suas principais responsabilidades incluem definir a estrutura das entidades, estabelecer os relacionamentos entre elas, garantir a integridade dos dados e aplicar mecanismos de segurança e controle de acesso. Entre suas competências estão a modelagem de dados, o entendimento das regras de negócio do produto e a capacidade de traduzir requisitos funcionais em uma estrutura de informação organizada. Como entrega, este profissional produz o modelo conceitual das entidades, as regras de integridade e as diretrizes de segurança do banco.

O profissional de QA (Quality Assurance) atua na garantia da qualidade do sistema, sendo responsável por planejar, criar e executar testes que verifiquem se as funcionalidades desenvolvidas atendem aos requisitos definidos pelo Product Owner. Suas competências envolvem pensamento analítico, atenção a cenários de erro e capacidade de documentar casos de teste de forma clara. Como entrega, o QA produz a estratégia de testes e os casos de teste que cobrem os principais fluxos do sistema.

No projeto Clínica-Tech, Banco de Dados e QA trabalham em conjunto: um estrutura onde e como a informação é guardada, o outro verifica se o que foi construído sobre essa estrutura realmente funciona como esperado.

## 2. Atuação no Clínica-Tech

A rede de clínicas populares enfrenta hoje dificuldades de gerenciamento porque parte das informações é registrada por telefone, mensagens e planilhas soltas, sem integração entre si. O Clínica-Tech busca resolver isso centralizando os principais dados da operação: pacientes, profissionais, unidades, agendamentos e atendimentos.

Nesse cenário, o Banco de Dados sustenta as funcionalidades definidas pelo PO ao garantir que cada cadastro, cada agendamento e cada atendimento tenham um local correto e consistente para serem armazenados, evitando duplicidade e perda de informação. Já o QA garante que essas funcionalidades — cadastro, agendamento, atendimento, lembretes e controle de acesso — realmente se comportem como o PO especificou, identificando falhas antes que cheguem ao usuário final.

## 3. Informações que precisam ser armazenadas

Considerando apenas o que está previsto na solução oficial, o sistema precisa armazenar:

* Dados de identificação e contato dos pacientes;
* Dados de identificação, registro profissional e especialidade dos profissionais;
* Dados das unidades da rede (endereço, contato, horário de funcionamento);
* Especialidades e serviços oferecidos pela clínica;
* Registros de agendamento (quem, com quem, onde, quando);
* Registros de atendimento efetivamente realizado;
* Lembretes enviados aos pacientes sobre suas consultas;
* Histórico de atendimentos por paciente;
* Informações de controle de acesso conforme o perfil de cada usuário.

## 4. Entidades principais

**Paciente** — finalidade: armazenar os dados de quem utiliza os serviços da clínica. Principais informações: nome, CPF, data de nascimento, telefone, e-mail, endereço e data de cadastro. Relaciona-se com Agendamento.

**Profissional** — finalidade: armazenar os dados de quem realiza os atendimentos. Principais informações: nome, CPF, registro profissional, especialidade, unidade de atendimento e status. Relaciona-se com Unidade, Especialidade e Agendamento.

**Unidade** — finalidade: representar cada clínica da rede. Principais informações: nome, endereço, telefone, horário de funcionamento e status. Relaciona-se com Profissional e Agendamento.

**Especialidade** — finalidade: descrever os serviços oferecidos. Principais informações: nome, descrição, duração média do atendimento e status. Relaciona-se com Profissional e Agendamento.

**Agendamento** — finalidade: registrar a marcação de uma consulta. Principais informações: paciente, profissional, unidade, especialidade, data, horário, status e data de criação. É a entidade central, relacionando-se com Paciente, Profissional, Unidade, Especialidade, Atendimento e Lembrete.

**Atendimento** — finalidade: registrar a realização efetiva da consulta. Principais informações: agendamento relacionado, data, profissional responsável, status e observações. Relaciona-se com Agendamento.

**Lembrete** — finalidade: registrar os avisos enviados aos pacientes. Principais informações: agendamento relacionado, tipo de lembrete, data e horário do envio, canal utilizado e status do envio. Relaciona-se com Agendamento.

## 5. Relacionamentos

De forma conceitual, os relacionamentos relevantes do sistema são:

* Um paciente pode ter vários agendamentos, mas cada agendamento pertence a um único paciente;
* Um profissional pode ter vários agendamentos, mas cada agendamento é atribuído a um único profissional;
* Uma unidade pode ter vários profissionais e vários agendamentos vinculados a ela;
* Uma especialidade pode estar associada a vários profissionais;
* Um agendamento pode originar um atendimento, quando a consulta é efetivamente realizada;
* Um agendamento pode ter um ou mais lembretes associados a ele.

Esses relacionamentos permitem consultar as informações de forma organizada — por exemplo, saber todos os agendamentos de um paciente, ou toda a agenda de um profissional em uma unidade — mantendo a consistência dos dados em todo o sistema.

## 6. Integridade dos dados

Para evitar inconsistências e duplicidades, a estrutura do banco deve prever: identificadores únicos para cada registro, relacionamentos corretos entre as entidades, campos obrigatórios preenchidos e validação das informações inseridas.

O ponto de maior atenção é o controle de agendamentos: o sistema deve impedir que um mesmo profissional tenha dois pacientes marcados para o mesmo horário, e deve impedir que um mesmo horário de um profissional seja ocupado duas vezes. Da mesma forma, cancelamentos e remarcações precisam atualizar corretamente o status do agendamento, sem deixar registros conflitantes ou órfãos (por exemplo, um lembrete associado a um agendamento que já foi cancelado).

## 7. QA e estratégia de testes

O papel dos testes no projeto é identificar problemas antes que o sistema chegue ao usuário final, verificando se cada funcionalidade entregue corresponde ao que foi definido nos requisitos do PO. No Clínica-Tech, a estratégia de testes dá atenção especial a cadastro, agendamento, atendimento, lembretes e controle de acesso — por serem os fluxos que mais impactam diretamente pacientes e profissionais caso falhem. Os testes cobrem tanto cenários positivos (o caminho esperado de uso) quanto cenários negativos (dados inválidos, tentativas de conflito, acessos não autorizados), já que ambos são igualmente importantes para garantir confiabilidade.

## 8. Casos de teste

**CT01 - Agendamento em horário disponível**
Dado que um paciente e um profissional estão cadastrados,
Quando o paciente seleciona um horário disponível e confirma o agendamento,
Então o sistema deve registrar o agendamento e apresentar a confirmação ao usuário.

**CT02 - Conflito de horário para o mesmo profissional**
Dado que um profissional já possui um agendamento confirmado em determinado horário,
Quando outro paciente tenta agendar com o mesmo profissional no mesmo horário,
Então o sistema deve impedir a marcação e informar que o horário não está disponível.

**CT03 - Cancelamento de agendamento**
Dado que um agendamento está confirmado,
Quando o paciente ou a clínica cancela o agendamento,
Então o status deve ser atualizado para "cancelado" e o horário deve voltar a ficar disponível.

**CT04 - Remarcação de consulta**
Dado que um agendamento existente precisa ser alterado,
Quando o usuário seleciona uma nova data e horário disponíveis,
Então o sistema deve atualizar o agendamento sem duplicar o registro original.

**CT05 - Cadastro com dado obrigatório ausente**
Dado que o usuário está cadastrando um novo paciente,
Quando um campo obrigatório (como CPF) não é preenchido,
Então o sistema deve exibir uma mensagem de erro e não deve concluir o cadastro.

**CT06 - Acesso restrito por perfil**
Dado que um usuário está autenticado com um perfil sem permissão para determinada informação,
Quando ele tenta acessar dados fora do seu perfil,
Então o sistema deve negar o acesso e não expor a informação solicitada.

## 9. Entregas desta área

* Modelo conceitual das entidades e seus relacionamentos;
* Regras de integridade aplicáveis aos agendamentos e cadastros;
* Diretrizes de segurança e controle de acesso ao banco;
* Estratégia de testes cobrindo cadastro, agendamento, atendimento, lembretes e segurança;
* Conjunto de casos de teste documentados no formato Dado/Quando/Então.

## 10. Integração com os demais papéis

O Back-end depende diretamente do modelo de dados definido nesta área para implementar as regras de negócio e a comunicação com o banco. O Front-end depende de que os dados estejam corretamente estruturados e disponíveis para exibir informações consistentes ao usuário. O QA, por sua vez, valida a integração completa entre essas camadas: quando um usuário solicita um agendamento, o fluxo passa pelo Front-end, pelo Back-end e pelo Banco de Dados, retornando a confirmação ao usuário — e é justamente esse fluxo, incluindo o tratamento de conflitos de horário, que os testes precisam cobrir.

## 11. Impacto da ausência desta função

Sem uma estrutura de dados bem definida, o sistema corre o risco de armazenar informações duplicadas, inconsistentes ou desconectadas, o que compromete a confiabilidade dos agendamentos e do histórico de atendimentos. Sem QA, erros nos fluxos de agendamento, cancelamento ou controle de acesso poderiam chegar até pacientes e profissionais sem terem sido identificados antes, gerando conflitos de horário, retrabalho e perda de confiança na solução.

## 12. Riscos, limitações e cuidados

* Risco de conflitos de horário caso as regras de integridade não sejam aplicadas de forma consistente;
* Necessidade de cuidado especial com dados sensíveis de pacientes e profissionais, aplicando controle de acesso adequado;
* Dependência de que o Back-end respeite as regras de negócio definidas junto ao modelo de dados;
* Cobertura de testes limitada ao escopo definido pelo PO, sem extrapolar para funcionalidades não previstas;
* Necessidade de manter o histórico de atendimentos íntegro mesmo diante de cancelamentos e remarcações frequentes.

## 13. Pontos a validar com o Product Owner

* Confirmar o formato e o canal padrão utilizados para o envio de lembretes (SMS, e-mail, WhatsApp, etc.);
* Validar quais perfis de acesso existem no sistema e quais informações cada um pode visualizar;
* Confirmar se há um prazo mínimo permitido para cancelamento ou remarcação de uma consulta;
* Validar se o histórico de atendimentos deve ficar disponível de forma indefinida ou por um período determinado.
