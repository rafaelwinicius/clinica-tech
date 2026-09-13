# Organização do Projeto — Clínica-Tech

## 1. Objetivo

Organizar o trabalho da equipe de forma que cada integrante produza sua contribuição a partir de uma mesma definição de produto, com registro das decisões e revisão antes da incorporação ao repositório principal.

O arquivo `01-produto-requisitos/produto-e-requisitos.md` é a **fonte oficial das decisões de produto**.

---

## 2. Estrutura do repositório

```text
clinica-tech/
│
├── README.md
│
├── 01-produto-requisitos/
│   ├── produto-e-requisitos.md
│   ├── linkedin-po.md
│   └── apresentacao-po.pptx
│
├── 02-ux-ui/
│   ├── ux-ui.md
│   ├── linkedin-ux-ui.md
│   └── apresentacao-ux-ui.pptx
│
├── 03-frontend/
│   ├── frontend.md
│   ├── linkedin-frontend.md
│   └── apresentacao-frontend.pptx
│
├── 04-backend-seguranca/
│   ├── backend-seguranca.md
│   ├── linkedin-backend-seguranca.md
│   └── apresentacao-backend-seguranca.pptx
│
├── 05-banco-qa/
│   ├── banco-qa.md
│   ├── linkedin-banco-qa.md
│   └── apresentacao-banco-qa.pptx
│
├── 06-organizacao/
│   └── organizacao-do-projeto.md
│
└── 07-apresentacao-final/
    ├── clinica-tech-final.pptx
    └── clinica-tech-final.pdf
```

Cada integrante entrega **três arquivos principais** em sua pasta:

1. documentação da área em Markdown;
2. proposta individual de postagem para LinkedIn;
3. apresentação individual em PPTX.

---

## 3. Organização das demandas

Será criada **uma Issue por área**, contendo:

- objetivo da entrega;
- referência ao `produto-e-requisitos.md`;
- arquivos esperados;
- prazo interno do grupo;
- eventuais observações do PO.

As Issues servem como registro objetivo do que precisa ser produzido.

---

## 4. Branches

A branch principal será:

```text
main
```

Cada integrante trabalhará em uma branch própria, seguindo o padrão:

```text
feature/area
```

Exemplos:

```text
feature/ux-ui
feature/frontend
feature/backend-seguranca
feature/banco-qa
```

---

## 5. Fluxo de trabalho

```text
Issue
  ↓
Branch da área
  ↓
Produção dos 3 arquivos
  ↓
Commits
  ↓
Push
  ↓
Pull Request
  ↓
Revisão
  ↓
Ajustes, se necessários
  ↓
Aprovação
  ↓
Merge na main
```

---

## 6. Pull Requests

Cada integrante abrirá **uma Pull Request** contendo o pacote completo de sua área.

### Critérios mínimos para aprovação

- os três arquivos previstos foram entregues;
- a documentação está coerente com `produto-e-requisitos.md`;
- não foram incorporadas novas funcionalidades ou regras como decisão definitiva sem validação do PO;
- o texto do LinkedIn é coerente com o papel profissional;
- a apresentação representa o conteúdo documentado;
- eventuais pontos pendentes foram identificados;
- os arquivos estão na pasta correta.

O PO fará a revisão de coerência com produto, escopo, MVP e requisitos. Revisões técnicas complementares poderão ser feitas pelos colegas.

---

## 7. Registro das decisões

### Decisões de produto

São registradas no arquivo:

```text
01-produto-requisitos/produto-e-requisitos.md
```

Mudanças que alterem escopo, requisitos, regras de negócio, perfis, permissões, dados obrigatórios ou MVP deverão atualizar esse documento por meio de commit e Pull Request.

### Decisões técnicas

Cada integrante registra no próprio Markdown as decisões de sua área que não alterem o escopo do produto.

### Nova necessidade identificada

Se durante o desenvolvimento da documentação surgir uma necessidade não prevista:

1. o integrante registra o ponto;
2. comunica ao PO;
3. o PO avalia o impacto;
4. se aprovada, a definição é incorporada ao documento oficial;
5. somente depois ela passa a ser tratada como requisito do projeto.

---

## 8. Commits

Os commits devem registrar alterações de forma objetiva.

Exemplos:

```text
docs: adiciona documentação de ux-ui
docs: ajusta requisitos de acessibilidade
slides: adiciona apresentação de frontend
fix: corrige regra de remarcação
```

O histórico de commits registra **o que foi alterado**. A versão vigente das decisões do produto permanece consolidada no `produto-e-requisitos.md`.

---

## 9. Consolidação da apresentação

Após aprovação e merge das entregas individuais:

1. o PO fará download dos PPTX individuais;
2. os slides serão reunidos em uma apresentação única;
3. serão feitos apenas ajustes de padronização e transição, sem alterar o conteúdo técnico aprovado;
4. a versão final será salva em PPTX e exportada para PDF;
5. os dois arquivos serão publicados em `07-apresentacao-final/`.

A apresentação em sala será feita a partir do conteúdo publicado no próprio GitHub.

---

## 10. Princípio de organização

A documentação foi estruturada para que outra pessoa consiga compreender:

- qual problema está sendo resolvido;
- qual solução foi proposta;
- quais decisões já foram tomadas;
- qual é a contribuição de cada integrante;
- como as entregas foram revisadas e integradas.

O objetivo não é reproduzir um processo corporativo completo, mas demonstrar organização, rastreabilidade e integração compatíveis com o escopo acadêmico da atividade.
