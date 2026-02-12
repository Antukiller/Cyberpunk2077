# 🦾 Proyecto: Regina’s Database (Night City Override)

![Status: Classified](https://img.shields.io/badge/Status-Classified-red)
![Role: Netrunner](https://img.shields.io/badge/Role-Netrunner-cyan)
![Location: Night_City](https://img.shields.io/badge/Location-Night_City-yellow)

## 📝 1. El Escenario
Eres un **Netrunner** de élite trabajando para **Regina Jones**. Tu misión es gestionar la base de datos de los mercenarios y cyberpsicóticos más peligrosos que operan en Night City. En las calles, la información es vida: el sistema debe ser ultra rápido. Si el escaneo de un objetivo tarda demasiado durante un tiroteo, el cliente terminará en una bolsa de cadáveres de Trauma Team.

---

## 🧩 2. Entidades (Software de Escaneo)
El sistema debe procesar dos tipos de objetivos principales. Cada entidad se identifica mediante un **ID (Hash único)**.

### Reglas de Arquitectura:
* **Sin Herencia:** Se debe utilizar una Interfaz (`IObjetivo`) para definir el comportamiento común.
* **Validación:** El sistema debe rechazar Alias vacíos y niveles de Amenaza fuera del rango (1-50).

### Atributos:
* **Atributos Comunes:** ID, Alias, Nivel de Amenaza (1-50), Eurocréditos ($€$) de recompensa.
* **Mercenario:** Atributo específico de `Cromo` (Porcentaje de mejora cibernética 0-100%).
* **Netrunner:** Atributo específico de `Memoria RAM` disponible (GB).

---

## ⚡ 3. El Oráculo (Programación Funcional)
No utilices métodos convencionales. Debes programar **Funciones de Extensión** para `List<IObjetivo>` que permitan manipular datos mediante **Delegados y Lambdas**:

* `Filtrar()`: Devuelve una nueva lista con los objetivos que cumplan una condición específica.
* `ContarSi()`: Devuelve el número de objetivos que cumplen un criterio (estadísticas de la ciudad).
* `Buscar()`: Encuentra al primer objetivo que coincida con el predicado o devuelve `null`.

---

## 💾 4. El "Sandevistan" de Datos (La Caché)
Para optimizar el rendimiento y evitar procesamientos redundantes en la red, implementa una **Capa de Caché Genérica**:

* **Mecánica:** Crea un Singleton llamado `CyberCache` que almacene resultados en un `Dictionary<string, object>`.
* **Identificador de Consulta:** Genera una "Key" única para cada consulta (ej: `"netrunners_peligrosos"`).
* **Invalidación:** Si se añade un nuevo mercenario o se elimina un objetivo de la lista, la caché debe limpiarse automáticamente para evitar datos obsoletos.



---

## 📊 5. Consultas de la Misión
El programa debe ejecutar y mostrar por consola las siguientes operaciones, priorizando siempre la extracción desde la caché:

1.  **Escaneo de Netrunners:** Listar aquellos con más de 16GB de RAM.
2.  **Rastreo de Objetivo:** Buscar al mercenario con el Alias "V" o "David".
3.  **Análisis de Riesgo:** Calcular la suma total de Eurocréditos ($€$) de todos los objetivos con nivel de amenaza > 40.

---

## ⚠️ Reglas del Fixer (Restricciones)

* **Colecciones:** Utiliza la colección que evite duplicados por ID de forma natural y eficiente.
* **Precisión:** Los Eurocréditos deben mostrarse con el formato `$€ 1,250.00`.
* **Feedback Visual:** Cada vez que los datos se recuperen de la caché, imprime en color cian:
    `[LOG] >> Accediendo a memoria local (Sandevistan activo)...`

---
*"No intentes doblar la cuchara, intenta comprender la verdad... no hay cuchara, solo un List<IObjetivo>."*