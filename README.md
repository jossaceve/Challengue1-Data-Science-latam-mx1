import pandas as pd

# Si estás en Colab normalmente ya viene instalado pandas
!pip install pandas numpy

import pandas as pd
import numpy as np# Cargar datos
df1 = pd.read_csv("challenge1-data-science-latam-main/base-de-datos-challenge1-latam/tienda_1.csv")
df2 = pd.read_csv("challenge1-data-science-latam-main/base-de-datos-challenge1-latam/tienda_2.csv")
df3 = pd.read_csv("challenge1-data-science-latam-main/base-de-datos-challenge1-latam/tienda_3.csv")
df4 = pd.read_csv("challenge1-data-science-latam-main/base-de-datos-challenge1-latam/tienda_4.csv")

# Agregar columna identificadora de tienda
df1["tienda"] = "Tienda 1"
df2["tienda"] = "Tienda 2"
df3["tienda"] = "Tienda 3"
df4["tienda"] = "Tienda 4"

# Unir todos los datos en un solo DataFrame
df = pd.concat([df1, df2, df3, df4], ignore_index=True)
# 1️⃣ Facturación total por tienda
df["facturacion"] = df["precio"] * df["cantidad"]
facturacion_tienda = df.groupby("tienda")["facturacion"].sum()

# 2️⃣ Categorías más populares por tienda
categorias_populares = (
    df.groupby(["tienda", "categoria"])["cantidad"]
    .sum()
    .sort_values(ascending=False)
)

# 3️⃣ Promedio de evaluación por cliente
promedio_evaluacion = df.groupby("evaluacion_cliente")["evaluacion_cliente"].mean()

# 4️⃣ Productos más y menos vendidos por tienda
productos_vendidos = df.groupby(["tienda", "producto"])["cantidad"].sum()
mas_vendidos = productos_vendidos.groupby("tienda").idxmax()
menos_vendidos = productos_vendidos.groupby("tienda").idxmin()

# 5️⃣ Costo promedio de envío por tienda
costo_envio_promedio = df.groupby("tienda")["costo_envio"].mean()

# Mostrar resultados
print("\nFacturación total por tienda:")
print(facturacion_tienda)

print("\nCategorías más populares:")
print(categorias_populares)

print("\nPromedio de evaluación:")
print(promedio_evaluacion)

print("\nProductos más vendidos:")
print(mas_vendidos)

print("\nProductos menos vendidos:")
print(menos_vendidos)

print("\nCosto promedio de envío por tienda:")
print(costo_envio_promedio)


# Crear columna de facturación
df["facturacion"] = df["precio"] * df["cantidad"]

facturacion_tienda = df.groupby("tienda")["facturacion"].sum().sort_values(ascending=False)

print("Facturación total por tienda:")
display(facturacion_tienda)

print("\nTienda con mayor facturación:")
print(facturacion_tienda.idxmax())
