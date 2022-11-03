---
title: Select a Single item in a FlatList
description: A collection of react native things i would like to share
hide_table_of_contents: true
tags: [ReactNative, FlatList]
---

# Select an Item in a FlatList - React Native

I recently wanted to implement the above mentioned feature but didnt find good quality videos so I am going to write one. For Begginers as a Begginer, not a Pro.

### Step 1 - Create a Flatlist

Let's continue assuming that you have already setup your FlatList, since you've searched for how to select an item.
If not, here's a boilerplate code for you to follow along.

```
const Demo = () => {
  return (
    <View>
      <FlatList
        data={YourData}
        renderItem={({ item }) => {
          return (
            <TouchableOpacity onPress={YourFunction}>
              <TheComponentYouWantToRender passYourData={item} />
            </TouchableOpacity>
          );
        }}
      />
    </View>
  );
};
```

### Step 2 - Create the onPress function to select the item

1. We shall take the item prop from the renderItem option in the FlatList and pass it on the the onPress function

```
<FlatList
  data={YourData}
  renderItem={({ item, index }) => {
    return (
      <TouchableOpacity onPress={YourFunction(item)}>
        <TheComponentYouWantToRender passYourData={item} />
      </TouchableOpacity>
    );
  }}
/>
```

2. Add `selected: false` to all the items in your data and a key value if you dont have one already, for example:

```
export default[
  {
    key:1,
    title: 'New',
    selected: false
  },
  {
    key:2,
    title: 'Videos',
    selected: false
  },
]
```
This will be used to check if the user has selected the item or not later on 

3. Create a state using the `useState` hook from react to edit the state of the selected item. Set it's default dataues as your data by passing YourData to the state

:::note

If you don't know how **useState** works. Check out [this video](https://youtu.be/kkuq0gTGRFQ?t=116).

:::

```
import { useState } from "react";

const Demo = () => {

  const [isSelected, setIsSelected] = useState(YourData);

  function YourFunction(item) {}

  return (
    ----X----           //just a placeholder for the above code
  )
}
```
currently the value of `isSelected` is the same as `YourData` which has `selected: false`

4. Create the onPress function for your component
```
function YourFunction(item) {
    const tempArray = [];
    isSelected.map((data) => {
      if (data.key === item.key) {
        tempArray.push({ ...data, selected: true });
      } else {
        tempArray.push({ ...data, selected: false });
      }
    });
    setIsSelected(tempArray);
  }
```

Here we do a few things which let us select the item we want, let me explain how it works.

- Create an array named `tempArray` which is initialized with an empty array, hence we have nothing stored in `tempArray` at the moment. This will later be used to store the modied data.
- Next, we map the data in the `isSelected` state which we created earlier and pass on the data to a function. This will loop across all the elements in the array.
- This function has an has an if statement, which checks if the key of the data we passed from the FlatList onPress option is equal to the Key of the data which is being iterated on by the `isSelected.map()` loop. This condition will only be true for the item the user selected from the FlatList.
- We edit the data in `isSelected` if the condition was true. This is done by passing the unrequired data as `...data` and just set the selected value to true using `selected: true`. We push this edited data into the `tempArray` that we had created.
- Else if the key of the data is not equal to the key of the FlatList item we just push the same data into the `tempArray` where the value of selected is false `selected:false`
- After the the `isSelected.map()` is finished iterating through all the values in the data and only setting `selected:true` for the item the user selected. We set the value of `isSelected` as the data we stored in the `tempArray` using `setIsSelected(tempArray)` 

### Step 3 - use the data stored in the state to make the change you want to the selected item



