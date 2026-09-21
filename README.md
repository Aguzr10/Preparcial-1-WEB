# Preparcial – Internacionalización (I18N) con Next.js 16

Este proyecto implementa todos los requerimientos funcionales y técnicos solicitados para el preparcial de Desarrollo Web (Universidad de los Andes).

---

## 🎯 Objetivos Cumplidos

1. **Enrutamiento dinámico por prefijo de idioma**:
   - Soporte para `/es` y `/en` en todas las rutas mediante la convención `app/[lang]/`.
2. **Detección de idioma mediante Proxy**:
   - Implementado en `proxy.ts` siguiendo la convención de Next.js 16.
   - Detecta automáticamente el idioma preferido del navegador usando la cabecera `Accept-Language` con `@formatjs/intl-localematcher` y `negotiator`.
3. **Gestión de diccionarios de contenido (JSON)**:
   - Archivos `dictionaries/es.json` y `dictionaries/en.json`.
   - Carga asíncrona en Server Components con `getDictionary(lang)`.
   - Llaves obligatorias implementadas: `welcome` ("Bienvenido" / "Welcome") y `profile` ("Perfil" / "Profile").
4. **Persistencia de preferencia de idioma**:
   - Selector interactivo en el cliente (`components/LanguageSwitcher.tsx`).
   - Al cambiar de idioma, se guarda la cookie `NEXT_LOCALE`.
   - El proxy lee primero la cookie para mantener el idioma seleccionado incluso al ingresar directamente a la raíz `/`.
5. **Validaciones obligatorias**:
   - Atributo `lang` dinámico en `<html lang={lang}>` dentro de `app/[lang]/layout.tsx`.
   - **0% texto quemado**: Todos los textos de la interfaz provienen de los diccionarios.
6. **Ejemplo pedagógico de API Route para el examen**:
   - Ubicado en `app/api/items/route.ts` con explicaciones detalladas para repasar antes del parcial (lectura de query params, métodos GET/POST, y cómo consumir APIs externas).

---

## 📁 Estructura del Proyecto

```text
├── app/
│   ├── [lang]/
│   │   ├── layout.tsx         # Root layout con <html lang={lang}> dinámico y Navbar
│   │   ├── page.tsx           # Página principal (Home) con llave 'welcome'
│   │   └── profile/
│   │       └── page.tsx       # Página de perfil con llave 'profile'
│   ├── api/
│   │   └── items/
│   │       └── route.ts       # Route Handler didáctico para el parcial
│   └── globals.css            # Estilos globales limpios y modernos
├── components/
│   └── LanguageSwitcher.tsx   # Componente para cambiar idioma y persistir en cookies
├── dictionaries/
│   ├── es.json                # Diccionario en español
│   └── en.json                # Diccionario en inglés
├── lib/
│   └── dictionaries.ts        # Función asíncrona getDictionary con server-only
├── proxy.ts                   # Proxy de Next.js 16 para detección y redirección
└── preparcial_web.pdf         # Enunciado (ignorado en git vía .gitignore)
```

---

## 🚀 Cómo Ejecutar el Proyecto

1. Instalar dependencias (si no están instaladas):
   ```bash
   npm install
   ```

2. Iniciar el servidor de desarrollo:
   ```bash
   npm run dev
   ```

3. Abrir en el navegador:
   - Ingresa a [http://localhost:3000](http://localhost:3000)
   - El Proxy te redirigirá automáticamente a `/es` o `/en` según las preferencias de tu navegador o tu cookie guardada.

---

## 🧪 Pruebas Rápidas de los Requerimientos

- **Redirección automática**: Entra a `http://localhost:3000` y observa cómo el Proxy te redirige a `/es`.
- **Cambio de idioma y persistencia**: Haz clic en el botón `🇺🇸 EN` en la barra superior. Verás que la URL cambia a `/en` y los textos cambian a inglés. Si refrescas la página o vuelves a ingresar a `http://localhost:3000`, recordará tu selección mediante la cookie `NEXT_LOCALE`.
- **Ruta secundaria de perfil**: Navega a `/es/profile` o `/en/profile` usando el enlace en el menú.
- **Atributo lang dinámico**: Abre las herramientas de desarrollo (F12) e inspecciona el elemento `<html>`. Verás `<html lang="es">` en español y `<html lang="en">` en inglés.
- **API para el examen**: Abre [http://localhost:3000/api/items](http://localhost:3000/api/items) para ver la respuesta JSON del Route Handler.
