# DatVis Portfolio: Kelley Schweissing

#### dat2002

## Entry 1: US vs. World Gini Coefficient
![Visualization 1](/Rplot.png)

This was a test chart to get the feel of GitHub and make sure I could actually upload something.  Obviously a lot is wrong with this chart from color use to labels and the information in general.  But like I said, this was a first attempt at creating a GitHub page and I am pretty excited to continue on and learn more as well as create my own graphics from data I care about.

## Entry 2Wealth Needed to Buy a Home
<img width="2340" height="1300" alt="quarterly_mortgage_payments" src="https://github.com/user-attachments/assets/4995a93c-0690-4206-8859-132c336fc339" />

This was a test image created in RStudio using the AI Perplexity.  It keeps with our previous theme of housing and shows how much more wealth is needed to by a house in 2026 than in 1981.

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
###### 5) ; SSTI Blog — 2022 data with New York (0.5208) as the highest, followed by Connecticut, Massachusetts, California, and Louisiana.

```
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
```

## Entry 4: Economics: What's a Dollar Worth, The Devaluation of $100  (HW 2 Part 2)

<img width="844" height="498" alt="What&#39;s a Dollar Worth 1900" src="https://github.com/user-attachments/assets/2bdcdfe8-d261-424d-bcbd-93871e73eba3" />

<img width="844" height="498" alt="$100 Devaluation" src="https://github.com/user-attachments/assets/4605c985-38ad-4930-b7ca-c1ee66d1273d" />


Unfortunately, I went full “vibe coding” for this one.  I am a little embarrassed about it as I have been so staunchly anti-AI.  But man this was easy and useful.  I think the main lessons I took away from this is that the ease of use is not necessarily a plus.  Using AI allows data designers to get instant gratification.  I am still not sure how much of this can really be considered my work and how much is the AI.  It seems like it would create a false sense of accomplishment for data designers.  On top of that I did not vet the sources at all for this project. I let the AI run wild and I did very little data cleaning, wrangling or verification.  I once heard AI described as mansplaining as a service.  It will tell you, with confidence, the wrong information.  It is becoming way to easy to become certain about spurious conclusions.  It is up to professionals like myself to properly verify the information.  Not doing so would be irresponsible and who knows how dangerous.  I think what this exercise taught me is that we are all coders and programmers now in the same way that a 3D printer makes us all manufacturers.  Coding and programming has been  a craft reserved for the trained few.  Now everyone, anyone, has access to the ability to program, code, and develop.  In the same way that a loom made anyone a weaver.  As I said earlier, I was floored.  I spent a whole day on my weekend having an AI build interesting visualizations for me.  I created interactive graphics and dashboards and am looking forward to loading them up on this page once I figure out how.  Maybe I will ask AI.  Working at the college and having access to AR and VR tech and now this is really heady.  Its a Brave New World…

Anyhow, this is a graphic show the purchasing power of a 1900 dollar today.  A dollar is worth 2.5 cents apparently.  I spent a lot of time with economics graphs this weekend and this was one of my favorites as I feel it starkly explains why things feel harder today.  We all know  twenty dollars isn’t twentying like it used to and this graph is expressing that feeling.  This chart still could use some optimizing regarding labels and type face, but it came out pretty clean for a vibe code.  The second Image is essentially the same but for $100.  I like this chart because it implies that had inflation occurred without and increase in the money supply, which is just deflation, money would have become more scarce and valuable.  Its illuminating why it feels like previous generations were compensated better than young workers today.  Because they essentially were.  Money has be devalued.

##### This Data Visualization was created in RStudio and by using the AI Perplexity 
###### I am both awed by AI and ashamed I used it

##### This Data Visualization was created in RStudio from code generated by the AI Perplexity 

##### The data was (supposedly) pulled from Federal Reserve Economic Data and the Minneapolis FED

```
# =============================================================================
# Devaluation of $100: what $100 from 1900 is worth, 1900-2026
#   Value = $100 x (CPI in 1900 / CPI in each month), shown in 1900 dollars
#   1913-2026: monthly BLS CPI-U (not seasonally adjusted, FRED: CPIAUCNS)
#   1900-1912: annual Minneapolis Fed historical CPI, rescaled at 1913
# =============================================================================

pkgs <- c("dplyr", "ggplot2", "scales")
new  <- pkgs[!pkgs %in% installed.packages()[, "Package"]]
if (length(new)) install.packages(new)
library(dplyr)
library(ggplot2)
library(scales)

# ---- Load data ---------------------------------------------------------------
cpi_monthly <- read.csv("https://fred.stlouisfed.org/graph/fredgraph.csv?id=CPIAUCNS")
names(cpi_monthly) <- c("date", "cpi")
cpi_monthly$date <- as.Date(cpi_monthly$date)
cpi_monthly$cpi  <- suppressWarnings(as.numeric(cpi_monthly$cpi))

early_cpi <- data.frame(
  year    = 1900:1913,
  cpi_old = c(25, 25, 26, 27, 27, 27, 27, 28, 27, 27, 28, 28, 29, 29.7)
)
bls_1913_avg  <- mean(cpi_monthly$cpi[format(cpi_monthly$date, "%Y") == "1913"])
splice_factor <- bls_1913_avg / early_cpi$cpi_old[early_cpi$year == 1913]

early <- early_cpi |>
  filter(year < 1913) |>
  transmute(date = as.Date(paste0(year, "-07-01")), cpi = cpi_old * splice_factor)

cpi_all <- bind_rows(early, select(cpi_monthly, date, cpi)) |>
  filter(!is.na(cpi), date <= as.Date("2026-12-31")) |>
  arrange(date)

# ---- Value of $100 in 1900 dollars ------------------------------------------
cpi_base_1900 <- cpi_all$cpi[1]
dollar_value <- cpi_all |> mutate(value_100 = 100 * cpi_base_1900 / cpi)

latest   <- dollar_value |> slice_max(date, n = 1)
pct_lost <- 100 - latest$value_100

# Labeled years (first available observation in each year)
label_years <- c(1900, 1920, 1945, 1970, 1990, 2010)
marks <- dollar_value |>
  mutate(year = as.integer(format(date, "%Y"))) |>
  filter(year %in% label_years) |>
  group_by(year) |> slice_min(date, n = 1) |> ungroup() |>
  mutate(label = paste0(year, ": ", dollar(value_100, accuracy = 0.01)),
         vjust = ifelse(year == 1920, 2.2, -1))

peak_1933 <- dollar_value |>
  filter(date >= as.Date("1930-01-01"), date <= as.Date("1935-12-31")) |>
  slice_max(value_100, n = 1)

# ---- Chart -------------------------------------------------------------------
p <- ggplot(dollar_value, aes(date, value_100)) +
  annotate("rect", xmin = as.Date("1900-01-01"), xmax = as.Date("1912-12-31"),
           ymin = -Inf, ymax = Inf, fill = "grey92") +
  annotate("text", x = as.Date("1901-01-01"), y = 5, hjust = 0, size = 2.8,
           color = "grey40", label = "1900-1912:\nannual estimates") +
  geom_area(fill = "#1f4e79", alpha = 0.12) +
  geom_line(color = "#1f4e79", linewidth = 0.9) +
  geom_point(data = marks, color = "#c0504d", size = 2) +
  geom_text(data = marks, aes(label = label, vjust = vjust),
            hjust = -0.1, size = 3.3, color = "grey15") +
  annotate("text", x = peak_1933$date, y = peak_1933$value_100 + 4, hjust = 0,
           size = 3, color = "grey35",
           label = paste0("Depression deflation\n", format(peak_1933$date, "%b %Y"),
                          ": ", dollar(peak_1933$value_100, accuracy = 0.01))) +
  geom_point(data = latest, color = "#c0504d", size = 3) +
  geom_text(data = latest,
            aes(label = paste0(format(date, "%b %Y"), "\n",
                               dollar(value_100, accuracy = 0.01))),
            hjust = 1.1, vjust = -0.6, size = 3.8, fontface = "bold",
            color = "#c0504d") +
  scale_x_date(breaks = seq(as.Date("1900-01-01"), as.Date("2020-01-01"), "10 years"),
               date_labels = "%Y",
               limits = as.Date(c("1899-01-01", "2028-06-01")),
               expand = expansion(mult = c(0.005, 0))) +
  scale_y_continuous(labels = dollar, limits = c(0, 115), breaks = seq(0, 100, 20)) +
  labs(title = "What $100 from 1900 is worth, 1900-2026",
       subtitle = sprintf("Purchasing power of $100 in 1900 dollars. It has lost %.1f%% of its value.",
                          pct_lost),
       x = NULL, y = "Value in 1900 dollars",
       caption = paste("Source: BLS CPI-U via FRED (monthly, 1913-2026);",
                       "Minneapolis Fed historical CPI (annual, 1900-1912, shaded).")) +
  theme_minimal(base_size = 12) +
  theme(panel.grid.minor = element_blank(),
        panel.grid.major.x = element_blank(),
        plot.title = element_text(face = "bold", size = 16),
        plot.caption = element_text(color = "grey40", hjust = 0))

print(p)
ggsave("devaluation_of_100_1900_2026.png", p, width = 12, height = 6.5, dpi = 300, bg = "white")
write.csv(dollar_value, "devaluation_of_100_1900_2026.csv", row.names = FALSE)
```

