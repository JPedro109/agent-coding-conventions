# agent-toolkit

Base de convenções de desenvolvimento voltada ao consumo por agentes de IA e pela equipe. O repositório padroniza arquitetura, estilo de código e práticas de teste para projetos.

Os documentos são agnósticos de ferramenta: cada arquivo Markdown descreve uma convenção específica e pode ser fornecido como contexto a qualquer agente de IA ou lido diretamente pela equipe.

---

## Para que serve

- Alimentar agentes de IA com o padrão arquitetural e de código esperado, para que o código gerado já nasça aderente.
- Servir como fonte única de verdade das convenções para a equipe.

---

## Estrutura

```text
.
├── Agents/       # Definições de agentes especializados reutilizáveis
├── Hooks/        # Automações que disparam em eventos do ciclo de desenvolvimento
├── Skills/       # Habilidades atômicas e reutilizáveis que agentes podem invocar
└── Steerings/    # Documentos de contexto e convenções fornecidos a agentes de IA
```

| Pasta | Propósito |
|-------|-----------|
| [`Agents/`](./Agents/README.md) | Agentes especializados com papéis, instruções e habilidades definidas. |
| [`Hooks/`](./Hooks/README.md) | Automações baseadas em eventos (pré/pós tool-use, save, commit, etc.). |
| [`Skills/`](./Skills/README.md) | Habilidades atômicas que encapsulam uma capacidade reutilizável por múltiplos agentes. |
| [`Steerings/`](./Steerings/README.md) | Documentos de convenção (arquitetura, código, testes) consumidos como contexto por agentes. |

---


## Como usar com um agente de IA

Forneça ao agente o(s) documento(s) relevantes como contexto — por exemplo, as convenções de `Steerings/Java/convention-layer-domain.md` ao implementar uma entidade Java, ou os documentos de teste ao escrever specs.

Para configurar automações, consulte `Hooks/`. Para reutilizar capacidades prontas, consulte `Skills/`. Para agentes especializados por papel, consulte `Agents/`.
