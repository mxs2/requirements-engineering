# Padrões de Projeto Criacionais

<div align="center">

![Design Patterns](https://refactoring.guru/images/patterns/content/index/full/patterns-01.png)

</div>

## Tabela Comparativa

| Padrão | Propósito Principal | Mecanismo de Ação |
| :--- | :--- | :--- |
| **Builder** | Construção passo a passo de objetos complexos. | Isola a lógica de variação em etapas de configuração. |
| **Singleton** | Garantir instância única e acesso global. | Restringe a instanciação de uma classe a um único objeto. |
| **Factory Method** | Delegar a criação para subclasses. | Define uma interface de criação, mas deixa as subclasses decidirem o tipo. |
| **Abstract Factory** | Criar famílias de objetos relacionados. | Provê uma interface para criar objetos sem especificar suas classes concretas. |
| **Prototype** | Clonagem de instâncias existentes. | Copia objetos existentes sem depender de suas classes ou expor campos privados. |

---

## Análise Detalhada (Problema vs. Solução)

### 1. Builder
* **Problemas:** O antipadrão do construtor telescópico (construtores com excesso de parâmetros opcionais) e a dificuldade de criar diferentes representações de um objeto complexo.
* **Solução:** Divide a construção em **etapas granulares**. Um objeto Diretor ou o próprio cliente decide quais etapas executar para obter a configuração desejada.

### 2. Singleton
* **Problemas:** Conflitos de acesso a recursos compartilhados (como logs ou bancos de dados) e a necessidade de um ponto de acesso global para evitar múltiplas instâncias consumindo memória.
* **Solução:** Esconde o construtor da classe e expõe um método estático que gerencia a **instância única** (criando-a apenas se não existir).

### 3. Factory Method
* **Problemas:** O acoplamento rígido entre o código que utiliza o objeto e a classe concreta do objeto. Facilita a extensão do código para novos tipos sem quebrar o código legado.
* **Solução:** Substitui chamadas diretas de construção por um **método de fábrica**, permitindo que subclasses sobrescrevam esse método para retornar diferentes tipos de produtos.

### 4. Abstract Factory
* **Problemas:** A necessidade de garantir que produtos de uma mesma família (ex: botões e janelas de um tema Dark) sejam compatíveis entre si, evitando a mistura de estilos incompatíveis.
* **Solução:** Define uma interface para criar cada produto básico da família. O código cliente interage apenas com as interfaces, garantindo a **consistência do ecossistema**.

### 5. Prototype
* **Problemas:** O custo computacional alto de criar objetos do zero e a dependência de classes concretas durante a cópia (especialmente quando os atributos são privados).
* **Solução:** Declara uma interface comum para todos os objetos que suportam clonagem. O objeto original é responsável por **replicar a si mesmo**, mantendo a integridade dos dados.

---

## Como executar

```
go run ./src/builder
go run ./src/singleton
```
> Certifique-se de estar na raiz do projeto (`requirements-engineering/01`) para que os imports funcionem corretamente.