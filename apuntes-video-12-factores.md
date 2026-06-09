# Las aplicaciones de 12 factores para un mejor desarrollo

> Video: [Las aplicaciones de 12 FACTORES para un mejor desarrollo](https://www.youtube.com/watch?v=DfUJkaM42gI)  
> Autor/canal: Feregrino  
> Nota: no pude extraer automáticamente la transcripción literal del video porque YouTube bloqueó el acceso desde el entorno actual. Este documento deja una versión ordenada de los temas que trata el video según el título y la metodología **The Twelve-Factor App**. Si pegás la transcripción, puedo convertirlo en una versión fiel minuto a minuto.

## Idea central

El video explica la metodología de las **aplicaciones de 12 factores**, una guía de buenas prácticas para construir aplicaciones modernas, mantenibles, portables y preparadas para desplegarse en distintos entornos, especialmente en contextos cloud, DevOps y software como servicio.

La idea no es usar una tecnología específica, sino seguir principios que ayudan a que una aplicación sea más fácil de desarrollar, configurar, desplegar, escalar y operar.

## ¿Qué problema intentan resolver los 12 factores?

En muchos proyectos, las aplicaciones terminan dependiendo demasiado del entorno donde corren, de configuraciones manuales, de librerías instaladas globalmente o de procesos difíciles de repetir.

Los 12 factores proponen separar responsabilidades y hacer que la aplicación sea:

- reproducible;
- fácil de configurar;
- portable entre entornos;
- simple de desplegar;
- escalable horizontalmente;
- observable mediante logs;
- apta para integración y despliegue continuo.

## Los 12 factores

### 1. Código base

Una aplicación debe tener **un solo código base** versionado en un sistema de control de versiones, como Git.

Puede haber múltiples despliegues de esa misma aplicación —desarrollo, pruebas, producción—, pero todos deben salir del mismo repositorio o código fuente.

**Idea clave:** una aplicación corresponde a un código base; los entornos son despliegues distintos de ese mismo código.

---

### 2. Dependencias

La aplicación debe declarar explícitamente sus dependencias.

No debería asumir que ciertas librerías, paquetes o herramientas ya están instaladas en el sistema operativo. Cada dependencia debe estar listada en archivos como `package.json`, `requirements.txt`, `pom.xml`, `go.mod`, etc.

**Idea clave:** cualquiera debería poder instalar y ejecutar el proyecto a partir de la declaración de dependencias.

---

### 3. Configuración

La configuración debe estar separada del código.

Datos como claves, contraseñas, URLs de bases de datos, tokens, nombres de buckets o endpoints externos no deben estar escritos directamente en el código fuente.

La práctica recomendada es usar variables de entorno u otro mecanismo externo de configuración.

**Idea clave:** el mismo código debe poder correr en distintos entornos cambiando solo la configuración.

---

### 4. Servicios de respaldo

Servicios como bases de datos, colas, cachés, almacenamiento externo o APIs de terceros deben tratarse como recursos conectados.

La aplicación no debería depender de que un servicio esté “pegado” a ella de manera especial. Si se cambia una base local por una remota, o un proveedor por otro, debería bastar con cambiar la configuración.

**Idea clave:** los servicios externos son recursos reemplazables mediante configuración.

---

### 5. Construir, desplegar y ejecutar

El ciclo de vida de la aplicación debe separar claramente tres etapas:

1. **Build:** convertir el código en un artefacto ejecutable.
2. **Release:** combinar el artefacto con la configuración del entorno.
3. **Run:** ejecutar la aplicación.

No conviene mezclar estas fases porque dificulta repetir despliegues, auditar versiones y volver atrás ante errores.

**Idea clave:** build, release y ejecución son pasos distintos.

---

### 6. Procesos

La aplicación debe ejecutarse como uno o más procesos sin estado.

No debería guardar estado importante en memoria local o en el filesystem del proceso. El estado persistente debe vivir en servicios externos, como bases de datos, almacenamiento de objetos o cachés compartidas.

**Idea clave:** si un proceso muere, otro debe poder reemplazarlo sin perder información crítica.

---

### 7. Asignación de puertos

La aplicación debe exponer sus servicios mediante puertos.

En vez de depender de un servidor externo preconfigurado, la aplicación debería poder iniciar y escuchar en un puerto propio, por ejemplo mediante HTTP.

**Idea clave:** la aplicación es autocontenida y publica su servicio por un puerto.

---

### 8. Concurrencia

La aplicación debe poder escalar mediante procesos.

En lugar de depender solamente de hilos internos o de una máquina más grande, se recomienda poder aumentar la cantidad de procesos o instancias que ejecutan la aplicación.

**Idea clave:** escalar horizontalmente debe ser natural.

---

### 9. Desechabilidad

Los procesos deben poder iniciarse y detenerse rápido.

Una aplicación bien diseñada arranca rápido, se apaga de forma ordenada y tolera que el entorno reinicie procesos cuando sea necesario.

Esto ayuda en despliegues, escalamiento, recuperación ante fallos y operación en contenedores.

**Idea clave:** los procesos son reemplazables y deben manejar bien el apagado.

---

### 10. Paridad entre desarrollo y producción

Los entornos de desarrollo, pruebas y producción deberían parecerse lo más posible.

Cuanto más distintos sean, más probable es que aparezcan errores que solo ocurren en producción.

La paridad incluye versiones de servicios, configuración, dependencias y flujo de despliegue.

**Idea clave:** reducir diferencias entre entornos reduce sorpresas.

---

### 11. Logs

La aplicación debe escribir logs como un flujo de eventos.

No debería encargarse internamente de rotar archivos, archivarlos o procesarlos. Lo recomendable es escribir a la salida estándar y dejar que la plataforma de ejecución recolecte, procese y almacene esos logs.

**Idea clave:** la aplicación produce logs; la infraestructura los gestiona.

---

### 12. Procesos administrativos

Las tareas administrativas deben ejecutarse como procesos puntuales usando el mismo entorno de la aplicación.

Ejemplos:

- migraciones de base de datos;
- scripts de mantenimiento;
- tareas de reparación;
- cargas iniciales de datos.

Estas tareas deben correr con el mismo código, dependencias y configuración que el resto de la app.

**Idea clave:** las tareas administrativas son parte del ciclo normal de operación.

## Resumen práctico

Una aplicación alineada con los 12 factores:

- tiene su código en control de versiones;
- declara dependencias explícitamente;
- separa configuración y secretos del código;
- trata bases de datos y servicios externos como recursos intercambiables;
- separa build, release y ejecución;
- no guarda estado crítico en procesos locales;
- expone servicios por puertos;
- escala agregando procesos;
- arranca y se detiene rápido;
- mantiene entornos similares;
- emite logs como flujo de eventos;
- ejecuta tareas administrativas de forma reproducible.

## Aplicación en proyectos reales

Estos principios son especialmente útiles cuando una aplicación va a ejecutarse en:

- contenedores;
- Kubernetes;
- plataformas cloud;
- pipelines de CI/CD;
- entornos con múltiples despliegues;
- sistemas que necesitan escalar o recuperarse rápido.

No todos los proyectos cumplen los 12 factores desde el inicio, pero sirven como checklist para mejorar arquitectura, despliegue y operación.

## Checklist rápida

- [ ] ¿El código está en un repositorio versionado?
- [ ] ¿Las dependencias están declaradas explícitamente?
- [ ] ¿La configuración está fuera del código?
- [ ] ¿Los servicios externos se conectan por configuración?
- [ ] ¿Build, release y run están separados?
- [ ] ¿La app evita guardar estado local crítico?
- [ ] ¿Expone su servicio por puerto?
- [ ] ¿Puede escalar agregando procesos o instancias?
- [ ] ¿Arranca y se apaga correctamente?
- [ ] ¿Desarrollo y producción son parecidos?
- [ ] ¿Los logs salen como flujo de eventos?
- [ ] ¿Las tareas administrativas son reproducibles?

## Pendiente para versión literal

Para convertir este documento en una transcripción o resumen fiel del video, falta obtener una de estas fuentes:

1. transcripción copiada desde YouTube;
2. subtítulos `.srt` o `.vtt`;
3. archivo de audio/video descargado;
4. acceso habilitado a YouTube desde el entorno Pi mediante login de Chrome o `GEMINI_API_KEY`.
