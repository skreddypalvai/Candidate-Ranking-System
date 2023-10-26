##  **Potential Talents:**

### **Background:**
As a talent sourcing and management company, we are interested in finding talented individuals for sourcing these candidates to technology companies. Finding talented candidates is not easy, for several reasons. The first reason is one needs to understand what the role is very well to fill in that spot, this requires understanding the client’s needs and what they are looking for in a potential candidate. The second reason is one needs to understand what makes a candidate shine for the role we are in search for. Third, where to find talented individuals is another challenge.

The nature of our job requires a lot of human labor and is full of manual operations. Towards automating this process we want to build a better approach that could save us time and finally help us spot potential candidates that could fit the roles we are in search for. Moreover, going beyond that for a specific role we want to fill in we are interested in developing a machine learning powered pipeline that could spot talented individuals, and rank them based on their fitness.

We are right now semi-automatically sourcing a few candidates, therefore the sourcing part is not a concern at this time but we expect to first determine best matching candidates based on how fit these candidates are for a given role. We generally make these searches based on some keywords such as “full-stack software engineer”, “engineering manager” or “aspiring human resources” based on the role we are trying to fill in. These keywords might change, and you can expect that specific keywords will be provided to you.

Assuming that we were able to list and rank fitting candidates, we then employ a review procedure, as each candidate needs to be reviewed and then determined how good a fit they are through manual inspection. This procedure is done manually and at the end of this manual review, we might choose not the first fitting candidate in the list but maybe the 7th candidate in the list. If that happens, we are interested in being able to re-rank the previous list based on this information. This supervisory signal is going to be supplied by starring the 7th candidate in the list. Starring one candidate actually sets this candidate as an ideal candidate for the given role. Then, we expect the list to be re-ranked each time a candidate is starred.

### **Objective:**
Our primary goal is to compute the fitness score of each candidate's job title based on the provided keywords and subsequently rank them according to their fitness score. Following the ranking, we must re-rank the candidates when a candidate is starred/selected. This involves calculating the similarity score between the selected candidate's information and the information of all the candidates.

### **Data Description**
The data originates from the company's sourcing efforts. They gathered candidates' information from their LinkedIn profiles and excluded any fields that could directly disclose personal details. Instead, they assigned a unique identifier to each candidate.

**Keywords:** “Aspiring human resources” or “seeking human resources”
#### Attributes:
* id : unique identifier for candidate (numeric)
* job_title : job title for candidate (text)
* location : geographical location for candidate (text)
* connections: number of connections candidate has, 500+ means over 500 (text)
  
### **Goal(s):**
Predict how fit the candidate is based on their available information (variable fit)

### **Success Metric(s):**
*  Rank candidates based on a fitness score.
*  Re-rank candidates when a candidate is starred.


### **Project Overview:**
*  After examining the dataset, it's confirmed that there are no null values. However, there are noticeable duplicate rows. After removing them, it's clear that 'human', 'resources', and 'aspiring' are the most frequently occurring words in the job_title column.
  
![image](https://github.com/skreddypalvai/WxTzkoMxQimJnzBZ/assets/137756791/492e21cd-35f9-401e-9753-624088945a27)  
 #### TF-IDF Vector:
 
By processing the text data and using TF-IDF vectors, along with cosine similarity calculations, it produced a decent fitness score for the candidates by matching them with the provided keywords. However, for some candidates even though the key words match their job titles, the similarity score is very low due to the presence of additional words and ideally it scored zero to the unmatched job titles.   


![image](https://github.com/skreddypalvai/WxTzkoMxQimJnzBZ/assets/137756791/a4aa6331-98d4-41bc-9468-82c389523570)
_________________________________________________________________________________________________________________
![image](https://github.com/skreddypalvai/WxTzkoMxQimJnzBZ/assets/137756791/2841c4dc-e64b-4d27-a7c1-f237bc378e26)
 #### BERT:
 
BERT's similarity score is higher for job titles that match the keywords, and we can see that there are extra words in those job titles. We're certain that BERT embeddings are more advanced than regular word embeddings because they take into account the words around them in a sentence. We also see a high fitness score for the job titles that don't match.

![image](https://github.com/skreddypalvai/WxTzkoMxQimJnzBZ/assets/137756791/2f1183a0-0b6c-4fce-a64a-91a0547bc36d)
_________________________________________________________________________________________________________________
![image](https://github.com/skreddypalvai/WxTzkoMxQimJnzBZ/assets/137756791/d1e1c4f0-8622-4652-9344-92d09f2b6239)

#### Sentence - Transformers:

The Sentence Transformer model shows high cosine similarity scores for the job titles that match the keywords. We also notice that it tends to give lower scores for job titles without matching keywords compared to the BERT model. Therefore, we can conclude that the Sentence Transformer model is more robust compared to TF-IDF and BERT.

![image](https://github.com/skreddypalvai/WxTzkoMxQimJnzBZ/assets/137756791/633e2c00-0923-4168-928c-f74018499cc0)
_________________________________________________________________________________________________________________
![image](https://github.com/skreddypalvai/WxTzkoMxQimJnzBZ/assets/137756791/4e12a495-3081-4110-8b34-3b35baa015cb)

#### Re-Ranking based on the selected candidate:
Decided to use Sentence - Transformers model as a Rank decider as it will calculate the similarity score of every candidate based on the selected candidate information.

![image](https://github.com/skreddypalvai/WxTzkoMxQimJnzBZ/assets/137756791/f19b195a-7429-40c4-83b7-0930d2010669)
__________________________________________________________________________________________________________________
![image](https://github.com/skreddypalvai/WxTzkoMxQimJnzBZ/assets/137756791/e388399c-9280-4ba2-9538-779124e4d746)

 In this case, I selected an aspiring human resources student from Humber College. The ST model successfully ranked every aspiring human resources student/individual at the top and tend to score low for unmatched ones.

###  **Bonus Suggestions for the Talent Acquisition Team:**
*  The suggested algorithm uses Sentence-Transformers with pre-trained models to handle tasks related to semantic similarity. This method improves candidate rankings by including positive feedback actions, making the system more robust over time.
*  To remove irrelevant candidates, you can apply a pre-processing step, which involves setting specific criteria and using similarity score thresholds. 
*  To strike a balance between inclusivity and precision across various roles, it's essential to establish a universal similarity score cut-off point. 
*  To avoid human bias, consider exploring techniques such as adversarial debiasing, and maintaining continuous feedback loops with human reviewers. These actions collectively ensure fairness and transparency in the automated candidate ranking process.
