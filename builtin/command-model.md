# Command model

## Metadata

| Field    | Value    |
| -------- | -------- |
| Language | es       |
| Origin   | authored |

## Methodology and implementation

La metodología define los conceptos, su semántica, sus relaciones y el comportamiento esperado.

La implementación determina cómo esos conceptos se materializan en una tecnología, herramienta, interfaz o plataforma concreta.

Un command pertenece al modelo metodológico.

Su implementación concreta pertenece a otra capa.

Por ejemplo:

```text
Canonical command
    task.run(...)
        ↓
Implementation
    CLI
    Codex adapter
    API
    other platform
```

Cambiar la forma de invocar un command desde una plataforma no debe modificar su significado canónico.

---

## Canonical commands

Un command representa una **operación semántica canónica**.

No representa directamente:

* un comando de shell;
* una función de un lenguaje de programación;
* una llamada HTTP;
* una instrucción específica para un agente;
* una operación propia de una plataforma concreta.

Los commands se identifican mediante un dominio y un verbo:

```text
<object>.<verb>
```

Por ejemplo:

```text
task.start
task.run
task.done
task.rerun
task.reopen
```

El dominio identifica el tipo de objeto sobre el que opera el command.

El verbo identifica la operación.

---

## Command definition

La definición de un command incluye una firma canónica.

Por ejemplo:

```text
task.run(
    selector,
    completion = "auto"
)
```

La firma define:

* los parámetros disponibles;
* su orden canónico;
* cuáles son obligatorios;
* cuáles son opcionales;
* sus valores por defecto;
* cuál es el primary parameter.

La firma forma parte del contrato del command.

---

## Usage

Los commands utilizan una notación funcional.

Por ejemplo:

```text
task.run(
    selector,
    completion = "auto"
)
```

Una invocación mínima puede ser:

```text
task.run("001-create-binary")
```

Una invocación explícita:

```text
task.run(
    selector = "001-create-binary"
)
```

Y una invocación con argumentos opcionales:

```text
task.run(
    selector = "001-create-binary",
    completion = "manual"
)
```

---

## Parameters

Los parámetros pueden proporcionarse:

* por posición;
* por nombre.

### Positional binding

Un argumento sin nombre se asigna al primer parámetro disponible según el orden definido por la firma.

Por ejemplo:

```text
task.run("pepe")
```

con la firma:

```text
task.run(
    selector,
    completion = "auto"
)
```

equivale a:

```text
task.run(
    selector = "pepe"
)
```

### Named binding

Un argumento con nombre se asigna al parámetro indicado, independientemente de su posición textual dentro de la llamada.

Por ejemplo:

```text
task.run(
    selector = "pepe",
    completion = "manual"
)
```

es equivalente a:

```text
task.run(
    completion = "manual",
    selector = "pepe"
)
```

En ambos casos `selector` sigue siendo el primer parámetro canónico de la firma.

---

## Primary parameter

El primer parámetro definido en la firma tiene un significado especial.

Es el **primary parameter**.

Representa el objeto principal sobre el que opera el command.

Por ejemplo:

```text
task.run(
    selector,
    completion = "auto"
)
```

define:

```text
selector
```

como primary parameter.

El primary parameter no deja de serlo por la forma concreta en la que se escriba la llamada.

Estas dos expresiones utilizan el mismo primary parameter:

```text
task.run("pepe")
```

```text
task.run(
    selector = "pepe"
)
```

También:

```text
task.run(
    completion = "manual",
    selector = "pepe"
)
```

sigue teniendo `selector` como primary parameter.

El papel especial del parámetro viene determinado por la **firma del command**, no por su posición textual dentro de una invocación concreta.

---

## Literal values and references

Los valores entre comillas representan literales.

Por ejemplo:

```text
"pepe"
```

representa literalmente el valor:

```text
pepe
```

Los valores sin comillas representan referencias que deben resolverse en el contexto de ejecución.

Por ejemplo:

```text
pepe
```

representa una referencia cuyo valor debe buscarse en el entorno o contexto disponible.

Por tanto:

```text
task.run("pepe")
```

utiliza el literal `pepe`.

Mientras que:

```text
task.run(pepe)
```

intenta resolver la referencia `pepe`.

Lo mismo aplica a named parameters:

