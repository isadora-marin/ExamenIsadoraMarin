
import random 
import csv
def sueldoaleatorio():
    return random.randint(300000,2500000)
Trabajadores = [
    {"Nombre": "Juan Perez", "Sueldo": sueldoaleatorio()},
    {"Nombre": "Maria Gracia", "Sueldo": sueldoaleatorio()}, 
    {"Nombre": "Carlos Lopéz", "Sueldo": sueldoaleatorio()},
    {"Nombre": "Ana Martinez", "Sueldo": sueldoaleatorio()},
    {"Nombre": "Pedro Rodrigez", "Sueldo": sueldoaleatorio()},
    {"Nombre": "Laura Hernandez", "Sueldo": sueldoaleatorio()},
    {"Nombre": "Miguel Sanchez", "Sueldo": sueldoaleatorio()},
    {"Nombre": "Isabel Gomez", "Sueldo": sueldoaleatorio()},
    {"Nombre": "Francisco Diaz", "Sueldo": sueldoaleatorio()},
    {"Nombre": "Elena Fernandez", "Sueldo": sueldoaleatorio()} 
]

tablasmenores_800k = []
tablasentre_800ky_2M = []
tablasmayores_2M = []

total_menores_800k = 0
totalentre_800ky_2M = 0
totaLmayores_2M = 0
totalsueldos = 0

for Trabajadores in Trabajadores:
    nombre = Trabajadores["Nombre"]
    sueldo = Trabajadores["Sueldo"]
    totalsueldos += sueldo
    if sueldo < 800000: 
        tablasmenores_800k.append(Trabajadores)
        total_menores_800k += 1
    elif sueldo >= 800000 <= 2000000:
        tablasentre_800ky_2M.append(Trabajadores)
        totalentre_800ky_2M += 1
    else:
        tablasmayores_2M.append(Trabajadores)
        totaLmayores_2M += 1

def imprimir_empleados(Trabajadores):
    print("{:<20} {:<10}".format("Nombre empleado", "Sueldo"))
    for Trabajadores in Trabajadores:
        nombre = Trabajadores["Nombre"]
        sueldo = Trabajadores["Sueldo"]
        print("{:<20}${:,}".format(nombre,sueldo))

def imprimir_reporte(Trabajadores):
    print("{:20}{:<10}{:<10}{:<10}{:<15}".format(
        "Nombre Empleado", "Sueldo", "Descuento Salud", "Descuento AFP", "Sueldo Liquido"
    ))
    for Trabajadores in Trabajadores:
        nombre = Trabajadores["Nombre"]
        sueldo = Trabajadores["Sueldo"]
        descuento_salud = sueldo * 0.07
        descuento_AFP = sueldo * 0.12
        sueldo_liquido = sueldo - descuento_AFP - descuento_salud
        print("{:<20}${:<10,.2f}${:<10,.2f}f{:<10,.2f}{:<15,.2f}".format(
            nombre, sueldo, descuento_salud, descuento_AFP, sueldo, sueldo_liquido
        ))
        
print("Sueldos menores a 800.000 TOTAL: {}".format(total_menores_800k))
imprimir_empleados(tablasmenores_800k)

print("\nSueldos entre 800.000 y 2.000.000 TOTAL: {}".format(totalentre_800ky_2M))
imprimir_empleados(tablasentre_800ky_2M)

print("n\Sueldos mayores a 2.000.000 TOTAL: {}".format(totaLmayores_2M))
imprimir_empleados(tablasmayores_2M)

print("TOTAL SUELDOS: ${:,}".format(totalsueldos))

def exportaracsv(Trabajadores, nombre_archivo):
    with open(nombre_archivo, mode="w", newline="") as archivo:
        writer = csv.writer(archivo)
        writer.writerow(["Nombre empleado", "Sueldo Base", "Descuento salud", "Descuento AFP", "Sueldo Liquido"])
        for Trabajadores in Trabajadores:
            nombre = Trabajadores["Nombre"]
            sueldo = Trabajadores["Sueldo"]
            descuento_salud = sueldo * 0.07
            descuento_AFP = sueldo * 0.12
            sueldo_liquido = sueldo - descuento_AFP - descuento_salud
            writer.writerow([nombre, sueldo, descuento_salud, descuento_AFP, sueldo_liquido])