# A note for Guy
I would like to learn how to put interactive graphics and dashboards on my page.  Is that up coming in the curriculum or should I see you outside of class time?  The following is the R code for some of my stuff I was messing with this weekend.  I had a blast vibe coding, I hate to say it but I did.  The first image is the amount of wealth needed to by a house in the years 1981 and 1986.  I will write more about it when I next update this page.  I also have some code for interactive graphics and a dashboard I would like to put on this page.  Feel free to run them and let me know what you think!

I am a big fan of the term "Work Slop" which means sloppy work produced by an AI.  I have told the people I most directly work with that I will not accept their work slop coming across my desk.  I bring this up because I feel that some of the visuals I am generating at this moment test the limits of work slop, but I want you to know that I am very conscious of the time you take to grade my work and don't want to send you work slop as I would find that highly offensive myself.  I am learning a lot in your class and just have not had time to edit these vibe coded graphics enough to make the presentable.  In you class I am learning how to edit code and use AI responsibly and as the class progresses my quality of work will improve.


## Housing Market Bubbles Modeler

```
# =============================================================================
# What happens when a bubble pops?  Interactive Shiny app for RStudio
#
#   Gold circle = real value (what the asset is fundamentally worth)
#   Red circle  = speculative value (what the market is paying)
#
# TWO MODES (opens on actual data, 1900-2026)
#   1. Simulated scenario - a stylised bubble: Boom -> Peak -> Crash -> Panic
#      (market falls BELOW real value) -> Recovery. Sliders set the size of
#      the bubble, the depth of the panic and how much the crash damages
#      real value itself.
#   2. Actual US housing data, 1900-2026 - the same circles driven by real
#      history. Pick the full century or a single boom-and-bust episode.
#
# HOW TO RUN IN RSTUDIO
#   1. Install packages once (Console):
#        install.packages(c("shiny", "ggplot2", "ggforce", "dplyr", "tidyr",
#                           "haven", "lubridate"))
#   2. Save this file as app.R in its own folder, open it, click "Run App".
#   The first time you choose "Actual US housing data" the app downloads the
#   data (~1 MB) and saves housing_history.csv next to app.R; later runs load
#   that file instantly. Delete the CSV to force a fresh download.
#
# ACTUAL-DATA METHOD
#   Multiplier (market / real) = price-to-rent ratio / its 1990-1999 average.
#     1900-1989: Jorda-Schularick-Taylor Macrohistory Database (R6), US housing
#                rent yield, nominal house prices and CPI.
#                https://www.macrohistory.net/database/
#     1990-2026: FRED - Case-Shiller US National Home Price Index (CSUSHPINSA),
#                CPI Rent of Primary Residence (CUUR0000SEHA), CPI (CPIAUCSL).
#   Speculative value = house prices adjusted for inflation (FRED series are
#                       chained onto JST levels at 1990).
#   Real value        = speculative value / multiplier, i.e. the rent-justified
#                       price, adjusted for inflation.
#   Both are indexed so real value = 100 in the first year of the chosen period,
#   which lets you see real value itself rise and fall.
#   Dollar amounts (1945+): Federal Reserve Z.1, owner-occupied real estate at
#   market value (FRED HOOREVLMHMV), nominal dollars.
#   Annual averages; 2026 is year-to-date.
#
# The simulated mode is a stylised model, not a forecast.
# =============================================================================

library(shiny)
library(ggplot2)
library(ggforce)
library(dplyr)
library(tidyr)
library(haven)       # read the JST Stata file
library(lubridate)

GOLD <- "#D4A017"; RED <- "#C0392B"; BLUE <- "#3B7DD8"; BG <- "#FAF8F3"
T_MAX <- 100            # simulated model time steps

# =============================================================================
# 1. Simulated model
# =============================================================================
T_PEAK   <- 40          # bubble peaks
T_TROUGH <- 58          # panic bottom (market below real value)
T_HEAL   <- 90          # market back to fair value

smooth <- function(x) x * x * (3 - 2 * x)     # smooth 0 -> 1 ramp

simulate <- function(peak, trough, damage, real0 = 100, growth = 0.002) {
  t <- 0:T_MAX
  mult <- case_when(
    t <= T_PEAK   ~ 1 + (peak - 1) * smooth(t / T_PEAK),
    t <= T_TROUGH ~ peak + (trough - peak) * smooth((t - T_PEAK) / (T_TROUGH - T_PEAK)),
    t <= T_HEAL   ~ trough + (1 - trough) * smooth((t - T_TROUGH) / (T_HEAL - T_TROUGH)),
    TRUE          ~ 1
  )
  # crash damage to real value hits after the peak; half is repaired later
  hit <- case_when(
    t <= T_PEAK        ~ 0,
    t <= T_TROUGH + 6  ~ damage * smooth((t - T_PEAK) / (T_TROUGH + 6 - T_PEAK)),
    TRUE               ~ damage * (1 - 0.5 * smooth(pmin((t - T_TROUGH - 6) / 30, 1)))
  )
  real <- real0 * (1 + growth)^t * (1 - hit)
  tibble(t, mult, real, spec = real * mult, market_value = NA_real_, real_value = NA_real_)
}

phase_sim <- function(t, mult) {
  case_when(
    t == 0                       ~ "Start: fairly priced",
    t >= T_HEAL                  ~ "Aftermath: fairly priced again, but real value is scarred",
    t <  T_PEAK - 2              ~ "Boom: speculation inflates the red ring",
    t <= T_PEAK + 2              ~ "Peak: maximum bubble",
    mult >= 1                    ~ "Crash: speculative value collapses",
    t <= T_TROUGH + 2 & mult < 1 ~ "Panic: market falls BELOW real value",
    TRUE                         ~ "Recovery: prices climb back toward real value"
  )
}

# =============================================================================
# 2. Actual US housing data, 1900-2026
# =============================================================================
BASE_YEARS <- 1990:1999
JST_URL    <- "https://www.macrohistory.net/app/download/9834512469/JSTdatasetR6.xlsx"  # served as Stata .dta
CACHE      <- "housing_history.csv"

EPISODES <- list(
  "Full history (1900-2026)"                    = c(1900, 2026),
  "WWI boom & Great Depression (1914-1945)"     = c(1914, 1945),
  "Post-war housing boom (1940-1965)"           = c(1940, 1965),
  "2000s bubble & Great Recession (1995-2015)"  = c(1995, 2015),
  "Pandemic boom (2012-2026)"                   = c(2012, 2026)
)

read_fred <- function(id) {
  url <- paste0("https://fred.stlouisfed.org/graph/fredgraph.csv?id=", id)
  df  <- read.csv(url, stringsAsFactors = FALSE, na.strings = ".")
  names(df) <- c("date", "value")
  df %>%
    mutate(year = as.integer(year(as.Date(date))), value = as.numeric(value)) %>%
    filter(!is.na(value)) %>%
    group_by(year) %>%
    summarise(value = mean(value), .groups = "drop")
}

build_history <- function() {
  tmp <- tempfile(fileext = ".dta")
  download.file(JST_URL, tmp, mode = "wb", quiet = TRUE)
  jst <- read_dta(tmp) %>%
    filter(iso == "USA", year >= 1900, !is.na(housing_rent_yd)) %>%
    transmute(year = as.integer(year), pr = 1 / housing_rent_yd, hp = hpnom, cpi = cpi)
  jst <- jst %>% mutate(ratio = pr / mean(pr[year %in% BASE_YEARS]))

  fred <- read_fred("CSUSHPINSA") %>% rename(hp = value) %>%
    inner_join(read_fred("CUUR0000SEHA") %>% rename(rent = value), by = "year") %>%
    inner_join(read_fred("CPIAUCSL")     %>% rename(cpi  = value), by = "year") %>%
    mutate(pr = hp / rent) %>%
    mutate(ratio = pr / mean(pr[year %in% BASE_YEARS]))

  # chain FRED price and CPI levels onto JST levels at 1990
  k_hp  <- jst$hp[jst$year == 1990]  / fred$hp[fred$year == 1990]
  k_cpi <- jst$cpi[jst$year == 1990] / fred$cpi[fred$year == 1990]

  mv <- read_fred("HOOREVLMHMV") %>% rename(market_value = value)   # $ millions

  bind_rows(
    jst  %>% filter(year <  1990) %>% select(year, ratio, hp, cpi),
    fred %>% filter(year >= 1990) %>% transmute(year, ratio, hp = hp * k_hp, cpi = cpi * k_cpi)
  ) %>%
    filter(year <= 2026) %>%
    mutate(spec_idx = hp / cpi,              # inflation-adjusted market price
           real_idx = spec_idx / ratio) %>%  # inflation-adjusted rent-justified price
    left_join(mv, by = "year") %>%
    mutate(real_value = market_value / ratio) %>%
    arrange(year)
}

load_history <- function() {
  if (file.exists(CACHE)) return(read.csv(CACHE, stringsAsFactors = FALSE))
  d <- build_history()
  write.csv(d, CACHE, row.names = FALSE)
  d
}

history_window <- function(hist, from, to) {
  w  <- hist %>% filter(year >= from, year <= to)
  k  <- 100 / w$real_idx[1]                 # real value = 100 in the first year
  w %>% transmute(t = year, mult = ratio, real = real_idx * k, spec = spec_idx * k,
                  market_value, real_value)
}

phase_real <- function(mult, prev_mult) {
  rising <- !is.na(prev_mult) && mult > prev_mult
  case_when(
    mult < 0.98             ~ "Market BELOW real value: homes are undervalued",
    mult < 1.02             ~ "Fairly priced: market close to real value",
    mult >= 1.4 &  rising   ~ "Danger zone: bubble still inflating",
    mult >= 1.4            ~ "Danger zone: bubble starting to deflate",
    rising                  ~ "Boom: speculative premium growing",
    TRUE                    ~ "Deflating: speculative premium shrinking"
  )
}

fmt_t <- function(m) ifelse(is.na(m), "n/a", sprintf("$%.1f trillion", m / 1e6))

# =============================================================================
# Plots (shared by both modes)
# =============================================================================
bubble_plot <- function(row, r_lim, real0 = 100) {
  r_gold <- sqrt(row$real / real0)        # AREA proportional to value
  r_red  <- sqrt(row$spec / real0)
  r_ref  <- 1                             # starting real value, for reference
  p <- ggplot()
  if (row$spec >= row$real) {
    p <- p +
      geom_circle(aes(x0 = 0, y0 = 0, r = r_red), fill = RED, colour = NA, alpha = 0.9) +
      geom_circle(aes(x0 = 0, y0 = 0, r = r_gold), fill = GOLD, colour = NA)
  } else {
    # market below real value: blue ring = undervaluation gap,
    # gold outline = real value, red disc = what the market is actually paying
    p <- p +
      geom_circle(aes(x0 = 0, y0 = 0, r = r_gold), fill = BLUE, colour = NA, alpha = 0.35) +
      geom_circle(aes(x0 = 0, y0 = 0, r = r_red), fill = RED, colour = NA, alpha = 0.9) +
      geom_circle(aes(x0 = 0, y0 = 0, r = r_gold), colour = GOLD, linewidth = 2.5)
  }
  txt_col <- if (row$spec >= row$real) "#2B2B2B" else "white"
  p +
    geom_circle(aes(x0 = 0, y0 = 0, r = r_ref), colour = "#555555",
                linetype = "dotted", linewidth = 0.7) +
    annotate("text", 0, 0.08, label = sprintf("%.2fx", row$mult),
             fontface = "bold", size = 13, colour = txt_col) +
    annotate("text", 0, -0.17, label = "market / real", size = 4, colour = txt_col) +
    annotate("text", 0, -r_lim * 0.97, size = 3.4, colour = "#777777",
             label = "dotted circle = starting real value") +
    coord_equal(xlim = c(-r_lim, r_lim), ylim = c(-r_lim, r_lim)) +
    theme_void() +
    theme(plot.background = element_rect(fill = BG, colour = NA))
}

line_plot <- function(sim, t_now, xlab, ylab) {
  long <- sim %>%
    select(t, `Real value` = real, `Speculative value` = spec) %>%
    pivot_longer(-t, names_to = "series", values_to = "value")
  under <- sim %>% mutate(lo = pmin(spec, real), hi = real)
  over  <- sim %>% mutate(lo = real, hi = pmax(spec, real))
  t_pk  <- sim$t[which.max(sim$mult)]
  t_lo  <- sim$t[which.min(sim$mult)]
  y_top <- max(sim$spec, sim$real)

  p <- ggplot() +
    geom_ribbon(data = over,  aes(t, ymin = lo, ymax = hi), fill = RED,  alpha = 0.15) +
    geom_ribbon(data = under, aes(t, ymin = lo, ymax = hi), fill = BLUE, alpha = 0.25) +
    geom_line(data = long, aes(t, value, colour = series), linewidth = 1.1) +
    scale_colour_manual(values = c("Real value" = GOLD, "Speculative value" = RED), name = NULL) +
    geom_vline(xintercept = t_now, colour = "#2B2B2B", linewidth = 0.5) +
    annotate("text", t_pk, y_top * 1.05, size = 3.4, colour = "#555",
             label = sprintf("Peak %.2fx", max(sim$mult)))
  if (min(sim$mult) < 1)
    p <- p + annotate("text", t_lo, y_top * 1.12, size = 3.4, colour = "#555",
                      label = sprintf("Low %.2fx", min(sim$mult)))
  p +
    scale_y_continuous(limits = c(0, y_top * 1.16)) +
    labs(x = xlab, y = ylab) +
    theme_minimal(base_size = 12) +
    theme(plot.background = element_rect(fill = BG, colour = NA),
          legend.position = "top", panel.grid.minor = element_blank())
}

# =============================================================================
# App
# =============================================================================
ui <- fluidPage(
  tags$head(tags$style(HTML(sprintf(
    "body{background:%s;font-family:Helvetica,Arial,sans-serif;color:#2B2B2B}
     .phase{font-size:20px;font-weight:700;margin:4px 0 10px;min-height:52px}
     .stat{font-size:15px;margin:5px 0}
     .note{font-size:12px;color:#666}
     .key span{display:inline-block;width:12px;height:12px;border-radius:50%%;margin:0 5px 0 12px;vertical-align:middle}",
    BG)))),
  titlePanel("What happens when a bubble pops?"),
  div(class = "key",
      HTML(sprintf(paste0(
        "<span style='background:%s'></span>Real value",
        "<span style='background:%s'></span>Speculative value (market price)",
        "<span style='background:%s;opacity:.5'></span>Undervaluation gap (market below real value; gold outline = real value)"),
        GOLD, RED, BLUE))),
  br(),
  sliderInput("t", "Year (press play)", min = 1900, max = 2026, value = 1900, step = 1,
              sep = "", width = "100%",
              animate = animationOptions(interval = 1000, loop = FALSE)),   # 1 second per year
  fluidRow(
    column(3,
      wellPanel(
        radioButtons("mode", "Data",
                     c("Actual US housing data, 1900-2026" = "real", "Simulated scenario" = "sim"),
                     selected = "real"),
        conditionalPanel("input.mode == 'sim'",
          h4("Scenario"),
          sliderInput("peak", "Peak bubble (market / real)", 1.1, 2.5, 1.56, step = 0.01),
          sliderInput("trough", "Panic bottom (market / real)", 0.5, 1.0, 0.80, step = 0.01),
          sliderInput("damage", "Damage to real value from the crash (%)", 0, 40, 15, step = 1),
          p(class = "note",
            "Damage = how much the crash itself lowers fundamentals: foreclosures, fire sales, ",
            "job losses and tighter credit push rents and incomes down. Half of it is repaired ",
            "during the recovery.")
        ),
        conditionalPanel("input.mode == 'real'",
          selectInput("episode", "Period", names(EPISODES),
                      selected = "Full history (1900-2026)"),
          p(class = "note",
            "Values are adjusted for inflation and indexed so real value = 100 in the first ",
            "year of the period. Real value = what homes would cost if prices had tracked rents ",
            "(1990s price-to-rent ratio = fair)."),
          p(class = "note",
            "Pick a shorter period to zoom in: the Great Depression shows the market falling ",
            "below real value; the 2000s show the bubble popping.")
        )
      )
    ),
    column(4,
      div(class = "phase", textOutput("phase")),
      plotOutput("bubble", height = "400px")
    ),
    column(5,
      fluidRow(
        column(6,
          div(class = "stat", strong("Real value: "), textOutput("real", inline = TRUE)),
          div(class = "stat", strong("Market value: "), textOutput("spec", inline = TRUE))),
        column(6,
          div(class = "stat", strong("Gap: "), textOutput("gap", inline = TRUE)),
          div(class = "stat", strong("Market vs. peak: "), textOutput("drop", inline = TRUE)))
      ),
      uiOutput("dollars"),
      plotOutput("lines", height = "340px")
    )
  ),
  uiOutput("footer")
)

server <- function(input, output, session) {
  hist <- reactiveVal(NULL)

  # load the history the first time "actual data" is selected
  observeEvent(input$mode, {
    if (input$mode == "real" && is.null(hist())) {
      withProgress(message = "Loading 1900-2026 housing data...", value = 0.5, {
        hist(load_history())
      })
    }
  })

  # reset the timeline whenever the mode or period changes
  observeEvent(list(input$mode, input$episode, hist()), {
    if (input$mode == "sim") {
      updateSliderInput(session, "t", min = 0, max = T_MAX, value = 0)
    } else if (!is.null(hist())) {
      rng <- EPISODES[[input$episode]]
      updateSliderInput(session, "t", min = rng[1], max = rng[2], value = rng[1])
    }
  })

  sim <- reactive({
    if (input$mode == "sim") {
      simulate(input$peak, input$trough, input$damage / 100)
    } else {
      req(hist())
      rng <- EPISODES[[input$episode]]
      history_window(hist(), rng[1], rng[2])
    }
  })

  row <- reactive({
    r <- sim()[sim()$t == input$t, ]
    req(nrow(r) == 1)                      # wait for the slider to catch up
    r
  })
  prev_mult <- reactive({
    p <- sim()$mult[sim()$t == input$t - 1]
    if (length(p)) p else NA
  })
  r_lim <- reactive(sqrt(max(sim()$spec, sim()$real, 100) / 100) * 1.05)

  output$bubble <- renderPlot(bubble_plot(row(), r_lim()), bg = BG)
  output$lines  <- renderPlot({
    if (input$mode == "sim")
      line_plot(sim(), input$t, "Time", "Value (starting real value = 100)")
    else
      line_plot(sim(), input$t, NULL, "Inflation-adjusted value (start = 100)")
  }, bg = BG)

  output$phase <- renderText({
    if (input$mode == "sim") phase_sim(row()$t, row()$mult)
    else paste0(row()$t, ": ", phase_real(row()$mult, prev_mult()))
  })
  output$real <- renderText(sprintf("%.0f (%+.0f%% vs. start)", row()$real, row()$real - 100))
  output$spec <- renderText(sprintf("%.0f", row()$spec))
  output$gap  <- renderText({
    g <- row()$spec - row()$real
    if (g >= 0) sprintf("%.0f speculative premium", g) else sprintf("%.0f below real value", -g)
  })
  output$drop <- renderText(sprintf("%+.0f%%", 100 * (row()$spec / max(sim()$spec) - 1)))

  output$dollars <- renderUI({
    if (input$mode != "real") return(NULL)
    r <- row()
    if (is.na(r$market_value))
      return(div(class = "note", "Dollar totals start in 1945, when Federal Reserve data begin."))
    div(class = "stat",
        strong("All US owner-occupied homes: "),
        sprintf("market %s, real %s (not inflation-adjusted)",
                fmt_t(r$market_value), fmt_t(r$real_value)))
  })

  output$footer <- renderUI({
    if (input$mode == "sim")
      p(class = "note",
        "Stylised model, not a forecast. Defaults are loosely based on US housing: the market peaked at about ",
        "1.56x rent-justified value in 2006, and in the 1930s prices fell to about 0.8x.")
    else
      p(class = "note",
        "Sources: Jorda-Schularick-Taylor Macrohistory Database (1900-1989); S&P CoreLogic Case-Shiller ",
        "US National Home Price Index, BLS CPI Rent of Primary Residence and CPI via FRED (1990-2026); ",
        "Federal Reserve Z.1 via FRED (dollar totals, 1945-2026). Annual averages; 2026 is year-to-date. ",
        "The two price-to-rent sources are joined at 1990.")
  })
}

shinyApp(ui, server)
```

