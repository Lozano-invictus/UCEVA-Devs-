# Presupuestador de obra · UCEVA Devs

Sistema web para armar el presupuesto de un trabajo de obra: se eligen
insumos de un catálogo, se indican cantidades y el sistema calcula cuánto
cuesta, cuánto hay que cobrar y a partir de qué volumen el trabajo deja de
perder dinero.

Reemplaza la hoja de cálculo copiada de un trabajo a otro. Cada presupuesto
conserva los precios del día en que se armó y deja rastro de quién lo creó y
quién lo aprobó.

## Qué hace
- Catálogo de insumos con unidad de medida y precio unitario
- Presupuestos por capítulos e ítems, con costo directo
- AIU discriminado, precio de venta y los dos márgenes (sobre costo y sobre venta)
- Punto de equilibrio y comparación de dos escenarios de precios
- Evaluación financiera: VPN, TIR y amortización
- Exportación a CSV, versiones y análisis de sensibilidad

## Arquitectura
| Capa | Tecnología |
|---|---|
| Frontend | Angular (standalone + signals) |
| Backend | Spring Boot: `insumo-service`, `presupuesto-service`, `calculo-service` |
| Cálculo financiero | `libfinanzas.so` en C, invocada desde Java con JNA |
| Identidad | Keycloak (OAuth 2.0 / OIDC, Authorization Code + PKCE) |
| Despliegue | Docker + Kubernetes / Docker Swarm |

El requisito de calidad central es el **peso exacto**: el total debe
coincidir con una hoja de control, sin una diferencia de un peso.

## Roles
- **Presupuestador:** crea y edita presupuestos, mantiene el catálogo.
- **Revisor:** consulta y aprueba presupuestos.

## Equipo
Andrés Felipe Vargas Ceballos · Esteban Lozano Jaramillo · Juan David
González Ospina · Diego Alejandro Laverde Restrepo · Luis Alejandro Pino
Bellorín

Proyecto de **Programación en Ambiente Web 2** · UCEVA
