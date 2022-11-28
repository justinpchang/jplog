---
layout: post
title: "Budget app beginnings"
date: 2022-11-28 12:44:00 -0500
---

# Budget app beginnings

My general wish for this blog is to be a space where I am forced to flesh out my thoughts. During my time in college, I found that writing is the best method for thinking deeply, and I'm also hoping that the push to publish it on a public site will augment the benefit of just writing for myself. I don't really care who is reading it; in fact, I consciously am never going to add engagement features like liking, sharing, commenting, etc., so that I never have to think about who is reading. There just has to be the possibility that somebody could be reading so that I can orient my voice to the general reader.

It's fitting, then, that my first *real* post (disregarding the Hello World test post that seems to be a requirement for all developer blogs) is an attempt to concretize my ideas about my current side project.

## Motivation

There seem to be two veins of personal budgetting apps, where the primary differentiator is the level of manual control given to the user:

- Hands-off apps: Auto-pulls transactions from your various cards and bank accounts, auto-categorizes them, auto-budgets. Examples: Mint Mobile [1].

- Hands-on apps: Manual entering of transactions, manual categorization, manual analysis. Examples: Plaintext accounting [2].

I've experimented with both hands-off and hands-on apps, and I find that I lean towards the lattern. I probably leans towards hands-on, minimal computer intervention apps for all uses, despite my profession as a software developer. This will be another blog post for another day, but, briefly, I think that apps shouldn't get too smart: they should be optimizing our daily workflows without ever taking away control. Once these hands-off apps start guessing how much you should be spending based on how much you spent in previous apps, I get uncomfortable, and I think you should, too. Security is another concern with the hands-off apps; do I really want Ryan Reynolds, owner of Mint Mobile, to own all my transaction data, all the credentials to my financial accounts, and already compiled analytics of my personal spending happens? Hell, no.

So, I favor the hands-off apps. The lineage of these apps can be traced back to the most manual accounting that you can do: a hand-written ledger. This is honestly a really good solution in the face of all the high tech solutions that the industry is churning out. It's incredibly secure (depending on your ability to not misplace the notebook), categorization is as easy as physical filing, and the actual act of writing in a transaction gives more meaning to using money in a world where I can spend thousands of dollars at once with the swipe of a little plastic card. The downsides of this approach are that it's hard to run analysis of your spending habits without either fast calculator skills or entering all of the data into a computer, and that you have to either lug around your budgetting notebook or the receipts of your daily transactions in order to log them by hand. This has led many to use spreadsheet software as their budgeting apps, and this, too, is a great solution that solves both of the downsides of the hand-written ledger.

I've been experimenting with Google Sheets for a few months, and it seems to be an almost-perfect approach. You get all of the benefits of the hand-written ledger outlined above, and you also get as many analysis reports as your data-loving heart wishes through the spreadsheet formula language, which became Turing complete last year [3]. Now, the only downside (oh, those pesky downsides) is that spreadsheet software works like absolute hot garbage on mobile platforms. The benefit of having a virtual ledger is that I can access it from anywhere, but the dismal UX of mobile spreadsheet apps means I never want to actually open the Google sheets app (why is startup so slow??) and enter in my data after zooming-in and out trying to find where I am in the sheet.

## Enter, Moolah (name pending)

The purpose of my budget app tries to improve on the options detailed above by including all the analytics wins from using spreadsheet formulas, while solving for the data entry problem by having a mobile-first app design for transaction viewing and entry. It's a very simple concept, but I haven't found anyone who has done it before in an implementation that I like. People have created hacky approaches of a web frontend with a Google Sheets backend, but I don't want the ugly spreadsheets to be a part of the process at all. It's not like I'm constantly writing new and different reports; I want to spend some upfront effort writing a collection of reports that I want to see, and then I want to easily view those reports with updated data in my hand.

## Implementation

We may then separate the two main concerns of the app as follows:

1. Data entry in a clean, mobile-first design

2. Robust, custom data analytics

For the first concern, I plan to create a PWA with a minimalistic design for viewing and adding transactions. The app must be very usable through touch controls, and above all, it must be blazing fast. Currently, I am writing a Next + React app, but I may move to vanilla HTML/CSS/jQuery as required. This concern need only support the basic options like transaction amount, type, category, date, description, and notes. I have compiled this list of properties by looking at both hands-off app transaction properties and widely-used, premade Google Sheets. Each transaction should be editable and deleteable.

(This obviously requires some kind of data storage strategy. Currently, I am using a Supabase PostgreSQL database for all users, but I will detail future plans in the extensions section below.)

For the second concern, I plan to create a Javascript scripting editor. The user's script will run in an environment with all of their transaction data and access to some kind of data vizualisation library. Here are some examples of analysis scripts one might create:

- Create a pie chart of the current month's spending in each category.

- Create a line chart of past spending by month.

- Create a bar chart that details how much of each budget category they have spent and how much they have remaining in the month. This may require that the environment also has access to some kind of input controls (such as defining category budget amounts).

This second concern is really the part that excites me the most technologically. I am currently finishing up an MVP for the first concern, and I will most likely post another blog post mid-way through the second concern.

## Extensions

I think it's always good to have some dreams about a project, even if you may never get to them. These are what I call "extensions". With my current project, I've thought about the following extensions:

- Data ownership. I don't want to own my user's transaction data or worry about security. Lately, I have been reading about remoteStorage.js [4]. This library allows users to self-host a key-value storage while providing tools for app developers to interface with each user's storage *in an offline-first strategy*. This is really cool, but I need a SQL database. I think I want to combine it with sql.js [5]. This library compiles SQLite to WASM or JS to run in the browser. I am imagining an offline-first, self-hosted storage solution. That would be cool.

- Analytics marketplace. Many users might not be interested in or have the knowledge to create their own analysis reports with JS. I want to have a (free) marketplace where other users have written reports that can be imported in to one's own account.



I'll keep the blog updated with any progress I make on the app! That's all for now...



**References**

1. https://www.mintmobile.com/

2. https://plaintextaccounting.org/

3. [The Excel Formula Language Is Now Turing-Complete](https://www.infoq.com/articles/excel-lambda-turing-complete/)

4. https://remotestorage.io/

5. [GitHub - sql-js/sql.js: A javascript library to run SQLite on the web.](https://github.com/sql-js/sql.js/)[GitHub - sql-js/sql.js: A javascript library to run SQLite on the web.](https://github.com/sql-js/sql.js/)


