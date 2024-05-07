# Json

## Jpath

```
cat q11.json | jpath $.prizes[5].laureates[1]
```

```
cat q13.json | jpath '$[0,3]'
```

## Criteria

```json
$.car.wheels[?(@.location == "rear-right")].model
```


---
