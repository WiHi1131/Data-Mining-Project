<header>
        <h1>Data Cleaning</h1>
    </header>
The financial and profile data used was gathered via web-scraping and by pulling API's from various sources. Initially, the data was separated so the financial data could be preprocessed. "Not a Number", or NaN, values were spread through various columns including: investor_count, funding_count, funding_total, funding_last, funding_last_date, valuation, valuation_date, revenue_year, and revenue_total. The length of the dataset totaled almost 7000, so columns that contained less than 20% NaN values, we replaced with the median of the column. We decided to replace these values with the median rather than the mean because the distribution of each column was positively skewed. Indicating that each distribution contained outliers, and therefore, the mean wouldn't be a good measure of the midpoint of the data. A further in-depth explanation of the cleaning process can be found in the cleaning.ipynb folder. 

<header>
        <h1>Data Visualizations</h1>
    </header>

<main>
<div class="image-container">

<header>
<h2>Mosaic change vs date of most recent funding </h2>
</header>
<p>1. The mosaic score for a company is an internal metric designed by CB Insights (https://www.cbinsights.com/) for evaluating the long-term success of startups. Without a paid account, only the mosaic score change was available to scrape for each startup. This plot puts startups into bins based on their most recent funding date, then creates a violin plot for each bin to show the distribution of its mosaic score changes. From this plot, we can see that startups that have recently received funding tend to have more positive mosaic score changes. This intuitively makes sense: if a startup has not been funded for a long time, it is less likely to be a long-term success. 
</p>
<img src = "visualizations/michael-violinplot.png" style="width:800px;height:600px;">

<header>
<h2>Number of startups by country </h2>
</header>
<p>2. We have the country information for each of our startups, so we can plot a map showing how many startups are in each country in our dataset. From this plot, we get an idea of where the startups we are analyzing are located, and we can also decide if there are countries we want to drop or countries we want to gather more data for. 
</p>
<img src = "visualizations/michael-map-plot.png" style="width:800px;height:600px;">

<header>
<h2>Most common words in startup descriptions  </h2>
</header>
<p>3. Each of the startups in our dataset has a description written by CB Insights. Using these descriptions, we can extract the most common words and create a frequency plot. Some of the descriptions contain city names, so we are getting common city names and removing them from the descriptions before processing the words. We are also moving stopping words like 'the', 'and', and 'but'. From this frequency plot, we can get an idea of what types of companies we are looking at, and what the most popular areas are. 
</p>
<img src = "visualizations/michael-word-freq.png" style="width:800px;height:600px;">

<header>
<h2>Maximum Funding Awarded to a Company in Every Country y</h2>
</header>
<p>4. This graph illustrates the maximum amount of funding an individual company receives in each country. This will be vital to our analysis because we can predict if a company will receive more funding based on the country, they founded their company in. 
</p>
<img src = "visualizations/melbarh.png" style="width:600px;height:800px;">

<header>
<h2>Last Funding Type</h2>
</header>
<p>5. This pie chart illustrates the last funding type an individual company received. This information will be important for our analysis because we can predict the success of a company based on the type of funding that they receive.  
</p>
<img src = "visualizations/melpiechart.png" style="width:800px;height:600px;">

<header>
<h2>Box Plots</h2>
</header>
<p>6. The boxplot shows a median of 10 investors, with the middle 50% of the data lying fairly close to the median, a low whisker of 1 and a high whisker a bit higer than 25. The data appears somewhat symmetrically spread with a bit of a right skew towards higher numbers of investors, and a significant number of high outliers.
</p>
<img src = "visualizations/willboxplotinvestor.png" style="width:600px;height:600px;">

<p>7. The mosaic change boxplot shows a smaller negative mean, and a very symmetrical looking spread, with a very small right skew. There are a significant amount of both high and low outliers. 
</p>
<img src = "visualizations/willboxplotmosaicchange.png" style="width:600px;height:600px;">

<p>8. The funding count boxplot shows a heavy right skew, but a symmetrical middle 50% of the data, with a median of 5 (close to the mean) of the number of rounds of funding. There are high outliers but less outliers than in previous boxplots. 
</p>
<img src = "visualizations/willboxplotfundingcount.png" style="width:600px;height:600px;">

<p>9. The funding total boxplot is undiscernible because of the significant high outliers. Removal of the top 50 outliers was conducted and the data replotted: 
</p>
<img src = "visualizations/willboxplotfundingtotal.png" style="width:600px;height:600px;">

<p>10. This boxplot is now discernible due to removing outliers. We see a very small median with a heavy right skew, and still a significant number of very high outliers. The lowest whisker is close to 0 and not below. 
</p>
<img src = "visualizations/willboxplotfundingtotalnoout.png" style="width:600px;height:600px;">

<p>11. fill in caption 
</p>
<img src = "visualizations/willboxplotsentimentscore.png" style="width:600px;height:600px;">

<header>
<h2>Histograms</h2>
</header>

<p>12. fill in caption 
</p>
<img src = "visualizations/willhistinvestorcount.png" style="width:800px;height:600px;">

<p>13. fill in caption 
</p>
<img src = "visualizations/willhistmosaicchange.png" style="width:800px;height:600px;">

<p>14. fill in caption 
</p>
<img src = "visualizations/willhistfundingtotal.png" style="width:800px;height:600px;">

<p>15. fill in caption 
</p>
<img src = "visualizations/willhistfundingcount.png" style="width:800px;height:600px;">

<p>16. fill in caption 
</p>
<img src = "visualizations/willhistsentimentscore.png" style="width:800px;height:600px;">

<header>
<h2>Q-Q Plots</h2>
</header>

<p>17. fill in caption 
</p>
<img src = "visualizations/willqqinvestorcount.png" style="width:600px;height:600px;">

<p>18. fill in caption 
</p>
<img src = "visualizations/willqqmosaicchange.png" style="width:600px;height:600px;">

<p>19. fill in caption 
</p>
<img src = "visualizations/willqqfundingtotal.png" style="width:600px;height:600px;">

<p>20. fill in caption 
</p>
<img src = "visualizations/willqqfundingcount.png" style="width:600px;height:600px;">

<p>21. fill in caption 
</p>
<img src = "visualizations/willqqsentimentscore.png" style="width:600px;height:600px;">

<header>
<h2>Keywords vs Sentiment Score</h2>
</header>

<p>22. fill in caption 
</p>
<img src = "visualizations/willkeywordssentimentscore.png" style="width:800px;height:600px;">

<header>
<h2>Pair Plot</h2>
</header>

<p>23. fill in caption 
</p>
<img src = "visualizations/willpairplot.png" style="width:800px;height:800px;">

<header>
<h2>Heat Map</h2>
</header>

<p>24. fill in caption 
</p>
<img src = "visualizations/willheatmap.png" style="width:800px;height:800px;">

</div>
</main>
<a href="https://wihi1131.github.io/Data-Mining-Project/">Home</a>
