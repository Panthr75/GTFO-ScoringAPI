# Scoring API
Wiki for implementing the Scoring API in rundowns.

To implement custom scoring in a rundown, a `ScoreTable.json` must be included in the rundown's `/Custom` folder, and must be of a *ScoreTable* format.

## Formats
### ScoreTable
A *ScoreTable* format consists of the following JSON structure:
```ts
{
    "version": 1
    "primary": PrimaryScore[],
    "secondary": SecondaryScore[],
    "melee": MeleeScore
}
```
##### ScoreTable.version
**Description**: Internally used to differentiate different versions of ScoreTables if the format of them get updated. For now, this value should always be `1`.<br/>
**Type**: The integer `1`.

##### ScoreTable.primary
**Description**: Contains the scores for primary weapons, or GearStandard.<br/>
**Type**: An array of *PrimaryScore* formats, or [*PrimaryScore*](#primaryscore)[].

##### ScoreTable.secondary
**Description**: Contains the scores for secondary weapons, or GearSpecial.<br/>
**Type**: An array of *SecondaryScore* formats, or [*SecondaryScore*](#secondaryscore)[].

##### ScoreTable.melee
**Description**: Contains the score for melee weapons, or GearMelee.<br/>
**Type**: *MeleeScore* format, or [*MeleeScore*](#meleescore).

<br/><br/><br/>

### PrimaryScore
A *PrimaryScore* format consists of the following JSON structure:
```ts
{
    "persistentID": uint,
    "hitScore": uint,
    "killScore": uint
}
```
##### PrimaryScore.persistentID
**Description**: An ID that maps the weapon to the one the same persistent ID specified in the `GameData_ArchetypeDataBlock_bin.json`.<br/>
**Type**: An unsigned 32-bit integer, or `uint`. A `uint` can have a value between 0 and 4294967295 (inclusive).

##### PrimaryScore.hitScore
**Description**: The total score awarded when a player achieves a hitmarker on an enemy. This score will not be awarded if the player kills the enemy.<br/>
**Type**: A [*Score*](#score) format, or an unsigned 32-bit integer.<br/>
**Default Value**: The default value for a non-defined primary weapon is `10`.

##### PrimaryScore.killScore
**Description**: The total score awarded when a player achieves a kill.<br/>
**Type**: A [*Score*](#score) format, or an unsigned 32-bit integer.<br/>
**Default Value**: The default value for a non-defined primary weapon is `200`.

<br/><br/><br/>

### SecondaryScore
A *SecondaryScore* format consists of the following JSON structure:
```ts
{
    "persistentID": uint,
    "hitScore": uint,
    "killScore": uint
}
```
##### SecondaryScore.persistentID
**Description**: An ID that maps the weapon to the one the same persistent ID specified in the `GameData_ArchetypeDataBlock_bin.json`.<br/>
**Type**: An unsigned 32-bit integer, or `uint`. A `uint` can have a value between 0 and 4294967295 (inclusive).

##### SecondaryScore.hitScore
**Description**: The total score awarded when a player achieves a hitmarker on an enemy. This score will not be awarded if the player kills the enemy.<br/>
**Type**: A [*Score*](#score) format, or an unsigned 32-bit integer.<br/>
**Default Value**: The default value for a non-defined secondary weapon is `10`.

##### SecondaryScore.killScore
**Description**: The total score awarded when a player achieves a kill.<br/>
**Type**: A [*Score*](#score) format, or an unsigned 32-bit integer.<br/>
**Default Value**: The default value for a non-defined secondary weapon is `100`.

<br/><br/><br/>

### MeleeScore
A *MeleeScore* format consists of the following JSON structure:
```ts
{
    "hitScore": uint,
    "killScore": uint
}
```
##### MeleeScore.hitScore
**Description**: The total score awarded when a player achieves a hitmarker on an enemy. This score will not be awarded if the player kills the enemy.<br/>
**Type**: A [*Score*](#score) format, or an unsigned 32-bit integer.<br/>
**Default Value**: The default value for a non-defined melee weapon is `10`.

##### MeleeScore.killScore
**Description**: The total score awarded when a player achieves a kill.<br/>
**Type**: A [*Score*](#score) format, or an unsigned 32-bit integer.<br/>
**Default Value**: The default value for a non-defined melee weapon is `130`.

<br/><br/><br/>

### Score
An unsigned 32-bit integer, or `uint`. A `uint` can have a value between 0 and 4294967295 (inclusive).

Keep in mind the scoring system works in `10` increments, so `125` is not a valid score, but `120` is.

## Examples
##### MeleeScore Example (Standard Melee)
```json
{
    "hitScore": 10,
    "killScore": 130
}
```
##### SecondaryScore Example (Combat Shotgun)
```json
{
    "persistentID": 35,
    "hitScore": 10,
    "killScore": 150
}
```
##### PrimaryScore Example (Heavy Assault Rifle)
```json
{
    "persistentID": 67,
    "hitScore": 10,
    "killScore": 320
}
```
##### ScoreTable (Combination of the above examples)
```json
{
    "version": 1,
    "primary": [
        {
            "persistentID": 67,
            "hitScore": 10,
            "killScore": 320
        }
    ],
    "secondary": [
        {
            "persistentID": 35,
            "hitScore": 10,
            "killScore": 320
        }
    ],
    "melee": [
        {
            "hitScore": 10,
            "killScore": 130
        }
    ]
}
```
