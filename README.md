# Simulación de Minibanco Inteligente y Cuenta Bancaria
class Cuenta_BancariaAhorros:
    def __init__(self, NombreTitular, ApellidoTitular, NumeroDeCuenta, saldo):
        self.NombreTitular = NombreTitular
        self.ApellidoTitular = ApellidoTitular
        self.NumeroDeCuenta = NumeroDeCuenta
        self.historial = []
        self.saldo = saldo

    def mostrarInfo(self):
        print("NombreTitular:", self.NombreTitular)
        print("ApellidoTitular:", self.ApellidoTitular)
        print("NumeroDeCuenta:", self.NumeroDeCuenta)
        print("Saldo:", self.saldo)

    def depositar(self, monto):
        self.saldo += monto
        self.historial.append(('Deposito', monto, "Ok"))

    def retirar(self, monto):
        if monto <= self.saldo:
            self.saldo -= monto
            self.historial.append(('Retiro', monto, "Ok"))
        else:
            print("Saldo insuficiente")

    def ConsultarSaldo(self):
        print("Su saldo actual es de:", self.saldo)

    def transferir(self, monto, otra_cuenta):
        if monto <= self.saldo:
            self.retirar(monto)
            otra_cuenta.depositar(monto)
            self.historial.append(('Transferencia', monto, f"A{otra_cuenta.NumeroDeCuenta}"))
        else:
            self.historial.append(('Transferencia', monto, "Error: saldo insuficiente"))


# Diccionario de cuentas
cuentas = {}
cuentas_existentes = set()

def crear_cuenta(numero, nombre, apellido, saldo_inicial=0):
    if numero in cuentas_existentes:
        print("Cuenta ya existe")
    else:
        cuentas[numero] = Cuenta_BancariaAhorros(nombre, apellido, numero, saldo_inicial)
        cuentas_existentes.add(numero)
        print("Cuenta creada con éxito")



crear_cuenta(101, "Ibrahim", "Safadi", 500000)
crear_cuenta(102, "Juan Sebastian", "Rocha", 100000)
crear_cuenta(103, "Juan Esteban", "Rubio", 200000)
