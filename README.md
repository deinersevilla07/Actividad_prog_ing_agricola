# Actividad_prog_ing_agricola
Repository creado para la realización de las actividades de la materia de programación 


def mostrar_menu():
    print("\n--- Calculadora de Costos de Materiales para Cimientos ---")
    print("1. Calcular materiales y costos para una zapata aislada")
    print("2. Salir")


def solicitar_float(mensaje):
    while True:
        try:
            valor = float(input(mensaje))
            if valor <= 0:
                print("Por favor, ingrese un valor numérico mayor a cero.")
                continue
            return valor
        except ValueError:
            print("Entrada inválida. Por favor, ingrese un número válido.")


def calcular_volumen(largo, ancho, alto):
    return largo * ancho * alto


def calcular_materiales(volumen):
    """
    Dosificación estándar para 1 m³ de concreto:
    - Cemento: 7 sacos
    - Arena: 0.6 m³
    - Grava: 0.8 m³
    - Agua: 0.2 m³
    """
    return {
        'cemento_sacos': 7 * volumen,
        'arena_m3': 0.6 * volumen,
        'grava_m3': 0.8 * volumen,
        'agua_m3': 0.2 * volumen,
    }


def calcular_costos(materiales, costos_unitarios):
    return {
        'cemento_usd': materiales['cemento_sacos'] * costos_unitarios['cemento_usd_saco'],
        'arena_usd': materiales['arena_m3'] * costos_unitarios['arena_usd_m3'],
        'grava_usd': materiales['grava_m3'] * costos_unitarios['grava_usd_m3'],
        'agua_usd': materiales['agua_m3'] * costos_unitarios['agua_usd_m3'],
    }


def mostrar_resumen(volumen, materiales, costos, total):
    print("\n--- Resumen de Materiales y Costos ---")
    print(f"Volumen total del cimiento: {volumen:.3f} m³")
    print(f"Cemento: {materiales['cemento_sacos']:.2f} sacos")
    print(f"Arena:   {materiales['arena_m3']:.2f} m³")
    print(f"Grava:   {materiales['grava_m3']:.2f} m³")
    print(f"Agua:    {materiales['agua_m3']:.2f} m³")
    print("\n--- Costos estimados ---")
    print(f"Cemento: ${costos['cemento_usd']:.2f} USD")
    print(f"Arena:   ${costos['arena_usd']:.2f} USD")
    print(f"Grava:   ${costos['grava_usd']:.2f} USD")
    print(f"Agua:    ${costos['agua_usd']:.2f} USD")
    print(f"\nCOSTO TOTAL ESTIMADO: ${total:.2f} USD")
    print("-" * 45)


def main():
    # Base de datos de costos unitarios (puedes modificar estos valores)
    costos_unitarios = {
        'cemento_usd_saco': 8.5,
        'arena_usd_m3': 20.0,
        'grava_usd_m3': 25.0,
        'agua_usd_m3': 1.0
    }

    while True:
        mostrar_menu()
        opcion = input("Seleccione una opción: ").strip()
        if opcion == "1":
            print("\nIngrese las dimensiones del cimiento (en metros):")
            largo = solicitar_float("Largo (m): ")
            ancho = solicitar_float("Ancho (m): ")
            alto = solicitar_float("Altura (m): ")

            volumen = calcular_volumen(largo, ancho, alto)
            materiales = calcular_materiales(volumen)
            costos = calcular_costos(materiales, costos_unitarios)
            total = sum(costos.values())

            mostrar_resumen(volumen, materiales, costos, total)
        elif opcion == "2":
            print("¡Gracias por usar la calculadora!")
            break
        else:
            print("Opción inválida. Intente de nuevo.")


if __name__ == "__main__":
    main()    
