# MDST-Blight-Data-Challenge
The Michigan Data Science Team and the Michigan Student Symposium for Interdisciplinary Statistical Sciences (MSSISS) have partnered with the City of Detroit on a data challenge that seeks to answer the question: How can blight ticket compliance be increased?

Some feature engineering is performed to improve the baseline AUC score of ~0.5:

- 1 : a feature has been derived to address the hypothesis that high concentrations of 
      violations, geospatially, indicate overall lack of upkeep, 
      which then increases the likelihood of finding unpaid blight tickets in the area.
- 2 : features that are highly correlated with other variables or simply have
      too much variation in categorical value that creates too many features (one hot) have been dropped
- 3 : the 'time_to_pay' feature has been derived to address the hypothesis that the ticket_issued_date itself is not 
      influential from the perspective of the ticket receiver. It becomes useful in the context of the hearing_date.
      time_to_pay = hearing_date - ticket_issued_date. The smaller this value, the more urgent it is and that could motivate
      one way or the other. Or, it could be so short a time that it is impossible to pay. Or, it is so long a time
      one forgets to pay. This window of time seems to motivate ones actions more directly than the parent metrics.

The RandomForestClassifier produces good results. The parameters were tuned first with a scattershot type apprach, using RandomizedSearchCV,
then based on those results, GridSearchCV was used to determine the optimal parameters. There is still room for improvement in this model. One could
derive new features or sample the data differently.

This model achieves an AUC of 0.8066. 

For reference, the data sets are originally from:
https://www.kaggle.com/c/detroit-blight-ticket-compliance
