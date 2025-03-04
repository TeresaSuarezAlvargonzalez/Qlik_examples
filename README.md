# Qlik_examples

Objetivo del dashboard 

El objetivo principal del dashboard es ofrecer una visualización clara del rendimiento de las 
categorías y subcategorías de productos en términos de ventas y rentabilidad. Permite a los 
usuarios identificar rápidamente áreas de oportunidad y alertas dentro de la estructura 
jerárquica, facilitando la toma de decisiones sobre desempeño y rentabilidad. Además, 
ayuda a gestionar estrategias comerciales y de precios a través de la interacción con 
diferentes niveles de datos (Product Line → Product Group → Product Type → Product 
SubGroup).  

![das](https://github.com/user-attachments/assets/786b406c-fbbd-495e-9c60-5fc93fe47ee8)


Justificación de las Visualizaciones Seleccionadas 

Gráfico de Barras (Horizontal): Muestra las ventas acumuladas de las líneas Food y 
Drinks, ordenadas de mayor a menor, con orientación horizontal para facilitar su lectura y 
comparar rápidamente las líneas con mayores ventas. 

KPIs: 

1. Total Sales: Muestra el volumen total de ventas, ofreciendo una visión general del 
desempeño de las líneas de productos.

2. Total Margin: Indica el beneficio bruto generado, clave para evaluar la rentabilidad 
de las ventas. 

3. Gross Profit Margin: Muestra el porcentaje de ganancias, útil para medir la 
eficiencia 
operativa y detectar áreas de mejora en costos.

Razón de la elección: Estos KPIs proporcionan una visión completa del volumen 
de ventas, rentabilidad absoluta y eficiencia operativa, permitiendo una evaluación 
equilibrada del desempeño. 

Gráfico Mekko: Ideal para comparar categorías y explorar datos jerárquicos. Los 
rectángulos representan la distribución y tamaño según métricas cuantitativas, 
permitiendo identificar rápidamente categorías relevantes o en riesgo. Además, al pasar el 
cursor sobre cada rectángulo se muestran las métricas de Gross Profit Margin, Gross Profit 
Margin% y ROI.

Justificación del Diseño 

El diseño se enfoca en facilitar la comprensión y análisis de los datos clave, asegurando 
que los usuarios puedan interpretar rápidamente los resultados más relevantes. 

• KPI Gross Profit Margin: Se destaca visualmente con un fondo y emoticono llamativo 
(deseable   , alerta   , analizar con más detalle         
), lo que atrae la atención al 
rendimiento de la rentabilidad y mejora la accesibilidad para usuarios con deficiencias 
visuales. 

• KPI Total Sales y Total Margin: Se mantienen en un fondo discreto, permitiendo que el 
Gross Profit Margin sea el foco principal sin sobrecargar visualmente. 

• Colores: Los colores del KPI Gross Profit Margin utilizan colores brillantes que desvían 
la mirada y los cuales tenemos claramente asociados a estados; verde, amarillo y rojo 
para transmitir el estado de la rentabilidad. Los gráficos de barras para Food y Drinks 
usan diferenciados (#872025, #006580) pero apagados para no sobrecargar la 
visualización, y un color gris neutro para aquellos que comparten las categorías. El 
fondo verde grisáceo claro (#83AF9B) se usa sutilmente en las líneas de separación 
entre los gráficos, transmitiendo calma sin desentonar visualmente. 

Insights clave obtenidos a partir de los datos 

El dashboard ofrece una visión clara y estructurada de la rentabilidad de la empresa, 
destacando el Gross Profit Margin global del 41.3%, un dato relevante ya que supera el 
objetivo general del 40%. No obstante, cada grupo de productos tiene diferentes objetivos 
de rentabilidad, determinados por sus características específicas, como su 
posicionamiento en el mercado, costos de producción, elasticidad de la demanda y nivel 
de competencia. 

Este dashboard facilita la identificación rápida de las categorías que no alcanzan sus 
objetivos de rentabilidad, permitiendo un análisis más detallado a nivel de producto. La 
jerarquía del dashboard ayuda a profundizar en las causas subyacentes y detectar cuáles 
productos están afectando el desempeño de cada grupo. 

Un ejemplo claro de la utilidad de esta herramienta es el grupo de bebidas alcohólicas, que, 
al tratarse de productos premium, debería alcanzar un Gross Profit Margin del 50%. Sin 
embargo, el análisis revela que su margen actual es de solo 22.9%, lo que indica un 
desempeño por debajo de lo esperado. Al desglosar por subcategorías, se observa que el 
vino tiene un margen del 21.4% y un ROI del 27.22%, mientras que la cerveza tiene un 
margen superior del 30.7% y un ROI del 44.25%. Esto sugiere que el vino podría estar 
enfrentando costos elevados, estrategias de precios poco optimizadas o menor rotación 
en comparación con la cerveza. 

Gracias a este nivel de análisis, la empresa puede tomar decisiones estratégicas 
informadas, como revisar los costos de adquisición del vino, evaluar su estructura de 
precios o incluso replantear la estrategia comercial para mejorar su rentabilidad. 

Expresión Datos del KPI Gross Profit Margin 



If ( 
    
    GetSelectedCount([Product Group]) = 0,  
    
    Num(Sum(Margin) / Sum(Sales), '0.0%'),  // Mostrar el margen sin emoticono si no hay selección 

    If( 
    
        GetSelectedCount([Product Group]) > 1 AND (Sum(Margin) / Sum(Sales)) < 0.40,   // Calcular el promedio correcto de la rentabilidad 

        '         ' & Num(Sum(Margin) / Sum(Sales), '0.0%'),  // Si hay más de un producto seleccionados y la media es menor a 40%, mostrar el emoticono de advertencia 

        If( 
        
            ( [Product Group] = 'Produce' AND Sum(Margin) / Sum(Sales) < 0.35 ) OR 
            
            ( [Product Group] = 'Deli' AND Sum(Margin) / Sum(Sales) < 0.45 ) OR
            
            ( [Product Group] = 'Frozen Foods' AND Sum(Margin) / Sum(Sales) < 0.40 ) OR 
            
            ( [Product Group] = 'Snacks' AND Sum(Margin) / Sum(Sales) < 0.55 ) OR 
            
            ( [Product Group] = 'Canned Products' AND Sum(Margin) / Sum(Sales) < 0.35 ) OR 
            ( [Product Group] = 'Dairy' AND Sum(Margin) / Sum(Sales) < 0.30 ) OR 
            
            ( [Product Group] = 'Baking Goods' AND Sum(Margin) / Sum(Sales) < 0.35 ) OR 

            ( [Product Group] = 'Beverages' AND Sum(Margin) / Sum(Sales) < 0.45 ) OR 
            
            ( [Product Group] = 'Alcoholic Beverages' AND Sum(Margin) / Sum(Sales) < 0.50 ) OR 

            ( [Product Group] = 'Starchy Foods' AND Sum(Margin) / Sum(Sales) < 0.25 ) OR 

            ( [Product Group] = 'Breakfast Foods' AND Sum(Margin) / Sum(Sales) < 0.45 ) OR 

            ( [Product Group] = 'Eggs' AND Sum(Margin) / Sum(Sales) < 0.25 ) OR 
            
            ( [Product Group] = 'Baked Goods' AND Sum(Margin) / Sum(Sales) < 0.45 ) OR 
            
            ( [Product Group] = 'Meat' AND Sum(Margin) / Sum(Sales) < 0.30 ) OR 
            
            ( [Product Group] = 'Seafood' AND Sum(Margin) / Sum(Sales) < 0.45 ), 
            '    ' & Num(Sum(Margin) / Sum(Sales), '0.0%'),  // Si está por debajo del margen exigido, muestra el emoticono de advertencia

            '    ' & Num(Sum(Margin) / Sum(Sales), '0.0%')   // Si está por encima o igual, muestra el emoticono de éxito 
            
        ) 
        
    ) 
    
) 


Expresión Color de Fondo del KPI Gross Profit Margin 

=If( 
    GetSelectedCount([Product Group]) = 0,  
    RGB(0,0,0),  // Fondo negro si no hay selección 
    
    If( 
     GetSelectedCount([Product Group]) > 1 AND (Sum(Margin) / Sum(Sales)) < 0.40,  // Calcular el promedio correcto de la rentabilidad 
        RGB(255, 204, 0),  // Si hay más de un producto seleccionado y la media es menor a 40, mostrar el emoticono de advertencia 
        If( 
            ( [Product Group] = 'Produce' AND Sum(Margin) / Sum(Sales) * 100 < 35 ) OR 
            ( [Product Group] = 'Deli' AND Sum(Margin) / Sum(Sales) * 100 < 45 ) OR 
            ( [Product Group] = 'Frozen Foods' AND Sum(Margin) / Sum(Sales) * 100 < 40 ) OR 
            ( [Product Group] = 'Snacks' AND Sum(Margin) / Sum(Sales) * 100 < 55 ) OR 
            ( [Product Group] = 'Canned Products' AND Sum(Margin) / Sum(Sales) * 100 < 35 ) OR 
            ( [Product Group] = 'Dairy' AND Sum(Margin) / Sum(Sales) * 100 < 30 ) OR 
            ( [Product Group] = 'Baking Goods' AND Sum(Margin) / Sum(Sales) * 100 < 35 ) OR 
            ( [Product Group] = 'Beverages' AND Sum(Margin) / Sum(Sales) * 100 < 45 ) OR 
            ( [Product Group] = 'Alcoholic Beverages' AND Sum(Margin) / Sum(Sales) * 100 < 50 ) OR 
            ( [Product Group] = 'Starchy Foods' AND Sum(Margin) / Sum(Sales) * 100 < 25 ) OR 
            ( [Product Group] = 'Breakfast Foods' AND Sum(Margin) / Sum(Sales) * 100 < 45 ) OR 
            ( [Product Group] = 'Eggs' AND Sum(Margin) / Sum(Sales) * 100 < 25 ) OR 
            ( [Product Group] = 'Baked Goods' AND Sum(Margin) / Sum(Sales) * 100 < 45 ) OR 
            ( [Product Group] = 'Meat' AND Sum(Margin) / Sum(Sales) * 100 < 30 ) OR 
            ( [Product Group] = 'Seafood' AND Sum(Margin) / Sum(Sales) * 100 < 45 ), 
            RGB(255,0,0),  // Rojo si está por debajo del margen exigido 
            RGB(0,200,0)   // Verde si está por encima o igual al margen exigido 
        ) 
       ) 
) 

 
Expresiones Medidas etiquetas Gráfico Mekko 

• Gross Profit Margin 

=Num((Sum(Sales) - Sum(Cost))/Sum([Sales Qty]),'0.00') 

• Gross Profit Margin% 

=Num((Sum(Sales) - Sum(Cost)) / Sum(Sales),'0.00%') 

• ROI 

=Num((Sum(Sales) - Sum(Cost)) / Sum(Cost),'0.00%')

PALETA DE COLORES

![AdobeColor-My Color Theme (1)](https://github.com/user-attachments/assets/903ddeed-8b93-4660-b330-17c7fc03406e)

PRUEBAS DE COLOR 

https://www.color-blindness.com/coblis-color-blindness-simulator/
![das](https://github.com/user-attachments/assets/d7d3ddd0-8d99-447e-9f4c-ded660b46adb)
![2d](https://github.com/user-attachments/assets/00995a74-604e-475c-9101-add9c988229d)
![3d](https://github.com/user-attachments/assets/468fa651-6941-4b4e-a7fe-9cec9931033f)
![d10](https://github.com/user-attachments/assets/03fa77f7-5d67-410b-8f1c-a5dc68fbfc48)


![5d](https://github.com/user-attachments/assets/3097295d-43a1-40ed-8b06-5cb8fe94a301)
![8d](https://github.com/user-attachments/assets/71b1774a-03a4-4d6c-9d17-24c6e16e19d2)

![6d](https://github.com/user-attachments/assets/1300efc1-31d6-4ac6-a575-50c853b028a4)
![9d](https://github.com/user-attachments/assets/70120b18-7ecb-4c5e-9b84-6fc1b5a40534)


![4d](https://github.com/user-attachments/assets/afdeef73-76df-4f09-bdd6-09a7efe1a6a5)
![7d](https://github.com/user-attachments/assets/35e3dd24-3bef-4836-8688-6d215aa840b6)