```text
task.run(
    selector = "pepe"
)
```

utiliza un literal.

Mientras que:

```text
task.run(
    selector = pepe
)
```

utiliza una referencia.

Si una referencia no puede resolverse en el contexto de ejecución, la operación debe producir un error.

---

## Default values

Los valores por defecto pertenecen a la definición canónica del command.

Por ejemplo:

```text
task.run(
    selector,
    completion = "auto"
)
```

establece que:

* `selector` es obligatorio;
* `completion` es opcional;
* el valor por defecto de `completion` es `"auto"`.

Por tanto:

```text
task.run("pepe")
```

equivale a:

```text
task.run(
    selector = "pepe",
    completion = "auto"
)
```

Los defaults no deben quedar definidos exclusivamente en adapters o implementaciones.

La firma canónica es la fuente de verdad.

---

## Command invocation

La definición canónica y la invocación humana son conceptos diferentes.

La definición puede ser:

```text
task.run(
    selector,
    completion = "auto"
)
```

Una interfaz orientada a commands puede proyectarla conceptualmente como:

```text
/run <object> [arguments]
```

Todo command puede entenderse como:

```text
verb + object + arguments
```

Por ejemplo:

```text
/run task-001 completion=manual
```

donde:

```text
run                 = verb
task-001            = object
completion=manual   = argument
```

La sintaxis física concreta de esta invocación pertenece al adapter o implementación.

---

## Command chaining

Los commands pueden componerse cuando sus contratos son compatibles.

El primary parameter permite esta composición.

Conceptualmente:

```text
task.start("001-create-binary")
    ↓
task.run()
    ↓
task.done()
```

Cuando un command forma parte de una cadena y su primary parameter no ha sido proporcionado explícitamente, puede recibir la salida del command anterior.

Por ejemplo:

```text
task.start(
    selector = "001-create-binary"
)
    ↓
task.run(
    completion = "manual"
)
    ↓
task.done()
```

El resultado de `task.start` proporciona el objeto sobre el que opera `task.run`.

El resultado de `task.run` proporciona el objeto sobre el que opera `task.done`.

La implementación concreta del mecanismo de chaining no forma parte del contrato metodológico.

Puede utilizar:

* pipelines;
* composición funcional;
* llamadas encadenadas;
* estructuras intermedias;
* mecanismos equivalentes.

Lo importante es conservar la semántica canónica.

---

## Selectors

Algunos commands pueden operar sobre cero, uno o múltiples objetos.

En esos casos, el primary parameter puede aceptar un selector.

Conceptualmente:

```text
selector → 0..N objects
```

El modelo canónico no prescribe una sintaxis específica para los selectors.

Una implementación puede soportar:

* identificadores;
* patrones;
* conjuntos;
* listas;
* expresiones;
* queries;
* filtros;
* otros mecanismos apropiados.

Por ejemplo, una implementación podría admitir:

```text
"build-*"
```

pero el command canónico no depende de que el mecanismo utilizado sea globbing.

---

## No matches

Un selector puede no encontrar ningún objeto aplicable.

Esto no constituye un error.

Debe producir un aviso y finalizar sin realizar modificaciones.

Conceptualmente:

```text
selector
    ↓
0 matches
    ↓
warning
    ↓
no changes
```

Esto permite utilizar commands de forma segura en procesos automatizados cuando en una ejecución determinada no existe trabajo aplicable.

---

## Multiple matches

Un selector puede resolver múltiples objetos.

El conjunto completo debe resolverse antes de aplicar la operación.

Conceptualmente:

```text
selector
    ↓
resolve targets
    ↓
validate operation
    ↓
apply
```

La semántica del command debe mantenerse independientemente de que el selector resuelva uno o muchos objetos.

---

## Outputs

Un command puede producir:

* objetos;
* referencias;
* información;
* artefactos;
* resultados de ejecución.

Los outputs pueden utilizarse para:

* informar al usuario;
* alimentar otro command;
* actualizar el estado del proceso;
* servir de entrada para una operación posterior.

Cuando un output participe en command chaining, debe ser compatible con el primary parameter del command siguiente.

---

## Warnings and errors

Warnings y errors representan situaciones distintas.

### Warning

Un warning indica una condición válida que no impide completar el command.

Por ejemplo:

```text
No tasks matched the selector.
```

