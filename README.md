# Pokemon Analysis Project

## Project Read me

My project's goal is to use the data I have and the data analyst process which includes determining what data I need, cleaning, processing, analyzing, visualizing, and sharing it here. Using these steps I will determine the best pokemon based on their stats.

## Original spreadsheet information
Contains pokemon from Pokedex numbers 1-802. The original dataset came from https://www.kaggle.com/datasets/rounakbanik/pokemon and the creator says information is from ://serebii.net/
##Content Included
<br> •	Name
<br> •	Japanese_name
<br> •	Pokedex_number
<br> •	Percentage_Male
<br> •	Type_1
<br> •	Type_2
<br> •	Classification
<br> •	Height_m
<br> •	Weight_kg
<br> •	Capture_Rate
<br> •	Base_Egg_Steps
<br> •	Abilities
<br> •	Experience_Growth
<br> •	Base_Happiness
<br> •	Against_?
<br> •	Hp
<br> •	Attack
<br> •	Defense
<br> •	Sp_Attack
<br> •	Sp_Defense
<br> •	Speed
<br> •	Generation
<br> •	Is_Legendary

## Changed Version
My version of the data set contains Pokémon from Pokedex numbers 1-1010 also the different forms and versions of each (Alolan, Galarian, Hisuian, Mega, Paldean, Primal, etc.). Added and changed information is from https://pokemondb.net/ 
<br> • Pokedex_number
<br> • Name
<br> • Abilities
<br> • Weak_Against_?
<br> • Weak_Against_All_Concat
<br> • Strong_Against_?
<br> • Strong_Against_All_Concat
<br> • Type_1
<br> • Type_2
<br> • Type_1/Type_2 Concat
<br> • Base_Total
<br> • HP
<br> • Attack
<br> • Defense
<br> • SP_Attack
<br> • Sp_Defense
<br> • Speed
<br> • Height_m
<br> • Weight_Kg
<br> • Capture_Rate
<br> • Generation

## Programs used
<br> • Excel
<br> • SQL (Big Query)
<br> • Tableau

##  Cleaning/Preparation
<br> • Added columns Weak_Against_All_Concat, Strong_Against_?, and Type_1/Type_2 Concat
<br> • Removed columns Japanese_name, percentage_male, classification, base_egg_steps, experience growth, base_happiness, is_legendary.
<br> • Alternate forms of all pokemon were originally missing so those were added. They would include all pokemon with mega, alolan, galarian, hisuian, primal, paldean forms, Plus any forms that would normally have different stats.
<br> • Removed any null values and duplicates
<br> • made sure no information was in the incorrect columns
<br> • Made sure pokemon information was correctly inputted 

##Code Used Cleaning
```Excel
=CONCAT(D2,",",E2,",",F2,",",G2,",",H2,",",I2,",",J2,",",K2,",",L2,",",M2,",",N2,",",O2,",",P2,",",Q2,",",R2,",",S2,",",T2,",",U2)
```
Combines all Weak Against_? Columns
```Excel
=CONCAT(W2,",",X2, ",",Y2, ",", Z2, " ",AA2,",",AB2,",",AC2, ",",AD2, ",",AE2, ",", AF2, ",",AG2, ",",AH2, ",",AI2, ",",AJ2, ",",AK2, ",",AL2, ",", AM2,",",AN2)
```
Combines all Strong_Against_? Columns
```Excel
=CONCAT(AP2,"/",AQ2)
```
Shows Type_1 / Type_2
```Excel
=SUM(AT2:AY2)
```
Sum of HP, Attack, Defense, Sp_Attack, Sp_Defense, and Speed to form column Base_Total
```SQL
select distinct Type_1, Type_2 from pokemon-analysis-project.Pokedex.UpdatedPokedex9
Order by Type_1 asc;
```
Used to Select distinct combinations of Type_1 and Type_2
```SQL
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
```
Case statement used to validate Against_? columns 
```SQL
Select Name, Type_1, Type_2, Against_All_Concat,
CASE 
when Against_All_Concat = '1,1,1,1,1,1,2,1,1,1,1,1,1,0,1,1,1,1' then 'correct'
ELSE '-'
END AS Correct_Stats
FROM `pokemon-analysis-project.Pokedex.UpdatedPokedex2` 
WHERE Type_1 in ('Normal') And Type_2 is NULL
```
Updated case statement for validating Against_? columns 

## Data Analysis Questions
how do the types effect how strong a pokemon is?
what is the strongest pokemon?
what is the best type pairing?

## Code Used
```SQL
select Type_1_Type2_Concat, Count(*) as count FROM `pokemon-analysis-project.Pokedex.pokedex`
Group By Type_1_Type2_Concat
Order by count desc
```
```Excel
=AVERAGE(UpdatedPokedex9!D1096:U1096)
```
```Excel
=SUMPRODUCT((F2>=$F$2:$F$1191)/COUNTIF($F$2:$F$1191,$F$2:$F$1191))
```
```Excel
=(UpdatedPokedex9!A1096)
```
