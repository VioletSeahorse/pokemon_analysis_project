Pokemon Analysis Project
The original excel spreadsheet came from https://www.kaggle.com/datasets/rounakbanik/pokemon
But since getting it I have changed updated and added a lot of information. The information in the columns came from https://pokemondb.net/pokedex/. 
Added information, changes, and updates include.
1.	Alternate forms of all pokemon were originally missing so those were added. They would include all pokemon with mega, alolan, galarian, hisuian, primal, paldean forms, Plus any forms that would normally have different stats. 
2.	Added all pokemon with a pokedex number from 801-1110.
3.	Removed columns Japanese_name, percentage_male, classification, base_egg_steps, experience growth, base_happiness, is_legendary.
4.	Cleaned the data to make sure there were no null values anywhere.
5.	Pokemon with alternate forms had wrong stats, abilities, and types so I update those to be correct.

To start validating data I made a case statement to check if the Against_types for each type were correct. The select statement is being used to select name, type_1, and type_2 exp. Pikachu, Electric, Null(type_2 is null because Pikachu only has one type). The rest is a case statement saying when a column value = X then print correct if right or wrong if it doesn’t match. This example is set to view bug types against_types value.

SELECT Name, Type_1, Type_2,

CASE

When Against_Normal = 1 Then 'CORRECT'

When Against_fire = 2 Then 'CORRECT'

When Against_water = 1 Then 'CORRECT'

When Against_electric = 1 Then 'CORRECT'

When Against_grass = .5 Then 'CORRECT'

When Against_ice = 1 Then 'CORRECT'

When Against_fighting = .5 Then 'CORRECT'

When Against_poison = 1 Then 'CORRECT'

When Against_ground = .5 Then 'CORRECT'

When Against_flying = 2 Then 'CORRECT'

When Against_psychic = 1 Then 'CORRECT'

When Against_bug = 1 Then 'CORRECT'

When Against_rock = 2 Then 'CORRECT'

When Against_ghost = 1 Then 'CORRECT'

When Against_dragon = 1 Then 'CORRECT'

When Against_dark = 1 Then 'CORRECT'

When Against_steel = 1 Then 'CORRECT'

When Against_fairy = 1 Then 'CORRECT'

Else 'Wrong'

END AS Correct_Stats 

FROM `pokemon-analysis-project.Pokedex.Pokedex` 

Where Type_1 ='bug' AND Type_2 Is NULL

Order By Pokedex_number ASC;

The case statement ended up being time consuming so I made a new concat column of Against_types for to avoid needing to type of each number 1 at a time. The order is Against_Normal, Against_fire, Against_water, Against_electric, Against_grass, Against_ice, Against_fighting, Against_poison, Against_ground, Against_flying, Against_psychic, Against_bug, Against_rock, Against_ghost, Against_dragon, Against_dark, Against_steel, Against_fairy.

=CONCAT(D2,",",E2,",",F2,",",G2,",",H2,",",I2,",",J2,",",K2,",",L2,",",M2,",",N2,",",O2,",",P2,",",Q2,",",R2,",",S2,",",T2,",",U2)

