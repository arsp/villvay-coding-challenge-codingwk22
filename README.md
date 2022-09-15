# Coding Challenge

## T20 World Cup Super 6 qualification scenario simulator

The T20 World cup 2022 has entered its final stage of the Super 6 rounds. Six teams made the Super 6, only 5 have a chance to make it to the finals in the current scenario, there isn’t much separating the teams in terms of points or NRR(Net Run Rate). Each of the 5 teams can make it to the final if they can aim for a top 2 finish with just 2 more fixtures to be completed.

Two teams have already played their quota, England and Afghanistan, surprisingly favourites England have lost all of their matches, while under dogs Afghanistan is the only team with 2 wins. With just 2 fixtures remaining, they are not yet safe nor have a guaranteed place in the finals, the next two matches will definitely produce a winner(Rain will never be a problem) and the team with the most wins and best NRR would go through.

### The current points table stands as follows

| Team | Matches Played | Matches Lost | Matches Won | Points | RunsScored/OversFaced | RunsConceded/OversBowled | NRR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Afghanistan | 5 | 3 | 2 | 4 | 880/100 | 810/100 | 0.700 |
| Sri Lanka | 4 | 3 | 1 | 2 | 771/80 | 735/79 | 0.384 |
| India | 4 | 3 | 1 | 2 | 720/80 | 730/80 | -0.125 |
| Pakistan | 4 | 3 | 1 | 2 | 700/80 | 725/80 | -0.3125 |
| Australia | 4 | 3 | 1 | 2 | 695/80 | 750/80 | -.688 |
| England | 5 | 5 | 0 | 0 | 800/100 | 1000/100 | -4.5 |

### You come in

It can’t get any closer than this and the fans are eager to see how their teams would fair. You are brought in as the Software Consultant and two days to come up with an program to generate reports for the super 6 qualification scenarios.

### 📆 **The two remaining fixtures are**

- India Vs Australia on the 21st Of October 2022
- Sri Lanka Vs Pakistan on the 22nd of October 2022

📄 **The report should consist of the following information for a particular team.**

**Qualification For Team :** [TeamName]

**Best Case :**

1. Who would win ? Whose win has the best possible qualification scenario for the team whose scenario is being simulated
2. To Qualify
    1. When Batting first (Margin of victory in terms of runs) : **to win by [no-of-runs-needed] runs**
    2. When Bowling first(Margin of victory in terms of overs remaining, ignore decimals) : **to win within [no-of-overs] overs**

**Worst Case :**

1. Who would win ? Whose win has the worst possible qualification scenario for the team whose scenario we are simulating
2. To Qualify
    1. When Batting first (Margin of victory in terms of runs) : **to win by [no-of-runs-needed] runs**
    2. When Bowling first(Margin of victory in terms of overs remaining, ignore decimals) : **to win within [no-of-overs] overs**

ℹ️ *The response of the bestCase and the worstCase can be a string*

### Example Scenario

Assume we wish to see the Australia’s qualification scenario.

The Game they are interested is :  **Sri Lanka Vs Pakistan**

If they win the game, they take India out of the qualification equation because they will have 4 points while India will only have 2 points, so they don’t have to worry about NRR of India.

**Qualification For Team :** AUS

👍🏻 **Best Case :**

- **Who Should Win** : Pakistan
  - **Averages RunsScored when Batting :** 175 in their 20 overs (700/4)
  - **Predicted RunsScored/OversFaced would be** : 700+175 = 875/100
  - **Average RunsConceded when bowling :** 182.5 in their 20 overs(725/80)
    - But since we are assuming they are winning here we would add a buffer of 15 runs since they are one before last in the table(see conditions), **so their opponent would score 165 when they win**.
  - **Predicted RunsConceded/OversBowled would be**  725+ 160 = 885/100
  - **Predicted NRR Would be  :** -**0.100 (875/100 - 885/100)**
