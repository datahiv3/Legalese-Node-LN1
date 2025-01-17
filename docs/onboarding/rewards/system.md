# Reward System

The DataHive network implements a robust reward system to incentivize node operators for their performance, contribution, and long-term commitment. This document provides an overview of the reward structure, eligibility criteria, and calculation methodology.

---

## Reward Components

1. **Base Task Rewards**:
   - Earned for completing indexing, validation, and consensus tasks.
   - The reward amount depends on the task complexity and node tier.

2. **Performance Bonuses**:
   - Additional rewards based on metrics such as uptime, task completion, and validation accuracy.

3. **Staking Rewards**:
   - Distributed proportionally to the number of tokens staked.
   - Boosted by higher tiers and consistent performance.

4. **Achievement Bonuses**:
   - Awarded for reaching milestones such as top leaderboard rankings or special event participation.

5. **Network Contribution Multipliers**:
   - Nodes with high contribution scores receive reward multipliers to increase their earnings.

---

## Reward Eligibility

| **Criterion**             | **Requirement**                          |
|---------------------------|------------------------------------------|
| Task Completion Rate      | >98%                                     |
| Validation Accuracy       | >99%                                     |
| Uptime                   | >99.9%                                   |
| Staking Amount           | Meets or exceeds the tier minimum        |
| Contribution Score       | Above network average                    |

*Note: Nodes failing to meet these criteria may experience reduced rewards or temporary suspension from task allocation.*

---

## Reward Multipliers

| **Performance Tier** | **Multiplier** |
|----------------------|-----------------|
| Top 10%             | 3.0x           |
| Top 25%             | 2.5x           |
| Top 50%             | 2.0x           |
| Remaining           | 1.0x           |

---

## Calculation Methodology

Rewards are calculated using the following formula:

```
Reward = Base Task Reward + (Performance Bonus × Multiplier) + Staking Rewards
```

- **Base Task Reward**: Fixed for each task based on tier and complexity.
- **Performance Bonus**: Calculated using key metrics such as uptime, accuracy, and completion rates.
- **Staking Rewards**: A percentage of the total network staking pool distributed proportionally to individual stakes.

---

## Monitoring Rewards

- Use the [dashboard](/docs/onboarding/dashboard.md) to track earnings in real-time.
- View detailed reports on:
  - Task rewards
  - Staking yields
  - Bonus breakdowns

---

## Special Event Rewards

1. **Leaderboard Competitions**:
   - Operators ranked in the top 10% receive exclusive badges and bonus rewards.

2. **Seasonal Campaigns**:
   - Limited-time events offering increased rewards for specific tasks or milestones.

3. **Referral Rewards**:
   - Incentives for referring new operators to the network.

---

## Penalties and Deductions

1. **Performance Penalties**:
   - Metrics below thresholds result in reduced rewards.

2. **Early Unstaking Penalty**:
   - A percentage deduction applies to tokens unstaked before the lock-in period ends.

3. **Non-Compliance**:
   - Violations of network rules may lead to forfeiture of rewards and suspension.

---

## Tips for Maximizing Rewards

1. Maintain high [performance metrics](/docs/onboarding/performance/metrics.md).
2. Stake additional tokens to boost staking rewards.
3. Regularly monitor your [network contribution score](/docs/onboarding/network/contribution.md).
4. Actively participate in governance for additional bonuses.

---

Join the DataHive network today by registering at the [DataHive Node Registration Portal](https://www.datahive.network/nodes) and start earning rewards as a node operator.
