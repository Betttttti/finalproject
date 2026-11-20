# BST260 Final Project Proposal

Dear BST260 Teaching Team, Fall 2026,

I propose two analyses for my pkgdown site. The first links RAND’s
firearm legislation records to CDC firearm mortality rates. The second
examines the size of reported recreational-water outbreaks in CDC
surveillance data.

## State firearm background-check legislation and firearm mortality

**Research question.** Among U.S. states from 2014 through 2024, were
age-adjusted firearm mortality rates different in years following a
recorded restrictive background-check law change compared with years
following no such change?

**Data and population.** The unit of analysis will be one state in one
calendar year, covering the 50 states from 2014 through 2024. I will use
the course package’s `gunleg` records from the RAND State Firearm Law
Database and its `cdcfiremort` table from CDC’s National Center for
Health Statistics. I will join the sources by state and year after
standardizing state names and checking that the mortality table has one
record per state-year.

**Exposure and outcome.** I will code exposure as 1 if RAND recorded at
least one background-check law change classified as restrictive with an
effective year immediately before the mortality year, and 0 if the
available records show no qualifying change in that year. Multiple
changes in one year will count as one exposure. I will check law IDs,
effective years, and coding notes. If missing dates or classifications
make a state-year’s exposure ambiguous, I will code it as missing and
report how many observations I excluded. The outcome is the continuous
CDC age-adjusted firearm death rate per 100,000 residents. I will report
and exclude missing rates.

**Analysis and adjustment.** I will first plot the timing of qualifying
changes and summarize mortality rates by exposure group. I will then
estimate the adjusted difference in rates with a linear regression
including state and year fixed effects, with uncertainty clustered by
state. I chose state and year before fitting the model because
long-standing differences between states and national trends may
influence both legislative activity and firearm mortality.
State-specific changes in other firearm laws, economic conditions, or
earlier mortality trends could still confound the association. The
exposure measures recent legislative activity, so the estimate describes
an association with that activity.

## Recreational-water treatment and reported outbreak size

**Research question.** Among recreational-water outbreaks reported to
the CDC, did outbreaks linked exclusively to treated water have
different numbers of reported illnesses than outbreaks linked
exclusively to untreated water?

**Data and population.** The unit of analysis will be one reported U.S.
outbreak in the course package’s `waterborne` extract from the CDC
National Outbreak Reporting System. I will convert the nested list into
one row per outbreak, check for duplicate record IDs, and retain records
whose primary transmission mode is water. I will document the years and
reporting locations represented in the extract.

**Exposure and outcome.** I will code `water_exposure` as treated or
untreated using the corresponding single-category recreational-water
labels. I will exclude records with missing or undetermined exposure,
multiple water categories, or a different type of water exposure, and
report the exclusions. The outcome is the number of reported illnesses
per outbreak, a discrete quantitative count. I will preserve recorded
zeroes and report and exclude missing or invalid illness counts.

**Analysis and adjustment.** I will use a reusable R function to
summarize the number of outbreaks, median illness count, and
interquartile range by exposure group and season. I will plot the
distributions and use a count regression to estimate the adjusted ratio
of expected illness counts. Before fitting the model, I chose season,
calendar period, and U.S. Census region as adjustment variables because
recreational-water use and outbreak detection can differ across seasons,
years, and locations. I will derive season from the reported month and
report missing adjustment values. The findings will apply to reported
outbreaks. The dataset does not provide the number of people exposed to
each water type, so I will estimate outbreak size rather than individual
illness risk.
