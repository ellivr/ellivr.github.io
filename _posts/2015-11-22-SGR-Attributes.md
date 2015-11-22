---
layout: post
title: SGR Attributes
tag: sgr
---
List of attributes:
- **Mind** : Affect mental attack you do to the enemy.

- **Strength** : Affect physical attack you do to the enemy.
- **Vigour** : Affect your maximum Health. 
- **Endurance** : Affect how many stamina you regenerate per tick.
- **Reasoning** : Affect mental defense. Mental defense reduces mental damage you receive from enemy.
- **Resolve** : Affect physical defense. Physical defense reduces physical damage you receive from enemy.
- **Determination** : General purpose defense. Reduces both mental and physical damage.
- **Perception** : Critical Hit Chance of your attacks.
- **Reflex** : Reduces Critical Hit Chance of enemy attacks.
- **Luck** : Affect Critical Hit damage and Escape chance.

### Physical Damage Formula
> Physical Damage = (Skill Power/100) x (3 x Strength - (2 x Enemy's Resolve + 1 x Enemy's Determination)) + Skill Power/4

### Mental Damage Formula
> Mental Damage = (Skill Power/100) x (3 x Mind - (2 x Enemy's Reasoning + 1 x Enemy's Determination)) + Skill Power/4

### Shield Amount Formula 
> Shield Amount = (Skill Power/100) x (2 x Resolve + 1 x Determination)/2

### Heal Amount Formula
> Heal Amount = (Skill Power/100) x (2 x Reasoning + 1 x Determination)/2

### Health Max
> Health Max = 100 + (Vigour x 10)

### Stamina Max
> Constant: 100

### Stamina Regeneration
Stamina regenerate every 3 seconds tick. Every tick, the amount of Stamina regenerated is:
> Stamina Per Tick = ( (Endurance+1)/(10 x Level) ) x 100

Results will be rounded down.

### Skill Cooldown
> Skill Cooldown = 2 + (Skill Power / 10) Seconds

### Skill Power
Skill power (or just power) determine how badass that skill is. Minimum is 1, and Maximum is 100. A 1 Power Skill is like a poke, while 100 Power skill is like a heavy jab. The amount of Stamina required to execute that skill equals with its power. In short, a skill with 100 Power will eat all of your stamina in one shot. 

### Critical Hit Chance
Critical hit chance is the probability of *normal damage* replaced with *critical hit damage*. 
- The bigger the **Perception**, the more chance of crits hitting. 
- The bigger the **Luck**, more severe damage you deal in your crit. 
- The bigger the **Reflex**, the less chance of enemy crits hitting you. 

So
> Critical Hit Chance of Your Attacks = (Your Perception - Enemy's Reflex)%

> Critical Hit Damage of Your Attacks = Normal Damage + Bonus Damage

Where
> Bonus Damage = Normal Damage x Luck/100

### EXP Needed to Level Up

```Csharp
public static int ExpNeedToLevelUp(int currentLevel)
    {
        if (Userid != null)
        {
            if (currentLevel == 0)
            {
                return 2007483647;
            }

            float result;
            result = (((float)currentLevel * (float)currentLevel / 100) + ((float)currentLevel * (float)currentLevel / 20)) * 100;
            return (int)result;
        }
        else { return 2007483647; }
    }
```

Applies to both combat level and crafting level.

# SGR: Crafting

Materials nature:
  - **Paper Scrap** : Mind.
  - **Twig** : Strength.
  - **Metal Scrap** : Vigour. 
  - **Rotten Konjac** : Endurance.
  - **Screw** : Reasoning.
  - **Rubber Band** : Resolve.
  - **Cloth** : Determination.
  - **Chalk** : Perception.
  - **Coin** : Reflex.
  - **Omamori** : Luck.
 
All crafting requres Usable Part(s) based on total attributes it holds. 1 Usable Part requred per 5 attributes, the amount is ceil'd. For example, 
- Crafting +5 Strength Equiment will need 1 Usable Part
- Crafting +6 Strength Equipment will need 2 Usable Part
- Crafting +10 Strength Equipment will need 2 Usable Part
 
**Craft**, will grants 100% Crafting EXP + Item if successfull.
**Practice**, will grants 200% Crafting EXP and no item if successfull.

**Success Rate**, depends on your crafting level and total attributes of the item you are trying to craft. 

> Success Chance = ((Crafting Level - Total Attributes) x 10) + 50;

```Csharp
    int SuccesRate()
    {
       return ((craftinglevel - itemAttributes.Sum()) * 10) + 50;
    }
```

