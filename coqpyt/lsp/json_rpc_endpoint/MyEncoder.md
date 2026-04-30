# `MyEncoder(json.JSONEncoder)`

Encodes an object in JSON. This encoder overrides the value getter of the encoder to get all objects passed in as dictionaries. This is done so classes defined by CoqPyt can be passed into the encoder and can be converted to dictionaries without needing to create separate encoders for each class.

## Operations
```python
default(self, o) -> Dict
```
> Converts the passed value to a dictionary representation of all attributes.
>
> `o : Any`
> > The value to convert.