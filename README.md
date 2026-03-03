import pandas as pd

# Cargar datos
df = pd.read_csv("datos.csv")

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
