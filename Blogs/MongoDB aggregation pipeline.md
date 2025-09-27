## Today I learn about aggregation pipeline in mongoDB.
## What is aggregation pipeline ?
### Aggregation pipeline is a method in which we can process data from a collection/table and do further processing on the processed data.
### For example : 
```
const userAverageAge = await User.aggregate([
    {
        $group: {
            _id: null, // here we can pass any property of User to _id, like this : "$gender" and it will group all the users with gender, it will separate male and female and will make two groups. Giving null means we are not grouping by any property. Group all the elements in the User collection to only one group.
            averageAge: { $avg: "$age" } // and here we are calculating the average age of all the users in the User collection.
        }
    }
]);
```

### In the above example, we are calculating the average age of all the users in the User collection.


### Another example : 
```
[
  {
    $group: {
      _id : "$company.location.country", // grouping them based on the country of their residence
      count : {$sum : 1} // 1 means it will increment the count by 1, when found a new member of the group
    }
  },
  {
    $sort: {
      count: -1 // -1 means sort in descending order and 1 means in ascending order.
    }
  }
]
```
### In the above example, first we are grouping the user based on the country of their residence. And then we are counting them. And finally sorting them in descending order based on the count.