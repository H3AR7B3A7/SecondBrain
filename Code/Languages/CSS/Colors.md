# Colors
Color notations:

-   Built-in
-   Hex-value (hexagonal)
-   Rgb-value (red-green-blue)
-   Hsl-value (hue-saturation-lightness)

```
.color {
  background-color: red;
  background-color: #454531;
  background-color: rgb(243, 13, 57);
  background-color: hsl(107, 54%, 67%);
}
```

## HSL
Hsl-values are by far the most relatable notations of colors we can work with:

![[HSL.png]]

They are:

-   More easy to read
-   Give a better overlook of the palette
-   Work well with variables

```
.color  {
  --hue: 200;
  --saturation: 100%;
  --lightness: 50%;
  background-color: hsl(var(--hue), var(--saturation), var(--lightness));
}

.color:hover {
  --lightness: 30%;
}
```


---
#Styling #CSS 