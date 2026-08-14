# ou-basketball-possession-analytics
Modeling player shot-creation execution ratings (SCER) against turnover metrics to isolate playmaking efficiency in college basketball.
# NCAA Basketball: Player Risk vs. Reward Efficiency Matrix
**Project By:** First year University of Oklahoma Industrial & Systems Engineering / Data Science Student

## Project Overview
This sports analytics model evaluates the offensive footprint of the Oklahoma Men's Basketball roster by framing individual playmaking as a system optimization problem. Traditional box-score metrics fail to capture the true value of a playmaker by ignoring hidden statistics and heavily double-counting errors. 

This model resolves those biases by establishing a custom **Shot Creation Execution Rating (SCER)** on the X-Axis and mapping it directly against **Asset Risk (Turnover %)** on the Y-Axis to build a comprehensive, two-variable system trade-off matrix. 

---

## The Mathematical Framework
To isolate pure shot-creation performance from ball-handling errors, this model intentionally excludes turnovers from the scoring-opportunity denominator and standardizes all box-score totals into precise per-game averages using total games played ($G$).

### Shot Creation Execution Rating (SCER) Formula:
$$SCER = \left( \frac{\frac{\text{PTS}}{\text{G}} + 2\left(\frac{\text{AST}}{\text{G}} \times 0.69\right) + 3\left(\frac{\text{AST}}{\text{G}} \times 0.31\right) + \left(0.15 \times 2 \times \text{Team FT%}\right)}{\frac{\text{FGA}}{\text{G}} + 0.44\left(\frac{\text{FTA}}{\text{G}}\right) + \frac{\text{AST}}{\text{G}} + 0.15} \right) \times 100$$


### Advanced Environmental Adjustments:
1. **The Assist Type Mix:** Assists are weighted using the team's historical field goal distribution, assuming an offensive execution profile of **69% 2-pointers** and **31% 3-pointers** for made assists.
2. **The Teammate Free-Throw Constant (Team FT):** To prevent individual passer bias, points generated from un-tracked Free Throw Assists are anchored to an absolute-referenced **Overall Team Free Throw Percentage** cell, assuming a teammate shoots the collective team baseline whenever they receive a pass leading to a foul.

---

## Visual Model & Scatter Plot

<img width="1653" height="1652" alt="OU Basketball Offensive Productivity matrix-2 jpg" src="https://github.com/user-attachments/assets/260207f6-ed4a-45ac-9cc5-b317e56bbd67" />

![Roster Risk vs Reward Matrix](<img width="1653" height="1652" alt="OU Basketball Offensive Productivity matrix-2 jpg - Copy" src="https://github.com/user-attachments/assets/cd8ab035-d4ac-4909-ab63-74d2a0d958b5" />)

---

## Key Analytical Insights & Data Auditing

* **The Floor General Anchor (High Reward / Low Risk):** Point guard Nijel Pack anchors the elite quadrant of the system, showcasing a world-class **145.08 SCER** while maintaining an incredibly secure **12.00% Turnover Rate**, proving massive efficiency under high volume.
* **System Uniformity:** The core rotation exhibits a highly optimized system alignment, clustering tightly between an elite **130.00 and 146.00 SCER** baseline, showing no severe drop-off in output efficiency during bench rotations.
* **The Operational Bottleneck:** The roster features two clear statistical floor anomalies at **100.92 SCER** and **97.09 SCER**, pointing to a clear tracking bottleneck where possessions halt significantly compared to team performance.
* **Auditing Low-Volume Outliers:** Initial data passes generated an artificial **151.32 SCER** for a bench reserve. A root-cause error analysis revealed that near-zero per-game denominators float statistical outputs in small sample sizes. Standardizing the free-throw points metrics helped resolve the scaling skew without requiring artificial volume gates. The high **SCER** value could suggest the player is being underutilized. 

---

## Sources & Acknowledgments

* **Roster Statistics:** Raw metrics and data profiles compiled via [Sports-Reference College Basketball](https://sports-reference.com).
* **Free-Throw Assist Tracking:** The $0.15$ per-game Free Throw Assist volume constant was derived from NBA tracking parameters provided by [HoopsJunkie.io](https://hoopsjunkie.io), mathematically scaled down to adjust for collegiate game-duration and possession-pace differentials.
* **Theoretical Foundations:** Core tracking principles and the $0.44$ free-throw possession multiplier are based on frameworks pioneered by Dean Oliver in *Basketball On Paper*.
