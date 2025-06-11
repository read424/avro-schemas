# Avro Schemas

> **Definiciones de esquemas Avro compartidos para integración con Apache Kafka**

Este proyecto contiene todos los esquemas Avro utilizados en la arquitectura de microservicios de Walrex para garantizar la compatibilidad y evolución controlada de mensajes en Kafka.

## 🎯 **Propósito**

- **Centralizar** definiciones de esquemas Avro
- **Versionar** cambios de esquemas de forma controlada
- **Distribuir** automáticamente esquemas compilados via GitHub Packages
- **Garantizar** compatibilidad entre servicios

## 📦 **Contenido**

```
avro-schemas/
├── src/main/resources/avro/          # Esquemas Avro (.avsc)
│   ├── events/             # Eventos de dominio
│   ├── commands/           # Comandos
│   └── queries/            # Consultas
├── pom.xml                 # Configuración Maven
└── README.md
```

## 🚀 **Uso**

### **Como dependencia Maven:**

```xml
<dependency>
    <groupId>com.walrex</groupId>
    <artifactId>avro-schemas</artifactId>
    <version>1.0.0</version>
</dependency>
```

### **Configurar repositorio GitHub Packages:**

```xml
<repositories>
    <repository>
        <id>github</id>
        <url>https://maven.pkg.github.com/read424/avro-schemas</url>
    </repository>
</repositories>
```

## 🛠️ **Desarrollo**

### **Prerrequisitos:**
- Java 21+
- Maven 3.9+
- Apache Avro Tools

### **Compilar localmente:**

```bash
# Compilar esquemas
mvn clean compile

# Instalar en repositorio local
mvn clean install

# Generar clases Java
mvn generate-sources
```

### **Agregar nuevo esquema:**

1. Crear archivo `.avsc` en `src/main/avro/`
2. Compilar y probar localmente
3. Crear PR con los cambios
4. Merge y crear tag para release

## 📋 **Convenciones**

### **Naming:**
- **Message**: `UserCreatedMessage.avsc`
- **Eventos**: `UserCreatedEvent.avsc`
- **Comandos**: `CreateUserCommand.avsc`
- **Consultas**: `GetUserQuery.avsc`

### **Versionado:**
- **Esquemas**: Usar evolución compatible hacia atrás
- **Releases**: Semantic versioning (`v1.2.3`)
- **Breaking changes**: Mayor version bump

### **Estructura de esquema:**
```json
{
  "type": "record",
  "name": "ExampleEvent",
  "namespace": "com.walrex.events",
  "doc": "Descripción del evento",
  "fields": [
    {"name": "id", "type": "string", "doc": "Identificador único"},
    {"name": "timestamp", "type": "long", "doc": "Timestamp del evento"}
  ]
}
```

## 🔄 **CI/CD**

### **Workflow automático:**

```
Tag v* → GitHub Actions → Compile → Test → Publish to GitHub Packages
```

### **Para crear release:**

```bash
git tag v1.0.0
git push origin v1.0.0
```

### **Para usar en otros proyectos:**

```xml
<!-- Configurar autenticación para GitHub Packages -->
<servers>
    <server>
        <id>github</id>
        <username>${env.GITHUB_ACTOR}</username>
        <password>${env.GITHUB_TOKEN}</password>
    </server>
</servers>
```

## 🧪 **Testing**

```bash
# Validar esquemas
mvn test

# Verificar compatibilidad
mvn avro:schema-compatibility
```

## 📚 **Recursos**

- [Apache Avro Documentation](https://avro.apache.org/docs/)
- [Schema Evolution Best Practices](https://docs.confluent.io/platform/current/schema-registry/avro.html)
- [GitHub Packages Maven](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-apache-maven-registry)

## 🤝 **Contribución**

1. Fork del proyecto
2. Crear branch feature (`git checkout -b feature/nuevo-esquema`)
3. Commit cambios (`git commit -am 'feat: add nuevo esquema'`)
4. Push branch (`git push origin feature/nuevo-esquema`)
5. Crear Pull Request

## 📄 **Licencia**

Proyecto interno de Walrex - Todos los derechos reservados.

## 📧 **Contacto**

- **Maintainer**: read424
- **Project**: [Walrex Monolith Module](https://github.com/read424/monolith-module-v1)
- **Issues**: [GitHub Issues](https://github.com/read424/avro-schemas/issues)

---

**Built with ❤️ for Walrex ecosystem**