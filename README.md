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

```{r}
trips_data_2024_01 <- read.csv("C:/Users/Lenovo/Downloads/2024_Cyclistic_Data/202401-divvy-tripdata.csv") %>% 
  mutate(ride_length=difftime(ended_at,started_at,units = "mins")) %>% 
  select(rideable_type, started_at, ended_at, ride_length, start_lat, start_lng, end_lat, end_lng, member_casual)
trips_data_2024_02 <- read.csv("C:/Users/Lenovo/Downloads/2024_Cyclistic_Data/202402-divvy-tripdata.csv") %>% 
  mutate(ride_length=difftime(ended_at,started_at,units = "mins")) %>% 
  select(rideable_type, started_at, ended_at, ride_length, start_lat, start_lng, end_lat, end_lng, member_casual)
trips_data_2024_03 <- read.csv("C:/Users/Lenovo/Downloads/2024_Cyclistic_Data/202403-divvy-tripdata.csv") %>% 
  mutate(ride_length=difftime(ended_at,started_at,units = "mins")) %>% 
  select(rideable_type, started_at, ended_at, ride_length, start_lat, start_lng, end_lat, end_lng, member_casual)
trips_data_2024_04 <- read.csv("C:/Users/Lenovo/Downloads/2024_Cyclistic_Data/202404-divvy-tripdata.csv") %>% 
  mutate(ride_length=difftime(ended_at,started_at,units = "mins")) %>% 
  select(rideable_type, started_at, ended_at, ride_length, start_lat, start_lng, end_lat, end_lng, member_casual)
trips_data_2024_05 <- read.csv("C:/Users/Lenovo/Downloads/2024_Cyclistic_Data/202405-divvy-tripdata.csv") %>% 
  mutate(ride_length=difftime(ended_at,started_at,units = "mins")) %>% 
  select(rideable_type, started_at, ended_at, ride_length, start_lat, start_lng, end_lat, end_lng, member_casual)
trips_data_2024_06 <- read.csv("C:/Users/Lenovo/Downloads/2024_Cyclistic_Data/202406-divvy-tripdata.csv") %>% 
  mutate(ride_length=difftime(ended_at,started_at,units = "mins")) %>% 
  select(rideable_type, started_at, ended_at, ride_length, start_lat, start_lng, end_lat, end_lng, member_casual)
trips_data_2024_07 <- read.csv("C:/Users/Lenovo/Downloads/2024_Cyclistic_Data/202407-divvy-tripdata.csv") %>% 
  mutate(ride_length=difftime(ended_at,started_at,units = "mins")) %>% 
  select(rideable_type, started_at, ended_at, ride_length, start_lat, start_lng, end_lat, end_lng, member_casual)
trips_data_2024_08 <- read.csv("C:/Users/Lenovo/Downloads/2024_Cyclistic_Data/202408-divvy-tripdata.csv") %>% 
  mutate(ride_length=difftime(ended_at,started_at,units = "mins")) %>% 
  select(rideable_type, started_at, ended_at, ride_length, start_lat, start_lng, end_lat, end_lng, member_casual)
trips_data_2024_09 <- read.csv("C:/Users/Lenovo/Downloads/2024_Cyclistic_Data/202409-divvy-tripdata.csv") %>% 
  mutate(ride_length=difftime(ended_at,started_at,units = "mins")) %>% 
  select(rideable_type, started_at, ended_at, ride_length, start_lat, start_lng, end_lat, end_lng, member_casual)
trips_data_2024_10 <- read.csv("C:/Users/Lenovo/Downloads/2024_Cyclistic_Data/202410-divvy-tripdata.csv") %>% 
  mutate(ride_length=difftime(ended_at,started_at,units = "mins")) %>% 
  select(rideable_type, started_at, ended_at, ride_length, start_lat, start_lng, end_lat, end_lng, member_casual)
trips_data_2024_11 <- read.csv("C:/Users/Lenovo/Downloads/2024_Cyclistic_Data/202411-divvy-tripdata.csv") %>% 
  mutate(ride_length=difftime(ended_at,started_at,units = "mins")) %>% 
  select(rideable_type, started_at, ended_at, ride_length, start_lat, start_lng, end_lat, end_lng, member_casual)
trips_data_2024_12 <- read.csv("C:/Users/Lenovo/Downloads/2024_Cyclistic_Data/202412-divvy-tripdata.csv") %>% 
  mutate(ride_length=difftime(ended_at,started_at,units = "mins")) %>% 
  select(rideable_type, started_at, ended_at, ride_length, start_lat, start_lng, end_lat, end_lng, member_casual)

```

