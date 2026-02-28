# Padrões de Projeto Estruturais

<div align="center">

![Design Patterns](https://refactoring.guru/images/patterns/content/index/full/patterns-02.png)

</div>

## Tabela Comparativa

| Padrão | Propósito Principal | Mecanismo de Ação |
| :--- | :--- | :--- |
| **Adapter** | Compatibilizar interfaces incompatíveis. | Encapsula um objeto com uma interface adaptadora. |
| **Bridge** | Desacoplar uma abstração de sua implementação. | Separa hierarquias de abstração e implementação. |
| **Composite** | Tratar partes e composições uniformemente. | Estrutura objetos em árvores parte-todo. |
| **Decorator** | Adicionar responsabilidades dinamicamente. | Encapsula objetos com decoradores. |
| **Facade** | Simplificar acesso a subsistemas complexos. | Fornece uma interface unificada para um conjunto de interfaces. |
| **Flyweight** | Compartilhar dados comuns entre muitos objetos. | Externaliza estado compartilhado. |
| **Proxy** | Controlar acesso a outro objeto. | Fornece um substituto para controlar acesso. |

---

## Análise Detalhada (Problema vs. Solução)

### 1. Adapter

**Quais problemas o padrão resolve?**
* Incompatibilidade de interfaces entre componentes legados e novos
* Necessidade de integrar bibliotecas third-party com interfaces diferentes
* Reutilização de classes cujas interfaces não correspondem às esperadas

**Como o padrão resolve esses problemas?**
* Cria uma classe intermediária que implementa a interface esperada e traduz as chamadas para a interface da classe original
* Funciona como um "tradutor" entre dois mundos incompatíveis
* Permite que o código cliente use a classe adaptada sem conhecer sua implementação original

**Quais os passos/componentes para a implementação?**
* **Target**: Interface esperada pelo cliente
* **Adaptee**: Classe com interface incompatível que precisa ser adaptada
* **Adapter**: Implementa a Target e contém uma instância de Adaptee, traduzindo as chamadas
* **Client**: Usa o Adapter pensando que está usando a Target

---

### 2. Bridge

**Quais problemas o padrão resolve?**
* Explosão combinatorial de classes quando se tem múltiplas hierarquias de abstração e implementação
* Acoplamento forte entre abstrações e implementações concretas
* Dificuldade em estender tanto abstrações quanto implementações independentemente

**Como o padrão resolve esses problemas?**
* Separa a hierarquia de abstração da hierarquia de implementação
* A abstração contém uma referência para a implementação através de uma interface
* Permite que abstrações e implementações variem independentemente

**Quais os passos/componentes para a implementação?**
* **Abstraction**: Define a interface de alto nível
* **RefinedAbstraction**: Estende a abstração
* **Implementor**: Define a interface para as implementações concretas
* **ConcreteImplementor**: Implementa a interface Implementor
* **Bridge**: A Abstraction mantém uma referência a um Implementor

---

### 3. Composite

**Quais problemas o padrão resolve?**
* Tratamento heterogêneo de objetos simples e compostos
* Complexidade ao construir estruturas parte-todo (árvores)
* Necessidade de aplicar operações uniformemente a toda a hierarquia

**Como o padrão resolve esses problemas?**
* Define uma interface comum para folhas e compostas
* Compostas podem conter outras compostas ou folhas
* Cliente trata a estrutura uniformemente sem se preocupar com o tipo de objeto

**Quais os passos/componentes para a implementação?**
* **Component**: Interface comum para folhas e compostas
* **Leaf**: Implementa operações básicas e não contém filhos
* **Composite**: Implementa operações e gerencia uma coleção de componentes filhos
* **Client**: Trabalha com componentes através da interface Component

---

### 4. Decorator

**Quais problemas o padrão resolve?**
* Necessidade de adicionar responsabilidades a objetos dinamicamente
* Alternativa flexível à herança para estender funcionalidade
* Evitar a explosão de subclasses quando combinações de funcionalidades são necessárias

**Como o padrão resolve esses problemas?**
* Cria classes decoradoras que encapsulam os objetos originais
* Cada decorador implementa a mesma interface do objeto e adiciona novas responsabilidades
* Decoradores podem ser encadeados, formando um stack de funcionalidades

**Quais os passos/componentes para a implementação?**
* **Component**: Interface comum para objetos a serem decorados
* **ConcreteComponent**: Implementação básica
* **Decorator**: Encapsula um Component e implementa a mesma interface
* **ConcreteDecorator**: Estende Decorator e adiciona novas responsabilidades
* **Encadeamento**: Múltiplos decoradores podem ser aplicados em sequência

---

### 5. Facade

**Quais problemas o padrão resolve?**
* Complexidade de usar um subsistema com múltiplas classes interdependentes
* Necessidade de abstrair a complexidade interna de um sistema
* Reduzir o acoplamento entre cliente e subsistema

**Como o padrão resolve esses problemas?**
* Fornece uma interface unificada e simplificada para um conjunto complexo de interfaces
* Encapsula as interações entre múltiplas classes do subsistema
* O cliente só precisa conhecer a Facade, não o subsistema interno

**Quais os passos/componentes para a implementação?**
* **Facade**: Interface simplificada que delegada para múltiplas classes
* **Subsystem Classes**: Classes complexas que a Facade orquestra
* **Client**: Interage apenas com a Facade
* **Métodos Públicos**: A Facade expõe apenas as operações que importam ao cliente

---

### 6. Flyweight

**Quais problemas o padrão resolve?**
* Alto consumo de memória quando há muitos objetos similares
* Necessidade de instanciar milhares de objetos com dados comuns
* Otimização de performance em aplicações memory-constrained

**Como o padrão resolve esses problemas?**
* Compartilha estado comum (intrínseco) entre múltiplos objetos
* Externaliza estado variável (extrínseco) para o cliente
* Uma fábrica reutiliza flyweights já criados em vez de criar novos

**Quais os passos/componentes para a implementação?**
* **Flyweight**: Interface comum que define métodos que aceitam estado extrínseco
* **ConcreteFlyweight**: Implementa a interface e armazena estado intrínseco
* **FlyweightFactory**: Gerencia um pool de flyweights reutilizáveis
* **ExtrinsicState**: Estado que varia e é passado ao flyweight como parâmetro
* **IntrinsicState**: Estado comum compartilhado entre instâncias

---

### 7. Proxy

**Quais problemas o padrão resolve?**
* Controle de acesso a objetos caros ou remotos
* Inicialização lazy de objetos pesados
* Logging, caching ou autorização de operações
* Acesso a objetos em diferentes endereços de memória (remoto)

**Como o padrão resolve esses problemas?**
* Cria um objeto proxy que implementa a mesma interface do objeto real
* O proxy controla o acesso ao objeto real, adicionando lógica antes/depois
* O cliente trabalha com o proxy, que delega ao objeto real quando necessário

**Quais os passos/componentes para a implementação?**
* **Subject**: Interface comum para proxy e objeto real
* **RealSubject**: O objeto real que fornece a funcionalidade
* **Proxy**: Implementa Subject e controla o acesso ao RealSubject
* **Control Logic**: Proxy adiciona lógica (lazy loading, logging, autorização, etc.)
* **Delegation**: Proxy delega ao RealSubject após sua lógica de controle

---

## Implementações Presentes

Este projeto implementa:

* **Facade**: Exemplo de um `WalletFacade` que simplifica as operações de uma carteira digital, orquestrando `Account`, `SecurityCode`, `Wallet`, `Notification` e `Ledger`.

* **Flyweight**: Exemplo de um jogo com personagens que compartilham tipos de roupa (`TerroristDress` e `CounterTerroristDress`) através de uma `DressFactory`, economizando memória.

---

## Como executar

```bash
go run ./src/facade
go run ./src/flyweight
```

> Certifique-se de estar na raiz do projeto (`requirements-engineering/02`) para que os imports funcionem corretamente.