## An Economic Bubble Modeler

```
# =============================================================================
# What happens when a bubble pops?  Interactive Shiny app for RStudio
#
#   Gold circle = real value (what the asset is fundamentally worth)
#   Red circle  = speculative value (what the market is paying)
#
# A bubble goes through five phases: Boom -> Peak -> Crash -> Panic (overshoot,
# market value falls BELOW real value) -> Recovery. The crash also damages
# real value itself: foreclosures, fire sales, job losses and tighter credit
# lower rents and incomes, so the gold circle shrinks too.
#
# Press play on the timeline slider, or drag it, and adjust the scenario
# sliders to see how a bigger bubble, a deeper panic or more economic damage
# changes the picture.
#
# HOW TO RUN IN RSTUDIO
#   1. Install packages once (Console):
#        install.packages(c("shiny", "ggplot2", "ggforce", "dplyr", "tidyr"))
#   2. Open this file (app.R) and click "Run App".
#
# This is a stylised model, not a forecast. Default settings are loosely based
# on US housing: peak ~1.56x in 2006 (Case-Shiller / CPI rent, 1990s = fair),
# and the 1930s, when prices fell to ~0.8x of rent-justified value.
# =============================================================================

library(shiny)
library(ggplot2)
library(ggforce)
library(dplyr)
library(tidyr)

GOLD <- "#D4A017"; RED <- "#C0392B"; BLUE <- "#3B7DD8"; BG <- "#FAF8F3"
T_MAX <- 100            # model time steps (think "months" or "quarters")

# ---- Model --------------------------------------------------------------------
# Phase timing (fractions of the timeline)
T_PEAK   <- 40          # bubble peaks
T_TROUGH <- 58          # panic bottom (market below real value)
T_HEAL   <- 90          # market back to fair value

smooth <- function(x) x * x * (3 - 2 * x)     # smooth 0 -> 1 ramp

simulate <- function(peak, trough, damage, real0 = 100, growth = 0.002) {
  t <- 0:T_MAX
  # multiplier = market value / real value
  mult <- case_when(
    t <= T_PEAK   ~ 1 + (peak - 1) * smooth(t / T_PEAK),
    t <= T_TROUGH ~ peak + (trough - peak) * smooth((t - T_PEAK) / (T_TROUGH - T_PEAK)),
    t <= T_HEAL   ~ trough + (1 - trough) * smooth((t - T_TROUGH) / (T_HEAL - T_TROUGH)),
    TRUE          ~ 1
  )
  # real value: slow trend growth, minus crash damage that hits after the peak
  # and is only partly repaired by the end
  hit <- case_when(
    t <= T_PEAK        ~ 0,
    t <= T_TROUGH + 6  ~ damage * smooth((t - T_PEAK) / (T_TROUGH + 6 - T_PEAK)),
    TRUE               ~ damage * (1 - 0.5 * smooth(pmin((t - T_TROUGH - 6) / 30, 1)))
  )
  real <- real0 * (1 + growth)^t * (1 - hit)
  tibble(t, mult, real, spec = real * mult)
}

phase <- function(t, mult) {
  case_when(
    t == 0                       ~ "Start: fairly priced",
    t >= T_HEAL                  ~ "Aftermath: fairly priced again, but real value is scarred",
    t <  T_PEAK - 2              ~ "Boom: speculation inflates the red ring",
    t <= T_PEAK + 2              ~ "Peak: maximum bubble",
    mult >= 1                    ~ "Crash: speculative value collapses",
    t <= T_TROUGH + 2 & mult < 1 ~ "Panic: market falls BELOW real value",
    TRUE                         ~ "Recovery: prices climb back toward real value"
  )
}

# ---- Plots --------------------------------------------------------------------
bubble_plot <- function(row, r_lim, real0) {
  r_gold <- sqrt(row$real / real0)        # AREA proportional to value
  r_red  <- sqrt(row$spec / real0)
  r_ref  <- 1                             # starting real value, for reference
  p <- ggplot()
  if (row$spec >= row$real) {
    p <- p +
      geom_circle(aes(x0 = 0, y0 = 0, r = r_red), fill = RED, colour = NA, alpha = 0.9) +
      geom_circle(aes(x0 = 0, y0 = 0, r = r_gold), fill = GOLD, colour = NA)
  } else {
    # market below real value: blue ring = undervaluation gap,
    # gold outline = real value, red disc = what the market is actually paying
    p <- p +
      geom_circle(aes(x0 = 0, y0 = 0, r = r_gold), fill = BLUE, colour = NA, alpha = 0.35) +
      geom_circle(aes(x0 = 0, y0 = 0, r = r_red), fill = RED, colour = NA, alpha = 0.9) +
      geom_circle(aes(x0 = 0, y0 = 0, r = r_gold), colour = GOLD, linewidth = 2.5)
  }
  txt_col <- if (row$spec >= row$real) "#2B2B2B" else "white"
  p +
    geom_circle(aes(x0 = 0, y0 = 0, r = r_ref), colour = "#555555",
                linetype = "dotted", linewidth = 0.7) +
    annotate("text", 0, 0.08, label = sprintf("%.2fx", row$mult),
             fontface = "bold", size = 13, colour = txt_col) +
    annotate("text", 0, -0.17, label = "market / real", size = 4, colour = txt_col) +
    annotate("text", 0, -r_lim * 0.97, size = 3.4, colour = "#777777",
             label = "dotted circle = starting real value") +
    coord_equal(xlim = c(-r_lim, r_lim), ylim = c(-r_lim, r_lim)) +
    theme_void() +
    theme(plot.background = element_rect(fill = BG, colour = NA))
}

line_plot <- function(sim, t_now) {
  long <- sim %>%
    select(t, `Real value` = real, `Speculative value` = spec) %>%
    pivot_longer(-t, names_to = "series", values_to = "value")
  under <- sim %>% mutate(lo = pmin(spec, real), hi = real) %>% filter(spec < real)
  over  <- sim %>% mutate(lo = real, hi = pmax(spec, real))

  ggplot() +
    geom_ribbon(data = over,  aes(t, ymin = lo, ymax = hi), fill = RED,  alpha = 0.15) +
    geom_ribbon(data = under, aes(t, ymin = lo, ymax = hi), fill = BLUE, alpha = 0.25) +
    geom_line(data = long, aes(t, value, colour = series), linewidth = 1.1) +
    scale_colour_manual(values = c("Real value" = GOLD, "Speculative value" = RED), name = NULL) +
    geom_vline(xintercept = t_now, colour = "#2B2B2B", linewidth = 0.5) +
    annotate("text", T_PEAK, max(sim$spec) * 1.04, label = "Peak", size = 3.5, colour = "#555") +
    annotate("text", T_TROUGH, max(sim$spec) * 1.04, label = "Panic bottom", size = 3.5,
             colour = "#555") +
    scale_y_continuous(limits = c(0, max(sim$spec) * 1.08)) +
    labs(x = "Time", y = "Value (starting real value = 100)") +
    theme_minimal(base_size = 12) +
    theme(plot.background = element_rect(fill = BG, colour = NA),
          legend.position = "top", panel.grid.minor = element_blank())
}

# ---- App ----------------------------------------------------------------------
ui <- fluidPage(
  tags$head(tags$style(HTML(sprintf(
    "body{background:%s;font-family:Helvetica,Arial,sans-serif;color:#2B2B2B}
     .phase{font-size:22px;font-weight:700;margin:4px 0 10px}
     .stat{font-size:15px;margin:5px 0}
     .note{font-size:12px;color:#666}
     .key span{display:inline-block;width:12px;height:12px;border-radius:50%%;margin:0 5px 0 12px;vertical-align:middle}",
    BG)))),
  titlePanel("What happens when a bubble pops?"),
  div(class = "key",
      HTML(sprintf(paste0(
        "<span style='background:%s'></span>Real value",
        "<span style='background:%s'></span>Speculative value (market price)",
        "<span style='background:%s;opacity:.5'></span>Undervaluation gap (market below real value; gold outline = real value)"),
        GOLD, RED, BLUE))),
  br(),
  sliderInput("t", "Timeline (press play)", min = 0, max = T_MAX, value = 0, step = 1,
              width = "100%", animate = animationOptions(interval = 120, loop = FALSE)),
  fluidRow(
    column(3,
      wellPanel(
        h4("Scenario"),
        sliderInput("peak", "Peak bubble (market / real)", 1.1, 2.5, 1.56, step = 0.01),
        sliderInput("trough", "Panic bottom (market / real)", 0.5, 1.0, 0.80, step = 0.01),
        sliderInput("damage", "Damage to real value from the crash (%)", 0, 40, 15, step = 1),
        p(class = "note",
          "Damage = how much the crash itself lowers fundamentals: foreclosures, fire sales, ",
          "job losses and tighter credit push rents and incomes down. Half of it is repaired ",
          "during the recovery.")
      )
    ),
    column(4,
      div(class = "phase", textOutput("phase")),
      plotOutput("bubble", height = "400px")
    ),
    column(5,
      fluidRow(
        column(6,
          div(class = "stat", strong("Real value: "), textOutput("real", inline = TRUE)),
          div(class = "stat", strong("Market value: "), textOutput("spec", inline = TRUE))),
        column(6,
          div(class = "stat", strong("Gap: "), textOutput("gap", inline = TRUE)),
          div(class = "stat", strong("Market vs. peak: "), textOutput("drop", inline = TRUE)))
      ),
      plotOutput("lines", height = "360px")
    )
  ),
  p(class = "note",
    "Stylised model, not a forecast. Defaults are loosely based on US housing: the market peaked at about ",
    "1.56x rent-justified value in 2006, and in the 1930s prices fell to about 0.8x.")
)

server <- function(input, output, session) {
  sim   <- reactive(simulate(input$peak, input$trough, input$damage / 100))
  row   <- reactive(sim()[sim()$t == input$t, ])
  r_lim <- reactive(sqrt(max(sim()$spec, sim()$real) / 100) * 1.05)

  output$bubble <- renderPlot(bubble_plot(row(), r_lim(), 100), bg = BG)
  output$lines  <- renderPlot(line_plot(sim(), input$t), bg = BG)
  output$phase  <- renderText(phase(row()$t, row()$mult))
  output$real   <- renderText(sprintf("%.0f (%+.0f%% vs. start)", row()$real, row()$real - 100))
  output$spec   <- renderText(sprintf("%.0f", row()$spec))
  output$gap    <- renderText({
    g <- row()$spec - row()$real
    if (g >= 0) sprintf("%.0f speculative premium", g) else sprintf("%.0f below real value", -g)
  })
  output$drop   <- renderText(sprintf("%+.0f%%", 100 * (row()$spec / max(sim()$spec) - 1)))
}

shinyApp(ui, server)
```

