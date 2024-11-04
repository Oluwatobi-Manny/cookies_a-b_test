*An analysis to optimize the game starting gate and improve user experience.*

# **A/B Testing Use Case: Cookie Cats Game**

**Overview:**
---
This project aims to analyze the user retention rate of various gates for the game Cookie Cats using Python. By leveraging data analytics and machine learning techniques, we can identify if the gates have any effect on the retention of users and develop strategies to enable user play more game rounds.

**Objective:**
To determine if moving the initial gate in Cookie Cats from level 30 to level 40 (gate_30 vs. gate_40) has a significant impact on user retention.

**Data:**
We will use the provided Cookie Cats dataset, which includes the following columns:

<table>
  <thead>
    <tr>
      <th>Column Name</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Index</td>
      <td>Row index</td>
    </tr>
    <tr>
      <td>userid</td>
      <td>Unique identifier for each user</td>
    </tr>
    <tr>
      <td>version</td>
      <td>Indicates whether the user was in the control group (gate_30) or the treatment group (gate_40)</td>
    </tr>
    <tr>
      <td>sum_gamerounds</td>
      <td>Total number of game rounds played by the user in the first week</td>
    </tr>
    <tr>
      <td>retention_1</td>
      <td>Whether the user returned to play one day after installation (1 = yes, 0 = no)</td>
    </tr>
    <tr>
      <td>retention_7</td>
      <td>Whether the user returned to play seven days after installation (1 = yes, 0 = no)</td>
    </tr>
  </tbody>
</table>

**Key Questions:**
The A-B test analysis will address the following key questions:

  * Does moving the placement of in-app purchase gates impact player retention?
  * At what level should the first gate be placed to maximize both player engagement and revenue?

**Method:**
The analysis includes the following steps:

1. **EDA and Data Cleaning:**
    * Check for categorical data
    
    ![Categorical data](<Images/Screenshot (260).png>)

2. **Univariate Analysis:**
    * Categorical variables
    
    ![Categorical vars](<Images/Screenshot (262).png>)

    * Numerical variable

    ![Numerical var](<Images/Screenshot (264).png>)

3. **Bivariate Analysis:**
    * Version vs. Retention

    ![Version vs retention after day 7](<Images/Screenshot (266).png>)

    * Gamerounds vs. Retention

    ![Gamerounds vs. Retention after day 7](<Images/Screenshot (268).png>)

4. **Statistical Testing:**
    * Assessing the Impact of Gates on Retention

    ```python
    from scipy.stats import mannwhitneyu

    # Separate the data into two groups: ad and psa
    gate_30_group = data[data['version'] == 'gate_30']['retention_1']
    gate_40_group = data[data['version'] == 'gate_40']['retention_1']

    # Perform the Mann-Whitney U test
    stat, p_value = mannwhitneyu(gate_30_group, gate_40_group)

    # Define significance level
    alpha = 0.05

    # Print the results
    print(f"Mann-Whitney U Statistic: {stat.round(2)}")
    print(f"P-Value: {p_value.round(4)}")

    # Check if the result is significant
    if p_value < alpha:
        print("The result is statistically significant.")
        print("Reject the null hypothesis: There is a significant difference between the gate_30 and gate_40 groups.")
    else:
        print("The result is not statistically significant.")
        print("Fail to reject the null hypothesis: There is no significant difference between the gate_30 and gate_40 groups.")
    ```
    **Interpretation of Results:**
     * If the p-value is less than 0.05, we reject the null hypothesis and conclude that there is a statistically significant difference between the two groups.
     * If the p-value is greater than 0.05, we fail to reject the null hypothesis and conclude that there is no statistically significant difference between the two groups.
   
   * Analyzing Rounds Played and Retention Success

    ![Analyzing the rounds](<Images/Screenshot (271).png>)

    * Optimal Rounds Played

    ![Optimal players round](<Images/Screenshot (273).png>)


**Expected Outcomes:**

By the end of this A/B testing, we expect to:

 - Determine the ideal level or stage in the game where a gate should be placed to maximize player retention.
 - Assess how different gate placements affect metrics such as player retention, session length, and in-app purchase conversion rates.
 - Evaluate how gate placement influences player satisfaction and overall enjoyment of the game.
 - Use the insights gained from the A/B test to make data-driven decisions about future game design, including the placement of additional gates.

By conducting this A/B test and analyzing the results, we can make data-driven decisions about the optimal placement of the initial gate in Cookie Cats to maximize user retention and engagement.

**LIBRARIES AND VERSION**
---
- numpy: 1.26.4
- pandas: 2.2.2
- matplotlib: 3.9.1.post1
- seaborn: 0.13.2
- scipy: 1.13.1