It wasn't possible to open *'C:/Users/Lenovo/Downloads/2024_Cyclistic_Data/202410-divvy-tripdata.csv': No such file or directoryError en file(file, "rt"):* so we'll use all the other data except for that Data set.

The data is organized into rows and columns with the following fields:

-   rideable_bike: Type of bike (classic, docked, electric)
-   started_at: The date and time in which the ride started (yyyy/mm/dd hh:mm:ss)
-   ended_at: The date and time in which the ride ended (yyyy/mm/dd hh:mm:ss)
-   ride_length: The difference between started_at and ended_at (in minutes)
-   start_lat: The latitude of the starting station
-   start_lng: The longitude of the starting station
-   end_lat: The latitude of the ending station
-   end_lng: The longitude of the ending station
-   member_casual: The type of rider (member, casual)

Now let's take a look at some of our data:

```{r}
trips_data_2024_01 %>% 
  arrange(desc(ride_length)) %>% 
  head()
```

```{r}
trips_data_2024_05 %>% 
  arrange(desc(ride_length)) %>% 
  head()
```

With these Data frames we realize that some ride lengths are longer than 24 hours and that those are bikes that weren't returned to a station for a long period of time and might not be helpful for our analysis. We need to establish an usage margin that might help for our analysis, this margin should be from 10 minutes to 8 hours.

```{r}
trips_data_2024_01 <- filter(trips_data_2024_01, ride_length < 480 & ride_length > 10)
trips_data_2024_02 <- filter(trips_data_2024_02, ride_length< 480 & ride_length > 10)
trips_data_2024_03 <- filter(trips_data_2024_03, ride_length< 480 & ride_length > 10)
trips_data_2024_04 <- filter(trips_data_2024_04, ride_length< 480 & ride_length > 10)
trips_data_2024_05 <- filter(trips_data_2024_05, ride_length< 480 & ride_length > 10)
trips_data_2024_06 <- filter(trips_data_2024_06, ride_length< 480 & ride_length > 10)
trips_data_2024_07 <- filter(trips_data_2024_07, ride_length< 480 & ride_length > 10)
trips_data_2024_08 <- filter(trips_data_2024_08, ride_length< 480 & ride_length > 10)
trips_data_2024_09 <- filter(trips_data_2024_09, ride_length< 480 & ride_length > 10)
trips_data_2024_11 <- filter(trips_data_2024_11, ride_length< 480 & ride_length > 10)
trips_data_2024_12 <- filter(trips_data_2024_12, ride_length< 480 & ride_length > 10)
```

Let's take a look at one of the Data sets:

```{r}
trips_data_2024_03 %>% 
  arrange(desc(ride_length)) %>% 
  head()
```

Now we'll unite all the Data frames to start the cleaning process and the analysis.

```{r}
trips_data_2024 <- rbind(trips_data_2024_01,trips_data_2024_02,trips_data_2024_03,trips_data_2024_04,trips_data_2024_05,trips_data_2024_06,trips_data_2024_07,trips_data_2024_08,trips_data_2024_09,trips_data_2024_11,trips_data_2024_12)
```

Now we can remove all the other Data frames to free up some space.

```{r}
rm(trips_data_2024_01,trips_data_2024_02,trips_data_2024_03,trips_data_2024_04,trips_data_2024_05,trips_data_2024_06,trips_data_2024_07,trips_data_2024_08,trips_data_2024_09,trips_data_2024_11,trips_data_2024_12)
```

**PROCESSING DATA**

We'll start the cleaning process of our data, by eliminating NA or NULL values. First we need to check if we have any NA/NULL values:

```{r}
trips_data_2024 %>% 
  summarise(across(rideable_type:member_casual, ~ sum(is.na(.))))
```

