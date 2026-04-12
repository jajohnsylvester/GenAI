Prasanjit Paul’s How to Avoid Loss and Earn Consistently in the Stock Market is a guide centered on the "WIN" (Workable Investment Strategy) approach, focusing on long-term wealth creation through fundamental analysis and emotional discipline.

Based on the Table of Contents from Prasanjit Paul’s book, here are the key takeaways organized by the specific chapters shown in your image.

The core philosophy revolves around Fundamental Analysis and Risk Mitigation.
1. How to Avoid Loss in the Stock Market?

    Avoid "Hot" Tips: Don't buy based on rumors or news channel recommendations.

    Long-term Horizon: Real wealth is created over 5–10 years, not by day trading.

    Capital Preservation: Before looking at profits, ensure your principal is safe by avoiding high-debt or low-quality companies.

2. Stock Market is Not Risky at All

    Knowledge Over Chance: Risk comes from not knowing what you are doing. If you treat stocks like a business investment, the risk drops significantly.

    Volatility ≠ Risk: Temporary price drops are market noise; real risk is the permanent loss of capital due to poor business fundamentals.

3. First Step of Picking Winning Stocks

    Financial Health: Focus on companies with consistent sales and profit growth.

    Debt-Free Focus: High debt is the biggest reason for company failure; prioritize companies with zero or minimal debt.

    High Return on Equity (ROE): Look for businesses that can generate at least 15-20% ROE consistently.

4. How to Evaluate Management?

    Integrity: Check if management has a history of cheating minority shareholders.

    Skin in the Game: High promoter holding (usually >50%) suggests the owners believe in the business.

    Salary vs. Profits: Management should take a reasonable salary, not drain the company's cash.

5. Valuation – It Matters Much

    P/E Ratio: Don't buy a great company at an astronomical price.

    Margin of Safety: Always buy at a price that offers a "cushion" in case your growth assumptions are slightly off.

6. When to Buy and When to Sell?

    Buy: When the market is fearful or when a company's earnings growth is accelerating but the price hasn't caught up yet.

    Sell: Only if management integrity is questioned, the business model breaks, or the stock becomes extremely overvalued (bubble territory).

7. Do’s and Don’ts to Avoid Loss

    Don't Average Down: Avoid adding more money to a "falling knife" stock where the business is failing.

    Do Keep it Simple: You don't need complex derivative strategies to make money.

8. How to Construct Your Portfolio?

    Concentrated Diversification: Hold between 15 to 25 stocks. Too many stocks (over-diversification) makes it impossible to beat the index.

    Weightage: Allocate more to your high-conviction "Blue Chip" companies.

9. Is it Required to Follow an Equity Advisor?

    Self-Reliance: You can do better than most advisors if you learn the basics of reading a Balance Sheet and Profit/Loss statement.

    Hidden Agendas: Be wary of advisors who earn commissions on your trading frequency.

10. Quick Formula for Picking Winning Stocks

    The "Paul" Checklist: 1.  Debt-to-Equity < 0.5.
    2.  Promoter holding > 50% (unpledged).
    3.  Consistent Profit growth for 5 years.
    4.  Market Leader in its niche.

11. Little Bit of Myself – Important Lessons

    Learn from Mistakes: Every loss is a tuition fee paid to the market; analyze why you lost money to avoid repeating it.

    Consistency: Systematic, disciplined investing beats brilliant but sporadic flashes of luck.

Based on the "Quick Formula" by Prasenjit Paul detailed in your images, I have translated the criteria into a functional query for **Screener.in**.

The formula consists of a primary screening stage (efficiency, debt, and growth) followed by secondary checks for valuation and price momentum.

### **Screener.in Query**
Copy and paste the following into the "Query" box on the Screener.in "Create New Screen" page:

```sql
Average return on equity 3Years > 20 AND 
Average return on capital employed 3Years > 20 AND 
Debt to equity < 1 AND 
Pledged percentage < 10 AND 
Sales growth 3Years > 10 AND 
Profit growth 3Years > 12 AND 
Price to Earning < (2 * EPS growth 3Years) AND 
Return over 3years > 10 AND 
Return over 1year > 0
```

---

### **How the Query Maps to the Images**

The query is structured to filter stocks only if they meet **all** the requirements from your provided steps:

#### **Stage 1: Primary Screening (Step 1.jpeg)**
* **ROE & ROCE:** `Average return on equity 3Years > 20` and `Average return on capital employed 3Years > 20`.
* **Debt:** `Debt to equity < 1` (This targets the last financial year as requested).
* **Promoter Pledge:** `Pledged percentage < 10` (Filters for low risk of promoter interference).
* **Growth:** `Sales growth 3Years > 10` and `Profit growth 3Years > 12`.

