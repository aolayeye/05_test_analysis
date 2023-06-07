# 05_test_analysis

## Analytics in Practice: Using Optimization Models for Sales Planning at NBC1

1Based on Srinivas Bollapragada, Hong Cheng, Mary Phillips, Marc Garbiras, Michael Scholes, Tim Gibb, and Mark Humphreville, “NBC’s Optimization Systems Increase Revenues and Productivity,” Interfaces, 32, 1 (January–February 2002): 47–60.

The National Broadcasting Company (NBC), a subsidiary of General Electric, is primarily in the business of delivering eyeballs (audiences) to advertisers. NBC’s television network, cable network, TV stations, and Internet divisions generate billions of dollars in revenues. Of these, the television network business is by far the largest.

The television broadcast year in the United States starts in the third week of September. The broadcast networks announce their programming schedules for the new broadcast year in the middle of May. Shortly after that, the sale of inventory (advertising slots) begins. The broadcast networks sell about 60% to 80% of their airtime inventory during a brief period starting in late May and lasting about two to three weeks. This sales period is known as the up-front market. During this time, advertising agencies approach the TV networks with requests to purchase time for their clients for the entire season. A typical request consists of the dollar amount, the demographic (for example, adults between 18 and 49 years of age) in which the client is interested, the program mix, weekly weighting, unit-length distribution, and a negotiated cost per 1,000 viewers. NBC must develop a detailed sales plan consisting of the schedule of commercials to be aired to meet the requirements. In addition, the plan should also meet the objectives of NBC’s sales management, whose goal is to maximize the revenues for the available fixed amount of inventory.

Traditionally, NBC developed sales plans manually. This process was laborious, taking several hours. Moreover, most plans required a great deal of rework because, owing to their complexity, they initially met neither management’s goals nor the customer’s requirements. NBC developed a system using linear optimization that would generate sales plans quickly in a manner that made optimal use of the available inventory. The sales-planning problem was to minimize the amount of premium inventory assigned to a plan and the total penalty incurred in meeting goals, while meeting constraints on inventory, airtime availability, product conflicts, client requirements, budget, show mix, weekly weighting, and unit mix. The decision variables are the numbers of commercials of each spot length requested by the client that are to be placed in the shows and weeks included in the sales plan. The objective function includes a term that represents the total value of inventory assigned to the sales plan and terms that measure the penalties incurred in not meeting the client requirements these systems have provided.

The model and its implementation have saved millions of dollars of good inventory for NBC while meeting all the customer requirements; increased revenues; reduced the time needed to produce a sales plan from three to four hours to about 20 minutes; helped NBC to respond quickly to agencies and secure a greater share of the available money in the market; helped NBC sales managers to resolve deals more quickly than in the past and better read the market, resulting in a more accurate prediction of the upfront outcome; decreased rework on plans by more than 80%; and increased NBC’s revenues by at least $50 million a year.


### Example
We will begin with a simple scenario to illustrate the development and spreadsheet implementation of a linear optimization model. Sklenka Ski Company (SSC) is a small manufacturer of two types of popular all-terrain snow skis, the Jordanelle and the Deercrest models. The manufacturing process consists of two principal departments: fabrication and finishing. The fabrication department has 12 skilled workers, each of whom works seven hours per day. The finishing department has three workers, who also work a seven-hour shift. Each pair of Jordanelle skis requires 3.5 labor-hours in the fabricating department and 1 labor-hour in finishing. The Deercrest model requires 4 labor-hours in fabricating and 1.5 labor-hours in finishing. The company operates five days per week. SSC makes a net profit of $50 on the Jordanelle model and $65 on the Deercrest model. In anticipation of the next ski-sale season, SSC must plan its production of these two models. Because of the popularity of its products and limited production capacity, its products are in high demand, and SSC can sell all it can produce each season. The company anticipates selling at least twice as many Deercrest models as Jordanelle models. The company wants to determine how many of each model should be produced on a daily basis to maximize net profit.

### The Steps
#### Identifying Decision Variables, the Objective, and Constraints

The first thing to do is to read the problem statement carefully and identify the decision variables, objective, and constraints in plain language before attempting to develop a mathematical model or a spreadsheet.


Sklenka Ski Company: Identifying Model Components

    Step 1. Identify the decision variables. SSC makes two different models of skis. The decisions are stated clearly: how many of each model ski should be produced each day? Thus, we may define
