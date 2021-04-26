# ✨ So you want to sponsor a contest

This `README.md` contains a set of checklists for our contest collaboration.

Your contest will use two repos:
- **a _contest_ repo** (this one), which is used for scoping your contest and for providing information to contestants (wardens)
- **a _findings_ repo**, where issues are submitted, triaged, and deduped, responded to, etc.

Ultimately, when we launch the contest, this contest repo will be made public and will contain the smart contracts to be reviewed and all the information needed for contest participants. The findings repo will be made public after the contest is over and your team has mitigated the identified issues.

Some of the checklists in this doc are for **C4 (🐺)** and some of them are for **you as the contest sponsor (⭐️)**.

---

# Contest prep

## ⭐️ Sponsor: Contest prep
- [x] Modify the bottom of this `README.md` file to describe how your code is supposed to work with links to any relevant documentation and any other criteria/details that the C4 Wardens should keep in mind when reviewing
- [x] Add all of the code to this repo that you want reviewed.
- [x] Make sure your code is thoroughly commented using the [NatSpec format](https://docs.soliditylang.org/en/v0.5.10/natspec-format.html#natspec-format).
- [ ] Create a PR to this repo with the above changes.
- [ ] Please have final versions of contracts and documentation added/updated in this repo **no less than 8 hours prior to contest start time.**
- [x] Ensure that you have access to the _findings_ repo where issues will be submitted.
- [ ] Review the sponsor docs in the findings repo for your role in the judging process.
- [ ] Delete this checklist and all text above the line below when you're ready.

---

# Based Loans contest details
- $30k USDC main award pot
- Join [C4 Discord](https://discord.gg/EY5dvm3evD) to register
- Submit findings [using the C4 form](https://c4-basedloans.netlify.app/)
- [Read our guidelines for more details](https://code423n4.com/compete)
- Starts 2021-04-29 00:00:00 UTC
- Ends 2021-05-04 23:59:00 UTC

This repo will be made public before the start of the contest.

[ ⭐️ SPONSORS ADD INFO HERE ]

Based Loans is fork of Compound. In theory it should inherit Compound's security. However, any change made to smart contracts can introduce a critical bug. To make it easier for auditors, below is a summary of changes. Be aware that these are not all changes. Do code diff with compound contract to see all changes made.

If you are not familiar with Compound, feel free to read their documentation https://compound.finance/docs
Compound's original code is here: https://github.com/compound-finance/compound-protocol/tree/master

Changelog:
- `doTransferOut` function in `CEther.sol`
- Renamed `Comp.sol` to `Blo.sol`. Be aware that renaming was made only in few places. Across the code, you'll see variables and functions referencing `blo` and `comp` so keep in mind, it means the same thing (token).
- `UniswapAnchoredView.sol` contract
- `UniswapConfig.sol` contract
- `CErc20Immutable.sol` and `CToken.sol` contracts - mostly function visibility to accommodate new TWAP oracle with on-fly price updates
- `_setCompAddress` function in `Comptroller.sol` - new setter and corresponding storage changes in `ComptrollerStorage`
- Moved `doTransferOut` after storage update in `CToken.sol` for:
    - `_reduceReservesFresh`
    - `redeemFresh`
    - `borrowFresh`
