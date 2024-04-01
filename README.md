# CRNY-Survey-Data-Analysis
# Title of work:  

Revitalizing the Arts - Exploring Guaranteed Income and Artistic Insights in New York 

 

# Link to our data visualization: 

https://app.powerbi.com/links/z-iLpN2fgg?ctid=1113be34-aed1-4d00-ab4b-cdd02510be91&pbi_source=linkShare&bookmarkGuid=1ccb26f8-39e0-4653-856e-7a7190288014 

 

# Narrative about data visualization: 

The overarching narrative of our data visualization unfolds across four pivotal sections, each shedding light on distinct facets. Commencing with the "Applicant Demographics," we delve into the foundational metrics of eligible candidates, LGBTQIAP+ representation, immigrant percentages, and counts of Deaf and Disabled applicants. Transitioning to "Enrollment Summary" our exploration encompasses enrolled candidate figures, percentages involved in caregiving, recipients of public benefits, and those entangled with the legal system. "Financial Wellness" illuminates the financial landscape with survey responses, community-driven disparities, educational barriers, and debt metrics. Lastly, we scrutinize the "Impact of COVID" encapsulating emergency needs, health insurance coverage, alternative income sources, and the pervasive effects on physical and mental health. This nuanced journey employs an array of visualizations to empower users in unraveling intricate patterns within New York's diverse artist community. 

 

# Description of the methods used, including any data formatting/recoding: 

 

Applicant Data: 

In ‘g_enrollementstatus’ empty records are filled with ‘Not Enrolled’ for representation and working further with this column. 

 

City (g14): 

In g14_city, we have taken city name as input, to remove leading and trailing spaces, converting the name to lowercase, and then employed a series of conditional statements to map variations of city names to standardized forms. These variations include common misspellings, alternative spellings, and abbreviations. If the input city matches any of the predefined conditions, the function returns the corresponding standardized city name; otherwise, it converts the city name to title case (observe the code file to see all the variations for each city). 

 

Race ethnicity(g20): 

For the convenience we filled missing data with empty string in race columns ('g20_raceethnicity1' to 'g20_raceethnicity8'). 

We focused on addressing and enhancing the representation of multiracial identities within the 'new_gdata1' DataFrame. To achieve this, we identified rows where at least one of the specific race or ethnicity columns ('g20_raceethnicity2' to 'g20_raceethnicity8') had non-null values, indicating a multiracial background. Subsequently, we designated these individuals as 'Multiracial' by updating the corresponding values in the 'g20_raceethnicity1' column. This approach ensured that the dataset accurately reflects the diversity of respondents with multiracial affiliations. Additionally, to streamline and standardize the racial and ethnic categories, we replaced instances of 'Pacific Islander or Native Hawaiian' with 'Asian or Pacific Islander' in the overarching 'g20_raceethnicity' column. These adjustments contribute to a more inclusive and consistent representation of racial and ethnic identities. 

 

Gender (g23): 

There are some records with multiple identities. So, we categorize them in the following ways: 

If they select ‘I prefer not to answer’ and other options, those records are categorized into ‘I prefer not to answer.’ 

If they select ‘Others’ and any other options except ‘I prefer not to answer,’ those records are categorized into ‘Others.’ 

If they select ‘Two-spirit’ and any other options except ‘I prefer not to answer,’ ‘Others,’ and ‘non-binary,’ those records are categorized into ‘Two-spirit.’ 

If they select ‘non-binary’ and any other options except ‘I prefer not to answer,’ ‘Others,’ and ‘Two-spirit,’ those records are categorized into ‘non-binary.’ 

If they select ‘Two-spirit,’ ‘non-binary’ and any other options except ‘I prefer not to answer,’ ‘Others,’ those records are categorized into ‘Dual-Identity.’ 

If they select only ‘Man’ and ‘Woman’, those records are categorized into ‘non-binary’ 

Remaining records are categorized as usual without any ambiguity. 

 

Provide Care (g27): 

We introduced a new column, 'provide_care_status,' which categorizes respondents based on their affirmative responses to various caregiving-related questions. Through a series of nested conditional statements, we employed the 'map_provide_care' function to assess responses across multiple caregiving columns ('g27_providecare1' to 'g27_providecare5') and consolidate the outcomes into a unified status. Additionally, for a more nuanced understanding, we introduced another column, 'provide_care_count,' by counting the instances where respondents indicated providing care. This count specifically considers options such as caring for children, spouses, or other adults who are elderly, ill, or disabled. The resulting DataFrame provides a comprehensive view of caregiving statuses and counts, enabling us to explore and analyze the prevalence and diversity of caregiving responsibilities within our dataset. Furthermore, to handle missing values in the 'provide_care_status' column, we filled them with 'I prefer not to answer,' ensuring a complete representation of caregiving information. 

 

