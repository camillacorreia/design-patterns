# Factory Method

O padrão Factory Method é um padrão de design criacional que define uma interface para criar objetos, mas permite que as subclasses decidam qual classe instanciar. Ele ajuda a promover a coesão e desacoplamento entre a criação de objetos e seu uso. Em vez de chamar diretamente o construtor de uma classe, o padrão Factory Method permite que uma classe delegue a criação de seus objetos a uma subclasse.

<img src="/img/factory-method.png"/>

## Problema

Imagine que você está desenvolvendo um sistema para uma empresa de transporte que precisa criar diferentes tipos de veículos, como carros e bicicletas. No início, o sistema pode ser simples e apenas lidar com um tipo de veículo. No entanto, à medida que o sistema cresce, você precisa adicionar novos tipos de veículos sem modificar o código existente, garantindo que a criação de veículos novos não quebre o código já implementado.

## Implementação

1. Definir a Interface para o Veículo

```java
// Veículo.java
public interface Vehicle {
    String createVehicle();
}
```

2. Implementar Classes Concretas

```java
// Car.java
public class Car implements Vehicle {
    @Override
    public String createVehicle() {
        return "Car created";
    }
}

// Bicycle.java
public class Bicycle implements Vehicle {
    @Override
    public String createVehicle() {
        return "Bicycle created";
    }
}
```

3. Definir a Interface da Fábrica

```java
// VehicleFactory.java
public abstract class VehicleFactory {
    public abstract Vehicle createVehicle();
}
```

4. Implementar Fábricas Concretas

```java
// CarFactory.java
public class CarFactory extends VehicleFactory {
    @Override
    public Vehicle createVehicle() {
        return new Car();
    }
}

// BicycleFactory.java
public class BicycleFactory extends VehicleFactory {
    @Override
    public Vehicle createVehicle() {
        return new Bicycle();
    }
}
```

5. Utilizar a Fábrica

```java
// Main.java
public class Main {
    public static void main(String[] args) {
        VehicleFactory carFactory = new CarFactory();
        VehicleFactory bicycleFactory = new BicycleFactory();

        Vehicle car = carFactory.createVehicle();
        Vehicle bicycle = bicycleFactory.createVehicle();

        System.out.println(car.createVehicle());       // Output: Car created
        System.out.println(bicycle.createVehicle());  // Output: Bicycle created
    }
}
```

### Resumo

- **Interface Vehicle:** Define o contrato para os veículos.
- **Classes Car e Bicycle:** Implementam a interface Vehicle.
- **Interface VehicleFactory:** Define o contrato para fábricas de veículos.
- **Classes CarFactory e BicycleFactory:** Implementam a interface VehicleFactory e criam instâncias de Car e Bicycle, respectivamente.
- **Classe Main:** Demonstra como usar as fábricas para criar veículos sem precisar saber a classe concreta.

## Vantagens

- **Desacoplamento:** O código cliente não precisa saber qual classe concreta está sendo instanciada.
- **Facilidade de Extensão:** Novos tipos de veículos podem ser adicionados facilmente criando novas fábricas e classes concretas.
- **Manutenção Facilitada:** A lógica de criação de objetos está encapsulada em uma única classe, o que facilita a manutenção e evolução do código.

### Qual a diferença de factory method e abstract factory?

#### Objetivo

- **Factory Method:** Cria uma única classe de produto; o cliente precisa conhecer a classe de produto específica.
- **Abstract Factory:** Cria famílias de produtos relacionados; o cliente pode usar produtos relacionados sem conhecer suas classes concretas.

#### Complexidade

- **Factory Method:** É mais simples e focado na criação de um único tipo de produto.
- **Abstract Factory:** É mais complexo, pois lida com a criação de múltiplos produtos que são geralmente usados em conjunto.

#### Escalabilidade

- **Factory Method:** Mais adequado quando há apenas um tipo de produto que precisa ser criado.
- **Abstract Factory:** Mais adequado quando o sistema deve suportar diferentes famílias de produtos que são usados juntos.