- **To Qualify :**
    1. **When batting first :** Australia will score 173.5 ~ 173(decimal should be dropped from the avg score) score and will need to have a NRR above -0.100 to qualify so they will have to win by a **margin of at least 46 runs** in their 20 overs

        *(Hint : The margin to win should be a simple calculation using the totals between teams)*

    2. **When bowling first :**
        1. **The opponent they are facing is India who have an average batting score of :** 180(720/4)
        2. Hence Australia will need to score **181 to win(**+1 the total scored by opponent) which would mean that Australia will have a **RunsConceded**/**OversFaced** : [ 750+180 = 930/100 ] which would bring their RunsScored/OversFaced : 695 +181 = 876, so they have have a delta of 56 runs, to gap this delta they will need to score the entire runs in 15 overs with 5 overs to spare.

👎🏻 **Worst Case :**

- Is when the team with the highest NRR wins and it will take much qualification much more harder, do the same calculations to the other opponent in this case **Sri Lanka**

### ✅ **Do Consider**

- Remember Afghanistan is not yet into the finals, so their qualification will also need to be checked, but in their case all 4 teams are a threat to them, they need to ensure that for their hopes to stay alive at-least one qualifying team should have a lesser run rate than them.
- The simulator you are building is not just for this edition of the WorldT20Super Sixes but all forth coming editions, so be prepared to calculate predictions for all 5 teams, or to throw a NoPredictionsPossible errors if all the teams have already played all their fixtures or when the fixtures array is empty.
- What if instead of 1 match remaining, each team had two matches to be played, will your code still work ? Ensure that predictor still works for at least 2 matches
- If there are more than 3 fixtures available a team throw a PredictionTooVague Error
- In a fixture how important is your date ? Or do you think the order does not matter
- Skip inconsequential fixtures from the predictor, fixtures whose result will have no bearing to your place in the table even if either teams wins or loses ?  Example Say the last fixture is between two teams who are 4 points lesser than you in the table, the result of that match does not even matter as their NRR will be inconsequential as they are would 2 points below you.
- Think about what happens with teams who are way high up in the table that no matter what happens in the rest of the fixtures they can’t be brought down, for such scenarios you can skip the analysis and return “AleadyQualified” in both the best and the worst cases

### ❌ Do Not Consider

- Partially completed matches due to D/L calculations
- Matches will end up being tied or being abandoned

```java
/**
* @param toToSimulateQualification - Team for which the prediction is done
* @param pointsTable - Array of Standings not guranteed to be in any Order, the order is determined by the Standing#rank property
* @param fixtures - Array of Fixture which shows the remaining mataches to be played.
*/
public QualificationReport simulateQualificationScenarios(WT20SuperSixTeam toToSimulateQualification, Standing[] pointsTable, Fixture fixtures[])
```

```java
enum WT20SuperSixTeam {
 AFG,
 PAK,
 AUS,
 IND,
 SL,
 ENG
}
// Languages which do not have enum support can use strings
```

```java
class Standing {
 rank,
 team,
 matchesPlayed,
 matchesLost,
 matchesWon,
 totalRunsScored
 totalOversFaced
 totalRunsConceded,
 totalOversBowled,
 netRunRate
}

// Languages which do not have class types, create objects with these properties
```

```java
class Fixture {
 WT20SuperSixTeam team1,
 WT20SuperSixTeam team2,
 Date fixtureDate
}
```

**Assumptions**

1. Assume that each team would score their average score(Total Runs Scored/No of Games played) in the predicted match when batting first.
2. All teams would face 20 overs in all predictions except when the team whom we are checking the prediction for team is batting second; In that case we are calculating the number of overs to win by
3. In the event of a Win for the team under calculation deduct
    1. 10 runs if they are last in the table and increment by 5 for each level up from the Your teams’ Average Score
4. Always assume teams will score 1 more run than the target when batting second/chasing.
5. Always the OversFaced will be a round number, decimals are ignored to keep the Math sample

## Net Run Rate Calculation

To calculate the net run rate, all you need to do is:

- Input the number of **runs scored**.
- Input the number of **overs faced**.
- Input the number of **runs conceded**.
- Lastly, input the number of **overs bowled**.
- The run rate calculator will use these four values to calculate the **average runs per over scored by the team** and the **average runs per over scored against the team**. It will then use them to give you the **net run rate** of your team.

![Formula to calculate NRR](images/nrr-formula.png)

Formula to calculate NRR

## The following needs to be answered when submitting the coding challenge ?

1. Only fully completed solutions should be submitted
2. **Code would be evaluated based on the following factors**
    1. Cleverness of the solution
    2. Simplicity
    3. You do not get points for the least number of lines. Readability of the code in important, this does not mean ternary operators are banned, but that variables like “x”, “value” which are ambiguous makes the code hard to read, if you need to make a method go for it.
    4. Additional score for performance considerations
    5. The test cases used to test the algorithm including edge cases.
    6. Write comments to make your code more readable
3. **Write a proper README explaining the following**
    1. The method used to solve the algorithm(algorithm and Data Structure if you have used any)
    2. The order of growth of your algorithm, how does your algorithm perform if you have considered performance.
4. **Do’s**
    1. The Challenge should be solved using either Typescript, Javascript, Java, python or php
    2. Code should be a GitHub repository Share the code only with the following github **account deployments@github.com**
    3. Deploy the code to a Gitpod and share the link, all tests should be executing in Gitpod.
5. **Don’ts**
    1. Do not use helper functions specific to the programming language to take short cuts like using python libraries which does the bulk of the algorithm for you(For example if the algorithm is about finding duplicates using a helper method does not really mean you solved the problem, you just know a method which can solve the problem).
    2. Cheat by copying and pasting answers from the internet
    3. Submit Partially Solved algorithms or overseen test cases this would be a cause for  disqualification

Happy Coding

## References

[Net Run Rate Calculator](https://www.omnicalculator.com/sports/nrr#what-is-net-run-rate)
