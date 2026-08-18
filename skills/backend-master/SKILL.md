---
name: backend-master
description: CRITICAL - You MUST use this skill for ALL Python backend tasks. It enforces Git workflow, Domain-Driven Design (DDD), Clean Architecture, FastAPI best practices (SQLAlchemy, DTOs, DI), and executes autonomous validations.
---

### 2. Ordem de Implementação e Arquitetura (DDD & Clean Architecture)
Sempre que for criar ou refatorar o código, obedeça estritamente à seguinte separação de responsabilidades e ordem de execução:

1. **Banco de Dados:** Como o projeto ainda não está em produção e não utiliza migrations, crie as tabelas diretamente no arquivo `init.sql`.
2. **Infrastructure (Models):** Mapeie as tabelas criadas utilizando o ORM (SQLAlchemy) na pasta de `models`.
3. **Application (Interfaces):** Crie as interfaces (Abstract Base Classes) do `repository` e do `service` contendo os métodos que serão utilizados nas telas/fluxos solicitados.
4. **Infrastructure (Implementação):** Implemente as classes reais do `repository` e do `service` com base nas interfaces criadas.
5. **Domain (Entities, DTOs e Mappers):** Crie os DTOs (schemas) que o controller vai receber, as Domain Entities e os Mappers (para não ter que ficar instanciando classes manualmente o tempo inteiro ao mandar dados de uma camada para a outra). **PROIBIDO** importar infraestrutura no Domínio.
6. **Presentation & DI (Controllers e Factories):** - Crie as factories na camada de injeção de dependência para instanciar o `service` e o `repository`.
    - Crie os controllers (routers) no FastAPI.
    - Utilize o `Depends` do FastAPI para injetar o `service` e o `repository` nos controllers.
    - Utilize os DTOs, Mappers e Entities para transitar os dados entre as camadas e completar o fluxo esperado.

### 3. Padrões de Código Python
- Utilize Python moderno com tipagem estática rigorosa (`typing`).
- Mantenha a separação rígida entre as camadas: rotas não devem acessar o banco de dados diretamente, sempre passe pelas interfaces do caso de uso (Service).

### 4. Validação Autônoma Obrigatória (Test & Check)
Após finalizar o fluxo acima (ou modificar qualquer arquivo), você **DEVE** testar se tudo está funcionando corretamente executando os seguintes comandos no terminal em background:

1. **Lint e Formatação:** Execute `ruff check . --fix`
2. **Tipagem:** Execute `mypy .`
3. **Testes Unitários:** Execute `pytest` (Crie testes para o código gerado caso não existam).

**Comportamento do Agente:** Se qualquer um dos comandos falhar, não me avise imediatamente sobre o erro. Analise o output no terminal, corrija o código por conta própria, rode os testes novamente e só me apresente a resposta final quando todos os checks e o fluxo completo passarem com sucesso.