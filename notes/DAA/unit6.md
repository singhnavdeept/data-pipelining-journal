Okay, here are comprehensive and structured notes for Unit V: Introduction to Statistical Analysis, tailored for a BTech CSE student focusing on practical Python application and conceptual understanding for tests and vivas.

---

## **Unit V: Introduction to Statistical Analysis**

This unit bridges exploratory data analysis (EDA) with formal methods for drawing conclusions from data. We'll move from simply describing data to making inferences about larger populations based on samples, using the power of probability and hypothesis testing within the Python ecosystem.

**(CO5: perform statistical analysis and hypothesis testing using Python)**

---

### **1. Descriptive and Inferential Statistics**

*   **Conceptual Explanation:**
    *   Statistics is broadly divided into two main branches:
        1.  **Descriptive Statistics:** Focuses on *summarizing and describing* the main features of a dataset. Think of it as creating a profile or snapshot of the data you *have*. It doesn't try to make conclusions beyond that data. This includes calculating measures of central tendency (mean, median, mode), dispersion (variance, standard deviation, range, IQR), and shape (skewness, kurtosis), as well as creating visualizations like histograms and box plots (covered in Units III & IV).
        2.  **Inferential Statistics:** Focuses on *drawing conclusions or making inferences* about a larger **population** based on data collected from a smaller **sample**. Because we're generalizing from a sample, there's inherent uncertainty, which is managed using probability theory. Key techniques include hypothesis testing and confidence intervals.

*   **Real-World Use Cases:**
    *   **Descriptive:** A company calculates the average monthly sales for the *last quarter* to report performance. A data analyst creates histograms of customer ages *in their database* to understand demographics. A hospital tracks the range of recovery times for *patients admitted last week*.
    *   **Inferential:** A political pollster surveys 1000 voters (sample) to *predict the election outcome* for the entire voting population. A pharmaceutical company runs a clinical trial on 500 patients (sample) to *determine if a new drug is effective* for all potential patients (population). A/B testing uses sample user behavior to *infer which website design* will perform better for all future users.

*   **Python Implementation:**
    *   Descriptive statistics are primarily done using Pandas methods like `.describe()`, `.mean()`, `.median()`, `.std()`, `.var()`, `.skew()`, `.kurt()`, `.quantile()`, and plotting functions from Matplotlib/Seaborn (`.histplot()`, `.boxplot()`). (Covered in Units II, III, IV).
    *   Inferential statistics rely heavily on libraries like `scipy.stats` and `statsmodels` for hypothesis testing and modeling.

*   **Relationship:** Descriptive statistics provide the necessary summary of the sample data that fuels inferential statistical methods. You can't make good inferences without first understanding your sample.

---

### **2. Hypothesis Testing Framework**

*   **Conceptual Explanation:**
    *   Hypothesis testing provides a formal, structured way to make decisions based on data in the face of uncertainty. It's about testing a specific claim (hypothesis) about a population parameter using evidence from a sample.
    *   The core idea is to assume a default state (the "null hypothesis") and determine if the sample data provides strong enough evidence to reject that default state in favor of an alternative claim.
    *   **Key Components:**
        1.  **Null Hypothesis (H₀):** The statement of no effect, no difference, or status quo. It always includes equality (=, ≤, ≥). *Example: The average server response time is equal to 100ms.*
        2.  **Alternative Hypothesis (H₁ or Hₐ):** The statement we want to test for, contradicting H₀. It includes inequality (≠, <, >). *Example: The average server response time is different from 100ms.*
        3.  **Significance Level (α):** The *probability threshold* for rejecting H₀ *when H₀ is actually true*. It's the acceptable risk of making a **Type I error** (False Positive). Common values: 0.05 (5%), 0.01, 0.10. Setting α = 0.05 means we're willing to accept a 5% chance of wrongly concluding there *is* an effect.
        4.  **Test Statistic:** A value calculated from the sample data that measures how far the sample estimate (e.g., sample mean) deviates from the value specified by H₀, standardized by the estimated sampling error. The formula depends on the test used (e.g., Z, t, χ²).
        5.  **P-value:** The probability of observing a test statistic as extreme as, or more extreme than, the one actually observed, *assuming H₀ is true*. It quantifies the evidence *against* H₀.
        *   **Decision Rule:** If `p-value ≤ α`, reject H₀. The result is "statistically significant."
        *   If `p-value > α`, fail to reject H₀. The result is "not statistically significant."
    *   **Error Types:**
        *   **Type I Error:** Rejecting H₀ when it's true (False Positive). Probability = α.
        *   **Type II Error:** Failing to reject H₀ when it's false (False Negative). Probability = β. (Power = 1 - β).

*   **Real-World Use Cases:** Determining if a marketing campaign significantly increased sales, testing if a website redesign improved user engagement, checking if manufacturing changes affected defect rates, validating if a new drug performs better than a placebo.

*   **Workflow:** State H₀/H₁ -> Set α -> Choose Test -> Check Assumptions -> Calculate Test Statistic & p-value -> Compare p-value to α -> Conclude in Context.

---

### **3. Common Hypothesis Tests & Related Concepts**

#### **3.1 Z-Test**

