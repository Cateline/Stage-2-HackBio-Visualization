# Stage-2-HackBio-Visualization
Implementation of AMR Products Data Visualization in R

This task focuses on visualizing data related to Antimicrobial Resistance (AMR) products using the WHO AMR Products dataset. The analysis includes data visualizations such as pie charts, bar charts, stacked bar charts, scatter plots, and donut charts. Additionally, it implements an interactive Shiny dashboard for visualizing key parameters of AMR products.

## Prerequisites

To run this code, ensure you have the following software and libraries installed:

1. **R**: The project requires R
2. **RStudio**  A powerful IDE for R
3. **Libraries**: Install the following R packages if they are not already installed
   ```R
   install.packages(c("readr", "ggplot2", "dplyr", "ggrepel", "shiny"))
   ```

## Instructions for Implementation

1. **Download and Set Up the Dataset**

   Download the `WHO_AMR_PRODUCTS_DATA.tsv` dataset and save it in your working directory (e.g., `C:\\Users\\Administrator\\Desktop\\Hackbio Cancer Internship`). The code is set up to work with a tab-separated values (TSV) file.

   To verify that the file path is correct, run the following commands:

   ```R
   setwd("C:\\Users\\Administrator\\Desktop\\Hackbio Cancer Internship")  # Set the working directory
   getwd()  # Check the current working directory
   ```

2. **Load Required Libraries**

   The script uses multiple libraries for reading data and plotting graphs. Ensure these libraries are loaded:

   ```R
   library(readr)
   library(ggplot2)
   library(dplyr)
   library(ggrepel)
   library(shiny)
   ```

3. **Read the Dataset**

   To read the dataset, the script uses the `read_tsv` function from the `readr` package:

   ```R
   amr_data <- read_tsv("WHO_AMR_PRODUCTS_DATA.tsv")
   ```

4. **Pie Chart for Product Types**

   The first visualization is a pie chart showing the proportion of product types in the dataset. The chart uses `ggplot2` to create a pie chart with percentage labels:

   ```R
   ggplot(product_types, aes(x = "", y = Freq, fill = Var1)) +
     geom_bar(width = 1, stat = "identity") +
     coord_polar("y") +
     theme_void() +
     geom_text(aes(label = Label), position = position_stack(vjust = 0.5))
   ```

5. **Stacked Bar Chart for Products by R&D Phase**

   This bar chart displays the number of products by R&D phase. The `dplyr` library is used to summarize data, and `ggplot2` is used to create the bar plot:

   ```R
   ggplot(phase_data, aes(x = reorder(`R&D phase`, Num_Products), y = Num_Products)) +
     geom_bar(stat = "identity", fill = "steelblue") +
     coord_flip() +
     theme_minimal()
   ```

6. **Top 10 Developers by Number of Products**

   This horizontal bar plot shows the top 10 developers contributing to AMR products:

   ```R
   ggplot(developer_counts, aes(x = reorder(Developer, -product_count), y = product_count)) +
     geom_bar(stat = "identity", fill = "mediumpurple") +
     coord_flip() +
     theme_minimal()
   ```

7. **Bar Plot for Products by Pathogen Category and R&D Phase**

   This faceted bar plot shows the number of products by pathogen category and R&D phase:

   ```R
   ggplot(pathogen_rd_phase_counts, aes(x = reorder(`Pathogen category`, count), y = count, fill = `Pathogen category`)) +
     geom_bar(stat = "identity") +
     facet_wrap(~ `R&D phase`) +
     coord_flip() +
     theme_minimal()
   ```

8. **Scatter Plot for Innovative Products by R&D Phase and Product Type**

   A scatter plot visualizes the innovation status of products, differentiated by R&D phase and product type:

   ```R
   ggplot(amr_data, aes(x = `R&D phase`, y = `Product type`, color = `Innovative?`)) +
     geom_jitter(width = 0.3, height = 0.3) +
     theme_minimal()
   ```

9. **Interactive Donut Charts Using Shiny**

   The script includes a Shiny app to visualize donut charts for `Innovative`, `NCE`, and `Route of Administration`. To run the Shiny app:

   ```R
   shinyApp(ui = ui, server = server)
   ```

   The `create_donut_chart` function generates donut charts with percentage labels outside the slices using `geom_label_repel`.

10. **Bar Plots for Critical and Other Priority Pathogens**

    The final part of the script generates bar plots for critical priority pathogens and other priority pathogens:

    ```R
    ggplot(critical_pathogens, aes(x = `Pathogen name`, y = Count, fill = `Active against priority pathogens?`)) +
      geom_bar(stat = "identity") +
      theme_minimal()
    ```

## Running the Script

1. Make sure the dataset is correctly placed in the working directory.
2. Run the script step by step to generate the visualizations. If needed, modify file paths or column names to fit your dataset structure