Jordanelle = Number of pairs of Jordanelle skis produced/day
Deercrest = Number of pairs of Deercrest skis produced/day

    It is very important to clearly specify the dimensions of the variables, for example, “pairs of skis produced/day” rather than simply “Jordanelle skis.”

    Step 2. Identify the objective function. The problem states that SSC wishes to maximize net profit, and we are given the net profit figures for each type of ski. In some problems, the objective is not explicitly stated, and we must use logic and business experience to identify the appropriate objective.

    Step 3. Identify the constraints. To identify constraints, look for clues in the problem statement that describe limited resources that are available, requirements that must be met, or other restrictions. In this example, we see that both the fabrication and finishing departments have limited numbers of workers, who work only seven hours each day; this limits the amount of production time available in each department. Therefore, we have the following constraints:

        Fabrication: Total labor-hours used in fabrication cannot exceed the amount of labor-hours available.

        Finishing: Total labor-hours used in finishing cannot exceed the amount of labor-hours available.

In addition, the company anticipates selling at least twice as many Deercrest models as Jordanelle models. Thus, we need a constraint that states

Number of pairs of Deercrest skis must be at least twice the number of parts of Jordanelle skis.

Finally, we must ensure that negative values of the decision variables cannot occur. Nonnegativity constraints are assumed in nearly all optimization models.


#### Developing a Mathematical Model

The challenging part of developing optimization models is translating the descriptions of the objective and constraints into mathematical expressions. We usually represent decision variables by descriptive names (such as Jordanelle and Deercrest), abbreviations, or subscripted letters such as
and For mathematical formulations involving many variables, subscripted letters are often more convenient; however, in spreadsheet models, we recommend using descriptive names to make the models and solutions easier to understand. In Example 13.2, we show the importance of specifying the dimension of the decision variables. This is extremely helpful to ensure the accuracy of the model.


#### Sklenka Ski Company: Modeling the Objective Function

The decision variables are the number of pairs of each type of ski to produce each day. Because SSC makes a net profit of $50 on the Jordanelle model and $65 on the Deercrest model, then, for example, if we produce 10 pairs of Jordanelle skis and 20 pairs of Deercrest skis during one day, we would make a profit of ($50/pair of Jordanelle skis)(10 pairs of Jordanelle skis) + ($65/pair of Jordanelle skis)(20 pairs of Deercrest skis)

Because we don’t know how many pairs of skis to produce, we write each term of the objective function by multiplying the unit profit by the decision variables we have defined: Maximize Total Profit = $50 Jordanelle + $65 Deercrest
Note how the dimensions verify that the expression is correct: ($/pair of skis)(number of pairs of skis) = $

Constraints are generally expressed mathematically as algebraic inequalities or equations with all variables on the left side and constant terms on the right (this facilitates solving the model on a spreadsheet, as we will discuss later). To model the constraints, we use a similar approach. First, consider the fabrication and finishing constraints. We expressed these constraints as:

    Fabrication: Total labor-hours used in fabrication cannot exceed the amount of labor hours available.
    Finishing: Total labor-hours used in finishing cannot exceed the amount of labor hours available.

First, note that the phrase “cannot exceed” translates mathematically as "<="
In other constraints, we might find the phrase “at least,” which would translate as ">=" or “must contain exactly,” which would specify an “=” relationship. All constraints in optimization models must be one of these three forms.

Second, note that “cannot exceed” divides each constraint into two parts—the left-hand side (“total labor-hours used”) and the right-hand side (“amount of labor-hours available”). The left-hand side of each of these expressions is called a constraint function. A constraint function is a function of the decision variables in the problem. The right-hand sides are numerical values (although occasionally they may be constraint functions as well). All that remains is to translate both the constraint functions and the right-hand sides into mathematical expressions.


### Sklenka Ski Company: Modeling the Constraints

The amount of labor available in fabrication is: (12 workers) * (7 hours/day) = 84 hours/day
whereas in finishing we have (3 workers) * (7 hours/day) = 84 hours/day Because each pair of Jordanelle skis requires 3.5 labor-hours and each pair of Deercrest skis requires 4 labor-hours in the fabricating department, the total labor used in fabrication is 3.5 Jordanelle + 4 Deercrest  
Note that the dimensions of these terms are (hours/pair of skis)(number of pairs of skis produced per day) = hours.
Similarly, for the finishing department, the total labor used is 1 Jordanelle + 1.5 Deercrest

Therefore, the appropriate constraints are:
      Fabrication: 3.5 Jordanelle + 4 Deercrest <= 84
      Finishing: 1 Jordanelle + 1.5 Deercrest <= 21

