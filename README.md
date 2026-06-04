# Chatbot da Comissão de Estágio

Bot para Telegram desenvolvido em Python que automatiza a análise de elegibilidade para estágio de alunos de Ciência da Computação da UFRJ.

O sistema recebe o DRE do aluno, analisa seu BOA (Boletim de Orientação Acadêmica), verifica automaticamente os critérios definidos pela Comissão de Estágio e gera um parecer de autorização quando os requisitos são atendidos.

---

## Problema

Tradicionalmente, a verificação da aptidão para estágio exige análise manual do histórico acadêmico do aluno por professores que não têm essa como sua função principal, o que gera um longo período de espera por autorizações pelos estudantes de Ciência da Computação da UFRJ.

Este projeto automatiza esse processo por meio de um chatbot acessível pelo Telegram, reduzindo o tempo necessário para emissão de pareceres e atendimento aos estudantes.

---

## Funcionalidades

### Verificação de Elegibilidade

- Recebe o DRE do aluno.
- Solicita o envio do BOA em PDF.
- Extrai automaticamente informações acadêmicas.
- Verifica critérios definidos pela Comissão de Estágio.

### Análise Acadêmica

O sistema verifica:

- Aprovação nas disciplinas obrigatórias até o 4º período.
- CRA acumulado maior ou igual a 6.

### Emissão de Parecer

Caso o aluno esteja apto:

- Registra os dados em uma planilha Google Sheets (método utilizado atualmente para controle pelo Instituto de Computação da UFRJ).
- Gera automaticamente um parecer em PDF.
- Define validade de 3 meses para o documento.
- Envia o parecer diretamente ao aluno.

### Reemissão de Parecer

Alunos já cadastrados podem solicitar uma nova emissão do parecer sem necessidade de nova análise.

### Avaliação de Contratos

O sistema permite o envio de contratos de estágio para análise da comissão.

Após o envio:

- O contrato é encaminhado por e-mail.
- O contato do aluno é informado automaticamente.
- O arquivo é removido após o processamento.

---

## Arquitetura

```text
Aluno
   │
   ▼
Telegram Bot
   │
   ├── Recebe DRE
   ├── Recebe BOA (PDF)
   │
   ▼
Processamento do PDF
   │
   ├── Extração do DRE
   ├── Extração do CRA
   └── Verificação das disciplinas
   │
   ▼
Motor de Regras
   │
   ├── Apto
   └── Não apto
   │
   ▼
Geração de Parecer PDF
   │
   ▼
Google Sheets
   │
   ▼
Entrega ao aluno
```

---

## Tecnologias Utilizadas

### Backend

- Python

### Integrações

- Telegram Bot API
- Google Sheets API
- Gmail API

### Bibliotecas

- python-telegram-bot
- gspread
- oauth2client
- yagmail
- APScheduler

### Processamento de Documentos

- Tabula
- NumPy
- ReportLab

---

## Geração de Documentos

O sistema gera automaticamente um parecer oficial contendo:

- Nome do aluno
- DRE
- Data de emissão
- Data de validade
- Status de autorização

---

## Critérios de Aprovação

Um aluno é considerado apto para estagiar quando:

### CRA

```text
CRA ≥ 6.0
```

### Disciplinas

Todas as disciplinas obrigatórias até o 4º período devem estar concluídas.

Disciplinas ainda cursando ou pendentes impedem a autorização.

---

## Como Executar

### Clone o repositório

```bash
git clone https://github.com/Vitornunees38/chatbot-comissao-estagio.git
cd chatbot-comissao-estagio
```

### Instale as dependências

```bash
pip install -r requirements.txt
```

### Configure as credenciais

Adicione:

- credentials.json (Google Sheets)
- email_sender_credentials.json (Gmail OAuth)
- Token do Bot do Telegram

### Execute

```bash
python bot_cc_refatorado.py
```

---

## Conceitos Aplicados

Durante o desenvolvimento deste projeto foram utilizados:

- Integração com APIs
- Processamento de PDFs
- Automação de processos administrativos
- Geração dinâmica de documentos
- Manipulação de planilhas
- Programação assíncrona
- Aplicação de regras de negócio

---

## Autor

Vitor Nunes

- GitHub: github.com/Vitornunees38