Un selector sin coincidencias produce un warning.

### Error

Un error representa una condición que impide ejecutar correctamente la operación.

Por ejemplo:

* un parámetro inválido;
* una referencia que no puede resolverse;
* una transición de estado imposible;
* ausencia de información obligatoria;
* una operación que no puede completarse de forma segura.

La diferencia entre warning y error pertenece al contrato del command.

---

## Applies

Un command puede declarar las versiones para las que su definición resulta aplicable.

La metadata puede incluir:

```text
Applies
```

Ejemplos:

```text
>= 0.2.0
```

```text
= 0.2.0
```

```text
>= 0.2.0, < 1.0.0
```

```text
dev
```

Si `Applies` no contiene ninguna restricción, el command se considera aplicable de forma general.

---

## Commands and workflows

Un command representa una operación.

Un workflow representa una secuencia u orquestación de operaciones.

Conceptualmente:

```text
command  = operation
workflow = sequence and orchestration
```

Por ejemplo:

```text
task.start
    ↓
task.run
    ↓
task.done
```

La lógica de operación pertenece al command.

La lógica que decide qué operations se ejecutan, en qué secuencia y bajo qué condiciones pertenece al workflow.

---

## Commands and adapters

Los adapters proyectan los commands canónicos sobre plataformas o interfaces concretas.

Conceptualmente:

```text
canonical command
       ↓
adapter
       ↓
platform
```

Un adapter puede decidir:

* la sintaxis de invocación;
* cómo representar parámetros;
* cómo representar flags y options;
* cómo resolver selectors;
* cómo mostrar help;
* cómo mostrar warnings;
* cómo mostrar errors;
* cómo ejecutar físicamente la operación.

Pero no puede redefinir la semántica del command.

Por ejemplo:

```text
task.run(
    selector,
    completion = "auto"
)
```

puede proyectarse sobre una CLI como:

```text
iasi task run <selector> --completion <mode>
```

y sobre otro entorno mediante una representación completamente diferente.

Ambos adapters deben preservar la misma operación canónica.

---

# Task commands

## Task lifecycle

Las tasks tienen inicialmente tres estados principales:

```text
pending
active
done
```

El ciclo principal es:

```text
pending
   ↓
active
   ↓
done
```

Una task completada conserva además el resultado de su ejecución:

```text
done/
├── success/
├── failed/
├── partial/
└── cancelled/
```

Por tanto existen dos conceptos diferentes:

```text
state
outcome
```

El state indica dónde se encuentra una task dentro de su ciclo.

El outcome indica cómo terminó.

La definición Markdown de una task no necesita modificarse para reflejar ninguno de estos cambios.

---

## Task definition immutability

El contenido de la task describe el trabajo que debe realizarse.

El estado y el resultado de ejecución se representan externamente.

Por ejemplo:

```text
tasks/pending/foo.md
```

puede pasar a:

```text
tasks/active/foo.md
```

y finalmente:

```text
tasks/done/success/foo.md
```

sin modificar el contenido de `foo.md`.

Esto mantiene separados:

```text
task definition
task state
task outcome
```

---

## task.start

### Usage

```text
task.start(
    selector
)
```

Ejemplos válidos:

```text
task.start("001-create-binary")
```

```text
task.start(
    selector = "001-create-binary"
)
```

### Purpose

Iniciar una o varias tasks pendientes.

### Applicable state

```text
pending
```

### Transition

```text
pending
    ↓
active
```

Si el selector no encuentra ninguna task pendiente aplicable, se produce un warning y no se realiza ninguna modificación.

---

## task.run

### Usage

```text
task.run(
    selector,
    completion = "auto"
)
```

Ejemplos válidos:

```text
task.run("001-create-binary")
```

```text
task.run(
    selector = "001-create-binary"
)
```

```text
task.run(
    "001-create-binary",
    completion = "manual"
)
```

```text
task.run(
    selector = "001-create-binary",
    completion = "manual"
)
```

### Purpose

Ejecutar el trabajo definido por una o varias tasks activas.

### Applicable state

```text
active
```

### Repeated execution

Una task puede ejecutarse varias veces mientras permanezca activa.

Por ejemplo:

```text
active
  ↓
run
  ↓
active
  ↓
run
  ↓
active
```