Financial safety net (g29): 

We undertook a comprehensive analysis of artists' financial safety nets by transforming nuanced responses into quantifiable categories within the 'new_gdata1' DataFrame. Initially, we defined a mapping dictionary, 'mapping,' to convert lengthy descriptions of financial situations into succinct terms, such as 'No Safety Net' or 'Unmanageable Debt.' Subsequently, we iterated through specific columns ('g29_financialsafetynet1' to 'g29_financialsafetynet5') and applied this mapping, creating a more standardized representation of financial circumstances. To further enhance our analytical capabilities, we introduced five binary columns ('f_nosafety,' 'f_medical_emerg,' 'f_unmanageable,' 'f_unsure_income,' and 'f_none'), initialized with zeros, to indicate the presence or absence of each financial situation. This binary categorization was facilitated by creating a dictionary, 'fnet_dict,' which mapped the transformed values to their respective binary columns. The ensuing iteration through each row and financial safety net column allowed us to populate the binary columns appropriately, facilitating a more granular and quantifiable analysis of artists' financial landscapes within our dataset. 

 

Approach of artist’s practice (g31): 

In g31approach, we ensured uniformity in the representation of artistic approaches by eliminating trailing spaces from the 'g31_approach1' to 'g31_approach6' columns. Subsequently, a well-defined dictionary was created to map original values in these columns to their respective standardized categories. Through a streamlined loop, each approach column underwent a transformation, aligning diverse entries with their designated labels. Following values, we mapped in preprocessing: 

'I work as a solo artist.': 'Solo Artist', 

'I collaborate regularly with other artists.': 'Collaboration with Other Artists' 

'I collaborate regularly with other non-arts practitioners.': 'Collaboration with Non-arts Practitioners' 

'My practice requires public or community involvement to have meaning.': 'Practice Requires Public or Community Involvement' 

'Performing, presenting, or exhibiting to an audience or viewers is core to my practice.': 'Performing, Presenting, or Exhibiting to an Audience' 

'Teaching or educating others is core to my practice.': 'Teaching or Educating Others' 

We expanded the analytical capabilities of our 'new_gdata1' DataFrame by introducing six new binary columns—'solo,' 'performance,' 'collab_artists,' 'teach_edu,' 'public_involvement,' and 'collab_nonartists'—each initialized with zeros. These columns were designed to capture specific aspects of artistic approaches, providing a more granular understanding of the dataset. To populate these columns, we created a dictionary, 'approach_dict,' mapping distinct artistic approaches, such as solo work or collaboration with other artists, to their corresponding binary columns. Subsequently, we iterated through the original 'g31_approach1' to 'g31_approach5' columns, identifying the values that align with the defined approaches and updating the corresponding binary columns with ones accordingly. This strategic transformation allows us to quantitatively assess the prevalence of different artistic approaches, facilitating nuanced analyses and insights into the diverse practices within our dataset. 

 

 

Public Benefits (g32): 

We handled missing or placeholder values in the 'g32b_enrolled_name1' column. Specifically, we replaced occurrences of '(blank)' with NaN (Not a Number) using the NumPy library, ensuring accurate representation of empty entries. Subsequently, we introduced a novel analytical dimension by creating a new column, 'total_benefits_count,' which quantifies the total count of different benefits each artist is receiving. This count is derived by summing the non-null entries across multiple columns ('g32b_enrolled_name1' to 'g32b_enrolled_name9') that capture distinct types of enrolled benefits. The resulting DataFrame provides a valuable metric for gauging the breadth of benefits artists are currently enrolled in, contributing to a more nuanced understanding of the support systems and resources available to individuals within our dataset. 

Survey data: 

We iterated through each column, stripping leading and trailing whitespaces from object-type columns, ensuring uniform formatting. Subsequently, we addressed specific numerical columns ('p5_amountofenergy,' 'p6_amountoftime,' 'p7_financialcapacity,' and 'p8_financialstability') containing ranges of values. We employed the 'str.split' method to split these columns at the en dash ('–') and extracted the second part of the split, representing the upper limit of the range. After applying the 'str.strip' method to remove any remaining whitespaces, the columns now hold refined and standardized information, enabling more accurate analyses of energy levels, time commitments, and financial capacities within the dataset. 

 