For the market mixture constraint “Number of pairs of Deercrest skis must be at least twice the number of pairs of Jordanelle skis,” we have
Deercrest >= 2 Jordanelle

It is customary to write all the variables on the left-hand side of the constraint. Thus, an alternative expression for this constraint is:
Deercrest - 2 Jordanelle >= 0

The difference between the number of Deercrest skis and twice the number of Jordanelle skis can be thought of as the excess number of Deercrest skis produced over the minimum market mixture requirement. Finally, nonnegativity constraints are written as:

Deercrest >= 0
Jordanelle >= 0

The complete mathematical model for the SSC problem is:
    Maximize Total Profit =  50 Jordanelle + 65 Deercrest
                             3.5 Jordanelle + 4 Deercrest <= 84
                             1 Jordanelle + 1.5 Deercrest <= 21
                             Deercrest - 2 Jordanelle >= 0
                             Deercrest >= 0
                             Jordanelle >= 0
                             
#### Implementing Linear Optimization Models on Spreadsheets

We will learn how to solve optimization models using an Excel tool called Solver. To facilitate the use of Solver, we suggest the following spreadsheet engineering guidelines for designing spreadsheet models for optimization problems:

    Put the objective function coefficients, constraint coefficients, and right-hand values in a logical format in the spreadsheet. For example, you might assign the decision variables to columns and the constraints to rows, much like the mathematical formulation of the model, and input the model parameters in a matrix. If you have many more variables than constraints, it might make sense to use rows for the variables and columns for the constraints.

    Define a set of cells (either rows or columns) for the values of the decision variables. In some models, it may be necessary to define a matrix to represent the decision variables. The names of the decision variables should be listed directly above the decision variable cells. Use shading or other formatting to distinguish these cells.

    Define separate cells for the objective function and each constraint function (the left-hand side of a constraint). Use descriptive labels directly above these cells.
    
#### A Spreadsheet Model for Sklenka Skis

Figure 13.1 shows a spreadsheet model for the SSC example. (Excel file Sklenka Skis already has the optimal solution. Typically, you would start with all decision variables equal to zero as shown in Figure 13.1.). We use the principles of spreadsheet The engineering that we discussed in Chapter 2 to implement the model. The Data portion of the spreadsheet provides the objective function coefficients, constraint coefficients, and right-hand sides of the model. Such data should be kept separate from the actual model so that if any data are changed, the model will automatically be updated. In the Model section, the number of each product to make is given in cells B14 and C14. Also in the Model section are calculations for the constraint functions,
    3.5 Jordanelle + 4 Deercrest (hours used in fabrication, cell D15)
    1 Jordanelle + 1.5 Deercrest (hours used in finishing, cell D16) and the objective function, 
    50 Jordanelle + 65 Deercrest (cell D22).
    
   ![image](https://github.com/aolayeye/05_test_analysis/assets/67847583/2edcb6e7-e0fb-4dee-8e42-92d306848bb1)

To help you understand the correspondence between the mathematical model and the spreadsheet model more clearly, we will write the model in terms of formulas used in the spreadsheet cells: 
       Maximize Profit = D22 = B9*B14 + C9*C14

subject to the constraints:
        D15 = B6*B14 + C6*C14 <= D6 (fabrication)
        D16 = B7*B14 + C7*C14 <= D7 (finishing)
        D19 = C14 - 2*B14 >= 0 (market mixture)
              B14 >= 0, C14 >= 0 (nonnegativity)

Observe how the constraint functions and right-hand-side values are stored in separate cells within the spreadsheet.
In Excel, the pairwise sum of products of terms can easily be computed using the SUMPRODUCT function. For example, the objective function:
    = B9*B14 + C9*C14 is equivalent to SUMPRODUCT(B9:C9, B14:C14)

Similarly, for the labor limitation constraints:
    = B6*B14 + C6*C14 is equivalent to SUMPRODUCT(B6:C6, B14:C14)
    = B7*B14 + C7*C14 is equivalent to SUMPRODUCT(B7:C7, B14:C14)
    

The SUMPRODUCT function often simplifies the model-building process, particularly when many variables are involved.

We should note that optimization models that we develop can be used in all phases of analytics—descriptive, predictive, and prescriptive. For example, we can use the model to evaluate the profit and utilization of resources in a descriptive setting to answer the question “What are we doing now?” We might use the model in a predictive setting to evaluate forecasted cost increases or the effects of inflation in the future. Finally, we can ask “What is the best we can do with our current resources?” In this way, the model can be used as a prescriptive model.
