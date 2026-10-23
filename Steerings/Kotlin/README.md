# Steerings — Kotlin

Convenções de desenvolvimento para projetos **Kotlin** com arquitetura em camadas (Clean / Ports & Adapters) usando Spring Boot.

Forneça estes documentos como contexto a agentes de IA antes de gerar ou revisar código Kotlin, ou leia-os diretamente como guia de estilo da equipe.

---

## Documentos disponíveis

### Gerais

| Documento | Conteúdo |
|-----------|----------|
| [`convention-architecture.md`](./convention-architecture.md) | Princípios arquiteturais, estrutura de pastas (`core/`, `configuration/`, `shared/`), fluxo de dependências e de dados, responsabilidades de cada camada. |
| [`convention-code.md`](./convention-code.md) | Nomenclatura, constantes, formatação em blocos lógicos, ordenação de membros, injeção de dependência, logging, configurações tipadas, imports e análise estática. |
| [`convention-cache.md`](./convention-cache.md) | Convenções de cache. |

### Por camada

| Documento | Camada / Escopo |
|-----------|-----------------|
| [`convention-layer-domain.md`](./convention-layer-domain.md) | **Domain** — entidades, value objects, `Result<T>`, validações e exceções de negócio. Independente de frameworks. |
| [`convention-layer-application.md`](./convention-layer-application.md) | **Application** — casos de uso, orquestração e definição de contratos (portas). |
| [`convention-layer-external.md`](./convention-layer-external.md) | **External** — princípios transversais dos adaptadores de infraestrutura. |
| [`convention-layer-external-persistence.md`](./convention-layer-external-persistence.md) | Detalhes de persistência (DAO, Repository, Mapper, Model) dentro da External. |
| [`convention-layer-external-gateway.md`](./convention-layer-external-gateway.md) | Integração HTTP com outras aplicações (Feign Client + Resilience4j) dentro da External. |
| [`convention-layer-external-security.md`](./convention-layer-external-security.md) | Segurança dentro da camada External. |
| [`convention-layer-presentation.md`](./convention-layer-presentation.md) | **Presentation** — princípios transversais de acesso à aplicação. |
| [`convention-layer-presentation-controller.md`](./convention-layer-presentation-controller.md) | Acesso HTTP: controllers, payloads, Global Exception Handler e OpenAPI. |
| [`convention-layer-presentation-scheduler.md`](./convention-layer-presentation-scheduler.md) | Acesso via Scheduler com `@Scheduled` e ShedLock. |

### De teste

| Documento | Escopo |
|-----------|--------|
| [`convention-test-general.md`](./convention-test-general.md) | Layout, fixtures, padrão AAA, `@DisplayName`, AssertJ, Testcontainers, WireMock. |
| [`convention-test-layer-domain.md`](./convention-test-layer-domain.md) | Testes da camada Domain. |
| [`convention-test-layer-application.md`](./convention-test-layer-application.md) | Testes da camada Application. |
| [`convention-test-layer-external.md`](./convention-test-layer-external.md) | Testes da camada External. |
| [`convention-test-layer-external-persistence.md`](./convention-test-layer-external-persistence.md) | Testes de persistência. |
| [`convention-test-layer-external-gateway.md`](./convention-test-layer-external-gateway.md) | Testes de Gateway HTTP (adaptador Feign). |
| [`convention-test-layer-presentation-controller.md`](./convention-test-layer-presentation-controller.md) | Testes de Controller (`@WebMvcTest` / integração). |
| [`convention-test-layer-presentation-scheduler.md`](./convention-test-layer-presentation-scheduler.md) | Testes de Scheduler, unitários e sem contexto Spring. |

---

## Diferenças em relação ao Java

Kotlin possui um documento adicional por linguagem:

- O pacote `shared/` (funções de extensão e tipos utilitários) está documentado em `convention-architecture.md`.
- Contratos (interfaces) existem para inverter dependências entre camadas. Componentes de implementação única, como casos de uso, são utilizados diretamente, sem interface — o Kotlin favorece funções de extensão e data classes sobre hierarquias de interface desnecessárias.

---

## Fluxo de dependências

```text
Presentation  →  Application  →  Domain
External      →  Application  →  Domain
```

- **Domain**: não depende de nenhuma outra camada.
- **Application**: depende apenas de Domain.
- **External**: depende de Application e Domain.
- **Presentation**: depende de Application.

---

## Guia rápido por tarefa

| Tarefa | Documentos recomendados |
|--------|------------------------|
| Implementar entidade | `convention-architecture.md` + `convention-layer-domain.md` |
| Implementar caso de uso | `convention-layer-application.md` |
| Implementar controller | `convention-layer-presentation.md` + `convention-layer-presentation-controller.md` |
| Implementar persistência | `convention-layer-external.md` + `convention-layer-external-persistence.md` |
| Implementar gateway HTTP | `convention-layer-external.md` + `convention-layer-external-gateway.md` |
| Escrever testes | `convention-test-general.md` + documento de teste da camada |
| Revisão geral | Conjunto completo |