Since we don't have any NA/NULL values we can move on with the cleaning process and look for any duplicates.

```{r}
sum(duplicated(trips_data_2024))
```

As a result of the inspection, the program found 4 duplicates that we need to remove.

```{r}
unique(trips_data_2024)
```

Now that our Data has been cleaned, we can start with the process of analysis:

**ANALYSE DATA**

The things that might help us in our analysis are:

-   Knowing which month had the most travels
-   Which month had the most members usage and the month with most casual riders
-   The month with the most tourist in Chicago.
-   The month with the most new members
-   The type of bike each of the group prefers

First of all we'll add a month column of each trip.

```{r}
trips_data_2024$Month <- month(trips_data_2024$started_at, label = TRUE)
head(trips_data_2024)
```

We'll obtain the mean, maximum, and minimum values from the ride_length column:

```{r}
trips_data_2024 %>% 
  summarise(max(ride_length), min(ride_length), mean(ride_length))
```

With this information we now know the average ride length is 24.68 minutes which can help us to make special prices for different ride lengths or some packages or special offers depending on the usage.

```{r}
ggplot(data =  trips_data_2024) + geom_col(mapping = aes(x = Month, y = ride_length, color = member_casual)) + labs(x = "Month", y = "Ride length", fill = "Member-Casual", title = "Most travels by casual riders and members")

```

-*NOTE: The reason why there's a drop in the columns in October is due to the fact that it was unable to open that Data set.*

With this visualization we can know most of the things that might help us in our analysis which are:

-   Knowing which month had the most travels
-   Which month had the most members usage and the month with most casual riders
-   The month with the most new members

To know wich bike do users prefer we need another graph, but first we need to transform the data to numeric values:

```{r}
bike_types <- trips_data_2024 %>% 
  group_by(member_casual, rideable_type) %>% 
  summarize(sum_rideable_type = n())
head(bike_types)
```

Now we create the graph:

```{r}
ggplot(data = bike_types)+ geom_bar(mapping = aes(x=member_casual, y = sum_rideable_type, fill = rideable_type),stat = "sum", position = "dodge")+labs(title = "Users bikes preferences")
```

**SHARE THE ANALYSIS**

The data analysis process is almost complete, for the last part we need to make conclusions with the data we have, but first I think is important to know in which months are there more tourists in Chicago since this is a key aspect to know because it can affect our analysis. Since I don't have any data sets about average tourist volumes in Chicago I went on the internet and found a chart with this information:

![Average Tourist Volumes](attachment:eb4167ca-0e83-4f60-8de9-c474070a560f.png)

Image from [U.S. News](https://travel.usnews.com/Chicago_IL/When_To_Visit/)

With these information we now know that the months with the most tourists are the months from June through October which coincide with the months with the most bike travels.

There are several important points to this analysis:

-   Casual riders recorded a greater bicycle activity than Cyclistic members especially in the months from June through September.
-   There are three types of vehicles: classic bike, electric bike and electric scooter.
-   Cyclistic members and casual riders preferences show a much higher preference for classic bicycles and electric bicycles that electric scooters, and the highest used vehicle is the classic bike.
-   On average Cyclistic members use the bikes on shorter periods of time than casual riders.
-   Both Cyclistic members and casual riders have the lowest activity in January.
-   Both Cyclistic members and casual riders have the highest activity in July.

**ACT**

Recommendations:

From the analysis, we can design marketing strategies to convert casual riders to Cyclistic members.

-   Provide different types of memberships for different type of clients, like tourist and locals. Different time packages like weekly, monthly and yearly memberships.
-   Membership discounts, like family, couples or a larger group packages. It would also be a good Idea to have discounts on the months with fewer activity.
-   Engagement with our audience: Usage of digital media, like social media platforms, announcements, etc.
-   Special offers, by partnering with other companies we can offer special offers in their products for membership owners and access to exclusive events.

## Conclusion
This analysis provides information about the preferences and behaviors of both Cyclistic members and casual riders who can potentially become new members, with specific strategies Cyclistic could grow a bigger customer network and possibly expand to other cities.
