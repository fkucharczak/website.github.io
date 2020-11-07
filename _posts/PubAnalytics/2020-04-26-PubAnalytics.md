---
layout: post
title: Hackathon EUvsVirus
tags: [Hackaton, PubAnalytics]
---

## Presentation video

[![Presentation video](https://img.youtube.com/vi/6AHYLxZzThY/0.jpg)](https://www.youtube.com/watch?v=6AHYLxZzThY)


## Inspiration
The sudden outbreak of the COVID-19 pandemic caused by SARS-COV-2 virus is responsible for a major health, economic and social tragedy. It makes COVID-19 one of the biggest crisis in our lifetime. However, as this Hackathon shows, it is also the root of many collective initiatives which are, in turn, sources of hope for the future.

For its extraordinary nature in our contemporary lives and for the damage it causes in our societies, many researchers around the world mobilized themselves to try understand this new disease. Consequently, the number of search results related to the subject in medical article databases has exploded. For example, the keyword _COVID-19_ has 43,943 results on the _EuropePMC_ database on 04/24/2020, at the beginning of the Hackathon.

However, the result of this explosion in the number of publications, with numerous different scientific tracks, make it very difficult to apprehend these researches and to have an accurate overview.

## What it does
Our platform allows to access information that are usually not accessible with common research platforms.
For example, when one looks for a randomized clinical trial on COVID-19 on the _EuropePMC_ database, they will receive a list with numerous articles including their keywords "randomized clinical trial" and "COVID-19". Now, should one wants to find information about which potential COVID-19 treatments have been investigated in clinical trials, there are two solutions :

>* search each combination _"[treatment keyword]" + "randomized clinical trial"_ testing all the treatments one thinks that may have been investigated (at the high risk of forgetting some).

>* search _"randomized clinical trial"_, browse all the results and manually retrieve all the different treatments trials.

Unfortunately, both approaches are obviously not efficient nor satisfying.
What we offer with **PubAnalytics** ([link](pubanalytics.eu)) is a solution to this type of questions. We proposed a new way of dealing with big data to contextualize the user query.

Let's return to the previous example and see how **PubAnalytics** ([link](pubanalytics.eu)) works when one looks for a randomized clinical trial on COVID-19 on the _EuropePMC_ database :

>* search _"randomized clinical trial"_ (the database is restricted to papers about COVID-19 extracted from the _EuropePMC_ database for the challenge) click enter and ... let the magic happen!!

For now, we give access to three different visualization plots for the results :
* a diagram displaying all the treatments involved in a randomized clinical trial about COVID-19
* a diagram displaying the number of papers with the keyword "randomized clinical trial" and COVID-19
* a diagram displaying the country distribution of the randomized clinical trial about COVID-19
At the bottom, you can also can browse the results corresponding to the request in a more conventional way, as it is in
_EuropePMC_ website for example.

This is just an example of prototype for the platform we will build. The best is to try it out.
## How we built it
We constructed a website allowing to perform queries on the _EuropePMC_ database that gathers "_a worldwide collection of life science publications and preprints from trusted sources around the globe_".

In parallel, we constructed a database of molecules used in medical clinical routine practice approved by the _EMA_ and _FDA_ including the main treatments candidates tested in COVID-19 trials. C. Lozza, a PharmD, PhD researcher advised us for this task.

Then, we built a basic API allowing to search by keywords and improved the results by cross-referencing our molecule database and _EuropePMC_. Behind, autonomous agents take care of this process to improve the cross-referencing and improve our results day by day.

## Challenges we ran into
The challenges we ran into are closely related to the tasks we described in the previous section. We needed to pool and assemble very different skills from our team of computer science PhDs. As there were only three of us, we divided the tasks : S.B. was responsible for the database management, the front and backend of the website, V.I. was responsible for the visualization part and its integration in the website and F.K. was responsible for the coordination and the medical part. Communication was the key, and we are pleased with the way we have dealt with the challenges of this project.
## Accomplishments that we're proud of
We are proud to have succeeded in creating a website from scratch in two and a half days and teleworking due to the containment rules. And of course we hope that this new platform will, from now on, be useful to the scientific community and continue to develop itself since we truly believe in the potential of this project.

## What we learned
Building a website of this type, aggregating skills in so many different fields with so many different technologies, in a weekend, with only three people, was a great learning experience for us, at very different levels. It allowed us to surpass our limits and to set up an ambitious project. #TeamWork!

## What's next for PubAnalytics
This is just the beginning of PubAnalytics. By investing the time to reflect on this project, immersed in this Hackathon during 3 days, we imagined many development perspectives for **PubAnalytics** [link](pubanalytics.eu). The idea of the project, through this Hackathon, was to give access to more efficient, global, and clearer vision of COVID-19 treatments involved in medical studies for researchers and physicians. Even if some improvements and updates are still to be made, we are proud to have developed this website prototype.

We believe we can scale this initiative to medical research in a more global way, allowing researchers working in pre-clinical, hospital, or biology laboratories to have access to our literature research and visualization tools. We also think that this initiative could also be a new powerful platform for performing meta-analysis.
Indeed, the environment is conducive to the use of technologies such as machine learning, natural language processing (NLP), etc. These tools would greatly improve the analysis we provide, allowing the users to interact with the figures we provide, yielding to more accurate researches.

We definitely plan to keep on growing this project. It is obvious to us that this project must remain an open access tool. Thus, we plan to raise money from university institutions (2 of the members are working for University of Montpellier and Lille, in France) in order to continue to develop the functionalities of **PubAnalytics** and maybe, at least we hope so, contribute to research in our own way.
