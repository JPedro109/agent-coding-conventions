# Steerings

Esta pasta contém os **documentos de convenção** que servem como contexto para agentes de IA. Cada arquivo Markdown descreve uma convenção específica de arquitetura, código ou teste para uma linguagem.

Os documentos são agnósticos de ferramenta e podem ser fornecidos como contexto a qualquer agente de IA que aceite Markdown, ou lidos diretamente pela equipe como guia de estilo.

---

## Estrutura

```text
Steerings/
├── Java/     # Convenções para projetos Java
└── Kotlin/   # Convenções para projetos Kotlin
```

O conjunto de documentos é **espelhado** entre Java e Kotlin. Ao alterar uma convenção, atualize as duas versões para mantê-las alinhadas.

> **Extensibilidade:** novas linguagens podem ser adicionadas criando uma subpasta com o mesmo conjunto de documentos. Basta copiar a estrutura de `Java/` ou `Kotlin/`, adaptar os exemplos de código para a linguagem desejada e registrar a nova pasta na tabela de [Subpastas](#subpastas) abaixo.

---

## Convenções disponíveis

### Gerais

| Documento | Conteúdo |
|-----------|----------|
| `convention-architecture.md` | Princípios arquiteturais, estrutura de pastas (`core/`, `configuration/`), fluxo de dependências e de dados, responsabilidades de cada camada. |
| `convention-code.md` | Nomenclatura, constantes, formatação em blocos lógicos, ordenação de membros, injeção de dependência, logging, configurações tipadas, imports e análise estática. |
| `convention-cache.md` | Convenções de cache. |

### Por camada

A arquitetura define quatro camadas de negócio sob `core/`, com dependências sempre apontando para o centro:

| Documento | Camada |
|-----------|--------|
| `convention-layer-domain.md` | **Domain** — entidades, value objects, `Result<T>`, validações e exceções de negócio. Independente de frameworks. |
| `convention-layer-application.md` | **Application** — casos de uso, orquestração e definição de contratos (portas). |
| `convention-layer-external.md` | **External** — persistência, integrações, cache e demais adaptadores que implementam as portas. |
| `convention-layer-presentation.md` | **Presentation** — princípios transversais de qualquer forma de acesso à aplicação: sem regra de negócio, dependência exclusiva da Application. |

Subconvenções da camada External:

| Documento | Escopo |
|-----------|--------|
| `convention-layer-external-persistence.md` | Detalhes de persistência (DAO, Repository, Mapper, Model) dentro da External. |
| `convention-layer-external-gateway.md` | Integração HTTP com outras aplicações (Feign Client + Resilience4j) dentro da External. |
| `convention-layer-external-security.md` | Segurança dentro da camada External. |

Subconvenções da camada Presentation:

| Documento | Escopo |
|-----------|--------|
| `convention-layer-presentation-controller.md` | Acesso HTTP: controllers, payloads (Request/Response), Global Exception Handler, resolvers e documentação OpenAPI. |
| `convention-layer-presentation-scheduler.md` | Acesso via Scheduler: tarefas agendadas (`@Scheduled`) com lock distribuído obrigatório via ShedLock. |

### De teste

| Documento | Escopo |
|-----------|--------|
| `convention-test-general.md` | Layout dos testes, fixtures, padrão AAA, `@DisplayName`, AssertJ, Testcontainers e WireMock. |
| `convention-test-layer-domain.md` | Testes da camada Domain. |
| `convention-test-layer-application.md` | Testes da camada Application. |
| `convention-test-layer-external.md` | Testes da camada External. |
| `convention-test-layer-external-persistence.md` | Testes de persistência. |
| `convention-test-layer-external-gateway.md` | Testes de Gateway HTTP (adaptador Feign). |
| `convention-test-layer-presentation-controller.md` | Testes de Controller (slice HTTP com `@WebMvcTest` / integração). |
| `convention-test-layer-presentation-scheduler.md` | Testes de Scheduler, unitários e sem contexto Spring. |

---

## Como fornecer como contexto a um agente

Aponte os documentos relevantes para a tarefa em andamento:

- Implementando uma entidade → `convention-architecture.md` + `convention-layer-domain.md`
- Criando um caso de uso → `convention-layer-application.md`
- Escrevendo um controller → `convention-layer-presentation.md` + `convention-layer-presentation-controller.md`
- Escrevendo testes → `convention-test-general.md` + documento de teste da camada correspondente
- Revisão geral → forneça o conjunto completo da linguagem

---

## Subpastas

| Pasta | README |
|-------|--------|
| [`Java/`](./Java/README.md) | Convenções para projetos Java |
| [`Kotlin/`](./Kotlin/README.md) | Convenções para projetos Kotlin |
