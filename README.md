# Logger de Eventos Urbanos con Quarkus y Kafka

Este proyecto es un logger de eventos urbanos desarrollado con Quarkus y Apache Kafka. Forma parte de una serie de ejercicios de formación sobre eventos y mensajería asíncrona utilizando Kafka.

## Descripción

El logger consume mensajes de eventos urbanos desde un topic de Kafka y los registra en un archivo de logs. Es un ejemplo práctico de cómo integrar Quarkus con Kafka para procesar eventos en tiempo real.

## Tecnologías Utilizadas

- **Quarkus**: Framework Java para aplicaciones nativas en la nube.
- **Apache Kafka**: Plataforma de streaming de eventos.
- **Maven**: Herramienta de gestión de dependencias y construcción.
- **Java 17+**: Versión de Java requerida.

## Requisitos Previos

- Java 17 o superior instalado.
- Apache Maven 3.6+.
- Una instancia de Kafka corriendo (local o remota).
- Conocimientos básicos de Java y Kafka.

## Instalación

1. Clona el repositorio:
   ```bash
   git clone <url-del-repositorio>
   cd logger-quarkus
   ```

2. Instala las dependencias:
   ```bash
   ./mvnw clean install
   ```

## Configuración

Edita el archivo `src/main/resources/application.properties` para configurar la conexión a Kafka:

```properties
# Configuración de Kafka
mp.messaging.incoming.urban-events.connector=smallrye-kafka
mp.messaging.incoming.urban-events.topic=urban-events
mp.messaging.incoming.urban-events.bootstrap.servers=localhost:9092
mp.messaging.incoming.urban-events.group.id=urban-events-logger
mp.messaging.incoming.urban-events.auto.offset.reset=earliest

# Configuración de logging
quarkus.log.file.enable=true
quarkus.log.file.path=logs/urban-events-logger.log
quarkus.log.file.rotation.max-file-size=10M
quarkus.log.file.rotation.max-backup-index=5
```

## Ejecución

### Modo Desarrollo

Para ejecutar en modo desarrollo con recarga en vivo:

```bash
./mvnw quarkus:dev
```

La aplicación estará disponible en `http://localhost:8080`. La interfaz de desarrollo de Quarkus en `http://localhost:8080/q/dev/`.

### Empaquetado y Ejecución

1. Empaqueta la aplicación:
   ```bash
   ./mvnw package
   ```

2. Ejecuta el JAR:
   ```bash
   java -jar target/quarkus-app/quarkus-run.jar
   ```

### Ejecutable Nativo

Para crear un ejecutable nativo:

```bash
./mvnw package -Dnative
```

O en un contenedor si no tienes GraalVM:

```bash
./mvnw package -Dnative -Dquarkus.native.container-build=true
```

Ejecuta con:
```bash
./target/logger-quarkus-1.0.0-SNAPSHOT-runner
```

## Uso

Una vez ejecutándose, el logger se conectará automáticamente al topic `urban-events` de Kafka y comenzará a consumir mensajes. Los eventos se registrarán en el archivo `logs/urban-events-logger.log`.

Ejemplo de mensaje de evento esperado:
```json
{
  "id": "12345",
  "type": "traffic_incident",
  "location": "Calle Mayor, 10",
  "timestamp": "2023-10-01T12:00:00Z",
  "description": "Accidente de tráfico"
}
```

## Estructura del Proyecto

```
src/
├── main/
│   ├── java/
│   │   └── com/urbanevents/logger/
│   │       └── EventLogger.java
│   └── resources/
│       └── application.properties
└── test/
    └── java/
        └── com/urbanevents/logger/
            └── MyMessagingApplicationTest.java
```

## Contribución

Este proyecto es parte de ejercicios de formación. Para contribuir:

1. Fork el repositorio.
2. Crea una rama para tu feature (`git checkout -b feature/nueva-funcionalidad`).
3. Commit tus cambios (`git commit -am 'Añade nueva funcionalidad'`).
4. Push a la rama (`git push origin feature/nueva-funcionalidad`).
5. Abre un Pull Request.

## Licencia

Este proyecto está bajo la Licencia MIT. Ver el archivo `LICENSE` para más detalles.

## Recursos Adicionales

- [Documentación de Quarkus](https://quarkus.io/)
- [Guía de Kafka con Quarkus](https://quarkus.io/guides/kafka-getting-started)
- [Apache Kafka Documentation](https://kafka.apache.org/documentation/)

