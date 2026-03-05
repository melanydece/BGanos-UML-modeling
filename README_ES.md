[English](README.md) | **Español**

# B-Ganos UML y Diseño Dirigido por Modelos (MDD)

## Visión general

Este repositorio contiene el **diseño UML completo y la arquitectura dirigida por modelos** de la aplicación B-Ganos.

El proyecto fue desarrollado durante la asignatura **Modelado de Software** (3º curso, Ingeniería del Software, Universidad Complutense de Madrid, 2024–2025) por un equipo de 12 personas.

Este repositorio no solo contiene artefactos de documentación, sino que también refleja un **proceso completo de desarrollo dirigido por modelos** en el que los modelos UML fueron transformados directamente en código Java ejecutable.

> El sistema fue modelado completamente en UML y posteriormente el código Java fue generado automáticamente a partir del modelo utilizando IBM Rational Software Architect Designer (RSAD).

Este repositorio representa por tanto la base arquitectónica a partir de la cual se generó la aplicación.

---

## Enfoque de desarrollo dirigido por modelos

El flujo de desarrollo fue el siguiente:

1. Diseñar la arquitectura multicapa en UML.
2. Definir las entidades del dominio, los servicios, los componentes de persistencia y la estructura de presentación.
3. Configurar la transformación UML-a-Java (`UML2JAVA.tc`).
4. Generar automáticamente la estructura inicial del proyecto Java a partir del modelo.
5. Completar y refinar la implementación.

Este enfoque garantizó:

- Consistencia arquitectónica
- Separación clara de capas
- Reducción del código repetitivo
- Fuerte alineación entre diseño e implementación

---

## Arquitectura del sistema

El modelo UML define una arquitectura multicapa:

- **Capa de presentación**
- **Capa de negocio**
- **Capa de integración**

El sistema interactúa con una base de datos relacional gestionada a través de los mecanismos de persistencia modelados en la capa de integración.

Los principales mecanismos arquitectónicos modelados incluyen:

- Patrón DAO (persistencia basada en SQL)
- Persistencia con JPA
- Gestión de transacciones
- Patrón Application Controller
- Patrón Service to Worker
- Separación entre Business Objects y Transfer Objects
- Patrones de factoría
- Mecanismos de control de concurrencia

---

## Modelo de persistencia

La capa de persistencia del sistema fue diseñada utilizando **dos enfoques complementarios**: persistencia basada en DAO y persistencia basada en JPA.

Ambos modelos de persistencia siguen los mismos requisitos estructurales.

### Modelo DAO

El modelo de persistencia DAO se basa en el **patrón Data Access Object (DAO)**, donde el acceso a la base de datos se implementa manualmente utilizando SQL y componentes JDBC. Incluye:

- **6 entidades**
- **2 entidades especializadas (herencia)**
- **2 relaciones muchos a muchos**
  - una con atributos en la relación
  - una sin atributos

Además, el modelo DAO incluye **queries personalizadas** utilizadas para implementar consultas complejas requeridas por la especificación del proyecto.

Algunos ejemplos son:

- `CalcularLasTresFechasMasVendidasDeUnInvernadero`
- `ListarInformacionFabricantePorSistemasDeRiegoDeUnInvernadero`

Estas consultas se gestionan mediante una **Query Factory** que crea los objetos de consulta correspondientes.

Las seis entidades DAO definidas en el sistema son:

- Invernadero
- Planta
- Factura
- Fabricante
- Entrada
- SistemaDeRiego

Estas entidades se gestionan mediante interfaces DAO y sus implementaciones responsables de la interacción directa con SQL.

### Modelo JPA

El modelo de persistencia JPA utiliza **Java Persistence API (JPA)** para gestionar la interacción con la base de datos mediante mapeo objeto-relacional. Incluye:

- **6 entidades JPA**
- **2 entidades especializadas (herencia)**
- **2 relaciones M-N**
  - una con atributos en la relación
  - una sin atributos

El modelo JPA también demuestra el uso de **herencia entre entidades y operaciones polimórficas**, permitiendo que entidades especializadas extiendan entidades base del dominio.

Las seis entidades JPA definidas en el sistema son:

- ProveedorJPA
- ProductoJPA
- TurnoJPA
- VentaJPA
- MarcaJPA
- EmpleadoDeCajaJPA

Este modelo demuestra un enfoque alternativo de persistencia donde las operaciones de base de datos se gestionan mediante mapeos de entidades en lugar de SQL manual.

---

## Modelado de capas

El diseño UML organiza el sistema en tres capas principales.  
Cada capa encapsula un conjunto específico de responsabilidades e interactúa con las demás mediante interfaces claramente definidas.

