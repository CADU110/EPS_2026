# Relatório de Prontidão Técnica: Onboarding SecOps

**Disciplina:** Engenharia de Produto de Software (FGA0316) - 2026.1
**Aluno:** Carlos Eduardo Mota Alves
**Matrícula:** 221022248

## 1. Configuração do Ambiente (Zero Trust & Isolamento)

Conforme as diretrizes de Soberania Técnica, as seguintes configurações foram aplicadas:

* [x] **Python 3.12:** Instalado e verificado.
* [x] **Poetry:** Configurado para criar `.venv` dentro do projeto (`virtualenvs.in-project true`).
* [x] **Determinismo:** Arquivos `pyproject.toml` e `poetry.lock` gerados com sucesso.

## 2. Logs de Auditoria e Qualidade (Security Gate)

Abaixo constam os resumos das execuções dos comandos de segurança:

### 2.1. Auditoria Estática (Bandit)

**Resultado observado:** foram encontradas **1439 ocorrências** de `assert_used` em arquivos de dependências instaladas no ambiente virtual (`.venv`), principalmente em pacotes de terceiros como `anyio`, `pip`, `django`, `cffi`, `rich` e outros.
**Interpretação:** as ocorrências não estão no código-fonte da aplicação, mas sim em bibliotecas do ambiente de desenvolvimento.
**Comando:** `poetry run bandit -r .`

### 2.2. Verificação de Dependências (Safety)

**Resultado observado:** **0 vulnerabilidades reportadas**.
**Pacotes analisados:** 49
**Observação adicional:** o comando `safety check` aparece como **deprecated**; a ferramenta recomenda o uso de `safety scan`.
**Comando:** `poetry run safety check`

### 2.3. Qualidade e Conformidade (Ruff)

**Resultado observado:** **All checks passed!**
**Interpretação:** o código está em conformidade com as regras de lint/estilo verificadas no momento da execução.
**Comando:** `poetry run ruff check .`

## 3. Evidência de Integração Contínua (CI)

O pipeline automatizado foi executado com sucesso no GitHub Actions:

* **Link da Action de Sucesso:** 

## 4. Declaração de Soberania Técnica (CISSP Domain 8)

Eu, **Carlos Eduardo Mota Alves**, declaro que auditei manualmente as ferramentas e dependências deste projeto. Confirmo que o código gerado via IA (GitHub Copilot) passou pela minha revisão humana (*Human-in-the-loop*), garantindo que não há vazamento de segredos ou falhas lógicas críticas antes da migração para o ecossistema da PCDF.

---

## Observações gerais e específicas

1. O resultado do **Bandit** indica que a análise foi executada sobre a pasta inteira do projeto, incluindo a pasta `.venv`. Para uma auditoria mais fiel ao código da aplicação, recomenda-se excluir o ambiente virtual da varredura, por exemplo com `-x .venv`.
2. O **Safety** retornou resultado satisfatório, sem vulnerabilidades conhecidas nas dependências analisadas.
3. O comando `safety check` está **deprecado**, sendo recomendável atualizar o fluxo para `safety scan`.
4. O **Ruff** não apontou inconsistências no código analisado, indicando bom nível de conformidade com as regras definidas.

**Data de Entrega:** 01/04/2026

