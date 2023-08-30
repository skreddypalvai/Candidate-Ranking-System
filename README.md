###  **Potential Talents:**
As a talent sourcing and management company, they are interested in discovering talented individuals for sourcing these candidates for technology companies. However, finding talented candidates is not easy in general. This entails numerous challenges, including identifying potential candidates, determining what makes them the best choice, and pinpointing where to locate them. The nature of their job demands significant human effort and involves a high degree of manual operations. To streamline the process, save time, and identify the ideal candidate for a given role, they are seeking to develop a machine learning automation process. With this process, they can search for ideal candidates using specific keywords.

After successfully ranking the candidates based on their job titles by matching them with the keywords, the recruiter might not select the top-ranked candidate but rather the seventh. Consequently, each time the recruiter selects a candidate, the candidates need to be re-ranked based on the chosen candidate's information.

### **Objective:**
Our primary goal is to compute the fitness score of each candidate's job title based on the provided keywords and subsequently rank them according to their fitness score. Following the ranking, we must re-rank the candidates when a candidate is starred/selected. This involves calculating the similarity score between the selected candidate's information and the information of all the candidates.

### **Data Description**
The data originates from the company's sourcing efforts. They gathered candidates' information from their LinkedIn profiles and excluded any fields that could directly disclose personal details. Instead, they assigned a unique identifier to each candidate.

#### Attributes:
* id : unique identifier for candidate (numeric)
* job_title : job title for candidate (text)
* location : geographical location for candidate (text)
* connections: number of connections candidate has, 500+ means over 500 (text)

Output:
* fit - how fit the candidate is for the role? (numeric, probability between 0-1)

**Keywords:** “Aspiring human resources” or “seeking human resources”
