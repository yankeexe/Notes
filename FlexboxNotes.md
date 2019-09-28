# Flexbox Notes

## For Flex Containers

* `justify-content` is used to align contents horizontally. 

* `align-items` is used to align contents vertically. It helps when the height is defined. 
  `align-self` overrides the value of `align-items` imposed on an individual item.

* Whenever we change the direction of the flex, it carries the properties along with it. Like the `justify-content` and the `align-items` remain in the same place when they were in their default direction. 
  So now, when we change the direction from row to column, to align the content center, we have to use the `align-items` property instead of the `justify-content` although it seems we have to use `justify-content`. 

![Image](https://i.imgur.com/gYHQ1hI.png)

## For Flex Items

