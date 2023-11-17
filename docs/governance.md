# RWF2 Foundation Governance

**This is a proposal for a future governance model for the RWF2. It is not
presently active and may never be.**

## Goals

Membership in the RWF2 seeks to simultaneously encourage:

  * Diversity in progressing project milestones (the "bus factor").
  * External stewardship of the foundation and project.
  * Financial contributions.

In determining how to structure RWF2 membership, we specifically seek to avoid:

  * A pay-to-play model where financial contributions correlate directly with
    project direction.

## Member Responsibilities

Members of the RWF2 carry the following responsibilities and privileges:

  * Ability to vote on RFCs: major changes to RWF2 projects or processes.
  * Ability to vote on uGrant application approval.
  * Ability to vote on contentious pull requests.
  * Ability to promote on RWF2 properties.

## Membership Classes

The ability to dictate the direction of RWF2 and its projects is distributed
amongst members of the three groups: the board, team leads, and regular
contributors. Direction is effected through voting processes. A majority vote
(≥ 51%) is always required to pass a vote. Individuals may be members of more
than one class.

  * **Board**

    The board is primarily responsible for executive decisions pertaining to
    foundation and project direction and funds management. Membership in the
    board is either direct, by election of existing board members, or
    representation corresponding to contribution tiers.

  * **Team Lead**

    Leads of development teams are automatically members of the foundation. Team
    leads are always appointed by existing team leads, or in their absence,
    contributors.

  * **Contributor**

    Any individual who has contributed to any RWF2 project is automatically
    granted membership for a period of 30 days from their last contribution.

In addition, the **President of the Board** presides over the foundation with
the singular additional power of breaking ties. The president is elected.

## Voting

Members vote on RFCs, uGrant application, contentious pull requests, and team
leads. Voting power is distributed among member classes to ensure that 1) no
group can unilaterally control any process, and 2) the absence of all members of
any one group does not stall progress.

The table below summarizes voting power distribution.

| Member Class    | RFC Vote | uGrant Vote | PR Vote | Team Lead Vote |
|-----------------|----------|-------------|---------|----------------|
| **Board**       | 40%      | 40%         | 0%      | 0%             |
| **Team Lead**   | 40%      | 40%         | 60%     | 100%*          |
| **Contributor** | 20%      | 20%         | 40%     | 0%*            |
| Total           | 100%     | 100%        | 100%    | 100%           |

<small>*Team leads for a given team are appointed by existing leads for that
team. In their absence, contributors may vote.</small>

## Board Composition

The board is composed of _direct members_, which are elected by the existing
board, and _contribution members_, which are granted to individuals and entities
who maintain the corresponding level of financial sponsorship.

The board's vote is calculated as follows:

```
50% Direct + 50% [(Bronze + 2 * Silver + 5 * Gold + 10 * Diamond) / Contribution Shares]

Direct = # Direct Votes / # Direct Members

Bronze = # of Bronze Contribution Votes
Silver = # of Silver Contribution Votes
Gold = # of Gold Contribution Votes
Diamond = # of Diamond Contribution Votes

Contribution Shares = Total Number of Outstanding Contribution Shares
```

The table below summarizes this voting strategy:

|              | Direct | 🥉 Bronze        | 🥈 Silver           | 🥇 Gold        | 💎 Diamond     |
|--------------|--------|------------------|---------------------|----------------|----------------|
| Contribution | N/A    | $50/month        | $100/month          | $250/month     | $500/month     |
| Perks        | N/A    | [rwf2.org] promo | + [rocket.rs] promo | + release note | + monthly call |
| Vote Shares  | 50%    | 1                | 2                   | 5              | 10             |

[rwf2.org]: https://rwf2.org
[rocket.rs]: https://rocket.rs

# Open Questions

 * **Does the above meet the outlined goals and non-goals?**

 * **How do we automate and manage these processes?**

   We want _everything_ to be public. GitHub + robots + mirroring on rwf2.org
   seems like the obvious answer.