Amount of Energy and Time (p5 & p6): 

we introduced dictionary mappings to translate long-form descriptions of energy levels and time availability into more concise short forms. For the 'p5_amountofenergy' column, we created an 'energy_mapping' dictionary, associating phrases such as 'no energy' or 'more than enough energy' with their abbreviated counterparts ('no' and 'more than enough,' respectively). The 'map' method was then employed to apply these transformations to the 'p5_amountofenergy' column, ensuring a standardized representation of energy levels. Similarly, for the 'p6_amountoftime' column, a 'time_mapping' dictionary was established to map diverse descriptions like 'very little time' or 'no time at all' to abbreviated forms ('very little' and 'no time'). 

 

Financial Capacity and Stability (p7 & p8): 

We implemented targeted replacements to enhance the clarity and consistency of information in the 'p7_financialcapacity' and 'p8_financialstability' columns. Firstly, instances of 'my time fluctuates' in the 'p7_financialcapacity' column were replaced with '– my financial capacity to afford these items fluctuates,' providing a more explicit and contextually relevant description. Subsequently, for both the 'p7_financialcapacity' and 'p8_financialstability' columns, we introduced a dictionary, 'replacement_dict,' mapping long-form responses to abbreviated and standardized short forms. The 'replace' method was then applied to these columns, transforming varied descriptions of financial capacity and stability into concise categories such as 'Capacity Fluctuates' or 'Stability Fluctuates'. 

 

Carrying Debt (p14): 

A conditional statement is employed to check the values in the 'p14_carryingdebt' column. Specifically, if the value in the 'p14_carryingdebt' column is 'No,' indicating that the respondent is not carrying any debt, the corresponding 'p14b_debtmanageable' column is updated to 'No Debt.' This targeted approach ensures that the 'p14b_debtmanageable' column accurately reflects whether the respondent is carrying debt and, if not, appropriately categorizes the manageability of debt as 'No Debt.' 

Well-Being (p15 to p22): 

A dictionary named 'value_map' is defined, mapping the original response values to new standardized values. This mapping is established for the 'p15_physicalhealth' column and subsequently extended to other columns, including 'p16_mentalhealth,' 'p17_stablehousing,' 'p18_feedmyself,' 'p19_socialrelationships,' 'p20_purposefullife,' 'p21_agency,' and 'p22_optimistic.' The 'map' method is utilized for each column, replacing the original values with their corresponding standardized representations. 

 

Emergency Financial Assistance (p29 & p29b): 

New binary columns are created to represent different types of assistance received by respondents. The columns include 'Federal_relief,' 'Unemployment_benefits,' 'Emergency_grant,' 'Mutual_aid,' 'Familypersonal_assist,' and 'Other_assistance.' These columns are initialized with zeros. A dictionary named 'assistance_dict' is defined to map values from the 'p29b_typesofassistance' columns to the corresponding new binary columns. 

A loop iterates over each row in the DataFrame, and within this loop, another loop iterates over the 'p29b_typesofassistance' columns. For each cell value in these columns, it checks if the value is in the 'assistance_dict' keys. If a match is found, the corresponding binary column is updated to 1, indicating that the respondent received that type of assistance. 

 

Employment Impact, Artistic Practice, and Well-being (p30, p31, & p32): 

The methodology applied for assessing Employment Impact, Artistic Practice, and Well-being within the dataset follows a consistent approach. For each category, including Employment Impact, Artistic Practice, and Well-being, new binary columns were created to represent various aspects or subcategories related to the respective domain. These columns were initialized with zeros and systematically updated based on respondents' specific responses in relevant survey sections. A dictionary mapping original response values to standardized binary columns was defined to facilitate this transformation. 

 

Race and Gender (p38 & p41): 

We used the same methods used for applicant data to transform and categorize the records. 

 

Providing Care (p46): 

To capture and categorize respondents' caregiving responsibilities. A dictionary, "caregiving_mapping," was created to map various caregiving scenarios, such as providing care to a child, spouse/partner, or adult, as well as indicating the absence of caregiving responsibilities. A new column, "caregiving_status," was then generated by mapping the values from the original column, "p46_caregiving1," to their corresponding categories using the defined dictionary. To further enhance the analysis, a function, "count_non_null," was created to count the number of non-null entries in specific caregiving columns ('p46_caregiving1', 'p46_caregiving2', 'p46_caregiving3') for individuals with caregiving responsibilities. 

 

# List of tools/software used: 

Preprocessing: Jupyter Notebook, Python, SQL 

Visualization: Microsoft’s Power BI  
