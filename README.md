# Design Patterns

Design patterns ou"padrões de projeto", são soluções recorrentes para problemas comuns que surgem durante o desenvolvimento de software. Eles representam boas práticas de design, acumuladas ao longo do tempo por desenvolvedores experientes, e oferecem soluções reutilizáveis para problemas específicos.

Os design patterns fornecem um vocabulário comum e uma abordagem padronizada para resolver problemas de design de software. Eles não são códigos ou bibliotecas prontas, mas sim diretrizes sobre como estruturar o código para resolver determinados problemas.

### Existem vários design patterns, e eles são categorizados em três principais grupos:

**Padrões de Criação (Creational Patterns)**: Tratam da criação de objetos, ajudando a criar objetos de maneira adequada para a situação. Exemplos incluem Singleton, Factory Method e Abstract Factory.

**Padrões Estruturais (Structural Patterns)**: Lidam com a composição de classes e objetos para formar estruturas maiores. Exemplos incluem Adapter, Decorator e Composite.

**Padrões Comportamentais (Behavioral Patterns)**: Tratam da interação entre objetos e a responsabilidade na execução de tarefas. Exemplos incluem Observer, Strategy e Command.

Alguns benefícios de usar design patterns incluem a promoção da reutilização de código, a facilitação da manutenção e compreensão do código, além de fornecer uma linguagem comum para a comunicação entre desenvolvedores.

No entanto, é importante usá-los com discernimento, pois aplicar design patterns de forma inadequada ou em excesso pode tornar o código mais complexo do que necessário. O contexto e os requisitos específicos do projeto devem ser considerados ao decidir se e como aplicar um design pattern.

## Padrões de Criação (Creational Patterns)

### Factory Method

O Factory Method é um padrão de design creacional que fornece uma interface para criar objetos em uma superclasse, mas permite que as subclasses alterem o tipo de objetos que serão criados. 

Suponha que tenhamos uma interface **Animal** e duas implementações, **Dog** e **Cat**. Agora, vamos criar uma classe chamada **AnimalFactory** que contém o **_Factory Method_** para criar instâncias de Animal com base em um parâmetro:

```java
// Interface Animal
interface Animal {
    void makeSound();
}

// Implementação de Dog
class Dog implements Animal {
    @Override
    public void makeSound() {
        System.out.println("Woof! Woof!");
    }
}

// Implementação de Cat
class Cat implements Animal {
    @Override
    public void makeSound() {
        System.out.println("Meow!");
    }
}

// AnimalFactory com o Factory Method
class AnimalFactory {
    // Factory Method
    public Animal createAnimal(String type) {
        if ("Dog".equalsIgnoreCase(type)) {
            return new Dog();
        } else if ("Cat".equalsIgnoreCase(type)) {
            return new Cat();
        } else {
            throw new IllegalArgumentException("Tipo de animal desconhecido: " + type);
        }
    }
}

// Exemplo de uso
public class Main {
    public static void main(String[] args) {
        AnimalFactory animalFactory = new AnimalFactory();

        // Criando instâncias usando o Factory Method
        Animal dog = animalFactory.createAnimal("Dog");
        Animal cat = animalFactory.createAnimal("Cat");

        // Chamando o método makeSound para cada animal
        dog.makeSound(); // Saída: Woof! Woof!
        cat.makeSound(); // Saída: Meow!
    }
}
```

Neste exemplo, **AnimalFactory** é a classe que contém o **_Factory Method_** _createAnimal_, que cria instâncias de **Animal** com base no tipo fornecido como parâmetro. O cliente pode usar o **_Factory Method_** para obter a instância desejada sem precisar conhecer os detalhes de implementação das classes concretas Dog e Cat.

### Abstract Factory

O Abstract Factory é outro padrão de design creacional que fornece uma interface para criar famílias de objetos relacionados ou dependentes sem especificar suas classes concretas. Vamos criar um exemplo simples em Java para ilustrar o Abstract Factory:

Suponha que tenhamos dois tipos de animais, **Dog** e **Cat**, e para cada tipo, temos diferentes raças, como GoldenRetriever, Poodle para cães e Siamese, Persian para gatos. Vamos criar interfaces e classes concretas para representar esses objetos e, em seguida, uma fábrica abstrata chamada **AnimalFactory**:

```java
// Interfaces para animais
interface Animal {
    void makeSound();
}

interface Dog extends Animal {
    void bark();
}

interface Cat extends Animal {
    void meow();
}

// Implementações concretas para cães
class GoldenRetriever implements Dog {
    @Override
    public void makeSound() {
        System.out.println("Woof! Woof!");
    }

    @Override
    public void bark() {
        System.out.println("Barking loudly!");
    }
}

class Poodle implements Dog {
    @Override
    public void makeSound() {
        System.out.println("Woof!");
    }

    @Override
    public void bark() {
        System.out.println("Barking softly.");
    }
}

// Implementações concretas para gatos
class Siamese implements Cat {
    @Override
    public void makeSound() {
        System.out.println("Meow!");
    }

    @Override
    public void meow() {
        System.out.println("Meowing gracefully.");
    }
}

class Persian implements Cat {
    @Override
    public void makeSound() {
        System.out.println("Meow! Meow!");
    }

    @Override
    public void meow() {
        System.out.println("Meowing lazily.");
    }
}

// Abstract Factory para criar famílias de animais
interface AnimalFactory {
    Dog createDog();
    Cat createCat();
}

// Concrete Factory para criar famílias específicas de animais
class DomesticAnimalFactory implements AnimalFactory {
    @Override
    public Dog createDog() {
        return new Poodle(); // Podemos escolher qualquer implementação de Dog
    }

    @Override
    public Cat createCat() {
        return new Persian(); // Podemos escolher qualquer implementação de Cat
    }
}

// Exemplo de uso
public class Main {
    public static void main(String[] args) {
        // Criando uma fábrica abstrata para animais domésticos
        AnimalFactory animalFactory = new DomesticAnimalFactory();

        // Criando animais usando a fábrica abstrata
        Dog dog = animalFactory.createDog();
        Cat cat = animalFactory.createCat();

        // Chamando métodos específicos de cada animal
        dog.makeSound(); // Saída: Woof!
        dog.bark();      // Saída: Barking softly.

        cat.makeSound(); // Saída: Meow! Meow!
        cat.meow();      // Saída: Meowing lazily.
    }
}
```
Neste exemplo, **AnimalFactory** é a fábrica abstrata que declara métodos para criar famílias de objetos relacionados (Dog e Cat). **DomesticAnimalFactory** é uma implementação concreta dessa fábrica que cria objetos específicos (Poodle e Persian). O cliente pode usar a fábrica abstrata para criar instâncias de animais sem conhecer suas classes concretas.

