# New-Coder-Survey-Data-Visualizations
Data Visualization derived from Kaggle's New Coder Survey dataset
####**Job Interest and Age of New Coders**

These graphs examine the relationship between the job role interests of new coders against their age. In the scatterplot, new coders are also grouped by their desired company size/type. 

**Bar Graph**
![](New-Coder-Survey-Data-Visualizations/JobRoleInterest_Scatter.png ) 

**Scatterplot**
![](/Users/Janel/Dropbox/DataVisualization/DV_Rproject2/02\ Data\ Wrangling/JobRoleInterest_Scatter.png)

###**Interpretation of the data** 

There are signficantly more coders between the ages of 20 and 35 who want to become Full-Stack Web Developers relative to their middle to late-aged counterparts. Also, the scatterplot reveals that new millenial coders are more likely to desire employment at a medium-size company or start-up. There appears to be significantly more young coders who desire a career in Front-End Web Development as well. The remaining job role interest categories have a relatively unbiased age distribution.


###**Data Wrangling Steps**

**Step 1:** 
Called dplyr's ```select()``` function to remove unwanted columns from dataframe. 
```
df %>% dplyr::select(AGE,JOBROLEINTEREST, JOBPREF)
```

**Step 2**: Called dplyr's ```filter()``` function to remove null values from data frame.

```
 %>%  dplyr::filter(AGE!="null", JOBROLEINTEREST != "null", JOBPREF != "null")
```


**Step 3**: Called dplyr's ```group_by()``` function to group dataframe by AGE, JOBROLEINTEREST, and JOBPREF attributes.

```
 %>% dplyr::group_by(AGE, JOBROLEINTEREST, JOBPREF)
```

**Step 4**: Called dplyr's ```summarize()``` function to summarize the counts in the grouped tabled. 
```
 %>% dplyr::summarize(count = n())%>%dplyr::arrange(desc(count))
```

**Step 5**: Reordered rows in grouped table using dplyr's ```arrange()``` function.
```
 %>% dplyr::arrange(desc(count))
```
###Visualization Step

**Bar Graph**: The following ggplot layer was piped to the dataframe:

```ggplot(aes(AGE, count, fill=JOBROLEINTEREST))  + geom_bar(stat = "identity", position = "stack")  + labs(title='Job Interest of New Coders by Age') +labs(x="Age of New Coder", y= "Number of New Coders") +  scale_x_discrete(breaks = c(15,20,25,30,35,40,45,50,55,60,65)) + theme(plot.title = element_text(size=10), legend.title = element_text(size=8, face="bold")) + scale_fill_discrete(name="Job Role Interests")```

**Scatterplot**: The following ggplot layer was piped to the dataframe:
```ggplot(aes(AGE, count, color=JOBROLEINTEREST))  + theme(legend.title = element_text( size = 8)) + scale_color_discrete(name="Job Role Interest")+ geom_point(alpha = 0.7, stat = "identity", position = position_jitter(width=0.5, height= 0.5))+ labs(title='Job Interest of New Coders by Age') + labs(x="Age of New Coder", y= "Count") +facet_wrap(~JOBPREF) + scale_x_discrete(breaks = c(15,25,35,45,55,65))```

