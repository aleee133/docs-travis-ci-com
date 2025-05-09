---
title: Billing FAQ
layout: en
permalink: /user/billing-faq/

---

> Please see our **[Billing overview](/user/billing-overview/)** first.

## How can I get on an annual plan?

You can select one of the available annual plans via [Your Account->Settings->Plan](https://app.travis-ci.com/account/plan) page. The customised annual-based plans are available by contacting the Travis CI support team.

## How can one get on a Usage-based Plan?

The usage-based plan is available either on [Your Account->Settings->Plan](https://app.travis-ci.com/account/plan) page or by contacting the Travis CI Support team.

## How are the credits deducted?

The credits will be deducted from the credits pool after each build job is executed depending on the operation system used, VM type.

## How can I check how much I will pay for user licenses at the end of the month?

The unique users triggering builds within a month will constitute a number of actual user licenses consumed, and the payment method depends on whether the usage-based plan is a subscription or not.

To check how much active users you got during the last billing cycle you may generate a report for selected time period on your [Plan Usage](https://app.travis-ci.com/account/plan/usage) page or contact the support.
Travis CI also offers the user management functionality where you can:

* See how many users have the right to trigger the build.
* See how many were active or triggered the build during the last month.
* Select the users who can trigger the build.

This is available under each repository setting (in the https://app.travis-ci.com/{vcs provider identifier}/{your account name}/{repository name}/settings ) as a 'User Management' button.

For a subscription usage based plan, there are several flexible scenarios possible. See our [Billing overview](user/billing-overview/#usage---user-licenses).

For non-subscription usage based plan, at the end of the billing period, the total count of unique users triggering builds will be charged according to the rates in a selected plan.

By default Travis CI system provides the possibility to trigger a build to all members of your team on GitHub, Bitbucket, GitLab and Assembla who have writing rights on repositories.

If the team member has not triggered the build during the billing period, Travis CI will not charge you for that user.


## What if I am building open source?

Travis CI may grant an amount of special OSS credits per month assigned to run builds only on public repositories. To find out more about it, please [contact the Travis CI support team](mailto:support@travis-ci.com). In the email, please include:

* Your account name and your VCS provider (like travis-ci.com/github/[your account name] )
* How many credits (build minutes) you’d like to request (should you run out of credits again, you can repeat the process to request more or to discuss a renewable amount)


## How do I use credits?

You can use your credits to run builds on your public and private repositories.
You may have been assigned an amount of OSS credits to run builds on public repositories. When you run out of OSS credits but want to keep building on public repositories, you can go to the Plan page and turn the Credits consumption for OSS switcher to `On`. In this case,  once the ‘OSS credits’ pool is depleted, the system starts deducting from the ‘paid credits’ pool. Builds for OSS repositories will be allowed to start and will be deducted from the paid credits.

## How do I recharge my credit balance?

You can buy additional build credits anytime you need them by clicking on your profile icon in the upper right corner of the screen =>Settings, navigate to the Plan page, and press the ‘Buy add-ons’ button. You may also enable the [auto-refill](/user/billing-autorefill/) feature.
Please be advised that it is not possible to buy additional credits on a Free Plan.


## Do credits expire?

Credits which you purchase or obtain as a part of the free Plan do have an expiry date. Please check your [Plan Usage](https://app.travis-ci.com/account/plan/usage) page.

## Can you send me an invoice?

The invoice is sent automatically by the Travis CI system after the Plan purchase or subsequent charge is made.

## How do I cancel my paid plan?

If you want to cancel your paid plan, please contact our support. 

Travis CI's free Trial Plan provides 10,000 build credits to try out public and private repositories builds and unlimited users at no charge. Once you use up all credits or they expire, simply do not select any other plan.
If you want your account to be deleted, please contact the Travis CI support.


## Do these prices include tax?

No, not all prices include tax.

## Can I sign up for automatic renewals for Usage-based Plans?

Yes. Please select a usage-based plan, which is a periodical subscription, or contact the support.

You may also manually buy credits each time you are about to run out of them or enable the [auto-refill](/user/billing-autorefill/) functionality on your Plan page, which will refill your credits every time it drops below a certain threshold. Concurrency-based plans are not subject to auto-refill.

To help you track the build credit consumption, the Travis CI system will send notification emails each time your credit balance is used up by 50, 75, or 100%.


## Are add-ons limited to a certain number of users?

You can buy additional add-ons at any time you feel they are needed. You and your organization’s members can use the purchased add-ons without limitations.

## Why is my credit balance negative?

Your last build probably cost more than you had available in your credit balance. You won't be able to run any builds until your balance becomes positive. Replenish your credits (the negative balance will be deducted upon arrival of new credits creating new balance - see our [billing overview](/user/billing-overview/#negative-credits).

## Why am I asked for credit card details upon selecting a free Trial Plan?

Due to continued abuse of our free service and in order to make environment more secure and with fair access to shared infrastructure, Travis CI decided to introduce credit card validation step for every new user. There will be a small fee placed on your card in order to authorize the account and it will be returned after several days.


## How can I get additional credits when signed up for a manual payment plan?

Please contact the [Support team](mailto:support@travis-ci.com) for more information on acquiring additional credits on a manual payment plan.

