THE GREEN REVOLUTION GAME

13 March 2025

Abstract

Imagine a future in which every branch of a large global network,
scattered across metropolises and small, remote centers, receives clean
and sustainable energy. Each location has its own challenges: varying
costs, renewable sources to integrate, and environmental conditions to be
respected. The goal is ambitious: to achieve energy independence with
a carbon-neutral, or even negative, footprint. However, all of this with
limited resources, forcing careful choices and ingenious strategies.

Reply takes on this challenge by following an unconventional path:
through innovative technologies, creative solutions and a long-term vi-
sion, it strives to build an energy ecosystem where nothing is wasted and
every single Watt can make a difference. It is a story of ingenuity and re-
sponsibility in which efficiency, sustainability and adaptability intertwine
in a global mosaic of operational sites. The stakes are high: achieving
a perfect balance between demand, supply and budget, proving that it
is possible to grow, expand and prosper without ever losing sight of the
planet and future generations.

Now, imagine having to put all this into practice: activity rounds,
energy resources to balance, initial and maintenance costs, life cycles,
special effects. The problem is ready to reveal its complexity and test
your planning skills.

1

THE GREEN REVOLUTION GAME

1 PROBLEM STATEMENT

1 Problem Statement

The problem unfolds over a series of turns T , each characterized by:

• a minimum number of buildings to be powered (TM )
• a maximum number of buildings to be powered (TX )
• a unit profit per powered building (TR).

At the beginning of each turn, it is possible to purchase new resources by pay-
ing their activation costs. Subsequently, periodic maintenance costs must be
incurred. The starting budget (D) is updated at the end of each turn based on
the choices made and the ability to meet at least the minimum building target
(TM ).

If the minimum TM of buildings is not reached, the profit for that turn is zero.
Otherwise, the revenue is calculated as:

profit = min(n, TX ) × TR

where n is the number of buildings powered during the turn.

From this profit are subtracted the periodic costs of the living resources; the
result, positive or negative, updates the budget available for the following turn.

Energy Resources There are R available resources, each described by the
following parameters:

• RI: Resource identifier.

• RA: Activation cost (one-time initial expenditure).

• RP : Periodic cost for each turn of life (maintenance expense).

• RW : Number of consecutive turns in which the resource is active and

generates profit.

• RM : Number of downtime turns required after a full cycle of activity

(maintenance).

• RL: Total life cycle of the resource (in turns), including both active and

downtime periods, after which the resource becomes obsolete.

• RU : Number of buildings the resource can power in each active turn.

• RT : Special effect of the resource.

During the turn in which the resource is purchased, its first activity period
automatically begins.

Each resource is classified with a type of special effect (RT ) that affects the
global conditions of the system while it is active. The effects can be positive
(“green”), increasing efficiency and performance, or negative (“non-green”), re-
ducing overall effectiveness but, in return, offering greater productive capacity.

2

THE GREEN REVOLUTION GAME

1 PROBLEM STATEMENT

Special Effect Types (RT )

A (Smart Meter):

• Green Resource: increases the number of buildings powered by the

facilities by a percentage.

• Non-Green Resource: reduces the number of buildings powered by

the facilities by a percentage, down to a minimum of 0.

B (Distribution Facility):

• Green Resource: increases by a percentage the minimum (TM ) and

maximum (TX ) thresholds of buildings that can be powered.

• Non-Green Resource: decreases these thresholds by a percentage,
narrowing maximum and minimum capacity, down to a minimum of
0.

C (Maintenance Plan):

• Green Resource: extends by a percentage the life (RL) of all re-

sources.

• Non-Green Resource: reduces by a percentage the life (RL) of all

resources, down to a minimum of 1.

The influenced resources are all and only those that are purchased during
active turns of the C-type resource. The C-type resource permanently
changes the lifespan of each influenced resource only once.

D (Renewable Plant)

• Green Resource:
served (TR).

increases by a percentage the profit per building

• Non-Green Resource: reduces by a percentage the profit per building,

down to a minimum of 0.

E (Accumulator):

This resource type does not have a non-green variant. The resource can
accumulate, during its active period, the number of buildings that exceed
the maximum threshold (TX ) during more productive turns, to compen-
sate for those in which other resources do not reach the minimum threshold
(TM ).

Thus, in turns where the minimum threshold is not reached and the ac-
cumulator is in its active period, you can draw from it the amount

qaccumulator = TM − n

to add to n (the number of buildings served) to generate profit during the
turn. This operation is valid if the E-type resource has at least qaccumulator
buildings stored.

In other words, the E resource allows you to ”virtually store” surplus
buildings from one turn to meet minimum requirements in subsequent,

3

THE GREEN REVOLUTION GAME

2

INPUT FORMAT

less productive turns, thereby ensuring greater stability and continuity in
powering buildings.

At the end of the accumulator’s life, it loses all the stored buildings. Hav-
ing multiple accumulators simultaneously is equivalent to having a single
one with greater capacity. Consequently, when an accumulator reaches
the end of its life, it can transfer its stored charge to other available accu-
mulators, if any are present.

X (Base Resource):

This type of resource does not have any special effect.

Resources of type A, B, C, D, E have a parameter RE specifying the impact of
the resource on the ecosystem. The special effect is calculated starting from the
base value of each influenced parameter, and the rounding down is applied only
at the end of the calculation, after considering all special effects.

For example: For a X-type resource with RU = 5, the effect of two A-type
resources each with an influence percentage of 75% (RE = 75) has the following
effect:

RUnew = ⌊RU + 0.75 · RU + 0.75 · RU ⌋ =

= ⌊2.5 · RU ⌋ = ⌊12.5⌋ = 12

A resource’s effect also applies to itself.
Green Resource; otherwise, the resource is considered N on − Green.

