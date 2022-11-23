## Project description
I want to explore if fitness wearables improve people's discipline when it comes to doing sports.
Unfortunately, such data is not available as wearable manufacturers probably don't want to disclose it even in anonymized form.
The idea is that by looking at how the wearable is used 1 week/1 month/1 year/etc after it's activation, we can infer whether it's still actively used.

I've added several features which in my opinion should not have correlation with the labels(i.e. retention rate).
The opposite is also true, I have an assumption that some features are more relevant than others, and I generate them so that it's the case.

This problem is solved with logistic regression. There will be two types of output classes - either a user keeps on training on the same level after a year as they were after a month of using a wearable.
I have 6 features that should be used to identify the output labels:
1) data for 3 consecutive weeks after 1 month of wearing a tracker;
2) data for 3 consecutive weeks after 1 year of wearing a tracker;
I didn't want to use just one week in the beginning and the end, as it's more accurate to draw an average over several weeks, as there can be circumstances when people can't train.

My assumption when building the dataset is that the following features have an impact on training discipline(might be biased and not necessarily objective, but Ok for the sake of the experiment):
1) Age
2) Training before the wearable was bought
3) smoking
4) alcohol consumption
5) Body fat
See data_generation notebook for more details:
````
coef = (1 - weight*(0 if 25 <= age <= 45 else 1)
- weight*(not training_before)
- weight*(smoking)
- weight*(0 if alcohol <=2 else 1)
- weight*(0 if (gender == 'F' and body_fat <=25) or (gender == 'M' and body_fat <=18) else 1))
````

This research, if used on real data:
1) Help in identifying user profiles which need special approach(nudging, social pressure) to increase retention and make them adopt sports more actively;
2) Can also be used by wearable marketing teams to better understand their users.


## Resources
For structuring the project:
https://developer.ibm.com/articles/the-lightweight-ibm-cloud-garage-method-for-data-science/
https://github.com/claimed-framework/component-library/tree/master/coursera_capstone/guidelines
