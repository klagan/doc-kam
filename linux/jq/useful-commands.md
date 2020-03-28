# Useful commands

---

## Useful syntax

Run `jq` against a file: `jq '.' <filename>`
Run `jq` against a variable: `jq '.' <<< <my-variable>`

---

### Changing property values

**Change the property value for all items in a json collection and pipe the results to a file**

*Sample input-1.json*
```json
[
    {
        "property" : "something"
    },
    {
        "property" : "something else"
    }
}
```

```
jq '.[].property = "false"' input-1.json > output.json
```

**Change the property value for all items in a collection property and pipe the results to a file**

**Sample input-2.json**
```json
{
    "MyArray": 
    [
        {
        "property" : "something"
},
    {
        "property" : "something else"
    }
    ]
}
```

```
jq '.MyArray[].property = "false"' input-2.json > output.json
```