*   **Concept:** Used to test hypotheses about a population mean (µ) when the population standard deviation (σ) is *known*, OR when the sample size (n) is *large* (typically n ≥ 30), allowing the sample standard deviation (s) to reliably estimate σ due to the Central Limit Theorem (CLT). Assumes data normality *or* large n.
*   **Use Cases:** Quality control where process variability (σ) is historically known; comparing a large sample mean to a known population mean (e.g., comparing average IQ of a large group to the known population average of 100).
*   **Python Implementation (`statsmodels`):** `statsmodels.stats.weightstats.ztest` is commonly used. (`scipy.stats` doesn't have a direct Z-test assuming known σ).

    *   **`ztest(x1, x2=None, value=0, alternative='two-sided', usevar='pooled', ddof=1.0)`**
        *   **Purpose:** Performs a Z-test for one or two samples.
        *   **Why/When Used:** To compare a sample mean to a population mean (`x2=None`), or to compare the means of two independent samples (`x1`, `x2`) when population variances are known or sample sizes are large.
        *   **Inputs:**
            *   `x1`: Array-like data for the first sample.
            *   `x2` (optional): Array-like data for the second sample. If `None`, performs a one-sample test against `value`.
            *   `value`: The value under the null hypothesis (e.g., the population mean for one-sample, or the difference in means for two-sample, usually 0).
            *   `alternative`: {'two-sided', 'larger', 'smaller'} - Specifies the alternative hypothesis (≠, >, <).
            *   `usevar`: {'pooled', 'unequal'} - How variances are handled (less critical for Z-test as we assume known or large N).
            *   `ddof`: Degrees of freedom correction for variance calculation (usually 1 for sample variance).
        *   **Output:** A tuple: `(z_statistic, p_value)`

*   **Code Examples:**

    ```python
    import numpy as np
    import pandas as pd
    from statsmodels.stats.weightstats import ztest
    import matplotlib.pyplot as plt
    import seaborn as sns

    # Common setup for examples
    np.random.seed(42)
    population_mean = 100
    population_std = 15 # Assume known or large sample approximation

    # Example 1: One-Sample Z-Test (Large Sample)
    # H0: µ = 100, H1: µ ≠ 100, alpha = 0.05
    sample_large = np.random.normal(loc=103, scale=population_std, size=100) # Sample mean slightly higher
    print("\n--- Example 1: One-Sample Z-Test ---")
    print(f"Sample Mean: {sample_large.mean():.2f}")

    z_stat_1, p_value_1 = ztest(sample_large, value=population_mean, alternative='two-sided')
    print(f"Z-statistic: {z_stat_1:.4f}, P-value: {p_value_1:.4f}")

    if p_value_1 < 0.05:
        print("Result: Reject H0. Sample mean is significantly different from 100.")
    else:
        print("Result: Fail to reject H0. No significant difference found.")

    # Example 2: Two-Sample Z-Test (Large Samples)
    # H0: µ1 = µ2 (or µ1 - µ2 = 0), H1: µ1 ≠ µ2, alpha = 0.05
    sample1 = np.random.normal(loc=98, scale=population_std, size=120)
    sample2 = np.random.normal(loc=101, scale=population_std, size=150)
    print("\n--- Example 2: Two-Sample Z-Test ---")
    print(f"Sample 1 Mean: {sample1.mean():.2f}, Sample 2 Mean: {sample2.mean():.2f}")

    z_stat_2, p_value_2 = ztest(sample1, sample2, value=0, alternative='two-sided')
    print(f"Z-statistic: {z_stat_2:.4f}, P-value: {p_value_2:.4f}")

    if p_value_2 < 0.05:
        print("Result: Reject H0. The means of the two samples are significantly different.")
    else:
        print("Result: Fail to reject H0. No significant difference found between the means.")

    # Example 3: One-Sample One-Tailed Z-Test
    # H0: µ <= 100, H1: µ > 100, alpha = 0.05
    sample_check_higher = np.random.normal(loc=104, scale=population_std, size=80)
    print("\n--- Example 3: One-Tailed Z-Test (Right-tailed) ---")
    print(f"Sample Mean: {sample_check_higher.mean():.2f}")

    # Test if sample mean is significantly GREATER than 100
    z_stat_3, p_value_3 = ztest(sample_check_higher, value=population_mean, alternative='larger')
    print(f"Z-statistic: {z_stat_3:.4f}, P-value: {p_value_3:.4f}")

    if p_value_3 < 0.05:
        print("Result: Reject H0. Sample mean is significantly greater than 100.")
    else:
        print("Result: Fail to reject H0. No significant evidence that the mean is greater than 100.")
    ```

#### **3.2 t-Test**

*   **Concept:** Used to test hypotheses about population mean(s) when the population standard deviation (σ) is *unknown* and must be estimated from the sample(s). Uses the t-distribution, which accounts for the extra uncertainty from estimating σ, especially with smaller sample sizes.
*   **Assumptions:** Data should be approximately normally distributed (check visually or with Shapiro-Wilk), especially crucial for small N. Samples should be random. For independent tests, observations between groups must be independent. Homogeneity of variances (equal variances) is assumed for the standard two-sample test, but Welch's t-test (often the default or an option) handles unequal variances.
*   **Use Cases:** Extremely common in practice as σ is rarely known. Comparing sample mean to a target value (one-sample), comparing means of two different groups like control vs treatment (independent two-sample), comparing means of the same group before and after an intervention (paired).

*   **3.2.1 One-Sample t-Test (Python: `scipy.stats.ttest_1samp`)**

    *   **`ttest_1samp(a, popmean, axis=0, nan_policy='propagate', alternative='two-sided')`**
        *   **Purpose:** Tests if the mean of a single sample (`a`) is significantly different from a known or hypothesized population mean (`popmean`).
        *   **Why/When Used:** When you have one sample and want to compare its average to a specific target value or historical average, and σ is unknown.
        *   **Inputs:**
            *   `a`: Array-like sample data.
            *   `popmean`: The hypothesized population mean under H₀.
            *   `axis`: Axis along which to compute the test (usually 0).
            *   `nan_policy`: How to handle NaNs ('propagate', 'omit', 'raise').
            *   `alternative`: {'two-sided', 'less', 'greater'} - Specifies H₁.
        *   **Output:** `TtestResult` object containing `statistic` (t-statistic) and `pvalue`.

    *   **Code Examples:**

        ```python
        from scipy import stats

        np.random.seed(101)
        target_mean = 5.0

        # Example 1: Sample mean likely different from target
        sample_a = np.random.normal(loc=5.5, scale=1.5, size=25) # n=25, unknown std dev
        print("\n--- Example 1: One-Sample t-Test (Significant) ---")
        print(f"Sample Mean: {sample_a.mean():.2f}")
        t_stat_a, p_value_a = stats.ttest_1samp(sample_a, popmean=target_mean, alternative='two-sided')
        print(f"t-statistic: {t_stat_a:.4f}, P-value: {p_value_a:.4f}")
        if p_value_a < 0.05: print("Result: Reject H0. Sample mean is significantly different from 5.0.")
        else: print("Result: Fail to reject H0.")

        # Example 2: Sample mean likely NOT different from target
        sample_b = np.random.normal(loc=5.1, scale=1.5, size=25)
        print("\n--- Example 2: One-Sample t-Test (Not Significant) ---")
        print(f"Sample Mean: {sample_b.mean():.2f}")
        t_stat_b, p_value_b = stats.ttest_1samp(sample_b, popmean=target_mean, alternative='two-sided')
        print(f"t-statistic: {t_stat_b:.4f}, P-value: {p_value_b:.4f}")
        if p_value_b < 0.05: print("Result: Reject H0.")
        else: print("Result: Fail to reject H0. No significant difference found from 5.0.")

        # Example 3: One-Sample t-Test (One-tailed: 'greater')
        # H0: µ <= 5.0, H1: µ > 5.0
        sample_c = np.random.normal(loc=5.8, scale=1.5, size=20)
        print("\n--- Example 3: One-Sample t-Test (One-tailed 'greater') ---")
        print(f"Sample Mean: {sample_c.mean():.2f}")
        t_stat_c, p_value_c = stats.ttest_1samp(sample_c, popmean=target_mean, alternative='greater')
        print(f"t-statistic: {t_stat_c:.4f}, P-value: {p_value_c:.4f}")
        if p_value_c < 0.05: print("Result: Reject H0. Sample mean is significantly greater than 5.0.")
        else: print("Result: Fail to reject H0.")
        ```

*   **3.2.2 Two-Sample Independent t-Test (Python: `scipy.stats.ttest_ind`)**

    *   **`ttest_ind(a, b, axis=0, equal_var=True, nan_policy='propagate', permutations=None, random_state=None, alternative='two-sided', trim=0)`**
        *   **Purpose:** Tests if the means of two *independent* samples (`a` and `b`) are significantly different.
        *   **Why/When Used:** Comparing means of two distinct groups (e.g., control vs. treatment, male vs. female) when data for one group doesn't influence the other, and σ's are unknown.
        *   **Inputs:**
            *   `a`, `b`: Array-like sample data for the two groups.
            *   `equal_var`: If `True`, assumes equal population variances (standard pooled t-test). If `False` (recommended default unless you know variances are equal), performs **Welch's t-test**, which does *not* assume equal variances.
            *   `alternative`: {'two-sided', 'less', 'greater'} - Specifies H₁. 'less' tests if mean(a) < mean(b), 'greater' tests if mean(a) > mean(b).
        *   **Output:** `TtestResult` object containing `statistic` (t-statistic) and `pvalue`.

    *   **Code Examples:**

        ```python
        np.random.seed(10)

        # Example 1: Means likely different, assuming equal variance (less robust)
        group1 = np.random.normal(loc=10, scale=2, size=40)
        group2 = np.random.normal(loc=12, scale=2, size=45) # Different mean, same variance
        print("\n--- Example 1: Independent t-Test (Equal Var = True, Significant) ---")
        print(f"Group 1 Mean: {group1.mean():.2f}, Group 2 Mean: {group2.mean():.2f}")
        t_stat_eq, p_value_eq = stats.ttest_ind(group1, group2, equal_var=True, alternative='two-sided')
        print(f"t-statistic: {t_stat_eq:.4f}, P-value: {p_value_eq:.4f}")
        if p_value_eq < 0.05: print("Result: Reject H0. Means are significantly different.")
        else: print("Result: Fail to reject H0.")

        # Example 2: Means likely different, NOT assuming equal variance (Welch's - Recommended)
        group3 = np.random.normal(loc=10, scale=2, size=40) # Smaller variance
        group4 = np.random.normal(loc=12, scale=4, size=45) # Larger variance
        print("\n--- Example 2: Independent t-Test (Welch's, equal_var=False, Significant) ---")
        print(f"Group 3 Mean: {group3.mean():.2f}, Group 4 Mean: {group4.mean():.2f}")
        t_stat_welch, p_value_welch = stats.ttest_ind(group3, group4, equal_var=False, alternative='two-sided')
        print(f"t-statistic: {t_stat_welch:.4f}, P-value: {p_value_welch:.4f}")
        if p_value_welch < 0.05: print("Result: Reject H0. Means are significantly different (using Welch's).")
        else: print("Result: Fail to reject H0.")

        # Example 3: Means likely NOT different (Welch's)
        group5 = np.random.normal(loc=10, scale=3, size=50)
        group6 = np.random.normal(loc=10.5, scale=3, size=55) # Means are close
        print("\n--- Example 3: Independent t-Test (Welch's, Not Significant) ---")
        print(f"Group 5 Mean: {group5.mean():.2f}, Group 6 Mean: {group6.mean():.2f}")
        t_stat_ns, p_value_ns = stats.ttest_ind(group5, group6, equal_var=False, alternative='two-sided')
        print(f"t-statistic: {t_stat_ns:.4f}, P-value: {p_value_ns:.4f}")
        if p_value_ns < 0.05: print("Result: Reject H0.")
        else: print("Result: Fail to reject H0. No significant difference found.")

        # Visualization Helper
        df_ttest_ind = pd.DataFrame({ 'Value': np.concatenate([group5, group6]),
                                    'Group': ['Group 5'] * len(group5) + ['Group 6'] * len(group6)})
        plt.figure()
        sns.boxplot(data=df_ttest_ind, x='Group', y='Value')
        plt.title('Box Plot Comparison for Example 3')
        # plt.show()
        ```

*   **3.2.3 Paired t-Test (Dependent t-Test) (Python: `scipy.stats.ttest_rel`)**

    *   **`ttest_rel(a, b, axis=0, nan_policy='propagate', alternative='two-sided')`**
        *   **Purpose:** Tests if the mean difference between two *related* or *paired* samples (`a` and `b`) is significantly different from zero. The observations in `a` and `b` must correspond to each other (e.g., same subject before/after, matched pairs).
        *   **Why/When Used:** Before-and-after studies (measuring the same subjects twice), matched-pair designs (e.g., comparing twins on a metric). Reduces variability by controlling for individual differences.
        *   **Inputs:**
            *   `a`, `b`: Array-like sample data for the two paired conditions. Must have the same length.
            *   `alternative`: {'two-sided', 'less', 'greater'} - Specifies H₁. 'less' tests if mean(a) < mean(b), 'greater' tests if mean(a) > mean(b). Usually testing if mean(difference) is != 0, < 0, or > 0.
        *   **Output:** `TtestResult` object containing `statistic` (t-statistic) and `pvalue`.

    *   **Code Examples:**

        ```python
        np.random.seed(50)
        n_pairs = 30

        # Example 1: Significant difference (e.g., improvement after treatment)
        before_scores = np.random.normal(loc=70, scale=10, size=n_pairs)
        # After scores are generally higher + some random noise for each person
        improvement = np.random.normal(loc=5, scale=3, size=n_pairs)
        after_scores = before_scores + improvement
        print("\n--- Example 1: Paired t-Test (Significant Improvement) ---")
        print(f"Mean Before: {before_scores.mean():.2f}, Mean After: {after_scores.mean():.2f}")
        print(f"Mean Difference (After - Before): {(after_scores - before_scores).mean():.2f}")
        t_stat_p1, p_value_p1 = stats.ttest_rel(after_scores, before_scores, alternative='greater') # Test if After > Before
        print(f"t-statistic: {t_stat_p1:.4f}, P-value: {p_value_p1:.4f}")
        if p_value_p1 < 0.05: print("Result: Reject H0. The 'after' scores are significantly greater than 'before'.")
        else: print("Result: Fail to reject H0.")

        # Example 2: No significant difference
        before_scores_ns = np.random.normal(loc=70, scale=10, size=n_pairs)
        random_change = np.random.normal(loc=0.5, scale=3, size=n_pairs) # Small avg change
        after_scores_ns = before_scores_ns + random_change
        print("\n--- Example 2: Paired t-Test (Not Significant) ---")
        print(f"Mean Before: {before_scores_ns.mean():.2f}, Mean After: {after_scores_ns.mean():.2f}")
        print(f"Mean Difference: {(after_scores_ns - before_scores_ns).mean():.2f}")
        t_stat_p2, p_value_p2 = stats.ttest_rel(after_scores_ns, before_scores_ns, alternative='two-sided')
        print(f"t-statistic: {t_stat_p2:.4f}, P-value: {p_value_p2:.4f}")
        if p_value_p2 < 0.05: print("Result: Reject H0.")
        else: print("Result: Fail to reject H0. No significant difference found between 'before' and 'after'.")

        # Example 3: Significant decrease (Testing 'less')
        # H0: mean(a) >= mean(b), H1: mean(a) < mean(b)
        before_high = np.random.normal(loc=80, scale=8, size=n_pairs)
        decrease = np.random.normal(loc=-6, scale=4, size=n_pairs) # Negative mean change
        after_low = before_high + decrease
        print("\n--- Example 3: Paired t-Test (Significant Decrease, 'less') ---")
        print(f"Mean Before: {before_high.mean():.2f}, Mean After: {after_low.mean():.2f}")
        print(f"Mean Difference: {(after_low - before_high).mean():.2f}")
        # Test if 'after' is significantly less than 'before'
        t_stat_p3, p_value_p3 = stats.ttest_rel(after_low, before_high, alternative='less')
        print(f"t-statistic: {t_stat_p3:.4f}, P-value: {p_value_p3:.4f}")
        if p_value_p3 < 0.05: print("Result: Reject H0. The 'after' scores are significantly less than 'before'.")
        else: print("Result: Fail to reject H0.")

        # Visualization Helper
        df_paired = pd.DataFrame({'Before': before_high, 'After': after_low, 'Difference': after_low - before_high})
        plt.figure()
        sns.histplot(df_paired['Difference'], kde=True)
        plt.title('Distribution of Differences (Example 3)')
        plt.axvline(df_paired['Difference'].mean(), color='red', linestyle='--')
        # plt.show()
        ```

#### **3.3 Chi-Squared Test (χ²)**

*   **Concept:** Used for analyzing categorical data represented as counts or frequencies. Tests whether there's a significant difference between *observed* frequencies and *expected* frequencies (based on a hypothesis or assumption of independence).
*   **Assumptions:** Data are counts/frequencies. Observations are independent. Expected cell counts should generally be ≥ 5 for the test approximation to be reliable (if not, consider Fisher's Exact Test or combining categories).
*   **Use Cases:** Testing if sample proportions match hypothesized population proportions (Goodness-of-Fit). Testing if two categorical variables are associated or independent (Test of Independence). Common in survey analysis, A/B testing on conversion rates, genetics.

*   **3.3.1 Chi-squared Goodness-of-Fit Test (Python: `scipy.stats.chisquare`)**

    *   **`chisquare(f_obs, f_exp=None, ddof=0, axis=0)`**
        *   **Purpose:** Tests if the observed frequencies (`f_obs`) in different categories significantly differ from expected frequencies (`f_exp`).
        *   **Why/When Used:** To check if a sample distribution for a single categorical variable matches a known or theoretical distribution.
        *   **Inputs:**
            *   `f_obs`: Array-like containing the observed frequencies (counts) for each category.
            *   `f_exp` (optional): Array-like containing the expected frequencies. If `None`, assumes equal frequencies across categories. Must sum to the same total as `f_obs`.
            *   `ddof`: "Delta degrees of freedom". Adjustment if parameters were estimated from data (usually 0 here).
        *   **Output:** `Power_divergenceResult` object containing `statistic` (χ²-statistic) and `pvalue`.
        *   **H₀:** Observed frequencies = Expected frequencies.
        *   **H₁:** Observed frequencies ≠ Expected frequencies.

    *   **Code Examples:**

        ```python
        from scipy.stats import chisquare

        # Example 1: Testing against equal expected frequencies
        # H0: Proportions are equal (e.g., fair 4-sided die rolled 120 times)
        observed_counts_1 = np.array([25, 35, 32, 28]) # Sum = 120
        expected_counts_1 = np.array([30, 30, 30, 30]) # Expected if fair (120/4)
        print("\n--- Example 1: Chi-Sq Goodness-of-Fit (vs Equal Freq) ---")
        print(f"Observed: {observed_counts_1}")
        chi2_stat_1, p_value_1 = chisquare(f_obs=observed_counts_1, f_exp=expected_counts_1)
        print(f"Chi2 Statistic: {chi2_stat_1:.4f}, P-value: {p_value_1:.4f}")
        if p_value_1 < 0.05: print("Result: Reject H0. Distribution significantly differs from equal proportions.")
        else: print("Result: Fail to reject H0.") # Likely fail here as observed are close

        # Example 2: Testing against specific expected frequencies (different proportions)
        # H0: Observed matches expected proportions (e.g., 40%, 30%, 20%, 10%)
        total_obs = 200
        observed_counts_2 = np.array([75, 65, 45, 15]) # Sum = 200
        expected_props = np.array([0.40, 0.30, 0.20, 0.10])
        expected_counts_2 = expected_props * total_obs
        print("\n--- Example 2: Chi-Sq Goodness-of-Fit (vs Specific Freq) ---")
        print(f"Observed: {observed_counts_2}, Expected: {expected_counts_2}")
        chi2_stat_2, p_value_2 = chisquare(f_obs=observed_counts_2, f_exp=expected_counts_2)
        print(f"Chi2 Statistic: {chi2_stat_2:.4f}, P-value: {p_value_2:.4f}")
        if p_value_2 < 0.05: print("Result: Reject H0. Distribution significantly differs from expected.")
        else: print("Result: Fail to reject H0.")

        # Example 3: If f_exp is None (assumes equal freq)
        observed_counts_3 = np.array([50, 20, 30]) # Total 100
        print("\n--- Example 3: Chi-Sq Goodness-of-Fit (f_exp=None) ---")
        print(f"Observed: {observed_counts_3}")
        # Expects [33.3, 33.3, 33.3] implicitly
        chi2_stat_3, p_value_3 = chisquare(f_obs=observed_counts_3)
        print(f"Chi2 Statistic: {chi2_stat_3:.4f}, P-value: {p_value_3:.4f}")
        if p_value_3 < 0.05: print("Result: Reject H0. Distribution significantly differs from equal freq.") # Likely reject
        else: print("Result: Fail to reject H0.")
        ```

*   **3.3.2 Chi-squared Test of Independence (Python: `scipy.stats.chi2_contingency`)**

    *   **`chi2_contingency(observed, correction=True, lambda_=None)`**
        *   **Purpose:** Tests if there's a statistically significant association between two categorical variables based on their frequencies in a contingency table (`observed`).
        *   **Why/When Used:** To see if knowing the category of one variable gives information about the category of the other (e.g., is smoking status associated with lung condition? Is preference for OS associated with age group?).
        *   **Inputs:**
            *   `observed`: An array-like contingency table (e.g., created using `pd.crosstab`) showing the frequency counts for each combination of categories.
            *   `correction`: If `True` (default), applies Yates' correction for continuity, typically used for 2x2 tables. Can be set to `False`.
        *   **Output:** A tuple: `(chi2_statistic, p_value, degrees_of_freedom, expected_frequencies_array)`
        *   **H₀:** The two variables are independent (no association).
        *   **H₁:** The two variables are dependent (associated).

    *   **Code Examples:**

        ```python
        from scipy.stats import chi2_contingency
        import pandas as pd

        # Example 1: Clear Association
        # Data: Vote (Yes/No) vs. Party (A/B)
        print("\n--- Example 1: Chi-Sq Test of Independence (Association Likely) ---")
        observed_table_1 = pd.DataFrame({'Party A': [70, 30], 'Party B': [40, 60]}, index=['Vote Yes', 'Vote No'])
        print("Contingency Table 1:\n", observed_table_1)
        chi2_stat_t1, p_value_t1, dof_t1, expected_t1 = chi2_contingency(observed_table_1)
        print(f"\nChi2 Statistic: {chi2_stat_t1:.4f}, P-value: {p_value_t1:.4f}, DoF: {dof_t1}")
        print("Expected Frequencies:\n", pd.DataFrame(expected_t1, index=observed_table_1.index, columns=observed_table_1.columns).round(2))
        if p_value_t1 < 0.05: print("\nResult: Reject H0. There is a significant association between Party and Vote.")
        else: print("\nResult: Fail to reject H0.") # Should reject here

        # Example 2: Likely No Association
        print("\n--- Example 2: Chi-Sq Test of Independence (No Association Likely) ---")
        observed_table_2 = pd.DataFrame({'Group X': [55, 45], 'Group Y': [65, 55]}, index=['Outcome P', 'Outcome Q'])
        print("Contingency Table 2:\n", observed_table_2)
        chi2_stat_t2, p_value_t2, dof_t2, expected_t2 = chi2_contingency(observed_table_2)
        print(f"\nChi2 Statistic: {chi2_stat_t2:.4f}, P-value: {p_value_t2:.4f}, DoF: {dof_t2}")
        print("Expected Frequencies:\n", pd.DataFrame(expected_t2, index=observed_table_2.index, columns=observed_table_2.columns).round(2))
        if p_value_t2 < 0.05: print("\nResult: Reject H0.")
        else: print("\nResult: Fail to reject H0. No significant association found.") # Likely fail here

        # Example 3: Using pd.crosstab to create the table first
        print("\n--- Example 3: Chi-Sq Test using pd.crosstab ---")
        # Create sample data (like the 'tips' dataset simplified)
        np.random.seed(1)
        n_obs = 200
        data = pd.DataFrame({
            'Day': np.random.choice(['Thur', 'Fri', 'Sat', 'Sun'], size=n_obs, p=[0.2, 0.15, 0.35, 0.3]),
            'Smoker': np.random.choice(['Yes', 'No'], size=n_obs, p=[0.4, 0.6])
        })
        # Artificially create a slight association for demonstration
        data.loc[(data['Day']=='Sun') & (data['Smoker']=='Yes'), 'Smoker'] = np.random.choice(['Yes','No'], size=len(data.loc[(data['Day']=='Sun') & (data['Smoker']=='Yes')]), p=[0.6, 0.4])

        contingency_table = pd.crosstab(data['Day'], data['Smoker'])
        print("Contingency Table (Day vs Smoker):\n", contingency_table)

        chi2_stat_t3, p_value_t3, dof_t3, expected_t3 = chi2_contingency(contingency_table)
        print(f"\nChi2 Statistic: {chi2_stat_t3:.4f}, P-value: {p_value_t3:.4f}, DoF: {dof_t3}")
        # print("Expected Frequencies:\n", pd.DataFrame(expected_t3, index=contingency_table.index, columns=contingency_table.columns).round(2))
        if p_value_t3 < 0.05: print("\nResult: Reject H0. There is a significant association between Day and Smoker status.")
        else: print("\nResult: Fail to reject H0.")
        ```

#### **3.4 P-Value: Deeper Dive**

*   **Recap Definition:** Probability of observing the current sample result (or something more extreme) *if the null hypothesis (H₀) were true*.
*   **Interpretation as Evidence:** It's a measure of the *strength of evidence against H₀* provided by the data. A smaller p-value indicates stronger evidence against H₀.
*   **Not Probability of H₀:** Crucially, the p-value is *NOT* the probability that H₀ is true. Hypothesis testing doesn't assign probabilities to hypotheses themselves (that's Bayesian inference). It assesses the compatibility of the *data* with H₀.
*   **Not Probability of H₁:** It's also *NOT* the probability that H₁ is true.
*   **Threshold α:** Alpha (α) is the *pre-determined threshold* for deciding if the evidence (p-value) is strong enough to reject H₀. It's the risk tolerance for a Type I error.
*   **Statistical vs. Practical Significance:** A very small p-value (statistically significant) doesn't automatically mean the effect is large or important in a real-world sense (practical significance). With very large sample sizes, even tiny, trivial differences can become statistically significant. Always consider the *effect size* (e.g., the actual difference in means, the correlation coefficient) alongside the p-value.
*   **Common Misinterpretations (Avoid in Vivas!):**
    *   *Wrong:* "The p-value is 0.03, so there's only a 3% chance the null hypothesis is true."
    *   *Correct:* "The p-value is 0.03. Assuming the null hypothesis is true, there's a 3% chance of observing a test statistic this extreme or more extreme due to random sampling variability. Since 0.03 < 0.05, we reject the null hypothesis."
    *   *Wrong:* "The p-value is 0.7, so we accept the null hypothesis."
    *   *Correct:* "The p-value is 0.7. Since 0.7 > 0.05, we fail to reject the null hypothesis. The data does not provide sufficient evidence to conclude the alternative hypothesis is true."

#### **3.5 Shapiro-Wilk Test**

*   **Concept:** A statistical test specifically designed to check if a sample of data likely originated from a *normally distributed population*. It's considered one of the most reliable normality tests, particularly effective for smaller sample sizes (where visual checks like histograms can be misleading).
*   **Use Cases:** Essential for verifying the *normality assumption* required by parametric tests like t-tests and ANOVA before applying them, especially with small samples. Helps decide if non-parametric alternatives are needed.
*   **Hypotheses:**
    *   **H₀:** The sample data follows a normal distribution.
    *   **H₁:** The sample data does *not* follow a normal distribution.
*   **Python Implementation (`scipy.stats.shapiro`)**

    *   **`shapiro(x)`**
        *   **Purpose:** Performs the Shapiro-Wilk test for normality on the input sample data.
        *   **Why/When Used:** To get a quantitative measure (p-value) assessing the likelihood that the sample data came from a normal distribution. Use *before* running tests that assume normality if you are unsure.
        *   **Input:**
            *   `x`: Array-like sample data.
        *   **Output:** `ShapiroResult` object containing `statistic` (W test statistic) and `pvalue`.

*   **Code Examples:**

    ```python
    from scipy.stats import shapiro

    np.random.seed(22)

    # Example 1: Data likely from a Normal distribution
    normal_data = np.random.normal(loc=50, scale=5, size=50) # Generate normal data
    print("\n--- Example 1: Shapiro-Wilk Test (Likely Normal) ---")
    # Visualize
    plt.figure()
    sns.histplot(normal_data, kde=True)
    plt.title('Histogram of Likely Normal Data')
    # plt.show()

    stat_norm, p_norm = shapiro(normal_data)
    print(f"Shapiro-Wilk Statistic: {stat_norm:.4f}, P-value: {p_norm:.4f}")
    if p_norm > 0.05:
        print("Result: Fail to reject H0 (p > 0.05). The data is likely normally distributed.")
    else:
        print("Result: Reject H0 (p <= 0.05). The data likely does NOT follow a normal distribution.")

    # Example 2: Data likely NOT from a Normal distribution (e.g., Uniform)
    uniform_data = np.random.uniform(low=0, high=10, size=100) # Generate uniform data
    print("\n--- Example 2: Shapiro-Wilk Test (Likely NOT Normal) ---")
    # Visualize
    plt.figure()
    sns.histplot(uniform_data, kde=True)
    plt.title('Histogram of Uniform (Non-Normal) Data')
    # plt.show()

    stat_unif, p_unif = shapiro(uniform_data)
    print(f"Shapiro-Wilk Statistic: {stat_unif:.4f}, P-value: {p_unif:.4f}")
    if p_unif > 0.05:
        print("Result: Fail to reject H0 (p > 0.05).")
    else:
        print("Result: Reject H0 (p <= 0.05). The data likely does NOT follow a normal distribution.") # Should reject

    # Example 3: Small sample size (where visual check is hard)
    small_maybe_normal = np.random.normal(loc=20, scale=3, size=12)
    print("\n--- Example 3: Shapiro-Wilk Test (Small Sample) ---")
    plt.figure()
    sns.histplot(small_maybe_normal, kde=True)
    plt.title('Histogram of Small Sample')
    # plt.show()

    stat_small, p_small = shapiro(small_maybe_normal)
    print(f"Shapiro-Wilk Statistic: {stat_small:.4f}, P-value: {p_small:.4f}")
    if p_small > 0.05:
        print("Result: Fail to reject H0 (p > 0.05). No significant evidence against normality.")
    else:
        print("Result: Reject H0 (p <= 0.05). Significant evidence data is non-normal.")
    ```

#### **3.6 Variance Inflation Factor (VIF)**

*   **Concept:** VIF measures how much the variance of an estimated regression coefficient is "inflated" because of **multicollinearity** in the model. Multicollinearity exists when independent variables (predictors) in a regression model are highly correlated with *each other*.
*   **Use Cases:** Specifically used as a diagnostic tool *after* fitting a multiple linear regression model (or similar models). It helps identify which predictor variables are problematically correlated with others, potentially making their individual coefficient estimates unstable and hard to interpret reliably.
*   **Calculation:** For a given predictor `Xᵢ`, VIF is calculated as `1 / (1 - R²ᵢ)`, where `R²ᵢ` is the R-squared value obtained by regressing `Xᵢ` against all *other* predictor variables in the model. A high `R²ᵢ` means other predictors can explain `Xᵢ` well, leading to a high VIF.
*   **Interpretation:**
    *   VIF = 1: No multicollinearity for that variable (uncorrelated with others).
    *   1 < VIF < 5: Moderate multicollinearity, often acceptable.
    *   VIF > 5 or VIF > 10: High multicollinearity, indicates potential problems with coefficient stability and interpretation. (Thresholds are rules of thumb).
*   **What to Do if VIF is High:** Consider removing one of the highly correlated predictors, combining them into a single index/feature, or using regularization techniques (like Ridge regression) that are less sensitive to multicollinearity.
*   **Python Implementation (`statsmodels`):**

    *   **`statsmodels.stats.outliers_influence.variance_inflation_factor(exog, exog_idx)`**
        *   **Purpose:** Computes the VIF for a specific predictor variable.
        *   **Why/When Used:** After designing your feature set for regression, calculate VIF for each predictor to check for multicollinearity *before* finalizing the model or interpreting coefficients.
        *   **Inputs:**
            *   `exog`: The design matrix (NumPy array or DataFrame) of predictor variables. **Crucially, this matrix MUST include a constant (intercept) term for VIF calculation to be correct.** Use `statsmodels.api.add_constant` to add one if it's not already present.
            *   `exog_idx`: The integer index of the predictor column in `exog` for which to calculate the VIF.
        *   **Output:** The VIF value (float) for the specified predictor.

*   **Code Examples:**

    ```python
    import pandas as pd
    import numpy as np
    import statsmodels.api as sm # For add_constant
    from statsmodels.stats.outliers_influence import variance_inflation_factor

    np.random.seed(123)
    n_samples = 100

    # Example 1: Low Multicollinearity
    print("\n--- Example 1: VIF Calculation (Low Collinearity) ---")
    X1 = np.random.rand(n_samples) * 10
    X2 = np.random.rand(n_samples) * 5 # Largely independent
    X_low = pd.DataFrame({'X1': X1, 'X2': X2})
    X_low_const = sm.add_constant(X_low) # Add constant for intercept

    print("Design Matrix (Low Collinearity):\n", X_low_const.head())

    vif_X1_low = variance_inflation_factor(X_low_const.values, 1) # Index 1 corresponds to X1
    vif_X2_low = variance_inflation_factor(X_low_const.values, 2) # Index 2 corresponds to X2

    print(f"VIF for X1: {vif_X1_low:.4f}")
    print(f"VIF for X2: {vif_X2_low:.4f}")
    # Expect VIF values close to 1

    # Example 2: High Multicollinearity
    print("\n--- Example 2: VIF Calculation (High Collinearity) ---")
    X1_high = np.random.rand(n_samples) * 10
    X3_high = X1_high * 2 + np.random.normal(0, 1, n_samples) # X3 strongly depends on X1
    X_high = pd.DataFrame({'X1': X1_high, 'X3': X3_high})
    X_high_const = sm.add_constant(X_high) # Add constant

    print("Design Matrix (High Collinearity):\n", X_high_const.head())

    vif_X1_high = variance_inflation_factor(X_high_const.values, 1) # Index 1 for X1
    vif_X3_high = variance_inflation_factor(X_high_const.values, 2) # Index 2 for X3

    print(f"VIF for X1: {vif_X1_high:.4f}")
    print(f"VIF for X3: {vif_X3_high:.4f}")
    # Expect high VIF values (likely >> 5 or 10)

    # Example 3: Calculating VIF for all predictors in a DataFrame
    print("\n--- Example 3: Calculating VIF for all Predictors ---")
    # Add another moderately correlated variable
    X4 = X1_high * 0.5 + X3_high * 0.3 + np.random.normal(0, 2, n_samples)
    X_multi = pd.DataFrame({'X1': X1_high, 'X3': X3_high, 'X4': X4})
    X_multi_const = sm.add_constant(X_multi)

    vif_data = pd.DataFrame()
    vif_data["feature"] = X_multi_const.columns
    # Calculate VIF for each predictor variable (index > 0)
    vif_data["VIF"] = [variance_inflation_factor(X_multi_const.values, i) for i in range(X_multi_const.shape[1])]

    print(vif_data)
    # Note: VIF for the constant is usually very high but irrelevant for assessing multicollinearity among predictors.
    print("\nInterpretation: Features with VIF > 5 or 10 suggest high multicollinearity.")
    ```

---

### **4. Probability Distributions**

*   **Conceptual Explanation:** A probability distribution is a mathematical function that describes the likelihood of different possible outcomes for a random variable. Understanding distributions is fundamental to modeling uncertainty and forms the basis of statistical inference. We often assume data follows a certain distribution (or check this assumption) to apply statistical tests or build models.
*   **Use Cases:** Modeling real-world phenomena (customer arrivals, measurement errors, success/failure counts), generating synthetic data, calculating probabilities for hypothesis testing (p-values are derived from the assumed distribution of the test statistic under H₀), risk modeling.

*   **4.1 Uniform Distribution**

    *   **Concept:** Every outcome within a specified range [`a`, `b`] is equally likely. The probability density function (PDF) is constant within the range and zero outside.
    *   **Use Case:** Modeling random guesses, simulations where all possibilities are equal (like rolling a fair die - discrete version), generating random numbers for sampling.
    *   **Python (`scipy.stats.uniform`, `numpy.random.uniform`)**

        *   **`stats.uniform(loc=a, scale=b-a)`:** Represents the continuous uniform distribution object. `loc` is the minimum value (`a`), `scale` is the *width* (`b-a`). Has methods like `.pdf(x)`, `.cdf(x)`, `.rvs(size)` (random variates).
        *   **`np.random.uniform(low=a, high=b, size=None)`:** Directly generates random numbers uniformly distributed between `low` (inclusive) and `high` (exclusive).

    *   **Code Examples:**

        ```python
        from scipy.stats import uniform

        a = 5 # min
        b = 15 # max
        width = b - a

        # Example 1: Probability Density Function (PDF) value
        print("\n--- Example 1: Uniform Distribution PDF ---")
        # PDF is 1/width within the range [a, b]
        print(f"PDF at x=7: {uniform.pdf(7, loc=a, scale=width):.2f} (Should be 1/{width}={1/10:.2f})")
        print(f"PDF at x=16: {uniform.pdf(16, loc=a, scale=width):.2f} (Should be 0)")

        # Example 2: Cumulative Distribution Function (CDF) value
        print("\n--- Example 2: Uniform Distribution CDF ---")
        # CDF(x) is the probability that a variable is <= x
        print(f"CDF at x=10: {uniform.cdf(10, loc=a, scale=width):.2f} (Halfway point, should be 0.5)")
        print(f"CDF at x=20: {uniform.cdf(20, loc=a, scale=width):.2f} (Past max, should be 1.0)")

        # Example 3: Generating Random Samples and Visualizing
        print("\n--- Example 3: Uniform Distribution Samples ---")
        uniform_samples = np.random.uniform(low=a, high=b, size=10000)
        plt.figure()
        sns.histplot(uniform_samples, bins=20, kde=False)
        plt.title(f'Histogram of Uniform Samples ({a} to {b})')
        plt.xlabel("Value")
        plt.ylabel("Frequency")
        # plt.show() # Expect a relatively flat histogram between a and b
        print(f"Sample mean: {uniform_samples.mean():.2f} (Expected: {(a+b)/2 = 10})")
        ```

*   **4.2 Normal Distribution (Gaussian / Bell Curve)**

    *   **Concept:** A continuous distribution characterized by its symmetric, bell shape. Defined by mean (µ, center) and standard deviation (σ, spread). Mean=Median=Mode. Crucial due to the **Central Limit Theorem (CLT)**, which states that the distribution of sample means tends towards normal as sample size increases, regardless of the original population distribution (given finite variance).
    *   **Use Cases:** Modeling many natural phenomena (heights, measurement errors), basis for Z-tests and t-tests (especially via CLT), financial modeling (though often with adjustments for heavier tails).
    *   **Python (`scipy.stats.norm`, `numpy.random.normal`)**

        *   **`stats.norm(loc=µ, scale=σ)`:** Represents the normal distribution object. `loc` is the mean (µ), `scale` is the standard deviation (σ). Methods include `.pdf()`, `.cdf()`, `.sf()` (survival function, 1-CDF), `.ppf()` (percent point function, inverse CDF or quantile function), `.rvs()`.
        *   **`np.random.normal(loc=µ, scale=σ, size=None)`:** Directly generates normally distributed random numbers.

    *   **Code Examples:**

        ```python
        from scipy.stats import norm

        mu = 100 # Mean
        sigma = 15 # Standard Deviation

        # Example 1: PDF and CDF values
        print("\n--- Example 1: Normal Distribution PDF/CDF ---")
        print(f"PDF at x=100 (mean): {norm.pdf(100, loc=mu, scale=sigma):.4f} (Highest point)")
        print(f"PDF at x=130 (2 std dev): {norm.pdf(130, loc=mu, scale=sigma):.4f}")
        print(f"CDF at x=100 (mean): {norm.cdf(100, loc=mu, scale=sigma):.2f} (Should be 0.5)")
        # P(X > 115) = 1 - CDF(115) = Survival Function(115)
        print(f"P(X > 115) = 1-CDF(115): {1 - norm.cdf(115, loc=mu, scale=sigma):.4f}")
        print(f"P(X > 115) = SF(115): {norm.sf(115, loc=mu, scale=sigma):.4f} (Same result)")

        # Example 2: Finding Quantiles (Inverse CDF) using PPF
        print("\n--- Example 2: Normal Distribution Quantiles (PPF) ---")
        # Value below which 95% of data lies (95th percentile)
        percentile_95 = norm.ppf(0.95, loc=mu, scale=sigma)
        print(f"95th Percentile value: {percentile_95:.2f}")
        # Value for Z=1.96 (standard normal)
        z_value_975 = norm.ppf(0.975, loc=0, scale=1) # Mean=0, StdDev=1 for standard normal
        print(f"Z-score for 97.5th percentile: {z_value_975:.2f} (Used for 95% CI)")

        # Example 3: Generating Samples and Visualizing
        print("\n--- Example 3: Normal Distribution Samples ---")
        normal_samples = np.random.normal(loc=mu, scale=sigma, size=10000)
        plt.figure()
        sns.histplot(normal_samples, bins=50, kde=True)
        plt.title(f'Histogram of Normal Samples (µ={mu}, σ={sigma})')
        plt.xlabel("Value")
        plt.ylabel("Frequency")
        # plt.show() # Expect a bell-shaped curve centered at mu
        print(f"Sample mean: {normal_samples.mean():.2f}, Sample std dev: {normal_samples.std():.2f}")
        ```

*   **4.3 Binomial Distribution**

    *   **Concept:** A *discrete* distribution modeling the number of "successes" (`k`) in a fixed number (`n`) of independent Bernoulli trials (each trial has only two outcomes, Success/Failure), with a constant probability of success (`p`) per trial.
    *   **Use Cases:** Calculating probability of getting k heads in n coin flips, number of defective items in a sample of n, number of converted users out of n visitors (A/B testing).
    *   **Python (`scipy.stats.binom`, `numpy.random.binomial`)**

        *   **`stats.binom(n, p)`:** Represents the binomial distribution object. Methods include `.pmf(k)` (Probability Mass Function - P(X=k)), `.cdf(k)` (P(X≤k)), `.sf(k)` (P(X>k)), `.rvs(size)`.
        *   **`np.random.binomial(n, p, size=None)`:** Directly generates random numbers representing the number of successes in `n` trials.

    *   **Code Examples:**

        ```python
        from scipy.stats import binom

        n_trials = 10 # e.g., flip a coin 10 times
        prob_success = 0.5 # e.g., probability of heads

        # Example 1: Probability Mass Function (PMF) - P(exactly k successes)
        print("\n--- Example 1: Binomial Distribution PMF ---")
        k_successes = 7
        prob_k = binom.pmf(k_successes, n=n_trials, p=prob_success)
        print(f"P(X={k_successes} successes in {n_trials} trials | p={prob_success}): {prob_k:.4f}")
        k_successes_2 = 5
        prob_k_2 = binom.pmf(k_successes_2, n=n_trials, p=prob_success)
        print(f"P(X={k_successes_2} successes): {prob_k_2:.4f} (Most likely outcome)")

        # Example 2: Cumulative Distribution Function (CDF) - P(at most k successes)
        print("\n--- Example 2: Binomial Distribution CDF ---")
        k_max_successes = 6
        prob_at_most_k = binom.cdf(k_max_successes, n=n_trials, p=prob_success)
        print(f"P(X <= {k_max_successes} successes): {prob_at_most_k:.4f}")
        # P(more than 8 successes) = P(X > 8) = 1 - P(X <= 8) = SurvivalFunction(8)
        prob_more_than_8 = binom.sf(8, n=n_trials, p=prob_success)
        print(f"P(X > 8 successes): {prob_more_than_8:.4f}")

        # Example 3: Generating Samples and Visualizing PMF
        print("\n--- Example 3: Binomial Distribution Samples & PMF Plot ---")
        binomial_samples = np.random.binomial(n=n_trials, p=prob_success, size=10000)

        plt.figure()
        # Calculate frequencies and normalize for probability
        values, counts = np.unique(binomial_samples, return_counts=True)
        sns.barplot(x=values, y=counts/len(binomial_samples), color='skyblue')

        # Overlay theoretical PMF
        k_values = np.arange(0, n_trials + 1)
        pmf_values = binom.pmf(k_values, n=n_trials, p=prob_success)
        plt.plot(k_values, pmf_values, 'ro-', label='Theoretical PMF')

        plt.title(f'Binomial Distribution PMF (n={n_trials}, p={prob_success})')
        plt.xlabel("Number of Successes (k)")
        plt.ylabel("Probability")
        plt.legend()
        # plt.show() # Expect bars centered around n*p = 5
        print(f"Sample mean: {binomial_samples.mean():.2f} (Expected: n*p = {n_trials*prob_success})")
        ```

*   **4.4 Poisson Distribution**

    *   **Concept:** A *discrete* distribution modeling the number of events occurring within a fixed interval of time, space, area, or volume, given a known average rate (`λ`, lambda) of occurrence. Events occur independently and at a constant average rate. Mean = Variance = λ.
    *   **Use Cases:** Modeling customer arrivals per hour, website errors per day, typos per page, number of calls to a support center, rare event occurrences. Can approximate Binomial when n is large and p is small (λ ≈ n*p).
    *   **Python (`scipy.stats.poisson`, `numpy.random.poisson`)**

        *   **`stats.poisson(mu=λ)`:** Represents the Poisson distribution object. `mu` is the average rate (λ). Methods: `.pmf(k)` (P(X=k)), `.cdf(k)` (P(X≤k)), `.sf(k)` (P(X>k)), `.rvs(size)`.
        *   **`np.random.poisson(lam=λ, size=None)`:** Directly generates random numbers from a Poisson distribution.

    *   **Code Examples:**

        ```python
        from scipy.stats import poisson

        lambda_rate = 5 # e.g., average 5 customer arrivals per hour

        # Example 1: PMF - P(exactly k events)
        print("\n--- Example 1: Poisson Distribution PMF ---")
        k_events = 3
        prob_k_poisson = poisson.pmf(k_events, mu=lambda_rate)
        print(f"P(X={k_events} events | λ={lambda_rate}): {prob_k_poisson:.4f}")
        k_events_2 = 5 # Most likely outcome (around lambda)
        prob_k_poisson_2 = poisson.pmf(k_events_2, mu=lambda_rate)
        print(f"P(X={k_events_2} events): {prob_k_poisson_2:.4f}")

        # Example 2: CDF - P(at most k events)
        print("\n--- Example 2: Poisson Distribution CDF ---")
        k_max_events = 7
        prob_at_most_k_poisson = poisson.cdf(k_max_events, mu=lambda_rate)
        print(f"P(X <= {k_max_events} events): {prob_at_most_k_poisson:.4f}")
        # P(more than 10 events) = P(X > 10) = SF(10)
        prob_more_than_10 = poisson.sf(10, mu=lambda_rate)
        print(f"P(X > 10 events): {prob_more_than_10:.4f}")

        # Example 3: Generating Samples and Visualizing PMF
        print("\n--- Example 3: Poisson Distribution Samples & PMF Plot ---")
        poisson_samples = np.random.poisson(lam=lambda_rate, size=10000)

        plt.figure()
        values_p, counts_p = np.unique(poisson_samples, return_counts=True)
        # Ensure we have bars for possible 0 counts if needed, find max k observed
        max_k_observed = values_p.max()
        all_k = np.arange(0, max_k_observed + 2) # Go a bit beyond max observed
        observed_freq = {val: count for val, count in zip(values_p, counts_p)}
        counts_full = [observed_freq.get(k, 0) for k in all_k]

        sns.barplot(x=all_k, y=np.array(counts_full)/len(poisson_samples), color='lightgreen')

        # Overlay theoretical PMF
        pmf_values_p = poisson.pmf(all_k, mu=lambda_rate)
        plt.plot(all_k, pmf_values_p, 'bo-', label='Theoretical PMF')

        plt.title(f'Poisson Distribution PMF (λ={lambda_rate})')
        plt.xlabel("Number of Events (k)")
        plt.ylabel("Probability")
        plt.legend()
        plt.xlim(-0.5, max_k_observed + 1.5) # Adjust x-axis limits
        # plt.show() # Expect bars centered around lambda = 5
        print(f"Sample mean: {poisson_samples.mean():.2f} (Expected: λ = {lambda_rate})")
        ```

---

### **5. Introduction to A/B Testing**

*   **Conceptual Explanation:**
    *   A/B testing (or split testing) is a controlled experiment used to compare two versions (Version A - Control, Version B - Variant) of a single variable (e.g., webpage design, email subject line, button color) to determine which performs better against a specific, measurable goal (metric).
    *   It's essentially a practical application of the **two-sample hypothesis testing** framework (often independent t-test for means or chi-squared/Z-test for proportions) in a real-world, often business or product development, setting.
    *   Users are randomly assigned to experience either version A or B, and their behavior related to the target metric (e.g., click-through rate, conversion rate, average purchase value) is tracked.

*   **Real-World Use Cases:** Optimizing website conversion rates, improving email open rates, testing effectiveness of different ad creatives, determining optimal pricing strategies, improving user engagement features in an app.

*   **Workflow:**
    1.  **Define Goal & Metric:** Clear objective (e.g., increase newsletter sign-ups) and measurable metric (e.g., sign-up rate per visitor).
    2.  **Hypotheses:** H₀: No difference in metric between A and B. H₁: Difference exists (or B is better/worse). Set α.
    3.  **Design:** Determine sample size (power analysis), randomization method, test duration.
    4.  **Run:** Deploy A and B, collect data.
    5.  **Analyze:** Calculate metrics for A and B. Perform appropriate hypothesis test (e.g., Chi-squared test for sign-up counts, t-test for average time spent). Get p-value.
    6.  **Conclude:** Compare p-value to α. Reject or fail to reject H₀. Make a decision based on statistical *and* practical significance.

*   **Python Implementation Concept:** The analysis phase uses the statistical tests covered earlier.

    *   **If Metric is a Proportion (e.g., Conversion Rate):**
        *   Data: Counts of successes (e.g., conversions) and total trials (e.g., visitors) for group A and group B.
        *   Test:
            *   Create a 2x2 contingency table: `[[conv_A, visitors_A - conv_A], [conv_B, visitors_B - conv_B]]`.
            *   Use `scipy.stats.chi2_contingency()` on this table.
            *   Alternatively, use `statsmodels.stats.proportion.proportions_ztest([conv_A, conv_B], [visitors_A, visitors_B])`.
    *   **If Metric is a Mean (e.g., Average Order Value):**
        *   Data: Arrays/Series of continuous values for group A and group B.
        *   Test: Use `scipy.stats.ttest_ind(group_A_values, group_B_values, equal_var=False)` (Welch's t-test).

*   **Code Example (Conceptual Walkthrough - Proportions using Z-test):**

    ```python
    from statsmodels.stats.proportion import proportions_ztest

    # Example Scenario: Testing button color change on conversion rate
    print("\n--- A/B Testing Example (Proportions Z-test) ---")

    # Data Collected:
    visitors_A = 1050  # Control group (e.g., blue button)
    conversions_A = 100

    visitors_B = 980   # Variant group (e.g., green button)
    conversions_B = 115 # Seems higher rate, but is it significant?

    # Hypotheses:
    # H0: Conversion Rate(A) = Conversion Rate(B)
    # H1: Conversion Rate(A) != Conversion Rate(B)
    alpha = 0.05
    print("H0: p_A = p_B, H1: p_A != p_B, alpha = 0.05")

    # Combine counts for the test function
    conversion_counts = np.array([conversions_A, conversions_B])
    visitor_counts = np.array([visitors_A, visitors_B])

    # Perform the Z-test for proportions
    z_stat_ab, p_value_ab = proportions_ztest(conversion_counts, visitor_counts, value=0, alternative='two-sided')

    print(f"\nConversion Rate A: {conversions_A/visitors_A:.4f}")
    print(f"Conversion Rate B: {conversions_B/visitors_B:.4f}")
    print(f"\nZ-statistic: {z_stat_ab:.4f}")
    print(f"P-value: {p_value_ab:.4f}")

    # Conclusion
    if p_value_ab < alpha:
        print("\nResult: Reject H0. There is a statistically significant difference in conversion rates between the two button colors.")
    else:
        print("\nResult: Fail to reject H0. There is no statistically significant difference in conversion rates.") # Depends on actual values
    ```

---

### **Key Takeaways - Unit V**

*   **Foundation:** Statistical analysis moves from *describing* samples (mean, std dev, plots) to *inferring* conclusions about populations using probability (hypothesis testing, distributions).
*   **Hypothesis Testing Core:** Formal process (H₀/H₁, α, test stat, p-value) to evaluate claims based on sample evidence. Small p-value (≤α) -> Reject H₀ (significant evidence for H₁).
*   **Test Selection is Crucial:** Use Z-test for known σ or large N means, t-tests (1-sample, 2-sample indep., paired) for unknown σ means (check normality!), Chi-squared tests (GoF, Independence) for categorical counts.
*   **Key Diagnostics:** Shapiro-Wilk checks normality assumption crucial for t-tests. VIF checks multicollinearity hindering interpretation in regression models.
*   **Probability Distributions:** Understand properties and uses of Uniform (equal likelihood), Normal (CLT, symmetric), Binomial (count of successes in n trials), and Poisson (count of events in interval) distributions. They underpin statistical inference.
*   **A/B Testing:** A practical, data-driven application of hypothesis testing (typically t-tests or proportion tests) to compare variants (A vs B) and optimize metrics based on statistical evidence.

---
