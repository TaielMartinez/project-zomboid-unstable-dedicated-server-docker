# project-zomboid-unstable-dedicated-server-docker
Tutorial de como crear un servidor dedicado con docker para el Project Zomboid version Unstable con login de steam. Esta preconfigurado para usar la version unestable que salio hoy

# Comandos para ejecutar en un VPS

Clona el repositorio
`git clone https://github.com/TaielMartinez/project-zomboid-unstable-dedicated-server-docker`

Copia las configuraciones
`cp .env.example .env`

Edita las contraseñas
`nano .env`
Control + X para cerrar el editor

Ejecuta el servidor
`docker compose up -d`

Ver los logs del server
`docker logs projectzomboid -f`

# Docker compose
```yml
services:
  projectzomboid:
    image: indifferentbroccoli/projectzomboid-server-docker
    restart: unless-stopped
    container_name: projectzomboid
    stop_grace_period: 30s
    ports:
      - 16261:16261/udp
      - 16262:16262/udp
      - 27015:27015/tcp
    environment:
      GENERATE_SETTINGS: true
    env_file:
      - .env
    volumes:
      - ./projectzomboid/server-files:/project-zomboid
      - ./projectzomboid/server-data:/project-zomboid-config
```

# Configuraciones
| Variable | Default | Comentario (ES) |
|--------|---------|-----------------|
| PVP | true | Los jugadores pueden herir y matar a otros jugadores |
| PAUSE_EMPTY | true | El tiempo del juego se detiene cuando no hay jugadores conectados |
| GLOBAL_CHAT | true | Activa o desactiva el chat global |
| CHAT_STREAMS | s,r,a,w,y,sh,f,all | Canales de chat habilitados |
| OPEN | true | Permite que los clientes se unan sin estar previamente en la whitelist |
| SERVER_WELCOME_MESSAGE | Welcome to your Indifferent Broccoli Project Zomboid Docker server | Primer mensaje de bienvenida visible en el chat |
| AUTO_CREATE_USER_IN_WHITE_LIST | false | Agrega automáticamente usuarios desconocidos a la whitelist |
| DISPLAY_USER_NAME | true | Muestra el nombre de usuario sobre la cabeza del jugador |
| SHOW_FIRST_AND_LAST_NAME | false | Muestra nombre y apellido sobre la cabeza del jugador |
| SPAWN_POINT | 0,0,0 | Fuerza el punto de aparición inicial de nuevos jugadores |
| SAFETY_SYSTEM | true | Permite activar o desactivar PVP por jugador |
| SHOW_SAFETY | true | Muestra un icono de calavera sobre jugadores en modo PVP |
| SAFETY_TOGGLE_TIMER | 2 | Tiempo para entrar o salir del modo PVP |
| SAFETY_COOLDOWN_TIMER | 3 | Tiempo de espera antes de volver a cambiar el estado PVP |
| SPAWN_ITEMS |  | Objetos con los que aparecen los nuevos jugadores |
| DEFAULT_PORT | 16261 | Puerto principal del servidor |
| UDP_PORT | 16262 | Puerto UDP del servidor |
| RESET_ID | 563979383 | Identificador de reinicio del servidor |
| MODS |  | IDs de mods a cargar |
| MAP |  | Nombre de la carpeta del mapa |
| DO_LUA_CHECKSUM | true | Expulsa clientes con archivos modificados |
| DENY_LOGIN_ON_OVERLOADED_SERVER | false | Niega el ingreso si el servidor está sobrecargado |
| PUBLIC | true | Hace visible el servidor en el navegador del juego |
| PUBLIC_NAME | Indifferent Broccoli Project Zomboid Docker Server | Nombre público del servidor |
| SERVER_NAME | pzserver | Nombre interno del servidor |
| PUBLIC_DESCRIPTION | Welcome to your Indifferent Broccoli Project Zomboid Docker server | Descripción pública del servidor |
| MAX_PLAYERS | 32 | Máximo de jugadores simultáneos |
| PING_LIMIT | 400 | Ping máximo permitido antes de expulsar |
| HOURS_FOR_LOOT_RESPAWN | 0 | Horas para que reaparezca el loot |
| MAX_ITEMS_FOR_LOOT_RESPAWN | 4 | Máximo de ítems para que un contenedor regenere loot |
| CONSTRUCTION_PREVENTS_LOOT_RESPAWN | false | Evita respawn de loot en construcciones de jugadores |
| DROP_OFF_WHITE_LIST_AFTER_DEATH | false | Elimina al jugador de la whitelist al morir |
| NO_FIRE | false | Desactiva todo tipo de fuego excepto fogatas |
| ANNOUNCE_DEATH | false | Anuncia las muertes en el chat global |
| MINUTES_PER_PAGE | 1.0 | Minutos del juego para leer una página |
| SAVE_WORLD_EVERY_MINUTES | 0 | Intervalo de guardado automático del mapa |
| PLAYER_SAFEHOUSE | false | Jugadores pueden reclamar casas seguras |
| ADMIN_SAFEHOUSE | false | Solo administradores pueden reclamar casas seguras |
| SAFEHOUSE_ALLOW_TRESPASS | true | Permite entrar a casas seguras sin invitación |
| SAFEHOUSE_ALLOW_FIRE | true | Permite daño por fuego en casas seguras |
| SAFEHOUSE_ALLOW_LOOT | true | Permite robar objetos en casas seguras |
| SAFEHOUSE_ALLOW_RESPAWN | false | Permite respawn en la casa segura |
| SAFEHOUSE_DAY_SURVIVED_TO_CLAIM | 0 | Días sobrevividos requeridos para reclamar casa |
| SAFEHOUSE_REMOVAL_TIME | 144 | Horas sin visitar antes de perder la casa segura |
| SAFEHOUSE_ALLOW_NON_RESIDENTIAL | false | Permite reclamar edificios no residenciales |
| ALLOW_DESTRUCTION_BY_SLEDGEHAMMER | true | Permite destruir objetos con maza |
| SLEDGEHAMMER_ONLY_IN_SAFEHOUSE | false | Permite destruir solo dentro de casas seguras |
| KICK_FAST_PLAYERS | false | Expulsa jugadores que se mueven demasiado rápido |
| SERVER_PLAYER_ID | 88635698 | Identificador del servidor |
| RCON_PORT | 27015 | Puerto de la consola remota |
| DISCORD_ENABLE | false | Habilita integración del chat con Discord |
| DISCORD_TOKEN |  | Token del bot de Discord |
| DISCORD_CHANNEL |  | Nombre del canal de Discord |
| DISCORD_CHANNEL_ID |  | ID del canal de Discord |
| MAX_ACCOUNTS_PER_USER | 0 | Máximo de cuentas por usuario de Steam |
| ALLOW_COOP | true | Permite modo cooperativo o pantalla dividida |
| SLEEP_ALLOWED | false | Permite dormir sin ser obligatorio |
| SLEEP_NEEDED | false | Hace obligatorio dormir |
| KNOCKED_DOWN_ALLOWED | true | Permite derribar jugadores |
| SNEAK_MODE_HIDE_FROM_OTHER_PLAYERS | true | Oculta jugadores al usar sigilo |
| WORKSHOP_ITEMS |  | IDs de mods del Workshop |
| STEAM_SCOREBOARD | true | Muestra nombres y avatares de Steam |
| STEAM_VAC | true | Activa el sistema VAC de Steam |
| UPNP | true | Configura automáticamente el reenvío de puertos |
| VOICE_ENABLE | true | Habilita chat de voz |
| VOICE_MIN_DISTANCE | 10.0 | Distancia mínima para escuchar voz |
| VOICE_MAX_DISTANCE | 100.0 | Distancia máxima para escuchar voz |
| VOICE_3D | true | Habilita audio direccional |
| SPEED_LIMIT | 70.0 | Límite de velocidad permitido |
| LOGIN_QUEUE_ENABLED | false | Habilita cola de conexión |
| LOGIN_QUEUE_CONNECT_TIMEOUT | 60 | Tiempo máximo de espera en la cola |
| SERVER_BROWSER_ANNOUNCED_IP |  | IP anunciada al navegador del servidor |
| PLAYER_RESPAWN_WITH_SELF | false | Respawn en el punto donde murió |
| PLAYER_RESPAWN_WITH_OTHER | false | Respawn junto a otro jugador |
| FAST_FORWARD_MULTIPLIER | 40.0 | Velocidad del tiempo al dormir |
| DISABLE_SAFEHOUSE_WHEN_PLAYER_CONNECTED | false | Desactiva casas seguras si un miembro está conectado |
| FACTION | true | Permite crear facciones |
| FACTION_DAY_SURVIVED_TO_CREATE | 0 | Días requeridos para crear una facción |
| FACTION_PLAYERS_REQUIRED_FOR_TAG | 1 | Jugadores necesarios para crear etiqueta |
| DISABLE_RADIO_STAFF | false | Desactiva radio para staff |
| DISABLE_RADIO_ADMIN | true | Desactiva radio para administradores |
| DISABLE_RADIO_GM | true | Desactiva radio para game masters |
| DISABLE_RADIO_OVERSEER | false | Desactiva radio para overseers |
| DISABLE_RADIO_MODERATOR | false | Desactiva radio para moderadores |
| DISABLE_RADIO_INVISIBLE | true | Desactiva radio para jugadores invisibles |
| CLIENT_COMMAND_FILTER | -vehicle.*;+vehicle.damageWindow;+vehicle.fixPart;+vehicle.installPart;+vehicle.uninstallPart | Comandos no registrados en el log |
| CLIENT_ACTION_LOGS | ISEnterVehicle;ISExitVehicle;ISTakeEngineParts; | Acciones registradas en el log |
| PERK_LOGS | true | Registra cambios de habilidades |
| ITEM_NUMBERS_LIMIT_PER_CONTAINER | 0 | Límite de ítems por contenedor |
| BLOOD_SPLAT_LIFESPAN_DAYS | 0 | Días antes de eliminar manchas de sangre |
| ALLOW_NON_ASCII_USERNAME | false | Permite caracteres no ASCII en nombres |
| BAN_KICK_GLOBAL_SOUND | true | Sonido global al expulsar o banear |
| REMOVE_PLAYER_CORPSES_ON_CORPSE_REMOVAL | false | Elimina cadáveres de jugadores automáticamente |
| TRASH_DELETE_ALL | false | Permite borrar todo desde contenedores |
| PVP_MELEE_WHILE_HIT_REACTION | false | Permite golpear mientras se recibe daño |
| MOUSE_OVER_TO_SEE_DISPLAY_NAME | true | Requiere pasar el mouse para ver el nombre |
| HIDE_PLAYERS_BEHIND_YOU | true | Oculta jugadores fuera del campo visual |
| PVP_MELEE_DAMAGE_MODIFIER | 30.0 | Multiplicador de daño cuerpo a cuerpo PVP |
| PVP_FIREARM_DAMAGE_MODIFIER | 50.0 | Multiplicador de daño a distancia PVP |
| CAR_ENGINE_ATTRACTION_MODIFIER | 0.5 | Modificador de atracción de zombis a autos |
| PLAYER_BUMP_PLAYER | false | Permite empujar jugadores al correr |
| MAP_REMOTE_PLAYER_VISIBILITY | 1 | Visibilidad de jugadores en el mapa |
| BACKUPS_COUNT | 5 | Cantidad de backups |
| BACKUPS_ON_START | true | Backup al iniciar el servidor |
| BACKUPS_ON_VERSION_CHANGE | true | Backup al cambiar versión |
| BACKUPS_PERIOD | 0 | Intervalo de backups |
| ANTI_CHEAT_PROTECTION_TYPE1 | true | Protección anticheat tipo 1 |
| ANTI_CHEAT_PROTECTION_TYPE2 | true | Protección anticheat tipo 2 |
| ANTI_CHEAT_PROTECTION_TYPE3 | true | Protección anticheat tipo 3 |
| ANTI_CHEAT_PROTECTION_TYPE4 | true | Protección anticheat tipo 4 |
| ANTI_CHEAT_PROTECTION_TYPE5 | true | Protección anticheat tipo 5 |
| ANTI_CHEAT_PROTECTION_TYPE6 | true | Protección anticheat tipo 6 |
| ANTI_CHEAT_PROTECTION_TYPE7 | true | Protección anticheat tipo 7 |
| ANTI_CHEAT_PROTECTION_TYPE8 | true | Protección anticheat tipo 8 |
| ANTI_CHEAT_PROTECTION_TYPE9 | true | Protección anticheat tipo 9 |
| ANTI_CHEAT_PROTECTION_TYPE10 | true | Protección anticheat tipo 10 |
| ANTI_CHEAT_PROTECTION_TYPE11 | true | Protección anticheat tipo 11 |
| ANTI_CHEAT_PROTECTION_TYPE12 | true | Protección anticheat tipo 12 |
| ANTI_CHEAT_PROTECTION_TYPE13 | true | Protección anticheat tipo 13 |
| ANTI_CHEAT_PROTECTION_TYPE14 | true | Protección anticheat tipo 14 |
| ANTI_CHEAT_PROTECTION_TYPE15 | true | Protección anticheat tipo 15 |
| ANTI_CHEAT_PROTECTION_TYPE16 | true | Protección anticheat tipo 16 |
| ANTI_CHEAT_PROTECTION_TYPE17 | true | Protección anticheat tipo 17 |
| ANTI_CHEAT_PROTECTION_TYPE18 | true | Protección anticheat tipo 18 |
| ANTI_CHEAT_PROTECTION_TYPE19 | true | Protección anticheat tipo 19 |
| ANTI_CHEAT_PROTECTION_TYPE20 | true | Protección anticheat tipo 20 |
| ANTI_CHEAT_PROTECTION_TYPE21 | true | Protección anticheat tipo 21 |
| ANTI_CHEAT_PROTECTION_TYPE22 | true | Protección anticheat tipo 22 |
| ANTI_CHEAT_PROTECTION_TYPE23 | true | Protección anticheat tipo 23 |
| ANTI_CHEAT_PROTECTION_TYPE24 | true | Protección anticheat tipo 24 |
| ANTI_CHEAT_PROTECTION_TYPE2_THRESHOLD_MULTIPLIER | 3.0 | Multiplicador de umbral anticheat tipo 2 |
| ANTI_CHEAT_PROTECTION_TYPE3_THRESHOLD_MULTIPLIER | 1.0 | Multiplicador de umbral anticheat tipo 3 |
| ANTI_CHEAT_PROTECTION_TYPE4_THRESHOLD_MULTIPLIER | 1.0 | Multiplicador de umbral anticheat tipo 4 |
| ANTI_CHEAT_PROTECTION_TYPE9_THRESHOLD_MULTIPLIER | 1.0 | Multiplicador de umbral anticheat tipo 9 |
| ANTI_CHEAT_PROTECTION_TYPE15_THRESHOLD_MULTIPLIER | 1.0 | Multiplicador de umbral anticheat tipo 15 |
| ANTI_CHEAT_PROTECTION_TYPE20_THRESHOLD_MULTIPLIER | 1.0 | Multiplicador de umbral anticheat tipo 20 |
| ANTI_CHEAT_PROTECTION_TYPE22_THRESHOLD_MULTIPLIER | 1.0 | Multiplicador de umbral anticheat tipo 22 |
| ANTI_CHEAT_PROTECTION_TYPE24_THRESHOLD_MULTIPLIER | 6.0 | Multiplicador de umbral anticheat tipo 24 |


El tutorial se basa en este contenedor docker https://github.com/indifferentbroccoli/projectzomboid-server-docker
