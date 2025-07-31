# GEOG5003M_Project

Repo for GEOG5003M project assgnment

**Background**

North Northamptonshire is a unitary authority created in 2021 via the merger of four district and borough councils and disaggregated services from Northamptonshire County Council, the collapse of which caused the creation of two unitary authorities to cover its former area (the other being West Northamptonshire) (BBC News, 2021).

Tight budgets within local government in general (Institute for Fiscal Studies, 2024) mean that any spending needs to be targeted effectively in order to deliver the most possible good in the most cost efficient manner, and so a data led approach may prove beneficial in guiding spending to where it is needed most. 

For education departments this would mean ensuring that access to education is available to all, and so identifying those areas that appear to have lower access to education based upon the highest qualification attained by individuals is important, especially if there is a link to deprivation, as provision to these areas could benefit residents more than those that already have a higher level of education. 


**The Data**

Data was downloaded from Nomis Web and the Open Geography Portal. Initially on 10/07/2025 and subsequently on 25/07/2025.

TS011 - Households by deprivation dimensions: https://www.nomisweb.co.uk/query/construct/summary.asp?menuopt=200&subcomp

TS067 - Highest level of qualification: https://www.nomisweb.co.uk/query/construct/submit.asp?menuopt=201&subcomp=

Lower layer Super Output Areas (December 2021) Boundaries EW BFC (V10): https://geoportal.statistics.gov.uk/datasets/2bbaef5230694f3abae4f9145a3a9800_0/explore?location=52.954070%2C-1.023009%2C7.45

The Nomis Web (Census) data were filtered using the tools available on the download site, but the LSOA boundaries is a national dataset and therefore takes some time to read in.

**Potential Insights**

This analysis aims to determine whether the highest level of education achieved by individuals in an area can be used as a predictor of deprivation in an area.

This insight is aimed at local government officers, particularly those making decisions regarding education funding and provision.  It is assumed that they have some level of knowledge of GIS concepts, and this readme is available after a meeting where the visualisations have been presented and any questions arising have been answered. 

**The Code**

Initially the code installs and imports the necessary packages, reads them in and filters the LSOA dataframe to just those LSOAs within North Northamptonshire, including an initial visualisation to ensure that all of the LSOAs are present. 
Following the setup, an initial check examines the dataframes and checks that they contain the same number of rows and ensures there are no N/A values present. 
As one dataframe deals with individuals and another deals with households, it was decided to take the percentage values from these dataframes going forward through the analysis as this would allow a more consistent approach.
From here, there is code that splits the deprivation and education data into deciles and plots each dimension of deprivation/level of education differently. Upon reflection it wasn’t entirely necessary to run the same code twice as one set of deciles could have been created for one dataframe and all the deciles could have been mapped as part of the process, however this can be justified by the fact that it clearly demarcates exactly what parts of the dataset we are dealing with, and also allows for running one or the other in the event that this is all that is required. 

This step was taken to allow a cursory spatial visualisation of the variables to check if it appeared that they were indeed linked, and it appeared that there was a spatial relationship between deprivation and education, and so it was examined further. 
The first visualisation (non spatial) was chosen as a violin plot, and the pd.melt() function was used to create one dataframe that contained all deprivation dimensions and qualification levels (as percentage of population) in order to succinctly present  the data. For the sake of readability it has been split over two vertical plots which allows the plot frame itself to be stretched far enough horizontally for the violins to provide meaningful visualisation. 
Next, K-Means clustering was used to attempt to tease out patterns within the data that could be plotted spatially and demonstrate any relationships between the two datasets. 

This followed the process from the practical notes and resulted in five clusters, although a case could be made for six. Had this been run with OA data rather than LSOA it is suspected that there may have been more clusters reflecting the more granular nature of OA data. 
Median values for each variable by cluster were calculated which resulted in the cluster names used throughout the rest of the analysis. These were then added to the dataframe and plotted as an initial exploration. As is noted in the notebook (in more detail than here), the clusters make sense from a geographical perspective and using some local knowledge which Local Government officers will have, it is possible to see a relationship between different areas, their level of deprivation and the level of educational attainment. 

The final basemap provides an enhanced visualisation of this with a title, proper legend and a north arrow, with a colour scheme that was chosen based on accessibility following difficulties using the colourmap defined for the exploratory visualisation. 

**Potential Issues**

It is possible that people in higher paying jobs are more likely to have a higher level of education, therefore they are able to move to areas where property prices tend to be higher like the picturesque villages of Northamptonshire, or an urban extension near one of the railway stations to allow for a commute into London or elsewhere. In other words, even if education levels are lower in more deprived areas, is this a result of people coming from those areas having less access to education, or is it that those that do access education leave for greener pastures resulting in a brain drain effect?

One of the domains in which households can be deprived is deprivation, so it would potentially be more appropriate to create a more detailed dataset that takes into account dimensions of deprivation that aren’t education, and draw from a wider set of sources including foodbank use, more detailed consideration of the housing blend and both economic activity/inactivity status and profession. This would have proved challenging for the time restrictions on this exercise although it could possibly have been achieved by using K-Means Clustering in a manner similar to what has been done here. Potentially this would also have proven problematic as there is no guarantee that the data would be available in a format that matched with the LSOAs in the way those used here were, adding to the difficulty. 
The analysis may also diminish the struggles faced by the rural poor. This is a result of the modifiable aerial unit problem, as once the LSOAs extend into rural areas they become quite large, losing spatial resolution. Deprivation is captured far more readily in the towns as the LSOAs cover a significantly smaller spatial extent. Even here, however, there are issues. LSOAs provide a smoothing effect when there are OAs in close proximity to one another with highly diverse levels of deprivation and education. As a result of these problems, it would definitely be beneficial to run this analysis again at the OA level although time constraints mean that this is not possible currently. 

**References:**

BBC News, 2021. Elections 2021 in Northamptonshire: Votes to replace country's 'worst-run' council. [Online]. [Accessed 29 July 2025]. Available from: https://www.bbc.co.uk/news/uk-england-northamptonshire-56488909

Institute for Fiscal Studies. 2024. How have English councils’ funding and spending changed? 2010 to 2024. [Online]. [Accessed 29 July 2025]. Available from: https://ifs.org.uk/publications/how-have-english-councils-funding-and-spending-changed-2010-2024