### Modelado de la capa de integración

La capa de integración define los **mecanismos de persistencia e interacción con la base de datos**.

- Interfaces DAO e implementaciones (por ejemplo: `EntradaDAO`, `EntradaDAOImp`)
- Componentes de gestión de transacciones
- Elementos JDBC (Connection, PreparedStatement, ResultSet)
- Manejo de excepciones
- Abstracciones de factorías y consultas

---

### Modelado de la capa de negocio

La capa de negocio modela la **lógica principal del dominio del sistema** y los casos de uso de la aplicación.

Incluye:

- Entidades del dominio que representan los principales conceptos de negocio
- Servicios de negocio responsables de implementar las operaciones
- Implementaciones de servicios
- Transfer Objects utilizados para la comunicación con la capa de presentación
- Factorías de negocio utilizadas para obtener instancias de servicios

Ejemplos de servicios de negocio incluyen:

- `EntradaSA`
- `MarcaSA`
- `SistemaDeRiegoSA`

Entre los componentes de infraestructura de soporte se encuentran elementos como `EMFSingleton`, responsable de gestionar el contexto de persistencia.

---

### Modelado de la capa de presentación

La capa de presentación modela:

- ApplicationController
- Envío de peticiones desde el controlador hacia los servicios de negocio
- Componentes de interfaz gráfica (basados en Swing)
- Interacción con Transfer Objects (por ejemplo: `TMarca`)
- Flujo de comunicación entre el controlador y los servicios

---

## Principales artefactos UML

Los artefactos de diseño más relevantes incluyen:

- **Diagramas de clases**
  - Entidades del dominio que representan los conceptos principales del sistema
  - Interfaces DAO e implementaciones
  - Servicios de negocio
  - Controladores de presentación y componentes de la interfaz gráfica
- **Diagramas de secuencia**
  - Operaciones transaccionales
  - Flujos de ejecución de casos de uso
  - Interacciones Controller → Service → DAO
- **Diagrama de componentes**
  - Separación por capas del sistema
  - Dependencias entre módulos
- **Diagrama de despliegue**
  - Estructura de despliegue de la aplicación
  - Integración con la base de datos
- **Diagramas entidad-relación**
	
	Se incluyen diagramas ER separados para:

  - Modelo de persistencia DAO
  - Modelo de persistencia JPA

---

## Estructura del repositorio (simplificada)

```
B-Ganos-UML-Modeling/
├── Diagramas/
│ ├── Modelo de despliegue/
│ │ ├── Diagramas de componentes/
│ │ └── Diagramas de despliegue/
│ └── Modelo del Diseño/
│ │ ├── Diagramas de clase/
│ │ ├── Diagramas de secuencia/
│ │ └── Diagramas de formato libre/
│
├── Modelos/
│ ├── Modelo de despliegue/
│ └── Modelo del Diseño/
│ │ ├── Arquitectura/
│ │ ├── Integracion/
│ │ ├── Negocio/
│ │ └── Presentacion/
│
├── DiagramaEntidadRelacion/
│ ├── DAO.drawio.png
│ └── JPA.drawio.png
│
├── JPA Content/
│ └── persistence.xml
│
├── UML2JAVA.tc
└── src/ (empty - required by the Eclipse/RSAD project structure)
```

---

## Documentación del proyecto

El repositorio también contiene documentación extensa que se hizo durante el proyecto:

### Especificación de Requisitos de Software (SRS)

Un **documento de especificación de requisitos de 105 páginas** que describe:

- Funcionalidad del sistema
- Casos de uso
- Conceptos del dominio
- Requisitos del sistema
- Artefactos iniciales de diseño

El documento también incluye **diagramas entidad-relación** para los modelos de persistencia DAO y JPA.

### Memoria del proyecto

Un informe detallado del proyecto que describe:

- La arquitectura del sistema
- Los patrones arquitectónicos utilizados
- El proceso de modelado
- La gestión del proyecto y las herramientas de desarrollo utilizadas

---

## Herramientas utilizadas

- UML 2.x
- IBM Rational Software Architect Designer (RSAD) 9.6
- Transformación UML-a-Java
- Java 8 (entorno objetivo)

---

## Código de la aplicación

La implementación del sistema basada en este modelo UML está disponible en un repositorio aparte. Puede encontrarse aquí:

https://github.com/melanydece/BGanos-java-application

---

## Equipo

Desarrollado colaborativamente por un equipo de 12 personas como parte de un proyecto avanzado del grado de Ingeniería del Software. La lista completa de contribuyentes puede encontrarse en la sección **Contributors** del repositorio.