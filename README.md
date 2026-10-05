# DatVis Portfolio: Kelley Schweissing

#### dat2002

## Entry 1: US vs. World Gini Coefficient
![Visualization 1](/Rplot.png)

This was a test chart to get the feel of GitHub and make sure I could actually upload something.  Obviously a lot is wrong with this chart from color use to labels and the information in general.  But like I said, this was a first attempt at creating a GitHub page and I am pretty excited to continue on and learn more as well as create my own graphics from data I care about.

## Entry 2: Texas Precipitation by County

<img width="844" height="498" alt="Texas_Rain" src="https://github.com/user-attachments/assets/e748b3c8-7144-4427-9441-59a4adfab892" />

This is a chart created for a class assignment where we began considering color.  I selected brown for the dryer counties and green for the wetter counties as those colors symbolize arid and lush environments respectively.  You may also notice that two counties are not filled with any color.  This was a data wrangling issue I had regarding the spelling of county's name which I missed when merging that data.  I know how the correct the issue but I have not taken the time to do so due to conflicting life commitments.  I do know how to account for it going forward and will display the knowledge with completed charts.

## Entry 3: Maps, Color & And US Gini Coefficient By State (HW 2 Part 1)

### Map A
<img width="844" height="498" alt="US States" src="https://github.com/user-attachments/assets/aa3baba9-c6c5-43ba-bd56-3408ee0c9d29" />

### Map B
<img width="844" height="498" alt="US State Gini" src="https://github.com/user-attachments/assets/5f11fc02-3de9-42a7-b97f-2d0962cc5df1" />

This was a class exercise where we began exploring how to create maps in R.  I am really excited to be getting into these kinds of visuals as I enjoy seeing them in the wild and have often thought about the kinds I would like to create.  The first visual was a class exercise to create a generic map.  I wanted to alter the map in some way to make it more meaningful and since we have already worked with the Gini Coefficient in class I thought that would be a good place to start.  I also added boarders around each state to reduce the cognitive load on the view by making the states easier to pick out.  I played around with the format of the graph for as much time as I had in class and made my first step into AI use.  I consider myself an anti AI person but I was floored by how easy it made coding and correcting errors in the code.  Its astounding technology and exactly why I am taking this class.

##### This Data Visualization was created in RStudio

##### The geographical data was pulled from the class server provided by the instructor.  I am not sure what the original source is.  The Gini Coefficient data was aggregate by the AI Perplexity from 5 sources:

###### 1) Bureau of Economic Analysis (BEA) — Published Gini coefficients for all 50 states and D.C. based on 2023 statistics, ranging from 0.38 in West Virginia to 0.52 in Wyoming. This is the most recent and authoritative source.apps.bea
###### 2) U.S. Census Bureau (ACS) — Gini coefficients via the American Community Survey, available through data.census.gov.statehealthcompare.shadac
###### 3) Wikipedia: List of U.S. States by Gini Coefficient — A convenient table with all 50 states.wikipedia
###### 4) Sam Houston State University Panel — Annual Gini coefficients for all 50 states and D.C. from 1916 to 2023, useful for time-series analysis.profiles.shsu
###### 5) SSTI Blog — 2022 data with New York (0.5208) as the highest, followed by Connecticut, Massachusetts, California, and Louisiana.

'''
# US States Gini Coefficient Choropleth Map — Red to Gold Gradient
# ================================================================

library(ggplot2)
library(dplyr)

# -- Gini coefficients by state (2019, U.S. Census ACS) --
# Source: https://en.wikipedia.org/wiki/List_of_U.S._states_by_Gini_coefficient

gini_data <- data.frame(
  region = tolower(c(
    "New York", "District of Columbia", "Connecticut", "Louisiana", "Mississippi",
    "California", "Florida", "Massachusetts", "Illinois", "Georgia",
    "New Jersey", "New Mexico", "Kentucky", "Texas", "Arkansas",
    "Tennessee", "South Carolina", "Pennsylvania", "North Carolina", "Alabama",
    "Oklahoma", "Nevada", "Virginia", "Ohio", "West Virginia",
    "Michigan", "Missouri", "Rhode Island", "Montana", "Arizona",
    "Indiana", "Washington", "Maryland", "North Dakota", "Colorado",
    "Delaware", "Kansas", "Oregon", "Maine", "Vermont",
    "Minnesota", "Iowa", "New Hampshire", "Nebraska", "Hawaii",
    "Wisconsin", "Alaska", "South Dakota", "Wyoming", "Idaho", "Utah"
  )),
  gini = c(
    0.5149, 0.5115, 0.5024, 0.4978, 0.4964,
    0.4866, 0.4808, 0.4803, 0.4800, 0.4795,
    0.4782, 0.4768, 0.4764, 0.4753, 0.4750,
    0.4749, 0.4747, 0.4745, 0.4743, 0.4741,
    0.4739, 0.4710, 0.4690, 0.4651, 0.4644,
    0.4634, 0.4633, 0.4628, 0.4597, 0.4591,
    0.4584, 0.4577, 0.4558, 0.4558, 0.4548,
    0.4509, 0.4500, 0.4500, 0.4490, 0.4471,
    0.4434, 0.4422, 0.4406, 0.4400, 0.4397,
    0.4391, 0.4376, 0.4360, 0.4345, 0.4337, 0.4268
  )
)

# -- Load state map data and join Gini values --
state_map <- map_data("state")

map_gini <- state_map %>%
  left_join(gini_data, by = "region")

# -- Build the choropleth with red-to-gold gradient --
ggplot(data = map_gini, aes(x = long, y = lat, group = group)) +
  geom_polygon(aes(fill = gini), color = "black") +
  coord_quickmap() +
  scale_fill_gradient(
    name = "Gini\nCoefficient",
    low = "red",
    high = "gold",
    limits = c(0, 1)
  ) +
  labs(title = "Income Inequality by State (Gini Coefficient, 2019)") +
  theme_void() +
  theme(
    plot.title = element_text(hjust = 0.5, face = "bold", family = "Verdana"),
    legend.title = element_text(family = "Verdana", face = "bold"),
    legend.text = element_text(family = "Verdana")
  ) 
'''
