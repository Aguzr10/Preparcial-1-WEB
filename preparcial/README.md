# Preparcial Web - Internacionalizacion (i18n)

Proyecto de preparcial para la materia de Desarrollo Web (Universidad de los Andes).
Implementa internacionalizacion con Next.js 16 (App Router), soporte para espanol e ingles, deteccion de idioma por Proxy y persistencia mediante cookies.

## Integrantes
- Alejandro Guzman

## Caracteristicas del proyecto
- Enrutamiento dinamico bajo la estructura `app/[lang]/` para rutas `/es` y `/en`.
- Deteccion de idioma con `proxy.ts` (Next.js 16) usando las cabeceras `Accept-Language` del navegador.
- Persistencia de idioma mediante la cookie `NEXT_LOCALE`.
- Diccionarios en archivos JSON (`es.json` y `en.json`) con las llaves obligatorias `welcome` y `profile`.
- Carga asincrona de diccionarios en Server Components con `server-only`.
- Atributo `lang` dinamico en la etiqueta `html` dentro del root layout.
- Interfaz 100% traducida desde los diccionarios, sin texto quemado.
- Ejemplo de endpoint API (`/api/items`) para repasar el manejo de Route Handlers para el parcial.

## Estructura del repositorio

```text
S7/
├── preparcial_web.pdf          # Enunciado del preparcial
└── preparcial/                 # Aplicacion Next.js
    ├── app/
    │   ├── [lang]/
    │   │   ├── layout.tsx      # Layout con html lang dinamico y barra de navegacion
    │   │   ├── page.tsx        # Pagina principal con llave welcome
    │   │   └── profile/
    │   │       └── page.tsx    # Pagina de perfil con llave profile
    │   ├── api/
    │   │   └── items/
    │   │       └── route.ts    # Ejemplo didactico de API Route
    │   └── globals.css         # Estilos CSS de la aplicacion
    ├── components/
    │   └── LanguageSwitcher.tsx # Selector de idioma y guardado en cookie
    ├── dictionaries/
    │   ├── es.json             # Diccionario en espanol
    │   └── en.json             # Diccionario en ingles
    ├── lib/
    │   └── dictionaries.ts     # Helper para obtener diccionarios
    ├── proxy.ts                # Proxy de Next.js para redireccion y deteccion
    ├── package.json
    └── tsconfig.json
```

## Instrucciones para ejecutar

1. Entrar a la carpeta del proyecto:
   ```bash
   cd preparcial
   ```

2. Instalar dependencias:
   ```bash
   npm install
   ```

3. Iniciar el servidor de desarrollo:
   ```bash
   npm run dev
   ```

4. Abrir en el navegador:
   - http://localhost:3000
   - Redirige automaticamente a `/es` o `/en` segun el navegador o cookie.
