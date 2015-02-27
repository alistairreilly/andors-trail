# Combat system #
Combat in Andor's Trail is divided into _turns_. If the player engages in combat, the players starts with his or her turn. If a monster engages combat, the monsters start with their turn.
In the player's turn, the player is initially given an amount of Action Points (AP) to spend as the player sees fit. Actions that use up action points could be attacking, using a potion or moving to an adjacent tile.
The player's turn lasts until the player has no AP left to spend. Then combat proceeds with the monsters' turn. On the monsters' turn, all monsters are also given an initial amount of AP to spend. All monsters that are adjacent to the player attack in sequence until no monsters have any AP left to do any further actions.
The combat revolves this way until either all the monsters have been killed, or the player has been killed.

If all monsters are killed, the player is rewarded with experience and loot. The amount of experince and loot items (including gold) is determined by monster type.

If the player is killed in combat, the player loses 30% of the built up experience of the current level. Note that the percentage is within the current level, so you can never lose so much experience that you decrease in level.

## Base statistics and equipment effects ##
Each actor (player and monster) has a _Base combat statistics_, that determine how proficient the actor is at fighting. This is also called _Unequipped combat statistics_. These statistics are made up of the following components:
  * Attack cost (actions points)
  * Chance to hit (%)
  * Critical chance (%)
  * Critical multiplier
  * Damage potential
  * Block chance (%)
  * Damage resistance

The actor can wear weapons, clothing and items that affect these statistics, thereby creating a _Equipped combat statistics_. Equipped combat statistics is calculated by adding the item's combat statistics to the actor's base combat statistics. The only exceptions to this rule are the following:
  * Attack cost is purely determined by the weapon's attack cost.
  * Critical chance is purely determined by the weapon's critical chance.

## Attack action ##
When using the attack action in combat, the attack is handled in the following way:
  1. Determine the chance of the attacker hitting the target. Call this X. See below for how this is calculated.
  1. Roll a 100-sided dice.
  1. If the dice value is greater than X, the attack is considered a miss and no damage is done.
  1. Otherwise, the attack is considered a hit. Determine damage in the following way
  1. Using the attackers damage potiential, pick a random number in this interval. Call this D.
  1. If the attacker has a chance of doing a critical hit (has critical chance > 0%), roll a 100 sided dice. If the dice value is less than or equal to the critical chance, the attack is considered a critical hit. Multiply D by the attacker's critical multiplier.
  1. Subtract the target's damage resistance from D.
  1. The attack causes D HP to be lost on the target. If the target has 0 or less HP left, the target dies.

## Chance to hit ##
The chance to hit in Andor's Trail v0.6.6 is calculated in the following way:
  1. Determine the attacker's chance to hit. Call this A. (This value might be greaten than 100)
  1. Determine the target's block chance. Call this B.
  1. Calculate C = A - B
  1. Calculate F = 50 ` * ` (1 + (2/pi) ` * ` ATAN( (C - 50) / 40 ) )
    * This function will produce a number between 0 and 100.
    * If C is 50, then F will be 50.
    * If C is high (the attacker's chance to hit is higher than the target's block chance), then F will be near 100.
    * If C is low, then F will be 50.
  1. The chance to hit (in percent) is F.

## Damage ##
Damage is calculated by the attacker's damage potential, which is usually specified in an interval. The attack damage is a random number in that interval. If the target has any damage resistance, the resulting damage is reduced by the target's damage resistance.