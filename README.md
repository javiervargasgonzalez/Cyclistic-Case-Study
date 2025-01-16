This is a Case Study from the Google Data Analytics Professional Certificate

Feel free to take a look at my project, all the information was taken from https://divvybikes.com/data-license-agreement
## Cyclistic Bike-Share Analysis Case Study

### Converting Casual Cyclistic Riders to Annual Members

**Company Background**

In 2016, Cyclistic launched a successful bike-sharing offering. Since then, the program has grown to a fleet of 5,824 bicycles that are geotracked and locked into a network of 692 stations across Chicago. The bikes can be unlocked from one station and returned to any other station in the system anytime. ![Illustration by Freepick](https://img.freepik.com/premium-vector/bike-sharing-rental-service-thin-line-icon_116137-1289.jpg) Illustration by [Freepik](https://img.freepik.com/premium-vector/bike-sharing-rental-service-thin-line-icon_116137-1289.jpg)

These Data sets have been provided by Motivate International under this [license](https://divvybikes.com/data-license-agreement).

**DEFINING THE QUESTION**

The company's marketing director believes that the company’s future success depends on maximizing the number of annual memberships. Therefore, as a junior data analyst, my team and I have to understand how casual riders and annual members use Cyclistic bikes differently. From these insights, we will design a new marketing strategy to convert casual riders into annual members.

**PREPARING DATA**

For starters we need to upload our "tidyverse" and "ggplot2" packages.

```{r}
library(tidyverse)
library(ggplot2)
```

Now we add the Data frames that we're going to be using for this analysis and select only the columns that we'll be using, then we can unite all the Data frames and use it as a single Data frame for the analysis. We'll add a column called ride_length that will indicate us the length of the ride for each customer.

