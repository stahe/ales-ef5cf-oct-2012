# Migración de NHibernate a Entity Framework 5 (octubre de 2012)

Este documento ilustra una **arquitectura de aplicación ASP.NET flexible y escalable**
y muestra cómo se puede sustituir el ORM **NHibernate** por **Entity Framework 5**
sin modificar la capa de aplicación.

📄 El sitio web correspondiente se encuentra en la URL: https://stahe.github.io/ales-ef5cf-oct-2012/

---

## Antecedentes

**Entity Framework** es un ORM (mapeador objeto-relacional) desarrollado originalmente por Microsoft
y que es de código abierto desde julio de 2012.

En un curso de ASP.NET, este documento se basa en una arquitectura en capas,
lo que permite adaptar las tecnologías (ORM, DBMS) sin que ello afecte a la aplicación.

---

## Arquitectura general

El siguiente diagrama muestra las arquitecturas que se utilizan en la aplicación:

![Arquitectura de ASP.NET con NHibernate y Spring.NET](https://stahe.github.io/ef5cf-oct-2012/images/10000000000007D200000183315F4E40.png)

![Arquitectura ASP.NET con Entity Framework 5 y Spring.NET](https://stahe.github.io/ef5cf-oct-2012/images/10000000000007D7000001825B1CF7DD.png)

### Descripción de las capas

- **Aplicación ASP.NET**  
  Capa de presentación y lógica de la aplicación.

- **DAO (Objetos de acceso a datos)**  
  Interfaz de acceso a datos utilizada por la aplicación.

- **ORM (NHibernate / Entity Framework)**  
  Responsable de generar el código SQL y de la comunicación con ADO.NET.

- **ADO.NET**  
  Enlace con el DBMS.

- **DBMS**  
  Sistema de gestión de bases de datos.

- **Spring.NET**  
  Se encarga de la integración de las capas y de la inyección de dependencias.

---

## ¿Por qué usar un ORM?

Al vincular la capa DAO directamente con ADO.NET, la aplicación se vuelve dependiente del SGBD:

- diferencias en los tipos de datos;
- estrategias para generar claves primarias;
- SQL propietario;
- bibliotecas específicas del SGBD.

Con un ORM, cambiar de SGBD equivale, en la práctica, a **modificar la configuración**
del ORM. La capa DAO permanece inalterada.

---

## Función de Spring.NET

Spring.NET permite:

- que la aplicación ASP.NET obtenga una referencia a la capa DAO;
- crear esta capa a partir de un archivo de configuración;
- sustituir una implementación DAO por otra **sin modificar el código**,
  siempre y cuando la interfaz permanezca idéntica.

---

## Objetivo del documento

Demostrar concretamente que la arquitectura:

- **es resistente a los cambios en el SGBD**;
- **es resistente a los cambios en el ORM**;
- permite **reemplazar NHibernate por Entity Framework 5**
  sin modificar la capa de aplicación de ASP.NET.

---

## Enfoque seguido

La migración se lleva a cabo en varios pasos:

1. Exploración de **Entity Framework 5** con diferentes sistemas de gestión de bases de datos (DBMS);
2. Creación de una nueva capa de datos (**DAO2**);
3. Integración de la aplicación ASP.NET existente con esta nueva capa DAO.

---

## Público objetivo

- Desarrolladores de ASP.NET
- Estudiantes y profesores del área de arquitectura de software
- Cualquier persona interesada en arquitecturas desacopladas y escalables

---

## Licencia y uso

Documento educativo destinado a la enseñanza y demostración
de arquitecturas de aplicaciones escalables.
