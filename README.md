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
I would like to learn how to put interactive graphics and dashboards here next.  Is that up coming in the curriculum or should I see you outside of class time?  The following is the R code for some of my stuff I was messing with this weekend.

## Wealth Needed to Buy a Home
<img width="2340" height="1300" alt="quarterly_mortgage_payments" src="https://github.com/user-attachments/assets/4995a93c-0690-4206-8859-132c336fc339" />


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
