# Lombok

## Anotaciones Básicas

### @Getter y @Setter

Estas anotaciones generan automáticamente los métodos get y set para los campos de una clase.

```java
import lombok.Getter;
import lombok.Setter;

public class Persona {
    @Getter @Setter
    private String nombre;
    
    @Getter @Setter
    private int edad;
}
```

### @ToString

Genera un método toString() que incluye todos los campos de la clase.

```java
import lombok.ToString;

@ToString
public class Persona {
    private String nombre;
    private int edad;
}

```

### @EqualsAndHashCode

Genera métodos equals() y hashCode() basados en los campos de la clase.

```java
import lombok.EqualsAndHashCode;

@EqualsAndHashCode
public class Persona {
    private String nombre;
    private int edad;
}

```

## Constructor

### @NoArgsConstructor, @AllArgsConstructor, @RequiredArgsConstructor

- @NoArgsConstructor: Genera un constructor sin argumentos.
- @AllArgsConstructor: Genera un constructor con un argumento para cada campo.
- @RequiredArgsConstructor: Genera un constructor para los campos finales y no inicializados.

```java
import lombok.NoArgsConstructor;
import lombok.AllArgsConstructor;
import lombok.RequiredArgsConstructor;

@NoArgsConstructor
@AllArgsConstructor
@RequiredArgsConstructor
public class Persona {
    private final String nombre;
    private int edad;
}

```

## Ejemplo al completo

```java
import lombok.Data;
import lombok.NoArgsConstructor;
import lombok.AllArgsConstructor;

@Data
@NoArgsConstructor
@AllArgsConstructor
public class Persona {
    private String nombre;
    private int edad;
}

```

La anotación @Data es un atajo que combina @Getter, @Setter, @ToString, @EqualsAndHashCode y @RequiredArgsConstructor.

## Anotaciones Avanzadas

### @Builder

Permite construir objetos de manera más legible utilizando el patrón Builder.

```java
import lombok.Builder;

@Builder
public class Persona {
    private String nombre;
    private int edad;
}

// Uso
Persona persona = Persona.builder()
    .nombre("Juan")
    .edad(30)
    .build();

```

### @Value

Define una clase como inmutable, similar a @Data pero todos los campos son finales y privados, y no genera setters.

```java
import lombok.Value;

@Value
public class Persona {
    String nombre;
    int edad;
}

```

### @Singular

Usada junto con @Builder para manejar colecciones de forma elegante.

```java
import lombok.Builder;
import lombok.Singular;
import java.util.List;

@Builder
public class Equipo {
    @Singular
    private List<String> jugadores;
}

// Uso
Equipo equipo = Equipo.builder()
    .jugador("Juan")
    .jugador("Pedro")
    .build();

```

## Anotaciones para Logging

Lombok proporciona varias anotaciones para agregar fácilmente loggers a tus clases:

- @Log: Para java.util.logging.
- @Slf4j: Para org.slf4j.
- @Log4j: Para org.apache.log4j.

```java
import lombok.extern.slf4j.Slf4j;

@Slf4j
public class EjemploLogging {
    public void metodo() {
        log.info("Este es un mensaje de log");
    }
}

```

## Ejemplo uso de Lombok

```java
import lombok.Data;
import lombok.Builder;
import lombok.extern.slf4j.Slf4j;

@Data
@Builder
@Slf4j
public class Empleado {
    private final String nombre;
    private final int edad;
    private final String puesto;

    public void mostrarInfo() {
        log.info("Empleado: {} - Edad: {} - Puesto: {}", nombre, edad, puesto);
    }
}

// Uso
public class Main {
    public static void main(String[] args) {
        Empleado empleado = Empleado.builder()
            .nombre("Ana")
            .edad(28)
            .puesto("Desarrolladora")
            .build();

        empleado.mostrarInfo();
    }
}

```
