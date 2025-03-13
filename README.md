# Sistema de Validación de Productos
# Taller de programación con Python

import time

def solicitar_datos():
    """Solicita y valida los datos de un producto ingresado por el usuario."""
    while True:
        nombre = input("Ingrese el nombre del producto (o escriba 'salir' para terminar): ").strip()
        if nombre.lower() == "salir":
            return None, None, None
        if nombre:
            break
        print("El nombre no puede estar vacío. Inténtalo de nuevo.")
    
    while True:
        try:
            precio = float(input("Ingrese el precio del producto: "))
            if precio > 0:
                break
            print("El precio debe ser un número positivo. Inténtalo nuevamente.")
        except ValueError:
            print("Entrada no válida. Debe ser un número.")
    
    while True:
        try:
            stock = int(input("Ingrese la cantidad en stock: "))
            if stock >= 0:
                break
            print("El stock no puede ser negativo. Prueba otra vez.")
        except ValueError:
            print("Debes ingresar un número entero.")
    
    return nombre, precio, stock

def validar_producto(precio, stock):
    """Valida el producto en base a su precio y stock, determinando su categoría de venta."""
    if precio > 1000 and stock > 50:
        return "Producto aprobado para venta premium."
    elif precio <= 1000 and stock > 0:
        return "Producto disponible para venta regular."
    return "Producto no disponible para la venta."

def mostrar_resumen(productos):
    """Muestra un resumen de todos los productos ingresados, incluyendo el total."""
    print("\nResumen de productos ingresados:")
    print("=" * 50)
    total = 0
    for producto in productos:
        subtotal = producto['precio'] * producto['stock']
        total += subtotal
        print(f"{producto['nombre']} - ${producto['precio']:.2f} - Stock: {producto['stock']} unidades - {producto['estado']} - Subtotal: ${subtotal:.2f}")
    print("=" * 50)
    print(f"Total del inventario: ${total:.2f}")

def main():
    print("\nBienvenido al sistema de validación de productos")
    productos = []
    while True:
        nombre, precio, stock = solicitar_datos()
        if nombre is None:
            break
        estado = validar_producto(precio, stock)
        productos.append({"nombre": nombre, "precio": precio, "stock": stock, "estado": estado})
        print(f"\n{estado}\n")
        time.sleep(1)
    
    if productos:
        mostrar_resumen(productos)
    print("\nGracias por usar el sistema. Hasta luego.")

if __name__ == "__main__":
    main()
