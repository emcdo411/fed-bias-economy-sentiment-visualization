Here's a **GitHub-worthy README** for your project, including the details of the analysis and all relevant code.

---

# Federal Reserve Bias & Economic Sentiment Analysis

## Project Overview

This project explores public perceptions and sentiment regarding the **Federal Reserve** (Fed) and the **U.S. economy**. It uses state-level data to analyze:

1. **Political Bias of the Federal Reserve**  
   - Investigating the perceived political leanings of the Fed across U.S. states.
2. **Economic Sentiment**  
   - Analyzing public sentiment on the U.S. economy across states.

The data is visualized in interactive maps using **RStudio**, providing insights into how different states perceive the Federal Reserve and their view on the U.S. economy.

### Project Goals
- To visualize the **perceived political bias** of the Federal Reserve by state.
- To assess the **economic sentiment** regarding the U.S. economy on a state-by-state basis.
- To utilize **open data** to explore public opinion and enhance data-driven decision-making.

---

## Files Included

The following CSV files are included in this project:

- **[fed_bias_poll_by_state.csv](sandbox:/mnt/data/fed_bias_poll_by_state.csv)**: State-level data on perceived political bias of the Federal Reserve.
- **[economic_sentiment_poll_by_state.csv](sandbox:/mnt/data/economic_sentiment_poll_by_state.csv)**: State-level data on public sentiment regarding the U.S. economy.
  
### Example of CSV Data:

#### **fed_bias_poll_by_state.csv**
| State        | Political Affiliation | Percentage Believing Fed Favors Opposite Party |
|--------------|-----------------------|-----------------------------------------------|
| Alabama      | Republican            | 55%                                           |
| Alaska       | Independent           | 48%                                           |
| Arizona      | Democrat              | 60%                                           |
| ...          | ...                   | ...                                           |

#### **economic_sentiment_poll_by_state.csv**
| State        | Sentiment  | Percentage of Registered Voters |
|--------------|------------|---------------------------------|
| Alabama      | Negative   | 45%                             |
| Alaska       | Positive   | 65%                             |
| Arizona      | Negative   | 50%                             |
| ...          | ...        | ...                             |

---

## R Code for Data Visualizations

The following R code is used to visualize the data:

### 1. **Federal Reserve Bias by State**:
```r
# Load necessary libraries
library(ggplot2)
library(dplyr)
library(readr)
library(maps)
library(sf)

# Load the Federal Reserve Bias Poll data (state-level)
bias_data <- read_csv("fed_bias_poll_by_state.csv")

# Load US states map data
states_map <- map_data("state")

# Merge poll data with map data
bias_data$State <- tolower(bias_data$State)  # Ensure state names match the map data
map_data_bias <- left_join(states_map, bias_data, by = c("region" = "State"))

# Plot Federal Reserve Bias by State
ggplot(map_data_bias, aes(x=long, y=lat, group=group, fill=`Percentage Believing Fed Favors Opposite Party`)) +
  geom_polygon(color="white") +
  scale_fill_gradient(low="lightblue", high="darkblue") +
  labs(title="Perceived Political Bias of the Federal Reserve by State",
       fill="Bias Perception (%)") +
  theme_void()
```

### 2. **Economic Sentiment by State**:
```r
# Load the Economic Sentiment Poll data (state-level)
economic_data <- read_csv("economic_sentiment_poll_by_state.csv")

# Ensure state names are in lowercase
economic_data$State <- tolower(economic_data$State)

# Merge with US states map data
map_data_economy <- left_join(states_map, economic_data, by = c("region" = "State"))

# Plot Economic Sentiment by State
ggplot(map_data_economy, aes(x=long, y=lat, group=group, fill=`Percentage of Registered Voters`)) +
  geom_polygon(color="white") +
  scale_fill_gradient(low="gray", high="green") +
  labs(title="Public Sentiment on U.S. Economy by State",
       fill="Economy Sentiment (%)") +
  theme_void()
```

---

## Instructions

1. **Clone this repository** to your local machine or work directly on GitHub.
   
   ```bash
   git clone https://github.com/yourusername/federal-reserve-bias-economic-sentiment-analysis.git
   ```

2. **Install necessary R packages**:
   Make sure you have the following R packages installed:
   ```r
   install.packages(c("ggplot2", "dplyr", "readr", "maps", "sf"))
   ```

3. **Place the CSV files** in the working directory where your R script is located.
   
4. **Run the R scripts** in RStudio to generate the visualizations.

---

## Suggested Repository Name

I suggest naming the repository something like:

**`federal-reserve-bias-economic-sentiment-analysis`**  
or  
**`fed-bias-economy-sentiment-visualization`**

This will make the repo clear to future contributors or viewers regarding the content of the analysis.

---

## License

This project is licensed under the MIT License – see the [LICENSE](LICENSE) file for details.

---

Let me know if you'd like to modify any sections, or if you need additional guidance! 🚀
