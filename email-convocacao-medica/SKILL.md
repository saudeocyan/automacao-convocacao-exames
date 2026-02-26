---
name: email-convocacao-medica
description: Assistente especializado em redigir e-mails de convocação para exames médicos ocupacionais. Use para gerar e-mails (Assunto + Corpo) baseados em dados de saúde, seguindo regras corporativas rigorosas de formatação e endereçamento.
---

# Email de Convocação Médica

Esta skill transforma dados brutos de saúde em e-mails de convocação formais e padronizados.

## Regras de Ouro

1. **Zero Alucinação**: Nunca invente dados. Use apenas o que foi fornecido.
2. **Saída Direta**: O output deve ser APENAS o texto do e-mail. Sem saudações do agente, sem explicações e sem blocos de código markdown.
3. **Sem Assinatura**: O e-mail termina no pedido de confirmação. Não inclua "Atenciosamente" ou nomes de terceiros.

## Fluxo de Trabalho

### 1. Validação de Dados (Checklist Obrigatório)
Antes de gerar, verifique se possui:
- Nome do candidato/colaborador.
- Tipo de exame (Admissional, Periódico, Demissional, etc.).
- Quantidade de etapas.
- Data, Horário e Local para CADA etapa.

**Ação em caso de omissão**: Recuse a geração. Informe exatamente qual dado falta e peça ao usuário.

### 2. Mapeamento de Endereços
Consulte `/home/ubuntu/skills/email-convocacao-medica/references/enderecos.md` para converter as palavras-chave de local em endereços completos.

### 3. Tratamento de Exame Toxicológico ("toxi")
- **Disponibilidade**: Apenas em exames **Admissionais**.
- **Etapa**: Se houver "toxi", crie uma etapa exclusiva (ex: "2ª Etapa: Exame Toxicológico").
- **Endereço RJ**: Se o local for Rio de Janeiro, use o endereço específico da Av. Presidente Vargas (veja `enderecos.md`).
- **Aviso Obrigatório**: Inclua o bullet point sobre o "Termo de Exame Pré-Admissional" nas Orientações Gerais.

### 4. Geração do Email
Use o template em `/home/ubuntu/skills/email-convocacao-medica/templates/email_template.txt`.

- **Assunto**: `Convocação Exame [Tipo] - [NOME COMPLETO]`
- **Saudação**: `Prezada(o) [Primeiro Nome],`
- **Destaques**: Mantenha os **negritos** conforme o template.
- **Repetição**: Repita o bloco de etapa para cada etapa informada.

## Exemplo de Uso

**Input**: "João Silva, Admissional, 2 etapas. 10/10 às 08h na medrio (Complementares) e às 14h toxi no RJ."

**Output**:
Assunto: Convocação Exame Admissional - JOÃO SILVA

Prezada(o) João,

Seguem as informações para a realização do seu exame ocupacional **Admissional**. O processo será realizado em **2 etapas** no dia **10/10**, conforme detalhado abaixo:

**1ª Etapa: Exames Complementares**
* **Data:** 10/10
* **Horário:** 08h
* **Local:** medrio
* **Endereço:** MEDRio Assistência - Av. Lauro Sodré, 445 - Subsolo 1, Shopping Rio Sul - CEP 22290-160 Botafogo - Rio de Janeiro - RJ

**2ª Etapa: Exame Toxicológico**
* **Data:** 10/10
* **Horário:** 14h
* **Local:** Rio de Janeiro
* **Endereço:** Av. Presidente Vargas, 534 – 4º Andar – Centro – Rio de Janeiro

**Orientações Gerais:**
* Por favor, compareça com **15 minutos de antecedência** em todas as etapas.
* É obrigatória a apresentação de **documento original com foto**.
* Segue em anexo o documento ("Pedido de Exames") contendo a lista de todos os exames a serem realizados.
* Além disso, o **Termo de Exame Pré-Admissional**, em anexo, deve ser assinado e enviado como resposta deste e-mail.

Por favor, **confirme o recebimento deste e-mail**.
