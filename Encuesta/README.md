## Gráficos

### Frecuencia preguntas dicotómicas “si” y  “no”, por genero del total de encuestados

```r
barwidth = 0.35

val_one <- filter(df2, val == "Si") %>% 
    group_by(var) %>% arrange(-val) %>% 
    mutate(pos = cumsum(n) - n / 5)   # calculate the position of the label

val_two <- filter(df2, val == "No") %>% 
    group_by(var) %>% arrange(-val) %>% 
    mutate(pos = cumsum(n) - n / 5)  

ggplot() + 
    geom_bar(data = val_one, 
             mapping = aes(x = var, y = n, fill = p31), 
             stat="identity", 
             position='stack', 
             width = barwidth) + 
    geom_text(data = val_one, 
              aes(x = var, y = pos, label = n ),
              size=2.5) + 
    geom_text(data=val_one,
            aes(x=var,y=-7,label=val),
            size=3)+
    geom_bar(data = filter(df2, val=="No"), 
             mapping = aes(x = as.numeric(var) + barwidth + 0.06, y = n, fill = p31), 
             stat="identity", 
             position='stack' , 
             width = barwidth) + 
    geom_text(data = val_two, 
              aes(x = as.numeric(var) + barwidth + 0.06, y = pos, label = n ,),
              size=2.5,) + 
    geom_text(data = val_two,
              aes(x=as.numeric(var) + barwidth + 0.06,y=-6,label=val),
              size=3)+
    labs(fill  = "Genero", x="Preguntas", y="Conteo") +
    theme_classic()+
    coord_flip()+  
    scale_fill_jco()
```
![Resultado](https://github.com/MarianaFlorezRpo/Proyecto_Encuesta/blob/master/Encuesta/000003.png)
