# Calculadora de Propinas y Consumo

Aplicación web para calcular el consumo de un restaurante y la propina sugerida, desarrollada con React, TypeScript y Vite.

**Demo:** https://calculadora-propinas-erickgreco.netlify.app/

## Funcionalidades

- Menú de platillos con su precio.
- Agregar productos a la orden y llevar la cantidad de cada uno.
- Eliminar productos de la orden.
- Selección del porcentaje de propina.
- Cálculo automático del subtotal, la propina y el total a pagar.
- Formato de moneda consistente en toda la interfaz (USD).

## Stack

| Área                 | Tecnología                 |
| -------------------- | -------------------------- |
| UI                   | React                      |
| Lenguaje             | TypeScript                 |
| Bundler / Dev server | Vite                       |
| Estilos              | Tailwind CSS (`index.css`) |
| Despliegue           | Netlify                    |
| Control de versiones | Git + GitHub               |

## Arquitectura

La lógica de la orden está separada de la interfaz: los componentes solo renderizan y el estado vive en un hook personalizado. El formateo de moneda se centraliza en un helper reutilizable.

| Archivo                                | Responsabilidad                                                    |
| -------------------------------------- | ------------------------------------------------------------------ |
| `src/main.tsx`                         | Punto de entrada; monta la aplicación en el DOM                    |
| `src/App.tsx`                          | Componente raíz; consume `useOrder` y distribuye datos y funciones |
| `src/components/MenuItem.tsx`          | Elemento del menú; permite agregarlo a la orden                    |
| `src/components/OrderContents.tsx`     | Lista de productos de la orden actual                              |
| `src/components/TipPercentageForm.tsx` | Formulario para elegir el porcentaje de propina                    |
| `src/components/OrderTotals.tsx`       | Subtotal, propina y total a pagar                                  |
| `src/hooks/useOrder.ts`                | Hook personalizado con el estado y las operaciones de la orden     |
| `src/data/db.ts`                       | Menú de platillos (datos locales)                                  |
| `src/helpers/index.ts`                 | Funciones auxiliares, como `formatCurrency`                        |
| `src/types/index.ts`                   | Tipos de TypeScript compartidos                                    |
| `src/index.css`                        | Estilos globales                                                   |

### Formato de moneda

`formatCurrency` usa la API nativa `Intl.NumberFormat`, sin dependencias externas:

```typescript
export function formatCurrency(quantity: number) {
	return new Intl.NumberFormat('en-US', {
		style: 'currency',
		currency: 'USD',
	}).format(quantity);
}
```

Para cambiar de moneda o región basta con modificar el locale (`'en-US'`) y el código de moneda (`'USD'`) en un solo lugar.

## Ejecutar en local

Requisitos: Node.js (versión LTS) y npm.

```bash
git clone https://github.com/erickgreco/Calculadora-Propinas.git
cd Calculadora-Propinas
npm install
npm run dev
```

Scripts disponibles:

| Comando           | Descripción                                    |
| ----------------- | ---------------------------------------------- |
| `npm run dev`     | Servidor de desarrollo con recarga en caliente |
| `npm run build`   | Genera el build de producción en `dist/`       |
| `npm run preview` | Sirve localmente el build de producción        |

## Despliegue

El sitio se despliega en Netlify, conectado a este repositorio: cada `push` a `main` dispara un deploy automático.

| Configuración     | Valor           |
| ----------------- | --------------- |
| Build command     | `npm run build` |
| Publish directory | `dist`          |

## Autor

**Erick Gutierrez Sanchez**
GitHub: [@erickgreco](https://github.com/erickgreco)
