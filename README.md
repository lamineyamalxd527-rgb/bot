# Bot de Discord de Osint.es

Bot de Discord.js que publica una bienvenida con tarjeta azul y botones dentro,
y gestiona tickets privados para Osint.es.

El panel de tickets tiene las opciones Reports, Apelaciones, Donaciones, Soporte
y Streamer. Permite un ticket abierto por persona, muestra prioridad a quien
tenga el rol VIP configurado y envía la transcripción por mensaje directo al
cerrar. Tanto la bienvenida como el panel de ayuda usan tarjetas Components V2:
el banner y los botones Normativas/Tickets quedan agrupados dentro de la tarjeta
azul. Al elegir Soporte, el usuario debe completar los dos campos del formulario
con al menos 10 caracteres cada uno; las respuestas se agregan a la tarjeta azul
del ticket. Cada ticket muestra su tipo, quién lo abrió, el estado, el banner y
los botones Reclamar y Cerrar dentro de la misma tarjeta. Reclamar está limitado
a los roles enumerados en `TICKET_ACTION_ROLE_IDS`; esos roles también reciben
acceso a los canales privados de tickets. Solo ellos pueden reclamar o cerrar
un ticket. Cada tipo de ticket tiene una categoría propia creada automáticamente
(`tickets-soporte`, `tickets-reports`, etc.); sus canales usan el formato
`soporte-nombre`, `reports-nombre` y equivalente. Cualquier miembro puede
abrirlo desde el panel.

El comando `/postulaciones` publica la tarjeta de staff con acento azul y el botón
Postularme. El formulario tiene cinco campos obligatorios y envía las respuestas
a `APPLICATION_REVIEW_CHANNEL_ID`, que debe ser un canal privado no visible para
@everyone. El banner recortado de la imagen de referencia se carga desde
`assets/application-banner.png`. En el canal de revisión, quienes tengan alguno
de los roles de `TICKET_ACTION_ROLE_IDS` pueden aceptar o rechazar cada solicitud. La tarjeta muestra el
nombre, el ID y el avatar del postulante junto a sus respuestas; la decisión se
anuncia en `APPLICATION_DECISIONS_CHANNEL_ID` y se envía por mensaje privado al
postulante; los botones quedan desactivados.

El comando `/facciones` publica en el canal actual el panel azul de facciones
con el banner `assets/factions-banner.png`. Los botones PSG, PFA y Mafias usan
por ahora `https://discord.gg/` como enlace provisional; reemplazalos cuando
estén disponibles las invitaciones definitivas.

## Preparación

1. Instala Node.js.
2. Copia `.env.example` a `.env`.
3. Completa `DISCORD_TOKEN`, `RULES_CHANNEL_ID`, `APPLICATION_PANEL_CHANNEL_ID` y `APPLICATION_REVIEW_CHANNEL_ID`. El canal de revisión debe ser privado. `TICKET_ACTION_ROLE_IDS` contiene los roles que pueden reclamar/cerrar tickets y revisar postulaciones.
4. `VIP_ROLE_ID` es opcional; si se configura, el bot indica prioridad a quienes tengan ese rol.
5. En el [Discord Developer Portal](https://discord.com/developers/applications), activa **Server Members Intent** para el bot.
6. Invita el bot con permisos para gestionar canales, gestionar comandos, ver canales y enviar mensajes, embeds y archivos.
7. Ejecuta `npm install` y luego `npm start`.
8. Usa `/ticketpanel` para publicar el centro de ayuda en el canal indicado por `TICKETS_CHANNEL_ID`.

No compartas el token del bot. El archivo `.env` está excluido de Git.

El panel de tickets usa Components V2 para agrupar banner, texto y botones en
una misma tarjeta visual. Discord no permite botones dentro de un embed clásico.
# bot
