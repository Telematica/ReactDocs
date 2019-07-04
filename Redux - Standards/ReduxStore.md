# Redux - Store

The application has one single Redux Store that contains one single JavaScript root object.

The Redux Store root JavaScript object can have many child objects, called Slices which contains data for a given domain, area.

All data in the Redux Store should be plain JavaScript Objects or scalar values.

The redux store should not contain references to objects such as Date, Moment, React Element, Dom Elements, etc.

It should be possible to serialize all the data in the Redux Store to JSON and reload it states from JSON.



Similar to database design organize your data into separate slices to prevent having one slice containing unrelated data.

With Selectors you can access and combine data that is stored in separate slices.