## WHEN you bought your house change your reality

```
# =============================================================================
# Interactive: how WHEN you bought your house changes the cost-of-living
# reality you live in
#
# HOW TO RUN (pick one):
#   A) In the RStudio Console press Esc until you see a plain ">" prompt, then
#      type   source(file.choose())   and choose this file.
#   B) File > Open File > this file, then click the Source button.
#   Do not paste the code into the Console.
# It installs missing packages, downloads data from FRED (saved to
# ~/house_timing_data.csv so it still works offline later), and opens the app.
#
# HOW IT WORKS
#   1. Pick the year you bought. The app fills in that year's typical values:
#        house price      = US median sales price of houses sold
#        interest rate    = average 30-year fixed mortgage rate that year
#        average salary   = Social Security national average wage index for
#                           that year, per year before tax (x 2 for two
#                           earners). Take-home pay = salary minus the tax
#                           toggle (default 22%), per month
#        cost of living   = everyday non-housing spending per month: $1,600
#                           in 2026 dollars for one adult (+50% for a second),
#                           scaled back to the purchase year with the CPI
#   2. Toggle nominal dollars (dollars of each year) or real dollars
#      (inflation-adjusted to 2026 dollars), and dollars or share of pay.
#      Change any toggle: down payment, house price, interest rate, cost of
#      living, average salary, taxes (plus loan term, taxes/insurance, and the
#      growth assumptions for years after 2026).
#   3. The charts follow the loan year by year. The mortgage payment is FIXED,
#      but pay and prices keep rising (actual history through 2026, then your
#      assumptions), so the same loan can feel crushing or easy depending on
#      when it started.
#
# DATA (FRED, Federal Reserve Bank of St. Louis, https://fred.stlouisfed.org/)
#   MSPUS           median sales price of houses sold
#   MORTGAGE30US    30-year fixed mortgage rate (Freddie Mac)
#   LEU0252881500Q  median weekly earnings, full-time workers: extends the
#                   average wage past the latest SSA year (by its growth)
#   AHETPI          average hourly earnings, used to extend pay back before 1979
# Social Security Administration, National Average Wage Index (built in below)
#   https://www.ssa.gov/oact/cola/AWI.html
#   CPIAUCNS        consumer price index (cost of living, taxes and insurance)
# =============================================================================

# ---- 1. Install and load packages (only installs what is missing) -------------
packages <- c("shiny", "bslib", "plotly", "dplyr", "scales")
missing  <- packages[!packages %in% rownames(installed.packages())]
if (length(missing) > 0) install.packages(missing)
invisible(lapply(packages, library, character.only = TRUE))

TAX_DEFAULT   <- 22      # % of salary assumed to go to taxes (default of the tax toggle)
COL_2026      <- 1600    # one adult's everyday non-housing cost of living per month, 2026 dollars (preset)
COL_2ND       <- 0.5     # a second adult adds this share to the cost of living

# ---- 2. Data (downloads once, then uses the saved copy) ------------------------
cache <- file.path(path.expand("~"), "house_timing_data.csv")
# Built-in copy of the data (annual averages from FRED, downloaded October 2026).
# Used automatically if FRED cannot be reached and there is no saved copy, so
# the app always opens.
BUILT_IN <- read.csv(text = "year,price,rate,cpi,pay
1972,27525,7.383,41.817,7694
1973,32600,8.045,44.400,8164
1974,36050,9.187,49.308,8754
1975,39275,9.047,53.817,9348
1976,44225,8.866,56.908,9981
1977,48900,8.845,60.608,10727
1978,55850,9.642,65.233,11592
1979,62750,11.204,72.575,12506
1980,64750,13.742,82.408,13598
1981,68950,16.642,90.925,14716
1982,69225,16.044,96.500,15678
1983,75375,13.235,99.600,16263
1984,79950,13.878,103.883,16939
1985,84275,12.430,107.567,17862
1986,92025,10.187,109.608,18642
1987,104700,10.213,113.625,19396
1988,112225,10.342,118.258,20020
1989,120425,10.319,123.967,20774
1990,122300,10.129,130.658,21437
1991,119975,9.247,136.192,22191
1992,121375,8.390,140.317,22893
1993,126500,7.315,144.458,23842
1994,130425,8.381,148.225,24284
1995,133475,7.935,152.383,24908
1996,140250,7.806,156.850,25506
1997,145000,7.599,160.517,26169
1998,151925,6.943,163.008,27261
1999,160125,7.440,166.575,28535
2000,167550,8.053,172.200,29913
2001,173100,6.968,177.067,30979
2002,186025,6.537,179.875,31616
2003,192125,5.827,183.958,32227
2004,218150,5.839,188.883,33176
2005,236550,5.867,195.292,33852
2006,243750,6.413,201.592,34892
2007,244950,6.337,207.342,36114
2008,229550,6.027,215.303,37518
2009,215650,5.037,214.537,38454
2010,222700,4.690,218.055,38818
2011,224900,4.448,224.939,39325
2012,244400,3.658,229.594,39949
2013,266225,3.976,232.957,40378
2014,285775,4.169,236.736,41145
2015,294150,3.851,237.017,42081
2016,305125,3.654,240.007,43290
2017,322425,3.990,245.120,44720
2018,325275,4.545,251.107,46072
2019,320250,3.936,255.657,47684
2020,328150,3.112,258.811,51181
2021,383000,2.958,270.970,51870
2022,432950,5.344,292.655,55029
2023,426525,6.807,304.702,58019
2024,418975,6.721,313.689,60307
2025,415400,6.595,321.943,62469
2026,409600,6.431,331.655,64636")

# Download one FRED series, trying several times and two download methods.
# "Failure when receiving data from the peer" is usually a temporary network,
# firewall/VPN or SSL hiccup, so retrying with a longer timeout often works.
fred_y <- function(id, tries = 3) {
  url <- paste0("https://fred.stlouisfed.org/graph/fredgraph.csv?id=", id)
  old <- options(timeout = max(120, getOption("timeout"))); on.exit(options(old))
  methods <- c(if (capabilities("libcurl")) "libcurl", if (.Platform$OS.type == "windows") "wininet", "auto")
  for (k in seq_len(tries)) for (m in unique(methods)) {
    tmp <- tempfile(fileext = ".csv")
    ok <- tryCatch({
      suppressWarnings(download.file(url, tmp, method = m, quiet = TRUE, mode = "wb",
                                     headers = c("User-Agent" = "Mozilla/5.0 (RStudio)")))
      d <- read.csv(tmp, na.strings = ".")
      ncol(d) >= 2 && nrow(d) > 10
    }, error = function(e) FALSE)
    if (isTRUE(ok)) {
      names(d)[1:2] <- c("date", "value")
      return(d %>% mutate(year = as.integer(substr(date, 1, 4)), value = as.numeric(value)) %>%
               filter(!is.na(value)) %>% group_by(year) %>% summarise(value = mean(value), .groups = "drop"))
    }
    Sys.sleep(2 * k)
  }
  stop("Could not download ", id, " from FRED")
}
dat <- tryCatch({
  message("Downloading data from FRED ...")
  pay <- fred_y("LEU0252881500Q") %>% transmute(year, pay = value * 52)
  ahe <- fred_y("AHETPI") %>% rename(ahe = value)
  d <- fred_y("MSPUS") %>% rename(price = value) %>%
    inner_join(fred_y("MORTGAGE30US") %>% rename(rate = value), by = "year") %>%
    inner_join(fred_y("CPIAUCNS") %>% rename(cpi = value), by = "year") %>%
    left_join(pay, by = "year") %>% left_join(ahe, by = "year") %>% arrange(year)
  for (y in rev(d$year[is.na(d$pay)]))            # back-cast pay before 1979
    d$pay[d$year == y] <- d$pay[d$year == y + 1] * d$ahe[d$year == y] / d$ahe[d$year == y + 1]
  d <- d %>% select(year, price, rate, cpi, pay) %>% filter(year >= 1972, !is.na(pay))
  write.csv(d, cache, row.names = FALSE); d
}, error = function(e) {
  if (file.exists(cache)) {
    message("FRED download failed (", conditionMessage(e), "). Using your saved copy: ", cache); read.csv(cache)
  } else {
    message("FRED download failed (", conditionMessage(e), "). Using the built-in data (through 2026).")
    BUILT_IN
  }
})
# Average salary: SSA national average wage index (all workers' average yearly
# wages); years after the latest SSA value are extended with pay growth.
AWI <- read.csv(text = "year,awi
1972,7133.80
1973,7580.16
1974,8030.76
1975,8630.92
1976,9226.48
1977,9779.44
1978,10556.03
1979,11479.46
1980,12513.46
1981,13773.10
1982,14531.34
1983,15239.24
1984,16135.07
1985,16822.51
1986,17321.82
1987,18426.51
1988,19334.04
1989,20099.55
1990,21027.98
1991,21811.60
1992,22935.42
1993,23132.67
1994,23753.53
1995,24705.66
1996,25913.90
1997,27426.00
1998,28861.44
1999,30469.84
2000,32154.82
2001,32921.92
2002,33252.09
2003,34064.95
2004,35648.55
2005,36952.94
2006,38651.41
2007,40405.48
2008,41334.97
2009,40711.61
2010,41673.83
2011,42979.61
2012,44321.67
2013,44888.16
2014,46481.52
2015,48098.63
2016,48642.15
2017,50321.89
2018,52145.80
2019,54099.99
2020,55628.60
2021,60575.07
2022,63795.13
2023,66621.80
2024,69846.57")
dat <- dat %>% left_join(AWI, by = "year") %>% arrange(year)
for (y in dat$year[is.na(dat$awi)]) {
  if (y > max(AWI$year)) dat$awi[dat$year == y] <- dat$awi[dat$year == y - 1] * dat$pay[dat$year == y] / dat$pay[dat$year == y - 1]
}
dat$salary <- dat$awi
LAST <- max(dat$year); FIRST <- min(dat$year)
cpi_last <- dat$cpi[dat$year == LAST]

preset <- function(y, earners = 1) {
  r <- dat[dat$year == y, ]
  list(price = round(r$price, -2), rate = round(r$rate, 2),
       salary = round(earners * r$salary, -2),
       col = round(COL_2026 * (1 + COL_2ND * (earners - 1)) * r$cpi / cpi_last, -1))
}

# index paths: actual history through LAST, then assumed growth
path <- function(y0, years, col, g) {
  sapply(years, function(t) {
    if (t <= LAST) dat[[col]][dat$year == t] / dat[[col]][dat$year == y0]
    else dat[[col]][dat$year == LAST] / dat[[col]][dat$year == y0] * (1 + g)^(t - LAST)
  })
}

simulate <- function(y0, price, down_pct, rate, term, salary, tax, col, tax_ins, inc_g, inf_g, home_g = inf_g) {
  income <- salary * (1 - tax / 100) / 12          # monthly take-home pay in the purchase year
  loan <- price * (1 - down_pct / 100); i <- rate / 1200; n <- term * 12
  pi   <- if (i == 0) loan / n else loan * i / (1 - (1 + i)^-n)
  yrs  <- y0:(y0 + term - 1)
  inc_ix <- path(y0, yrs, "salary", inc_g / 100); cpi_ix <- path(y0, yrs, "cpi", inf_g / 100)
  home_ix <- path(y0, yrs, "price", home_g / 100)   # home value follows the US median price
  bal <- loan; interest <- numeric(term); principal <- numeric(term); bal_end <- numeric(term)
  for (k in 1:term) {
    for (m in 1:12) {
      int <- bal * i; prn <- pi - int; bal <- max(bal - prn, 0)
      interest[k] <- interest[k] + int; principal[k] <- principal[k] + prn
    }
    bal_end[k] <- bal
  }
  data.frame(year = yrs, t = seq_along(yrs) - 1,
             income = income * inc_ix,
             mortgage = pi,
             tax_ins = price * tax_ins / 100 / 12 * cpi_ix,
             living = col * cpi_ix,
             cpi_ix = cpi_ix, interest = interest, principal = principal,
             to_real = cpi_last / dat$cpi[dat$year == y0] / cpi_ix,     # x this = dollars of LAST
             loan = loan, rate = rate, bal_end = bal_end, home_value = price * home_ix) %>%
    mutate(left = income - mortgage - tax_ins - living)
}

# ---- 3. App --------------------------------------------------------------------
p0 <- preset(LAST)
money <- function(x) dollar(round(x))
COLS <- c(mortgage = "#C0392B", tax_ins = "#E59866", living = "#2C6E9B", left = "#2E8B57", short = "#7B241C")

budget_plot <- function(s, view, dollars) {
    u <- if (view == "pct") "pct" else dollars
    conv <- function(x) switch(u, pct = 100 * x / s$income, nom = x, real = x * s$to_real)
    lab  <- function(x) if (u == "pct") sprintf("%.1f%%", x) else dollar(round(x))
    df <- data.frame(year = s$year, mortgage = conv(s$mortgage), tax_ins = conv(s$tax_ins),
                     living = conv(s$living), left = conv(pmax(s$left, 0)), short = conv(pmin(s$left, 0)),
                     income = conv(s$income))
    p <- plot_ly(df, x = ~year)
    add <- function(p, y, name, col) add_trace(p, y = df[[y]], name = name, type = "bar",
                                               marker = list(color = col), text = lab(df[[y]]),
                                               hovertemplate = paste0("%{x} ", name, ": %{text}<extra></extra>"), textposition = "none")
    p <- p %>% add("mortgage", "Mortgage payment (fixed)", COLS["mortgage"]) %>%
      add("tax_ins", "Property tax + insurance", COLS["tax_ins"]) %>%
      add("living", "Cost of living", COLS["living"]) %>%
      add("left", "Left over", COLS["left"]) %>%
      add("short", "Shortfall (spending more than take-home pay)", COLS["short"])
    if (u == "pct") p <- p %>% add_trace(x = df$year, y = rep(100, nrow(df)), name = "Take-home pay (100%)", type = "scatter",
                                         mode = "lines", line = list(color = "#222", width = 2, dash = "dash"), hoverinfo = "skip")
    if (u != "pct") p <- p %>% add_trace(y = ~income, name = "Take-home pay", type = "scatter", mode = "lines",
                                         line = list(color = "#222", width = 2.5),
                                         text = lab(df$income), hovertemplate = "%{x} take-home pay: %{text}<extra></extra>")
    p %>% layout(barmode = "relative", bargap = 0.1, hovermode = "x unified",
                 yaxis = list(title = "", ticksuffix = if (u == "pct") "%" else "", tickprefix = if (u == "pct") "" else "$", tickformat = if (u == "pct") "" else ",.0f",
                              zeroline = TRUE),
                 xaxis = list(title = ""), legend = list(orientation = "h", y = -0.12, x = 0),
                 margin = list(t = 30),
                 shapes = if (LAST < max(df$year)) list(list(type = "line", x0 = LAST + 0.5, x1 = LAST + 0.5, yref = "paper",
                              y0 = 0, y1 = 1, line = list(dash = "dot", color = "#777"))) else NULL,
                 annotations = if (LAST < max(df$year)) list(list(x = LAST + 0.6, y = 1, yref = "paper", xanchor = "left",
                              text = "assumptions from here", showarrow = FALSE, font = list(size = 11, color = "#555"))) else NULL) %>%
      config(displaylogo = FALSE)
}

compare_plot <- function(a, b, y_you, y_cmp, view, dollars) {
    val <- function(s) if (view == "pct") 100 * s$left / s$income else if (dollars == "real") s$left * s$to_real else s$left
    ht  <- if (view == "pct") "Year %{x} of loan (%{text}): %{y:.1f}% left over<extra></extra>"
           else "Year %{x} of loan (%{text}): $%{y:,.0f} left over per month<extra></extra>"
    plot_ly() %>%
      add_lines(x = a$t, y = val(a), name = sprintf("You: bought %d", y_you),
                line = list(color = "#2E8B57", width = 3), text = a$year, hovertemplate = ht) %>%
      add_lines(x = b$t, y = val(b), name = sprintf("Typical buyer in %d", y_cmp),
                line = list(color = "#7F8C8D", width = 3, dash = "dash"), text = b$year, hovertemplate = ht) %>%
      layout(xaxis = list(title = "Years since buying"),
             yaxis = list(title = "", ticksuffix = if (view == "pct") "%" else "", tickprefix = if (view == "pct") "" else "$", tickformat = if (view == "pct") "" else ",.0f",
                          zeroline = TRUE),
             legend = list(orientation = "h", y = -0.25, x = 0), hovermode = "x unified", margin = list(t = 20)) %>%
      config(displaylogo = FALSE)
}


# ---- Dollar devaluation: how inflation changes a fixed-rate mortgage ----------
# A fixed-rate mortgage is a debt in dollars. As each dollar buys less, the same
# payment and the same remaining balance are worth less, while the house tends
# to keep its value. These helpers measure that effect.
dev_stats <- function(s) {
  term <- nrow(s); pay_year <- 12 * s$mortgage
  nominal_total <- sum(pay_year)
  real_total    <- sum(pay_year / s$cpi_ix)                    # in purchase-year dollars
  infl          <- s$cpi_ix[term]^(1 / max(term - 1, 1)) - 1   # average yearly inflation over the loan
  k10 <- min(11, term)
  list(nominal_total = nominal_total, real_total = real_total,
       erased = 1 - real_total / nominal_total,                  # share of the payments inflation wiped out
       infl = infl,
       real_rate = (1 + s$rate[1] / 100) / (1 + infl) - 1,       # realized real interest rate
       pay_real_10 = s$mortgage[k10] / s$cpi_ix[k10],             # payment in year 10, purchase-year dollars
       dollar_10 = 1 / s$cpi_ix[k10],                             # value of $1 after 10 years
       partly_assumed = max(s$year) > LAST)
}

dev_payment_plot <- function(s, y0) {
  real <- s$mortgage / s$cpi_ix
  plot_ly(x = s$year) %>%
    add_lines(y = rep(s$mortgage[1], nrow(s)), name = "Payment in dollars of each year (fixed)",
              line = list(color = "#C0392B", width = 3),
              hovertemplate = "%{x}: $%{y:,.0f} nominal<extra></extra>") %>%
    add_lines(y = real, name = sprintf("Same payment in %d dollars (what it really costs you)", y0),
              line = list(color = "#2C6E9B", width = 3),
              text = sprintf("$1 from %d is worth %s", y0, dollar(1 / s$cpi_ix, accuracy = 0.01)),
              hovertemplate = paste0("%{x}: $%{y:,.0f} in ", y0, " dollars<br>%{text}<extra></extra>")) %>%
    layout(yaxis = list(title = "", tickprefix = "$", tickformat = ",.0f", rangemode = "tozero"),
           xaxis = list(title = ""), hovermode = "x unified",
           legend = list(orientation = "h", y = -0.15, x = 0), margin = list(t = 20)) %>%
    config(displaylogo = FALSE)
}

dev_equity_plot <- function(s, y0) {
  hv <- s$home_value / s$cpi_ix; bl <- s$bal_end / s$cpi_ix
  plot_ly(x = s$year) %>%
    add_lines(y = hv, name = "Home value", line = list(color = "#2E8B57", width = 3),
              hovertemplate = paste0("%{x}: home $%{y:,.0f} in ", y0, " dollars<extra></extra>")) %>%
    add_lines(y = bl, name = "Loan you still owe", line = list(color = "#C0392B", width = 3),
              fill = "tozeroy", fillcolor = "rgba(192,57,43,0.10)",
              hovertemplate = paste0("%{x}: owed $%{y:,.0f} in ", y0, " dollars<extra></extra>")) %>%
    add_lines(y = s$bal_end, name = "Loan you still owe (nominal)", line = list(color = "#C0392B", width = 2, dash = "dot"),
              hovertemplate = "%{x}: owed $%{y:,.0f} nominal<extra></extra>") %>%
    layout(yaxis = list(title = "", tickprefix = "$", tickformat = ",.0f", rangemode = "tozero"),
           xaxis = list(title = ""), hovermode = "x unified",
           legend = list(orientation = "h", y = -0.15, x = 0), margin = list(t = 20)) %>%
    config(displaylogo = FALSE)
}

# every purchase year with that year's typical house, rate and pay
all_years <- function(earners, down, term, taxins, incg, infg, homeg) {
  do.call(rbind, lapply(FIRST:LAST, function(y) {
    p <- preset(y, earners)
    s <- simulate(y, p$price, down, p$rate, term, p$salary, TAX_DEFAULT, p$col, taxins, incg, infg, homeg)
    d <- dev_stats(s)
    data.frame(year = y, rate = p$rate, infl = 100 * d$infl, real_rate = 100 * d$real_rate,
               erased = 100 * d$erased, dollar_10 = d$dollar_10, partly = d$partly_assumed)
  }))
}

dev_years_plot <- function(A, y_you, y_cmp, metric) {
  m <- switch(metric,
    real = list(col = "real_rate", name = "Real interest rate you actually paid (mortgage rate minus inflation)", suf = "%"),
    erased = list(col = "erased", name = "Share of your 30 years of payments wiped out by inflation", suf = "%"),
    both = NULL)
  if (metric == "both") {
    p <- plot_ly(A, x = ~year) %>%
      add_bars(y = ~rate, name = "Mortgage rate when bought", marker = list(color = "rgba(192,57,43,0.35)"),
               hovertemplate = "%{x}: mortgage rate %{y:.2f}%<extra></extra>") %>%
      add_lines(y = ~infl, name = "Average inflation over the loan", line = list(color = "#2C6E9B", width = 3),
                hovertemplate = "%{x}: inflation %{y:.2f}%/yr<extra></extra>") %>%
      add_lines(y = ~real_rate, name = "Real rate actually paid", line = list(color = "#222", width = 3),
                hovertemplate = "%{x}: real rate %{y:.2f}%<extra></extra>")
  } else {
    p <- plot_ly(A, x = ~year, y = A[[m$col]], type = "bar", name = m$name,
                 marker = list(color = ifelse(A$year %in% c(y_you, y_cmp), "#C0392B",
                                              ifelse(A$partly, "rgba(44,110,155,0.45)", "#2C6E9B"))),
                 hovertemplate = paste0("%{x}: %{y:.1f}", m$suf, "<extra></extra>"))
  }
  hi <- A[A$year %in% c(y_you, y_cmp), ]
  ycol <- if (metric == "both") "real_rate" else m$col
  p %>% add_annotations(x = hi$year, y = hi[[ycol]], text = paste0("<b>", hi$year, "</b>"), showarrow = TRUE,
                        arrowhead = 0, ay = -35, font = list(color = "#C0392B")) %>%
    layout(yaxis = list(title = "", ticksuffix = "%", zeroline = TRUE), xaxis = list(title = "Year bought"),
           hovermode = "x unified", showlegend = metric == "both",
           legend = list(orientation = "h", y = -0.2, x = 0), margin = list(t = 20)) %>%
    config(displaylogo = FALSE)
}

ui <- page_sidebar(
  title = "When you bought your house: how timing changes your cost-of-living reality",
  theme = bs_theme(version = 5, bootswatch = "flatly", base_font = "system-ui"),
  sidebar = sidebar(width = 340,
    radioButtons("dollars", "Dollars", setNames(c("nom", "real"),
                 c("Nominal (dollars of each year)", sprintf("Real (inflation-adjusted, %d dollars)", LAST)))),
    radioButtons("view", "Charts show", c("Dollars" = "usd", "Share of take-home pay" = "pct"), inline = TRUE),
    hr(),
    sliderInput("year", "Year you bought", FIRST, LAST, LAST, step = 1, sep = ""),
    radioButtons("earners", "Household", c("One earner" = 1, "Two earners" = 2), inline = TRUE),
    actionButton("load", "Reset toggles to that year's typical values", class = "btn-sm btn-outline-primary"),
    hr(),
    sliderInput("down", "Down payment (% of price)", 0, 50, 20, step = 1, post = "%"),
    numericInput("price", "Price of house ($)", p0$price, min = 10000, step = 5000),
    sliderInput("rate", "Interest rate (30-year fixed, %)", 1, 19, p0$rate, step = 0.05, post = "%"),
    numericInput("col", "Cost of living: everyday non-housing spending ($ per month, in the year you bought)",
                 p0$col, min = 0, step = 50),
    numericInput("salary", "Average salary ($ per year before tax, in the year you bought; all earners combined)",
                 p0$salary, min = 0, step = 1000),
    sliderInput("tax", "Taxes taken out of salary", 0, 45, TAX_DEFAULT, step = 1, post = "%"),
    textOutput("takehome"),
    uiOutput("realnote"),
    accordion(open = FALSE, accordion_panel("More settings",
      radioButtons("term", "Loan term", c("30 years" = 30, "15 years" = 15), inline = TRUE),
      sliderInput("taxins", "Property tax + insurance (% of price per year)", 0, 4, 1.5, step = 0.1, post = "%"),
      sliderInput("incg", sprintf("Pay growth per year after %d", LAST), 0, 8, 3.5, step = 0.1, post = "%"),
      sliderInput("infg", sprintf("Inflation per year after %d", LAST), 0, 8, 2.5, step = 0.1, post = "%"),
      sliderInput("homeg", sprintf("Home value growth per year after %d", LAST), 0, 8, 3, step = 0.1, post = "%"))),
    sliderInput("compare", "Compare with someone who bought in", FIRST, LAST, 1981, step = 1, sep = "")
  ),
  layout_column_wrap(width = 1/4, fill = FALSE,
    value_box("Monthly mortgage payment", textOutput("vb_pay"), p(textOutput("vb_pay_sub"))),
    value_box("Housing share of take-home pay", textOutput("vb_share"), p(textOutput("vb_share_sub"))),
    value_box("Left over each month, year 1", textOutput("vb_left"), p(textOutput("vb_left_sub"))),
    value_box("Down payment", textOutput("vb_down"), p(textOutput("vb_down_sub")))
  ),
  card(full_screen = TRUE, card_header(textOutput("h1")), plotlyOutput("budget", height = "440px")),
  card(full_screen = TRUE, card_header(textOutput("h2")), plotlyOutput("compare_plot", height = "340px")),
  navset_card_tab(full_screen = TRUE,
    title = "The shrinking dollar: how inflation changes the house you bought",
    nav_panel("Your payment",
      uiOutput("dev_summary"),
      plotlyOutput("dev_payment", height = "360px")),
    nav_panel("What you own vs owe",
      p(class = "small text-muted", textOutput("dev_eq_text", inline = TRUE)),
      plotlyOutput("dev_equity", height = "360px")),
    nav_panel("Compare purchase years",
      radioButtons("dev_metric", NULL, inline = TRUE,
        c("Real rate actually paid" = "both", "Share of payments wiped out by inflation" = "erased")),
      plotlyOutput("dev_years", height = "380px"),
      p(class = "small text-muted", textOutput("dev_years_text", inline = TRUE)))
  ),
  card(card_footer(textOutput("note")))
)

server <- function(input, output, session) {
  load_year <- function(y) {
    p <- preset(y, as.numeric(input$earners))
    updateNumericInput(session, "price", value = p$price)
    updateSliderInput(session, "rate", value = p$rate)
    updateNumericInput(session, "col", value = p$col)
    updateNumericInput(session, "salary", value = p$salary)
  }
  observeEvent(list(input$year, input$earners), load_year(input$year), ignoreInit = TRUE)
  observeEvent(input$load, load_year(input$year))

  sim <- reactive({
    req(input$price, input$salary, input$col)
    simulate(input$year, input$price, input$down, input$rate, as.numeric(input$term),
             input$salary, input$tax, input$col, input$taxins, input$incg, input$infg)
  })
  sim_cmp <- reactive({
    p <- preset(input$compare, as.numeric(input$earners))
    simulate(input$compare, p$price, input$down, p$rate, as.numeric(input$term),
             p$salary, input$tax, p$col, input$taxins, input$incg, input$infg)
  })

  # multiplier for purchase-year amounts: 1 in nominal mode, CPI ratio to LAST in real mode
  fx  <- reactive(if (input$dollars == "real") sim()$to_real[1] else 1)
  tag <- reactive(if (input$dollars == "real") sprintf(" (%d dollars)", LAST) else sprintf(" (%d dollars)", input$year))

  output$vb_pay <- renderText(money(sim()$mortgage[1] * fx()))
  output$vb_pay_sub <- renderText({
    s <- sim(); tot <- if (input$dollars == "real") sum(s$interest * s$to_real) else sum(s$interest)
    sprintf("+ %s tax & insurance; total interest %s%s", money(s$tax_ins[1] * fx()), money(tot),
            if (input$dollars == "real") tag() else " (nominal)")
  })
  output$vb_share <- renderText({ s <- sim()[1, ]; percent((s$mortgage + s$tax_ins) / s$income, 1) })
  output$vb_share_sub <- renderText({
    s <- sim(); k <- min(10, nrow(s))
    sprintf("falls to %s after %d years as pay rises", percent((s$mortgage[k] + s$tax_ins[k]) / s$income[k], 1), k - 1)
  })
  output$vb_left <- renderText(money(sim()$left[1] * fx()))
  output$vb_left_sub <- renderText(sprintf("%s of take-home pay%s%s", percent(sim()$left[1] / sim()$income[1], 1),
                                           ifelse(sim()$left[1] < 0, " - a shortfall", ""), tag()))
  output$vb_down <- renderText(money(input$price * input$down / 100 * fx()))
  output$vb_down_sub <- renderText(sprintf("= %.1f years of saving 10%% of take-home pay%s",
                                           input$price * input$down / 100 / (0.1 * 12 * sim()$income[1]), tag()))
  output$takehome <- renderText(sprintf("Take-home pay: %s per month%s", money(sim()$income[1] * fx()), tag()))
  output$realnote <- renderUI({
    if (input$dollars != "real" || input$year == LAST) return(NULL)
    f <- fx()
    div(class = "small text-muted", style = "margin-top:6px",
        sprintf("Enter values in %d dollars. In %d dollars that is: house %s, salary %s/yr, cost of living %s/month.",
                input$year, LAST, money(input$price * f), money(input$salary * f), money(input$col * f)))
  })

  output$h1 <- renderText(sprintf("Your monthly budget over the life of a loan taken out in %d (%s)", input$year,
    if (input$view == "pct") "share of take-home pay"
    else if (input$dollars == "real") sprintf("real, %d dollars", LAST) else "nominal, dollars of each year"))
  output$h2 <- renderText(sprintf("Money left over each month%s: you (%d) vs a typical buyer in %d (same down payment and household)",
    if (input$view == "pct") " as a share of take-home pay"
    else if (input$dollars == "real") sprintf(" in %d dollars", LAST) else " in nominal dollars",
    input$year, input$compare))

  # ---- shrinking dollar ----
  sim_dev <- reactive({ req(input$price, input$salary, input$col); simulate(input$year, input$price, input$down, input$rate, as.numeric(input$term),
                        input$salary, input$tax, input$col, input$taxins, input$incg, input$infg, input$homeg) })
  cmp_dev <- reactive({ p <- preset(input$compare, as.numeric(input$earners))
                        simulate(input$compare, p$price, input$down, p$rate, as.numeric(input$term),
                                 p$salary, input$tax, p$col, input$taxins, input$incg, input$infg, input$homeg) })
  output$dev_summary <- renderUI({
    a <- dev_stats(sim_dev()); b <- dev_stats(cmp_dev()); s <- sim_dev()
    line <- function(y, d, rate) sprintf(
      "Bought %d at %.2f%%: inflation averaged %.1f%%/yr over the loan, so the real rate was %.1f%%. Inflation wiped out %.0f%% of the payments' value; by year 10 each $1 from %d buys %s.%s",
      y, rate, 100 * d$infl, 100 * d$real_rate, 100 * d$erased, y, dollar(d$dollar_10, accuracy = 0.01),
      if (d$partly_assumed) sprintf(" (years after %d use your assumptions)", LAST) else "")
    div(class = "small", style = "margin-bottom:8px",
        p(strong("You: "), line(input$year, a, input$rate),
          sprintf(" Your %s payment feels like %s in %d dollars by year 10.", money(s$mortgage[1]),
                  money(a$pay_real_10), input$year)),
        p(strong("Comparison: "), line(input$compare, b, preset(input$compare)$rate)))
  })
  output$dev_payment <- renderPlotly(dev_payment_plot(sim_dev(), input$year))
  output$dev_equity  <- renderPlotly(dev_equity_plot(sim_dev(), input$year))
  output$dev_eq_text <- renderText(sprintf(paste(
    "All in %d dollars. Inflation shrinks the real size of what you owe even before you pay it down (solid red vs dotted nominal),",
    "while the house tends to hold or gain value. Home value follows the US median house price through %d, then %.1f%%/yr."),
    input$year, LAST, input$homeg))
  years_tbl <- reactive(all_years(as.numeric(input$earners), input$down, as.numeric(input$term),
                                  input$taxins, input$incg, input$infg, input$homeg))
  output$dev_years <- renderPlotly(dev_years_plot(years_tbl(), input$year, input$compare, input$dev_metric))
  output$dev_years_text <- renderText(sprintf(paste(
    "Each year uses that year's typical mortgage rate and actual inflation afterward (lighter bars and years after %d rely on your inflation assumption).",
    "High inflation helps people who already hold a fixed-rate loan: 1970s buyers paid a real rate near zero or below, while buyers in the early 1980s",
    "locked in very high rates just before inflation fell. Refinancing, which many did when rates dropped, is not included."), LAST))

  output$budget <- renderPlotly(budget_plot(sim(), input$view, input$dollars))
  output$compare_plot <- renderPlotly(compare_plot(sim(), sim_cmp(), input$year, input$compare, input$view, input$dollars))

  output$note <- renderText(sprintf(paste(
    "Presets: median house price and average 30-year rate of the purchase year; average salary = SSA national average wage per earner; take-home pay = salary minus the tax toggle;",
    "cost of living = $%s/month per adult in %d dollars (+50%% for a second adult), scaled by the CPI. Pay and prices follow actual history through %d, then your assumptions.",
    "Does not include refinancing, raises above the average, or home-value gains."),
    format(COL_2026, big.mark = ","), LAST, LAST))
}

# ---- 4. Launch -------------------------------------------------------------------
# Opens wherever RStudio is set to show apps (Run App menu: Window or Viewer Pane)
runApp(shinyApp(ui, server), launch.browser = getOption("shiny.launch.browser", interactive()))
```
