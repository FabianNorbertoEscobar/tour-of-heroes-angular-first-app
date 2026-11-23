# Tour of Heroes

Aplicación de práctica basada en el tutorial **Tour of Heroes** de Angular. Permite explorar un catálogo de héroes y practicar la construcción de una aplicación de una sola página: componentes, navegación, formularios, servicios y comunicación HTTP simulada.

La interfaz está en inglés y los datos se mantienen en memoria: no requiere un servidor propio ni una base de datos, pero **los cambios se pierden al recargar la aplicación**.

## Funcionalidades

- **Dashboard:** muestra cuatro héroes del catálogo y permite acceder a sus detalles. La selección corresponde a las posiciones 2 a 5 de la lista, no a un ranking calculado.
- **Búsqueda por nombre:** filtra héroes desde el dashboard y enlaza cada resultado a su detalle.
- **Catálogo:** lista los héroes y permite agregar y eliminar registros. Los nombres vacíos o compuestos solo por espacios no se agregan.
- **Detalle:** muestra el identificador y el nombre, permite editar este último, guardar y volver a la página anterior.
- **Mensajes:** muestra un registro de operaciones y errores del servicio, con una opción para limpiarlo.

Cada héroe tiene un `id` numérico y un `name`. La API simulada comienza con diez registros y genera un identificador para cada héroe nuevo.

## Stack y conceptos practicados

| Tecnología | Uso en el proyecto |
| --- | --- |
| Angular 8 | Componentes, módulos, plantillas, servicios y enrutamiento. |
| TypeScript | Modelo de datos y lógica de la aplicación. |
| RxJS 6 | Observables para HTTP y búsqueda reactiva. |
| Angular Forms | Edición del nombre con `[(ngModel)]`. |
| Angular HttpClient | Operaciones HTTP sobre `api/heroes`. |
| angular-in-memory-web-api | Intercepta las solicitudes y simula una API con datos en memoria. |
| HTML y CSS | Plantillas, estilos globales y estilos por componente. |

Entre las características de Angular y RxJS utilizadas se encuentran:

- **Componentes y ciclo de vida:** componentes con sus propias plantillas y estilos; `ngOnInit` para cargar datos.
- **Plantillas y binding:** interpolación `{{ }}`, eventos como `(click)` e `(input)`, referencias locales, `*ngFor`, `*ngIf` y pipes como `uppercase` y `async`.
- **Inyección de dependencias:** `HeroService` centraliza el acceso a datos y `MessageService` comparte el registro de mensajes entre componentes.
- **Router:** `routerLink`, `router-outlet`, redirecciones y lectura del parámetro `id` mediante `ActivatedRoute`.
- **Programación reactiva:** la búsqueda usa un `Subject`, `debounceTime(300)`, `distinctUntilChanged` y `switchMap` para procesar los términos y cambiar a la búsqueda más reciente. El servicio también utiliza operadores como `tap` y `catchError`.

## Navegación

| Ruta | Pantalla |
| --- | --- |
| `/` | Redirige a `/dashboard`. |
| `/dashboard` | Héroes destacados y búsqueda. |
| `/heroes` | Listado, alta y eliminación. |
| `/detail/:id` | Detalle y edición de un héroe. |

## Datos y funcionamiento

`HeroService` realiza solicitudes `GET`, `POST`, `PUT` y `DELETE` a `api/heroes`. `HttpClientInMemoryWebApiModule`, configurado en `AppModule`, las intercepta y utiliza los datos iniciales de `InMemoryDataService`. Por eso se practica el flujo de una API HTTP sin conectarse a un backend real.

Los mensajes de operaciones y errores se almacenan en `MessageService`; los errores también se escriben en la consola. El manejo actual devuelve resultados alternativos para permitir que la aplicación continúe, por lo que es una implementación didáctica y no una estrategia completa de manejo de errores para producción.

## Ejecutar el proyecto

El repositorio incluye enlaces a StackBlitz:

- [Editar en StackBlitz](https://stackblitz.com/edit/angular-tour-of-heroes-fabi)
- [Abrir la vista previa](https://angular-tour-of-heroes-fabi.stackblitz.io)

### Estado de la ejecución local

Esta copia **no está lista para instalarse y ejecutarse localmente sin ajustes**:

- Las dependencias principales declaran Angular `8.2.14`, mientras que Angular CLI y el compilador de desarrollo están en la serie `7`; estas versiones deben alinearse junto con TypeScript y las demás dependencias compatibles.
- `angular.json` referencia archivos y directorios que no están en el repositorio, entre ellos `tsconfig.app.json`, `src/favicon.ico` y `src/assets`. Las configuraciones de pruebas, lint y e2e también referencian archivos ausentes.
- No hay archivo de bloqueo de dependencias ni una versión de Node.js fijada.

Para recuperar el flujo local, primero hay que completar la configuración faltante y alinear las versiones. Una vez resuelto, los scripts declarados en `package.json` se pueden invocar con:

```bash
npm install
npm start       # servidor de desarrollo de Angular
npm run build   # compilación; salida configurada en dist/
```

También se declaran `npm test`, `npm run lint` y `npm run e2e`, pero sus archivos de configuración y pruebas no están incluidos en esta copia. No se debe asumir que esos comandos funcionan sin completar el proyecto.

## Estructura principal

```text
src/
├── app/
│   ├── dashboard/           # portada y héroes destacados
│   ├── hero-detail/         # detalle y edición
│   ├── hero-search/         # búsqueda reactiva
│   ├── heroes/              # listado, alta y eliminación
│   ├── messages/            # visualización de mensajes
│   ├── app-routing.module.ts
│   ├── app.module.ts
│   ├── hero.ts              # modelo Hero
│   ├── hero.service.ts      # acceso HTTP a héroes
│   ├── in-memory-data.service.ts
│   └── message.service.ts
├── environments/            # configuración de entorno
├── index.html
├── main.ts                  # arranque de Angular
└── styles.css               # estilos globales
```

`mock-heroes.ts` contiene una lista estática de ejemplo, pero los datos que usa la aplicación configurada provienen de `InMemoryDataService`.

## Referencias

- [Tutorial Tour of Heroes de Angular](https://angular.io/tutorial)
- [Documentación de RxJS](https://rxjs.dev/)
- Los archivos de código incluyen avisos de copyright de Google y una referencia a la [licencia de Angular](http://angular.io/license).
