# Factory Method

O padrão Abstract Factory é um padrão de design criacional que fornece uma interface para criar famílias de objetos relacionados ou dependentes sem especificar suas classes concretas. Ele permite que você produza diferentes tipos de produtos que pertencem a uma mesma família, garantindo que os produtos criados sejam compatíveis entre si.

<img src="/img/abstract-factory.png"/>

## Problema

Imagine que você está desenvolvendo um aplicativo que precisa suportar dois temas diferentes (claro e escuro). Cada tema deve ter um conjunto diferente de componentes, como botões e caixas de texto, e esses componentes precisam ser compatíveis entre si. Ao adicionar novos temas, você deseja garantir que o sistema continue funcionando corretamente sem modificar o código existente.

## Implementação

1. Definir a Interface para os Produtos

```java
// Botão.java
public interface Button {
    String render();
}

// CaixaDeTexto.java
public interface TextBox {
    String render();
}
```

2. Implementar Produtos Concretos

```java
// BotãoClaro.java
public class LightButton implements Button {
    @Override
    public String render() {
        return "Light button";
    }
}

// CaixaDeTextoClaro.java
public class LightTextBox implements TextBox {
    @Override
    public String render() {
        return "Light text box";
    }
}

// BotãoEscuro.java
public class DarkButton implements Button {
    @Override
    public String render() {
        return "Dark button";
    }
}

// CaixaDeTextoEscura.java
public class DarkTextBox implements TextBox {
    @Override
    public String render() {
        return "Dark text box";
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
// FábricaClaro.java
public class LightThemeFactory implements ComponentFactory {
    @Override
    public Button createButton() {
        return new LightButton();
    }

    @Override
    public TextBox createTextBox() {
        return new LightTextBox();
    }
}

// FábricaEscura.java
public class DarkThemeFactory implements ComponentFactory {
    @Override
    public Button createButton() {
        return new DarkButton();
    }

    @Override
    public TextBox createTextBox() {
        return new DarkTextBox();
    }
}
```

5. Utilizar a Fábrica

```java
// Main.java
public class Main {
    public static void main(String[] args) {
        ComponentFactory lightFactory = new LightThemeFactory();
        ComponentFactory darkFactory = new DarkThemeFactory();

        Button lightButton = lightFactory.createButton();
        TextBox lightTextBox = lightFactory.createTextBox();

        Button darkButton = darkFactory.createButton();
        TextBox darkTextBox = darkFactory.createTextBox();

        System.out.println(lightButton.render());     // Output: Light button
        System.out.println(lightTextBox.render());    // Output: Light text box
        System.out.println(darkButton.render());      // Output: Dark button
        System.out.println(darkTextBox.render());     // Output: Dark text box
    }
}
```

### Resumo

- **Abstract Factory:** Define uma interface para criar famílias de produtos relacionados.
- **ConcreteFactory:** Implementa a criação de produtos concretos de uma família.
- **AbstractProduct:** Define interfaces para produtos que pertencem a uma família.
- **ConcreteProduct:** Implementa as interfaces dos produtos.
- **Client:** Usa a fábrica para obter produtos sem precisar conhecer suas classes concretas.