If the parameter is positive, it is a

Gameplay Sequence The sequence of each turn proceeds as follows:

1. Start of Turn: With the available budget at the beginning of the turn,
you can purchase new resources. If the sum of the activation costs exceeds
the available budget, the entire purchase of that turn is considered invalid.

2. Periodic Costs: You have to pay the maintenance costs (RP ) for each
alive resource. The operating resources provide a certain number of pow-
ered buildings (RU ). In the case of a resource with effect E, it is possible
to accumulate surpluses for subsequent turns.

3. Turn Profit: If the minimum threshold TM of buildings is met, calculate

the profit as previously described. Otherwise, profit = 0.

4. Budget Update: The periodic costs are subtracted from the profit. The

result updates the budget for the next turn.

In this context, planning which resources to activate or when to enhance them
through special effects, taking into account their life cycle and necessary main-
tenance, will be the key to balancing investments, efficiency, and results. Keep
in mind that each resource (identified by its ID) can be purchased an unlimited
number of times throughout the game.

2

Input format

The input file is an ASCII text file. Each line of the file is separated by a
single “\n” character (UNIX style). If a line contains multiple values, they are

4

THE GREEN REVOLUTION GAME

3 OUTPUT FORMAT

separated by a single space.

The first line of the input contains 3 integer values:

• D: initial capital availability

• R: total number of available resources

• T : number of game turns

The next R lines describe the available resources. Each line represents a single
resource r and is composed of:

RIr RAr RPr RWr RMr RLr RUr RTr REr

where:

• RIr, RAr, RPr, RWr, RMr, RLr, RUr are the integer parameters related

to the single resource r defined in the P roblem Statement.

• RTr: special effect type applied by the resource (A, B, C, D, E, X), as

defined above.

• REr: additional integer parameter (present or not, depending on the type
of effect) that represents the percentage of the special effect or the battery
capacity.

After defining the resources, the next T lines describe the turns. Each line
represents a turn t and contains:

T Mt T Xt T Rt

where:

• T Mt: the minimum number of buildings to be powered in that turn
• T Xt: the maximum number of buildings that can be powered in that turn
• T Rt: the profit for each powered building in that turn

3 Output format

The output file must be an ASCII text file. Each line of the output file must be
separated by the “\n” character. Each line indicates the resources acquired in
a given turn.

The format of each line is:

t Rt RI1 RI2

. . . RIRt

where:

• t: turn number (0-based, increasing)
• Rt: number of resources acquired in that turn (Rt ≤ 50)

5

THE GREEN REVOLUTION GAME

5 CONSTRAINTS

• RIx: ID of the acquired resource (x = 1...Rt).

4 Scoring rules

The total score of the solution is given by the sum of all the profits generated
over the entire horizon of the turns. In other words, the goal is to maximize
earnings during the game. The scoring equation is:

Score =

T
(cid:88)

t

prof itt

5 Constraints

• D ≥ 0

• R ≥ 0

• 0 ≤ t < T

• For each resource r:

RIr, RAr, RPr, RWr, RMr, RUr ≥ 0

RWr + RMr > 0

RLr > 0

• RTr assumes the values A, B, C, D, E, X
• For each turn t:

T Mt, T Xt, T Rt ≥ 0

T Xt > T Mt

• You can only purchase resources defined in the input file.

• The output file lists only the turns in which purchases are made. Turns

are listed in ascending order.

• In the output file, the number of resource IDs listed for the turn t is exactly

Rt, with 0 < Rt ≤ 50.

6

THE GREEN REVOLUTION GAME

6 EXAMPLE

6 Example

Example of input

10 5 6
1 16 3 1 1 3 6 D 2
2 2 2 1 3 5 4 X
3 14 15 2 2 5 3 C 1
4 20 9 2 1 3 4 E 3
5 10 8 2 1 3 3 X
3 5 4
5 6 3
2 7 4
4 6 3
4 7 1
5 7 4

In this example:

D = 10, R = 5, T = 6.

The following lines represent the 5 available resources:

1 16 3 1 1 3 6 D 2
2 2 2 1 3 5 4 X
3 14 15 2 2 5 3 C 1
4 20 9 2 1 3 4 E 3
5 10 8 2 1 3 3 X

The first one is a Green Resource of type D, which increases the unit profit per
powered building TR by 2%, and is defined as follows:

RI = 1, RA = 16, RP = 3, RW = 1, RM = 1, RL = 3, RU = 6

After defining the resources, information about turns is provided:

3 5 4
5 6 3
2 7 4
4 6 3
4 7 1
5 7 4

In this example, on turn t = 4:

T M4 = 4, T X4 = 7, T R4 = 1

Example of output

0 1 5
1 1 2
2 1 2
4 2 2 2
5 1 2

7

THE GREEN REVOLUTION GAME

6 EXAMPLE

On the first turn t = 0:

• Di = 10 the initial available budget is 10.
• The users bought 1 resource with RI = 5, so the total activation cost of

the turn is 10 ≥ Di, hence the turn is valid.

• The profit added to the final score is:

profit = min(n, TX ) × TR = min(3, 5) × 4 = 12

• The maintenance cost for all the active resources in this turn is 8.
• The final budget is Df = 10 − 10 + 12 − 8 = 4.

On the second turn t = 1:

• Di = 4 the initial available budget is 4.
• The users bought 1 resource with RI = 2, so the total activation cost of

the turn is 2 ≥ Di, hence the turn is valid.

• The profit added to the final score is:

profit = min(7, 6) × 3 = 18

• The maintenance cost for all the active resources in this turn is 8 + 2 = 10.
• The final budget is Df = 4 − 2 + 18 − 10 = 10.

By continuing the score calculation as above, a final score of 81 points is reached,
and all purchases are valid.

8


