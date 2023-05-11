# Question: Does being "Race out of Place" in San Jose lead to a more severe outcome at a police stop? 

## Project Goals
In this project, we aim to investigate a phenomenon known as "Race out of Place". It is well known that some racial groups experience more frequent and more severe outcomes in police interactions. We hypothesize that when people are in an area where they are not the majority race -- they are 'out of place' -- they will experience more severe outcomes (for instance, they are more likely to be arrested). Policing in the context of race is an extremely important question because of well known disparities between racial groups in police interactions. But, if police tend to more harshly police groups in areas where they are not the majority race, this signals that police may not only take into account the race of their suspect, but also the racial context around their suspect, an important distinction in understand the implicit biases of policing.

## Description of Data
Our data is drawn from two sources: U.S. census data and San Jose Police Data from the Stanford Open Policing Project.

### Census Data
Census data is divided into tracts, geographical areas with around 2,000 - 10,000 people each in San Jose
![](sj-cencus-by-pop.png)

The tracts are racially diverse, being fairly evenly split between plurality asian, white, and hispanic

![](sj-most-common-geo.png)

![](sj-most-common-race.png)

### Policing Data
Most stops tend to end with citations, but a significant portion end with a much more sever outcome: arrest.

![](sj-outcomes.png)

Most stops tend to be vehicular.

![](sj-stops-by-race-tbl.png)

There are clear racial disparities in policing based on race. This graph shows the total number of police interactions, based on the race of the suspect. Clearly, hispanics interact with the police a disportionate amount

![](sj-stops-by-race.png)

![](sj-race-arrest-bar)

## Modelling

### Preliminary General Model
This is a general model showing all of the features that we will use on the follwing train-test-split arrays we have created for each race in San Jose.

We will show coefficients for each and plots telling us about conditional dependencies. That means you interpret it by assuming all other features are held constant -- what is the likelihood of an arrest being made if you are Race out of Place vs not, with every other feature assumed.

You can interpret the bars as how much each factor contributes to the "likelihood" of being arrested at a stop.

![](general-feature-model.png)

### Model: Black experience in San Jose
![](feature-coef-black.png)

![](feature-model-black.png)

This model shows if you are stopped as a pedestrian and percieved as Black, you have a higher likelihood of being arrested when stopped. Uf you are in a vehicle your likelihood of being arrested rather than cited at this stop is lower.

You can see that for Black subjects in San Jose, because there are no census tracts in which a Black person can be "Race in Place," the "Race_OOP" has no bearing on the likelihood of being arrested at a stop. However, you can also see that if the census tract is primarily Asian or Pacific Islander, a Black person "out of place" in that census tract is much more likely to be arrested at a stop compared to majority Hispanic or majority white census tracts.

### Model: Asian experience in San Jose
![](feature-coef-asian.png)

![](feature-model-asian.png)

You can see here that for Asian subjects in San Jose, being Race out of Place leads to actually a very slight decrease (a coefficient of -0.005) in likelihood of being arrested over being cited. Counterintuitively to the Race out of Place hypothesis, an Asian subject is more likely to be arrested over cited in a majority Asian census tract compared to a majority White census tract. They are most likely to be arrested over cited in a majority Hispanic census tract.

### Model: Hispanic experience in San Jose
![](feature-coef-hispanic.png)

![](feature-model-hispanic.png)

Like with Black subjects, being Race out of Place matters very little for Hispanic subjects, despite Hispanic-majority census tracts being roughly 1/3 of all census tracts. For Hispanic subjects, they are more likely to be arrested than cited in Asian-majority census tracts, while less likely to be arrested than cited in white or Hispanic-majority census tracts, though Hispanic-majority census tracts have a nearly negligible effect.

### Model: White experience in San Jose
![](feature-coef-white.png)

![](feature-model-white.png)

Finally, with white subjects in San Jose, you can see that Race out of Place does have an effect on the likelihood of being arrested over cited, more so than with Hispanic, Black, or Asian subjects. They are most likely to be arrested over cited in majority Asian census tracts, with a coefficient on that variable, while less likely to be arrested over cited in majority Hispanic census tracts, and least likely to be arrested in majority white census tracts. Thus, white subjects in San Jose represent the most straightforward example of the Race out of Place hypothesis.

## Conclusion
San Jose is a major metropolitan area encompassing 1 million people, but it is also a unique geoeconomic zone, supported by commuters from the South Bay Area and San Francisco as well as housing commuters to the greater Bay Area locations. It also does not reflect the demographics of major cities outside California, like, say Detroit, NYC, or Chicago, which have more Black and Hispanic majority census tracts.

We found very different results of our investigation depending on the race of the subject being stopped. For example, with Black subjects, the likelihood of their stop resulting in an arrest is highest in majority white census tracts, while majority Hispanic and Asian census tracts actually have a minorly mitigating effect, with our model predicting it slightly more likely that a stop of a Black subject there would be a citation, not an arrest. All these variables have relatively very small effects on the overall probability of an arrest, but that is likely due to a limitation of the model and our data. Furthermore, an issue with using San Jose only in this model is that there are no majority Black census tracts in the city to properly test every aspect of the race out of place theory.

For Asian subjects, the census tracts in which they are most likely to be arrested are actually flipped. There is also a noticeably larger effect that the majority race of the census tract has on the overall probability or likelihood that a stop will result in an arrest for an Asian subject. Where the coefficient on the majority white census tracts for Black subjects was (0.015702), it is (-0.027291) for Asian subjects, an increase in importance of nearly double. Furthermore, the experience of Race out of Place is complicated for Asian subjects -- they actually experience a higher likelihood of being arrested in majority Asian census tracts, as well as in majority Hispanic tracts. This could possibly be explained by discrimination amongst sub-Asian ethnicities that is not captured by the census tract or police profiling data, which both only go down to a granularity of Asian. However, an Indian person in a South Korean majority neighborhood would visibly be race out of place, despite the data coding both ethnicities as Asian.

Hispanic subjects in San Jose experience a slightly higher likelihood of being arrested only in majority Asian census tracts, having decreased likelihoods when they are race in place, or in majority white census tracts. However, like with Black subjects, the coefficients on all census tract racial variables are very small, with the coefficient on a majority Asian census tract being the highest at (0.012869). This implies that the dominant race of the surroundings is less of an issue for Hispanic subjects to traffic stops, but could also be a result of confounding factors. After all, both white Hispanics and Afro-Latinos are put in the Hispanic category, and could still be race in place while in majority white tracts. There are overall fewer Asian Hispanics in the US, making up only 6% of the entire US Hispanic population, and so the likelihood of an Asian Hispanic in this dataset being stopped in an Asian neighborhood as race in place is lower than a White Hispanic stopped in a white neighborhood.

Finally, for Non-Hispanic Whites, they too only experience a higher likelihood of being arrested in majority Asian census tracts. In majority white or Hispanic tracts, they are less likely to be arrested rather than cited.