Una ejecución no implica necesariamente que todo el trabajo haya terminado.

---

## Automatic completion

El comportamiento por defecto es:

```text
completion = "auto"
```

Si la ejecución determina que el trabajo ha terminado, puede cerrar automáticamente la task.

El outcome es un **resultado de la ejecución**.

No es un parámetro elegido por el usuario.

Por ejemplo:

```text
active
   ↓
run
   ↓
execution result: success
   ↓
done/success
```

O:

```text
active
   ↓
run
   ↓
execution result: failed
   ↓
done/failed
```

Si el trabajo todavía no ha terminado:

```text
active
   ↓
run
   ↓
active
```

---

## Manual completion

Puede solicitarse explícitamente:

```text
completion = "manual"
```

Por ejemplo:

```text
task.run(
    "001-create-binary",
    completion = "manual"
)
```

La ejecución puede terminar correctamente, pero la task permanece:

```text
active
```

hasta que una operación explícita determine que puede cerrarse.

Este modo permite incorporar:

* revisión humana;
* inspección;
* aprobación;
* decisiones manuales;
* cualquier gate que no deba automatizarse.

---

## task.done

### Usage

```text
task.done(
    selector
)
```

Ejemplos válidos:

```text
task.done("001-create-binary")
```

```text
task.done(
    selector = "001-create-binary"
)
```

### Purpose

Cerrar explícitamente una o varias tasks activas después de una ejecución con `completion = "manual"` o cuando exista otro motivo para requerir cierre explícito.

### Important

`task.done` **no recibe el outcome como entrada**.

El outcome procede del resultado de ejecución existente.

Conceptualmente:

```text
run
 ↓
execution result
 ↓
outcome
 ↓
done
```

`task.done` consolida el resultado existente.

No lo decide.

### Applicable state

```text
active
```

### Result

La task se mueve al outcome correspondiente:

```text
done/success
done/failed
done/partial
done/cancelled
```

Completar una task no significa que su resultado haya sido validado.

```text
done != validated
```

---

## task.rerun

### Usage

```text
task.rerun(
    selector,
    completion = "auto"
)
```

Ejemplos:

```text
task.rerun("001-create-binary")
```

```text
task.rerun(
    "001-create-binary",
    completion = "manual"
)
```

### Purpose

Volver a ejecutar una task cuya ejecución anterior terminó en `failed`.

### Applicable state

```text
done/failed
```

### Operation

Conceptualmente:

```text
done/failed
    ↓
rerun
    ↓
active
    ↓
run
    ↓
new outcome
```

`rerun` representa un nuevo intento de la misma ejecución que anteriormente falló.

Su parámetro `completion` utiliza la misma semántica y el mismo default que `task.run`.

---

## task.reopen

### Usage

```text
task.reopen(
    selector
)
```

Ejemplos:

```text
task.reopen("001-create-binary")
```

```text
task.reopen(
    selector = "001-create-binary"
)
```

### Purpose

Volver a activar una task cerrada cuando se necesita continuar, ampliar, corregir o revisar trabajo previamente terminado.

### Operation

Conceptualmente:

```text
done/<outcome>
    ↓
reopen
    ↓
active
```

### Difference between rerun and reopen

```text
rerun
    = retry a failed execution

reopen
    = continue, extend, correct or revise closed work
```

Una task que terminó correctamente puede ser reabierta si posteriormente aparece nueva información o trabajo adicional.

---

## Automation by default

Cuando exista una alternativa razonable entre automatización e intervención manual, el comportamiento por defecto debe favorecer la automatización.

Por ejemplo:

```text
task.run(
    selector,
    completion = "auto"
)
```

utiliza `auto` como default.

La intervención manual debe solicitarse explícitamente:

```text
task.run(
    selector,
    completion = "manual"
)
```

La automatización es el camino normal.

La intervención humana sigue disponible cuando el contexto la requiere.

---

## Principle

El modelo define primero **qué significa una operación**.

Después se decide **cómo se implementa**.

```text
methodology
    ↓
canonical command
    ↓
adapter
    ↓
implementation
    ↓
platform
```

La tecnología puede cambiar.

La sintaxis concreta puede cambiar.

El mecanismo de ejecución puede cambiar.

La semántica canónica del command debe permanecer independiente de ellos.
