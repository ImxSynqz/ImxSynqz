Buenas, soy Ibai / ImxSynqz — Dev de Minecraft (Spigot / Paper)
Tengo 16 años, llevo más de 3 programando en Java y me centro exclusivamente en el desarrollo y la optimización de servidores de FullPvP y BoxPvP. No vengo a venderte humo corporativo ni configs de plugins públicos; sé picar código, optimizar eventos pesados y solucionar los exploits reales que rompen la economía de estas modalidades.

🛠️ Stack Técnico Real

APIs: Paper API, Purpur, Velocity (para redes multiserver).
Bases de Datos: MongoDB (con AdvancedMorphia o drivers asíncronos) y Redis para mensajería entre salas/bungee y almacenamiento en caché.
Herramientas: Gradle, Git, NMS (Net.Minecraft.Server) cuando la API de Paper se queda corta para paquetes visuales o payloads customizados.

📁 Proyectos Propios y Sistemas Reales
1. SynqzMines (Sistema de Minas Asíncronas para BoxPvP)
El problema de las minas públicas (como FastAsyncWorldEdit o MineResetLite mal configurados) es que cuando resetean una mina grande de 50x50, el hilo principal se congela y da un tirón de TPS.

Mi solución: Desarrollé un plugin propio que maneja la regeneración por bloques en lotes (batches) usando tareas asíncronas de la API de Paper, calculando los materiales en un hilo secundario.
Cero Lag Visual: Los bloques se envían directamente al jugador mediante paquetes de red (PacketPlayOutBlockChange), evitando sobrecargar el servidor con eventos BlockPlaceEvent innecesarios por cada bloque regenerado.
El plugin cuenta con un sistema interno de antipretextos para evitar que los jugadores se queden bugeados dentro de los bloques de la mina al resetearse.

2. SynqzCombat (FullPvP Combat Engine + Redis Sync)
Un core de combate diseñado para soportar más de 150 usuarios en una misma arena pegándose a la vez sin retraso en el registro de golpes.

Optimización de Eventos: El plugin intercepta el EntityDamageByEntityEvent y filtra las comprobaciones pesadas de rangos, regiones de WorldGuard y tags de combate en microsegundos, usando mapas de memoria (ConcurrentHashMap) en lugar de consultas directas a base de datos.
Sincronización con Redis: Las estadísticas de Kills, Deaths y Killstreaks se guardan en una caché local. Cada 5 minutos (o cuando el jugador se desconecta), los datos se envían a MongoDB de forma totalmente asíncrona. Si una sala de PvP se cae por un crash, ningún jugador pierde sus datos ni sus ítems de inventario.
Combat Log a prueba de fallos: Rompe el truco de tirar de la conexión (alt+f4) o usar comandos ilegales durante el combate. Si el jugador se desconecta taggeado, el plugin procesa su muerte de forma segura en el hilo del servidor y dropea su inventario (PlayerInventory) intacto en el suelo.

3. VirtualMerchants (Fix Definitivo a Dupeos de BoxPvP)
Los aldeanos físicos (Villagers vanilla) en la 1.20+ son una fuente constante de bugs de duplicación de ítems causados por desincronizaciones de chunks, embudos (hoppers) o crasheos intencionados del servidor.

Mi solución: Un sistema donde los aldeanos son simples entidades visuales (Paquetes de EntitySpawn). Al hacerles click derecho, se abre una GUI customizada gestionada al 100% por el plugin.
Seguridad: El intercambio de ítems no usa la mecánica nativa de Minecraft. El plugin valida los materiales del inventario del jugador, remueve los materiales exactos y añade el ítem final en un solo tic de servidor, usando transacciones seguras. Es imposible duplicar ítems mediante cierres de inventario forzados.

⚡ Solución de Problemas y Optimización de Servidores

Perfiles de Rendimiento (Spark/Timings): Sé leer e interpretar reportes de Spark para localizar qué plugin o qué evento específico está causando lag spikes en tu red.
Limpieza de Tareas: Sustituyo bucles repetitivos pesados (BukkitRunnable de un segundo) por un sistema basado en eventos puros.
Parcheo de Exploits: Bloqueo de exploits comunes en BoxPvP como el phaseo con bloques de comandos visuales, bugs de empuje con shulkers o caídas provocadas por spam de paquetes ilegales (Book Crasher, Custom Payloads).

¿Hablamos?
Si tu servidor va a tirones, necesitas un sistema único para diferenciarte de la competencia o quieres automatizar tu modalidad, escríbeme:

Discord: xxxx_010_

GitHub: :https://github.com/ImxSynqz/ImxSynqz/edit/main/README.md



