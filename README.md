# BabyReindeerPublication
This repository gives supplementary information to the publication. The first section will focus on giving an overview of what the different files do. The second section will give more in detail information on the methods used. 

# Files
## Scripts
- Scraper_Reddit.ipynb --> Code used to scrape the relevant discussions on Reddit
- Walkthrough.ipynb --> Main code used for the creation and processing of the data. Includes cleaning and data enrichment
- Reliability.Rmd --> R markdown file that walks through the evaluation process (creating sample to evaluate, and the krippendorff alpha claculation)
- Graphs_paper.Rmd --> R markdown file used to create the figures used for the paper (and more)

## Data
- bbreindeer.csv --> raw data scraped from reddit
- bbreindeer_clean.csv --> minimal data cleaning was done, now we seperate comments from the user name and have an id variable as well as a parent id variable
- bbreindeer_clean_with_GPT_for_Martha.csv --> clean data with martha mentions (direct or indirect)
- martha_presence_validation.csv --> human coding of random sample of martha mentions
- martha_labels.csv --> final version of martha lables
- bbreindeer_clean_with_GPT_for_Donny.csv --> clean data with donny mentions (direct or indirect)
- Donny_presence_validation.csv --> human coding of random sample of donny mentions
- donny_labels.csv --> final version of donny lables
- bbreindeer_vader.csv --> vader scores for all comments
- MasterData.csv --> dataset with all added variables
- martha_only_all.csv --> subset of master data with only mentions about Martha
- donny_only_all.csv --> subset of master data with only mentions about Donny
- donny_and_martha_all.csv --> subset of master data with only mentions about Martha and Donny
- to_code_sim_aug_11.csv --> sample for manual evaluation
- donny_empathy_labels.csv --> data with GPT lables added whether comments show empathy towards Donny
- martha_empathy_labels.csv --> data with GPT lables added whether comments show empathy towards Martha
- ValidationDonnyMartha.csv --> sample of 100 random comments used to evaluate how well the person detection worked
- ValidationDonnyMartha_coded.csv --> same as above but after human coding
- ValidationDonnyResponsible.csv --> sample of 100 random comments used to evaluate how well the "Donny is responsible" theme worked
- ValidationDonnyResponsible_coded.csv --> same as above but after human coding
- ValidationMarthaTraditionalStalker.csv --> sample of 100 random comments used to evaluate how well the "Martha as Traditional Stalker" theme worked (it did not work well)
- ValidationMarthaTraditionalStalker_coded.csv --> same as above but after human coding

# Methods
## Data
Founded in 2005, Reddit functions as a social media platform characterized by user-generated posts and specialized discussion boards referred to as "communities" or "subreddits" (Reddit, n.d.). These subreddits serve as dedicated forums where users engage in discourse and share content centered around specific themes. As of 2024, Reddit has amassed a user base exceeding 500 million registered accounts, with a substantial portion concentrated in the United States, closely followed by the United Kingdom. Demographic studies reveal that the platform's primary users are predominantly male, younger (primarily aged 18–29), and of White ethnicity (Pew Research Center, 2016).
A key aspect of Reddit's architecture is the use of dedicated subreddits for specific topics, communities, or interests, enabling users to engage in focused discussions and content sharing within niche areas. The subreddit "r/BabyReindeerTVSeries," which has a community of approximately 59,000 members, featured official discussion threads for each episode of the show. For this study, we leveraged the Python Reddit API Wrapper (PRAW) to systematically collect all user comments related to the seven individual episodes of Baby Reindeer. These concentrated discussions allowed for an in-depth exploration of various aspects of the show, particularly its portrayal of female stalkers, offering valuable insights into the broader cultural understanding of such representations in media.
	Data Analysis
