# Espaces réservés ChunkBlock

ChunkBlock enregistre les espaces réservés du bloc magique hérités du moteur AOneBlock, tous préfixés `chunkblock_`, plus cinq espaces réservés de territoire des siens.

!!! tip "Les cinq que vous voulez probablement sur votre tableau de bord"
    - `%chunkblock_island_chunks%` — chunks possédés
    - `%chunkblock_island_max_chunks%` — le plafond
    - `%chunkblock_island_chunk_credit%` — niveaux disponibles à dépenser maintenant
    - `%chunkblock_island_next_chunk_level%` — le niveau d'île qui achète le prochain chunk
    - `%chunkblock_island_ring%` — à quelle distance le territoire s'étend du centre

    `credit` et `chunks` ensemble sont la progression entière en un coup d'œil : *« 9 chunks, 3 à dépenser. »*

Les espaces réservés qui lisent l'île propre d'un **joueur** se résolvent à l'île qu'il possède, même s'il se tient sur l'île de quelqu'un d'autre. Les variantes `visited_island_*` lisent l'île sur laquelle le joueur se trouve actuellement.

{{ placeholders_bundle(gamemode_name="chunkblock") }}
