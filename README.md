# agent-coding-conventions

Base de convenções de desenvolvimento voltada ao consumo por agentes de IA e por pessoas da equipe. O repositório padroniza arquitetura, estilo de código e práticas de teste para projetos **Java** e **Kotlin** que seguem uma arquitetura em camadas (Clean / Ports & Adapters).

Os documentos são agnósticos de ferramenta: cada arquivo Markdown descreve uma convenção específica e pode ser fornecido como contexto a qualquer agente de IA ou lido diretamente pela equipe.

## Para que serve

- Alimentar agentes de IA com o padrão arquitetural e de código esperado, para que o código gerado já nasça aderente.
- Servir como fonte única de verdade das convenções para a equipe.
- Manter Java e Kotlin alinhados: o conjunto de documentos é espelhado entre as duas linguagens.

## Estrutura

```text
.
├── Java/
│   └── convention-*.md
└── Kotlin/
    └── convention-*.md
```

Cada linguagem possui o mesmo conjunto de documentos:

### Convenções gerais

| Documento | Conteúdo |
|-----------|----------|
| `convention-architecture.md` | Princípios arquiteturais, estrutura de pastas (`core/`, `configuration/`), fluxo de dependências e de dados, responsabilidades de cada camada. |
| `convention-code.md` | Nomenclatura, constantes, formatação em blocos lógicos, ordenação de membros, injeção de dependência, logging, configurações tipadas, imports e análise estática. |
| `convention-cache.md` | Convenções de cache. |

### Convenções por camada

A arquitetura define quatro camadas de negócio sob `core/`, com dependências sempre apontando para o centro (Domain não depende de ninguém; Application depende de Domain; External e Presentation dependem de Application):

| Documento | Camada |
|-----------|--------|
| `convention-layer-domain.md` | **Domain** — entidades, value objects, `Result<T>`, validações e exceções de negócio. Independente de frameworks. |
| `convention-layer-application.md` | **Application** — casos de uso, orquestração e definição de contratos (portas). |
| `convention-layer-external.md` | **External** — persistência, integrações, cache e demais adaptadores que implementam as portas. |
| `convention-layer-persistence.md` | **Persistence** — detalhes de persistência dentro da camada External. |
| `convention-layer-presentation.md` | **Presentation** — recepção de requisições, validação de entrada e conversão para DTOs da aplicação. |

### Convenções de teste

| Documento | Escopo |
|-----------|--------|
| `convention-test-general.md` | Layout dos testes, fixtures, padrão AAA, `@DisplayName`, AssertJ, Testcontainers e WireMock. |
| `convention-test-layer-domain.md` | Testes da camada Domain. |
| `convention-test-layer-application.md` | Testes da camada Application. |
| `convention-test-layer-external.md` | Testes da camada External. |
| `convention-test-layer-persistence.md` | Testes da camada de persistência. |
| `convention-test-layer-presentation.md` | Testes da camada Presentation. |

## Como usar

### Com um agente de IA

Forneça ao agente o(s) documento(s) da linguagem desejada como contexto — seja apontando os arquivos relevantes para a tarefa em andamento (por exemplo, as convenções da camada Domain ao implementar uma entidade), seja incluindo o conjunto completo. Por serem agnósticos de ferramenta, os documentos funcionam com qualquer agente que aceite contexto em Markdown.

### Como leitura de referência

Os documentos são autoexplicativos, com exemplos ✔ corretos e ❌ incorretos. Podem ser lidos diretamente como guia de estilo da equipe.

## Princípios centrais

- O domínio é o núcleo e não depende de nenhuma outra camada nem de frameworks.
- Toda dependência de infraestrutura é acessada por meio de contratos (portas e adaptadores).
- Conversões entre camadas são sempre explícitas; objetos de uma camada não atravessam outra sem conversão.
- Cada componente tem uma única responsabilidade; alto acoplamento é evitado e a coesão maximizada.
- Testes seguem layout por camada, usam fixtures (nunca dados inline ou aleatórios) e o padrão AAA.

## Contribuindo

Ao alterar uma convenção, atualize a versão **Java e Kotlin** para mantê-las espelhadas. Mantenha o formato de exemplos ✔/❌ para consistência.
