---
layout: post
title:      "How I Understood the Redux Concept"
date:       2018-03-16 20:29:48 +0000
---

When I was working on my final project for Flatiron, I could just barely understand how the redux store was supposed to work. There were several resources and videos that I reviewed, but it was when I was manipulating the different parts or slices of the store that I completely understood. Each part of my redux store is manipulated using the applicable reducer. It is a separation of concerns, so the medications reducer only deals with manipulating the medications, the reviews reducer only deals with the reviews, and so on. Once I understood that, I was able to write the various cases in the switch statements a lot easier. Here is my store:

```
Final Project Redux Store:
State: {
	medications [
		{},
		{},
		{}
	]
	medicationFormData {}
	reviewFormData {}
	reviews [
		{},
		{},
		{}
	]
	errors: boolean (true/false)
}
```

and here is my medications reducer:

```
export default (state = [], action) => {
	switch (action.type) {
		case 'MEDICATIONS_FETCH_DATA_SUCCESS':
			return action.medications;
		case 'ADD_MEDICATION_SUCCESS':
			return state.concat(action.medication)
		case 'DELETE_MEDICATION_SUCCESS':
			return state.filter(medication => medication.id !== +action.medicationId);
		default:
			return state;
	}
};
```

Once an action is dispatched, for example, ‘ADD_MEDICATION_SUCCESS’, that return statement immutably changes only the slice of redux store that is the medications and nothing else. In this example, the new medication is added to the medications array. This way you are more efficiently and quickly making these changes and rendering the results on the screen for the user. 

Another part of understanding redux was understanding the JSON objects being requested from the API. To make this easier, I needed to make the models independent of each other in the store. Instead of reviews belonging to medications, they needed to be listed in their own array of objects. Making the store “flat” like this was the best way to allow manipulation without mutation. There are other ways using different libraries like Immutable.js, but I felt like this would be learning a whole other language just to manipulate my store. What I did was change the routes of the API to allow for requesting the reviews on their own or as being owned by a medication. 

```
Rails.application.routes.draw do
  
  namespace :api do
  	resources :reviews
  	resources :medications do
  		resources :reviews, :only =>[:index, :show]
  	end
  end
end
```