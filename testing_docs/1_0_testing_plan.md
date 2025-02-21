# Test Plan 

#### links to related docs

- [Test Plan](./1_0_testing_plan.md)
- [HFvZ Setup](../README.md)
- [Phase 1 Testing Details](./1_1_phase_testing_details.md)
- [Intro to RAVEs (Three Layers)](./1_2_three_layers_of_raves.md)
- [Sample Code for Creating RAVEs](./rave_templates)
- [Feedback](https://github.com/orgs/unytco/projects/5/views/1)

#### Test Plan Phase 1: Basic Features, UI/UX Feedback
1. Why we are asking Partners to do testing
2. Test Plan
3. Feedback

### 1. Why we are asking Partners to do testing: 

Unyt Co tools are all built with automated unit testing and reliability testing, and Holochain is continually expanding their performance testing. So we’re not seeking functional testing, but we are looking for feedback about:

*  **UX and UI usability** for what could be a complex or confusing process for end-users and/or project administrators. 
* **Configurability to the needs and functions of your project**. We have gone from HoloFuel as a single-function currency, to one that must be able to function in a variety of ways. We need to make sure it functions how you need it to, because we can’t predict all those variants.
* **White Label / Branding dynamics**: We expect projects to customize some of the appearance of the interfaces to match their branding and we want to make sure we’ve made that work for your project.
* **Value Workflow**: You need to make sure the complete value flows work for your customers and service providers. Some questions you should consider: Do your customers have an appropriate way in? (They may already need to hold your token to buy internal units.) Do your service providers have a sensible way to prove the value they’re providing? Do they have a clear way to cash out of the internal units to your token? Are there any other value transfers needed, if so, can those be completed reasonably easily?
* **Administrative Workflow questions** to ask yourself: Do your technical people understand how to update your configuration? Can they do so successfully? What high level reports do you need to be able to see?

### 2. Test Plan

Phase 1: Basic Features & UI/UX Feedback
Start: January 29, 2025
Duration: 2-3 weeks

Test usability of the full range of basic transactional functionality

- [ ] set up new users / accounts (3?)
- [ ] send/receive via normal transactions, including credit limit enforcement and deduction of transaction fees
- [ ] send/receive via RAVEs, including credit limit enforcement and deduction of transaction fees
- [ ] Use conditional logic RAVEs (e.g. conditional forward / non-custodial escrow)

At present we expect to have a total of four phases of testing, each lasting about 2-3 weeks.

### 3. Feedback
We have set up this [feedback board](https://github.com/orgs/unytco/projects/5) for adding and tracking bugs, feature requests and other feedback. If you haven't yet done so, please share your github handle with us via our shared Telegram or Signal thread so that you can have access to that board.

If you haven't already, check out [Intro to RAVEs (Three Layers)](./1_2_three_layers_of_raves.md)