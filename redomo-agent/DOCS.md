# Agente Redomo

Ejecuta las automatizaciones de Redomo desde esta casa.

## Qué resuelve

Sin este complemento, las automatizaciones solo se ejecutan mientras alguien
tiene la app de Redomo abierta. Una automatización de "enciende las luces a las
7" no pasa nada a las 7: pasa cuando alguien abre la app, sean las 9 de la
mañana o las 6 de la tarde.

Con el complemento instalado, las automatizaciones corren aquí, en la casa, de
forma continua. Y como habla con Home Assistant por la red local, **siguen
funcionando aunque se caiga el internet**.

## Configuración

Las credenciales se generan desde el panel de administración de Redomo:
casa → pestaña **CASA** → **Centro de control** → *Generar credenciales del
agente*. Se muestran una sola vez.

| Opción | Qué es |
|---|---|
| `supabase_url` | Ya viene puesta. No se cambia. |
| `supabase_anon_key` | Ya viene puesta. No se cambia. |
| `agent_email` | El correo que muestra el panel al generar las credenciales |
| `agent_password` | La contraseña que muestra el panel |
| `tick_seconds` | Cada cuántos segundos revisa si toca ejecutar algo. 15 está bien. |

No hay que crear ningún token de acceso de Home Assistant: el complemento
recibe del propio Home Assistant la credencial que necesita.

## Comprobar que funciona

En el registro del complemento debe aparecer:

```
[agente] "Agente <nombre de la casa>" en marcha · casa ... · complemento de Home Assistant
[agente] revisando cada 15 s
```

Si dice `token de desarrollo` en vez de `complemento de Home Assistant`, algo
está mal configurado.

Y en la app del cliente, la pantalla de Automatizaciones debe mostrar en verde
*"Las automatizaciones corren desde tu centro de control Redomo"*. Si aparece en
rojo, el agente lleva más de tres minutos sin dar señales de vida.

## Qué permisos tiene

El agente solo puede, y solo sobre la casa a la que está asociado:

- leer sus automatizaciones, escenas, dispositivos y habitaciones
- marcar que una automatización se ejecutó
- escribir en el historial de actividad

No puede ver a las personas de la casa, ni invitar, ni expulsar, ni cambiar
roles, ni modificar una automatización, ni acceder a ninguna otra casa.
