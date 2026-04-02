# Introduction

Veuillez lire la page [Placeholders](../../../BentoBox/Placeholders).

# Placeholders

## Placeholders génériques

Ces placeholders sont disponibles dans tous les modes de jeu actuellement disponibles ([BSkyBlock](../../../gamemodes/BSkyBlock/Placeholders), [AcidIsland](../../../gamemodes/AcidIsland/Placeholders), [CaveBlock](../../../gamemodes/CaveBlock/Placeholders), [SkyGrid](../../../gamemodes/SkyGrid/Placeholders), [AOneBlock](../../../gamemodes/AOneBlock/Placeholders)).

**Liste des placeholders disponibles**

| Placeholder | Description | Versions Bank |
|-------------------------------------------------------|--------------------------------------------------------------------------------|-----------|
| `%Bank_[gamemode]_island_balance%` | Solde de l'île du joueur formaté par Vault | 1.1.0 |
| `%Bank_[gamemode]_visited_island_balance%` | Solde de l'île sur laquelle se tient le joueur, formaté par Vault| 1.1.0 |
| `%Bank_[gamemode]_island_balance_number%` | Solde de l'île du joueur - sans formatage. Valeur brute.| 1.4.0 |
| `%Bank_[gamemode]_visited_island_balance_number%` | Solde de l'île sur laquelle se tient le joueur - sans formatage. Valeur brute.| 1.4.0 |
| `%Bank_[gamemode]_island_balance_formatted%` | Solde de l'île du joueur formaté, par exemple 1.5M | 1.1.1 |
| `%Bank_[gamemode]_visited_island_balance_formatted%` | Solde formaté de l'île sur laquelle se tient le joueur. ex: 1.2k | 1.1.0 |
| `%Bank_[gamemode]_top_value_#RANK#%` | Solde de l'île du `#RANK#`-ème île du classement | 1.1.0 |
| `%Bank_[gamemode]_top_name_#RANK#%` | Nom du propriétaire de l'île du `#RANK#`-ème île du classement | 1.1.0 |

*Remarque*: `#RANK#` est un nombre entre 1 et le paramètre `number-of-ranks` du config.yml de Bank.

## Exemples d'utilisation
### Afficher les 10 premiers dans BSkyBlock
1. `%Bank_bskyblock_top_name_1% with island balance: %Bank_bskyblock_top_value_1%`
2. `%Bank_bskyblock_top_name_2% with island balance: %Bank_bskyblock_top_value_2%`
3. `%Bank_bskyblock_top_name_3% with island balance: %Bank_bskyblock_top_value_3%`
4. `%Bank_bskyblock_top_name_4% with island balance: %Bank_bskyblock_top_value_4%`
5. `%Bank_bskyblock_top_name_5% with island balance: %Bank_bskyblock_top_value_5%`
6. `%Bank_bskyblock_top_name_6% with island balance: %Bank_bskyblock_top_value_6%`
7. `%Bank_bskyblock_top_name_7% with island balance: %Bank_bskyblock_top_value_7%`
8. `%Bank_bskyblock_top_name_8% with island balance: %Bank_bskyblock_top_value_8%`
9. `%Bank_bskyblock_top_name_9% with island balance: %Bank_bskyblock_top_value_9%`
10. `%Bank_bskyblock_top_name_10% with island balance: %Bank_bskyblock_top_value_10%`