#### **Stage 2: Valuation (Step 2.jpeg)**
* **P/E vs. Growth:** `Price to Earning < (2 * EPS growth 3Years)`. This ensures you aren't paying more than double the earnings growth rate.

#### **Stage 3: Price Movement (Step 3.jpeg)**
* **Momentum:** `Return over 3years > 10` and `Return over 1year > 0`. This filters out "Avoid" stocks that have negative returns or stagnating 3-year performance.

### **Pro-Tips for Using This Query:**
1.  **Strictness:** This is a very high-quality filter. Because it requires a stock to be both high-growth (12%+ profit) and high-efficiency (20%+ ROE), you may only find a handful of stocks in the entire market that qualify at any given time.
2.  **Customization:** If you get zero results during a market downturn, you might slightly lower the `Pledged percentage` to `0` (which the author suggests is "better") or check if the `EPS growth` is being calculated over a specific period you prefer.

------------------------------------

To replicate the **"2 Minutes Check-up"** logic from the book on **Screener.in**, you can use the following query. 

This query is designed to flag companies that meet the "red flag" criteria mentioned in your images.

### The Screener.in Query

```sql
Average return on equity 3years < 10 AND
Debt to equity > 1 AND
Pledged percentage > 30
```

---

### How to use this and interpret the results
Based on the logic in the book "How to Avoid Loss and Earn Consistently in the Stock Market," here is how you should handle the results generated by this query:

* **If a stock appears in the results:** It meets all 3 negative criteria. According to the text, you should **"avoid the stock at any cost"** or exit if you already hold it.
* **To find "Safe" stocks:** If you want to find stocks that are the *opposite* of these red flags (i.e., healthy companies), use this inverted query instead:
    ```sql
    Average return on equity 3years > 15 AND
    Debt to equity < 1 AND
    Pledged percentage == 0
    ```

### Breakdown of the Parameters
1.  **Average ROE (3 Years) < 10%:** This identifies companies that have consistently struggled to generate efficient profits from shareholders' capital over a medium-term period.
2.  **Debt to Equity > 1:** This filters for companies that are "leveraged," meaning they owe more to lenders than they own in equity. 
3.  **Pledged Percentage > 30%:** This is a major warning sign in the Indian market. It means the promoters have used more than 30% of their shares as collateral for loans, which puts the stock at risk of a forced sell-off if prices drop.

### A Note on Limitations
As the second page of your upload mentions, this screener will automatically exclude **turnaround companies**. While some of those companies might eventually become profitable, the author suggests that since only 20-30% of turnarounds succeed, it is safer for most investors to simply stay away and stick to high-quality companies.

----------------------------------------

Last Chapter :

Based on the investment principles of Prasenjit Paul from his book *How to Avoid Loss and Earn Consistently in the Stock Market*, here are the specific Screener.in queries you can use.

### **1. Stocks to Avoid (The "Negative" List)**
According to the "Investment Pledge to avoid loss" (Page 221-222), you should **not** invest if **any** of these conditions are true. In Screener, use the `OR` operator to find these risky stocks:

```sql
Average return on equity 5Years < 12 OR
Debt to equity > 1 OR
Price to Earning > (Profit growth 3Years * 2) OR
Pledged percentage > 30
```

* **Logic:** This flags companies with poor efficiency, high debt, extreme overvaluation relative to growth (PE > 2x Growth), or high promoter risk.

---

### **2. Stocks to Buy (The "Selection" List)**
According to the "Investment Bet" criteria (Page 222), a stock is only considered if **all** of these parameters hold true. In Screener, use the `AND` operator:

```sql
Average return on equity 3Years > 18 AND
Debt to equity < 1 AND
Average return on equity 5Years > 10 AND
Price to Earning < (Profit growth 3Years * 2) AND
Pledged percentage < 10
```

* **Refinement:** The text mentions an "Average growth rate during last 5 years more than 10%." While Screener doesn't have a single button for 5-year average growth, you can use `Sales growth 5Years > 10` or `Profit growth 5Years > 10` to satisfy this condition.

---

### **Quick Guide to the Variables Used:**
| Book Criteria | Screener.in Variable |
| :--- | :--- |
| **ROE** | `Average return on equity 5Years` / `3Years` |
| **Debt to Equity** | `Debt to equity` |
| **P/E vs Growth** | `Price to Earning` vs `Profit growth 3Years` |
| **Promoter Pledge** | `Pledged percentage` |

**Pro-Tip:** When using the "Buy" screener, you might also want to add `Market Capitalization > 500` (or any value you prefer) to filter out extremely small micro-cap stocks that can be highly volatile regardless of their ratios.