To identify comments referencing the characters Martha and Donny, we employed a combination of word-based classification and large language model (LLM) facilitation. We searched for the characters' names, the names of the real individuals they were based on, and related pronouns and descriptors. GPT-4 was used to refine the classification, and manual checks were performed to ensure accuracy. Thus, we were certain that all posts that we classified as being about Donny or Martha were actually about these characters, or their real life counterparts. However, it is still possible that we missed some instances, and thus we tested the reliability of our classification by assessing 100 random reddit posts. The results demonstrated high intercoder reliability (Krippendorf alpha XXX) and also showed that additional to our perfect precision, recall was also high () with an overall F1 score of XXX. 
We assessed the valence of comments using Vader (Hutto & Gilbert, 2014), a sentiment analysis tool designed for social media texts. Additionally, we coded comments to identify expressions of empathy towards the characters, depictions of Martha as a traditional stalker, and whether Donny was considered responsible for being stalked. Open AI’s  GPT-4 was used for initial classification, followed by manual verification. Again, we used a random subset to test our human-AI pipeline against pure human coding and found good agreement (Krippendoff alpha = ) and high precision (), recall(), and F1, validating that our approach had reliably classified the reddit posts. 

## Meta data.
To determine whether the posts referenced Martha or Donny, we employed a combination of word-based classification and large language model (LLM)-facilitated data labeling. Initially, we used the characters' names and the names of the real individuals on whom the characters were based to ensure we captured all discussions where individuals may alternate between referring to the characters and the actual persons. Specifically, we searched for "Martha" and "Fiona" for the Martha character, and "Donny" and "Richard" for the Donny character. However, not all posts referencing a character included a direct naming variable and required us to broaden our search to capture indirect references through pronouns and related descriptors. For Martha, we incorporated terms such as "her," "she," and "stalker," while for Donny, we included "he," "his," "him," and "dude." Given that these indirect references could also pertain to other characters or individuals, we further refined this subset using GPT-4. The application of GPT-4 produced one of three classification labels: (a) the post is about Donny/Martha, (b) the post is not about Donny/Martha, or (c) Unsure. All posts marked as "Unsure" were subsequently manually reviewed and classified.
The specific prompt can be seen in APPENDIX XX. 
After classification, we also manually checked all classified comments for accuracy, and made adjustments when necessary. Thus, when it comes to the posts about Donny and Martha, we can be certain that all posts classified as containing the characters actually contains them (perfect precision), however we can be less sure that all posts that are labelled as not containing these characters actually do not contain them (potential for lower recall). However, a random analysis of 100 posts demonstrated that both our precision () and recall () was very high, and the F1 scores were xxx. The confusion matrix can be found in APPENDIX XX. 
	Comment valence. 
To assess the overall mood or tone of Reddit comments, known as valence, we used Vader, a sentiment analysis tool developed by Hutto and Gilbert (2014) specifically for social media texts. Vader employs a rule and dictionary-based approach to assign sentiment scores to individual words and symbols based on predetermined values. This method incorporates scores for standard English words, as well as abbreviations (e.g., LOL) and emoticons (e.g., 😊), to capture the subtleties of social media communication, using the Vader compound score—a normalized, weighted composite measure of valence that ranges from -1 (extremely negative) to +1 (extremely positive), with scores between -0.05 and 0.05 considered neutral.
Presence of Themes
Additionally, we coded comments to identify expressions of empathy towards the characters Donny and Martha. For comments addressing stalking, we also coded whether Martha was depicted as a traditional stalker and whether Donny was considered responsible for being stalked. Chat GPT was used for the initial classification of the comments, followed by manual checks of the results. The definitions for the three main themes coded are provided in Table 1 below.

### ADD TABLE
Concept
Definition
For which character
Empathy
Assess whether the reddit comment reflects an understanding or supportive acknowledgment of Donny’s/Martha’s feelings and experiences. Here, empathy is indicated by expressions that recognize Donny's/Martha’s perspective or emotional state in a way that shows sympathy or compassion for their actions.
Both
Traditional Stalker
Assess to what extent Martha is being characterised as a stalker in a traditional mediated sense. This includes behaviours such as unwanted contact, including phone calls, texts, and contact via social media, unwanted gifts, showing up/approaching an individual or their family/friends, monitoring, surveillance, property damage, and threats. Additionally, prior literature shows that it is often assumed that traditional stalkers have underlying mental health issues.

Code a comment as 1 if Martha is characterised as a traditional stalker, 0 if the comment talks about her being a stalker but not in the traditional sense, and 99 if the comment is not about her stalking behaviour. 
Martha
Blame for Being stalked
