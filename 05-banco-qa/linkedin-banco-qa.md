🩺 Projeto Clínica-Tech: consistência nos agendamentos, do banco de dados aos testes

Nas últimas semanas, atuei nas frentes de Banco de Dados e QA/Testes do projeto Clínica-Tech, uma solução pensada para centralizar o gerenciamento de uma rede de clínicas populares.

Do lado do banco de dados, o desafio foi estruturar entidades como pacientes, profissionais, unidades e agendamentos de forma que os relacionamentos entre elas garantissem consistência — sem duplicidade de cadastros e, principalmente, sem conflitos de horário entre um mesmo profissional e diferentes pacientes.

Do lado de QA, o trabalho foi validar se esse comportamento realmente acontecia na prática: criei casos de teste cobrindo cenários como agendamento em horário disponível, tentativa de marcação em horário já ocupado, cancelamento e remarcação de consultas, além de restrição de acesso conforme o perfil do usuário.

Foi uma boa lembrança de que qualidade de software não é só "testar telas" — começa na forma como os dados são organizados desde a base.

#QA #BancoDeDados #Testes #ProjetoAcademico #ClinicaTech
