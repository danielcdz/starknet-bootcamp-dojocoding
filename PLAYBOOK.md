# Cairo Masterclass: Bases sólidas para construir en Starknet

---
Cairo Masterclass: Bases sólidas para construir en Starknet
Daniel Calderon Diaz

Pre Requisitos:
  - Comprensión de tipos de datos en starknet
  - Conocimientos básicos de programación
  - Familiaridad con conceptos básicos de blockchain (wallets, transacciones, faucets, smart-contracts)
  - Entendimiento de fundamentos de Starknet
  
Herramientas requeridas:
  - asdf version 0.16.7
  - Scarb (v2.12.0) para compilación de Cairo
  - Starknet Foundry (v0.49.0) para unit tests
  - snforge y sncast 0.49.0 para despliegue de wallets y contratos desde CLI
  - Git
  - IDE de preferencia (Cursor, VSCode)
  - Extensión de VSCode para Cairo
---

## 🎯 Objetivos de aprendizaje

Al final de esta sesión, los participantes podrán:

* [ ] **Escribir programas en Cairo**: Crear 3 o más programas ejecutables que utilicen funciones, tipos de datos y control de flujo, compilando sin errores con `scarb build` y validando con pruebas unitarias mediante `scarb test`.
* [ ] **Dominar la sintaxis de Cairo**: Leer y comprender ≥90% de los ejemplos del repositorio [https://github.com/starknet-foundation/teaching-cairo](https://github.com/starknet-foundation/teaching-cairo); utilizar correctamente `felt252`, `u256`, `array`, `struct` y `enum`.
* [ ] **Comprender los smart contracts en Cairo/Starknet**: Explicar la arquitectura del contrato, su `storage`, los eventos y el ciclo de vida de una transacción; realizar lectura y escritura de estado; entender cómo se interactúa con un contrato usando una wallet como Ready (u otra compatible) y utilizar un *faucet* para obtener tokens de prueba en **Sepolia**.
* [ ] **Escribir y desplegar smart contracts en Cairo**: Desplegar un contrato funcional en testnet desde la línea de comandos con `sncast` y ejecutar transacciones reales (lectura/escritura), verificando sus resultados.
* [ ] **Aplicar correctamente los tipos de datos de Cairo**: Seleccionar y justificar el uso de `felt252`, `u256`, `array`, `struct` y `enum` según el caso de uso en los ejercicios.

## 📦 Entregables

* [ ] **Cuenta en Starknet con `sncast`** — Crear y **desplegar** una cuenta en testnet **Sepolia** desde la línea de comandos para poder firmar y enviar transacciones.

* [ ] **Contrato `HelloWorld` en Sepolia** — Compilar con `scarb build`, **declarar** y **desplegar** el contrato usando `sncast` (declare + deploy).


## 💡 Introducción

### ¿Por qué es importante esto?

Dominar Cairo abre puertas reales en la industria blockchain, especialmente dentro del ecosistema de rápido crecimiento de Starknet. Como lenguaje nativo de Starknet, Cairo te brinda las habilidades para diseñar contratos inteligentes seguros y escalables, integrarte a una comunidad de desarrolladores en pleno auge y crear productos que se benefician de bajas comisiones y alto rendimiento. Con esta base, puedes llevar un concepto desde el primer prototipo hasta un MVP, iterar hasta convertirlo en una startup lista para generar ingresos y posicionarte para postular a oportunidades de financiamiento no dilutivo de la Starknet Foundation.

### ¿Qué construiremos?

#### Fundamentos de Cairo (mini programas)

Escribiremos pequeños programas en Cairo para aprender la sintaxis esencial, los tipos de datos (`felt252`, `structs`, `enums`), funciones y módulos. Practicarás gestión de memoria, aserciones y pruebas básicas para que el lenguaje te “haga clic”.

#### Smart contracts simples (de cero a testnet)

Diseñaremos, implementaremos y desplegaremos un contrato inicial en la testnet de Starknet. Verás el flujo completo: compilar y probar con `snforge`, desplegar e interactuar desde la línea de comandos con `sncast` (lectura/escritura y eventos).

## ⚙️ Sección 1: Estudio de scripts en Cairo

### Concepto clave

Dominar la sintaxis de Cairo sienta las bases para comprender el ciclo de vida y la **ejecución** de un smart contract en Starknet. Con estos fundamentos podrás diseñar e implementar soluciones más seguras y escalables, reduciendo errores y fricción.

### Herramientas Requeridas

- asdf version 0.16.7
- Scarb v2.12.0: Herramienta de build para Cairo (instala vía `asdf install scarb 2.12.0` o https://docs.swmansion.com/scarb/download.html).
- Git
- IDE de preferencia (Cursor, VSCode)
- Extensión de VSCode para Cairo

### Ejercicio práctico: **Compilación** y **tests unitarios** de archivos Cairo

**Objetivo:** Analizar, comprender y ejecutar código Cairo de forma local.

**Pasos:**

1. **Clona** el repositorio oficial con ejemplos y *scripts* en Cairo:

   ```bash
   git clone https://github.com/starknet-foundation/teaching-cairo
   ```

2. **Abre** el proyecto en tu editor de código preferido.

3. **Explora** la carpeta `src/`: contiene ejemplos de sintaxis, estructuras de datos y flujos de control.

4. **Compila** el proyecto:

   ```bash
   scarb build
   ```

5. **Ejecuta** los tests del proyecto:

   ```bash
   scarb test
   ```

6. **Modifica** archivos y pruebas para observar comportamientos distintos (por ejemplo, cambiar valores, agregar *asserts* y volver a correr `scarb test`).

**Resultado esperado:** Sin cambios al código, el *build* debe finalizar exitosamente (mensaje de compilación exitosa en la terminal) y **todos los tests** deben pasar.

### ⚠️ Solución de problemas comunes

* **Error:** `scarb: command not found` o *mismatch* de versión.

**Solución:**

```bash
asdf install scarb 2.12.0
asdf set scarb 2.12.0
# opcional: verificar versión
scarb --version
```

Luego, **reinicia** la terminal e intenta nuevamente `scarb build` y `scarb test`.


## ⚙️ Sección 2: Creación del contrato HelloStarknet: compilación, declaración y despliegue

### Concepto clave

Comprender la **estructura y componentes** de un smart contract en Starknet, módulos, `storage`, eventos y puntos de entrada nos permite diseñar contratos más robustos que resuelvan las necesidades reales de nuestros proyectos. Además, dominar el flujo de **construcción → compilación → declaración → despliegue** sienta la base para **integrarlos de forma segura y eficiente** en nuestras dApps.


### Herramientas Requeridas

- asdf version 0.16.7
- Scarb v2.12.0: Herramienta de build para Cairo (instala vía `asdf install scarb 2.12.0` o https://docs.swmansion.com/scarb/download.html).
- snforge y sncast 0.49.0 para despliegue de wallets y contratos desde CLI (incluidos en Starknet Foundry)
- Wallet Argent X o Braavos: Para conexiones en testnet.
- Faucet: https://starknet-faucet.vercel.app/ para STRK en Sepolia.
- Git
- IDE de preferencia (Cursor, VSCode)
- Extensión de VSCode para Cairo

### Ejercicio práctico: Generación de plantilla de contrato, compilación, declaración y despliegue en Sepolia

**Objetivo:** Generar una **plantilla de contrato** con `snforge` y, a continuación, **compilarla, declararla y desplegarla** en **Sepolia** desde la línea de comandos con `sncast`.

**Pasos:**

1. **Genera la plantilla del contrato `HelloStarknet`:**

   ```bash
   snforge new hello_world
   cd hello_world
   ```

2. **Selecciona** *Starknet Foundry* como paquete de tests (si se te solicita).

3. **Abre** el proyecto en tu IDE preferido.

4. **Ubica** el contrato base en `src/lib.cairo`.

5. **Compila y prueba** el proyecto para generar artefactos y verificar que todo esté ok:

   ```bash
   scarb build
   snforge test
   ```

6. **Crea una cuenta** para firmar transacciones:

   ```bash
   sncast account create --network sepolia --name my_account
   ```

7. **Fondea la cuenta** con tokens de prueba `$STRK` usando el faucet (usa la **dirección** que te devolvió el paso anterior):
   
   Faucet STRK Sepolia: [https://starknet-faucet.vercel.app/](https://starknet-faucet.vercel.app/)

8. **Despliega la cuenta** en la red:

   ```bash
   sncast account deploy --network sepolia --name my_account
   ```

9. **Declara el contrato** en Sepolia (usa el nombre real del contrato en tu `Scarb.toml`, p. ej. `HelloStarknet`):

   ```bash
   sncast --account my_account declare --network sepolia --contract-name HelloStarknet
   ```

   > Guarda el `class_hash` que devuelve este paso.

10. **Despliega el contrato** usando el `class_hash` anterior:

    ```bash
    sncast --account my_account deploy --network sepolia --class-hash <CLASS_HASH>
    ```

    > Si tu contrato tiene constructor, agrega `--constructor-calldata <args>`.

11. **Verifica e interactúa** con tu contrato desde un *block explorer* (Voyager o StarkScan)

**Notas:**

* Reemplaza `my_account`, `HelloStarknet`, `<CLASS_HASH>` y `<CONTRACT_ADDRESS>` por tus valores.
* Asegúrate de haber corrido `scarb build` **antes** de `declare` para que existan los artefactos (Sierra/Casm).

**Resultado esperado:**

- `scarb build` finaliza **sin errores** y genera los artefactos (Sierra/CASM).
- `scarb test` muestra **todos los tests en "passed"** (N passed, 0 failed).
- **Cuenta en Sepolia** creada, fondeada y desplegada con `sncast account create/deploy` (dirección y hash registrados).
- **Contrato `HelloStarknet`** declarado y desplegado en Sepolia: se obtiene y guarda el `class_hash` y la `contract_address`.
- **Interacciones básicas verificadas**: una `call` de lectura devuelve el valor esperado y una `invoke` de escritura confirma hash de transacción/evento.
- **Comprobación en explorer** (Voyager/StarkScan) de transacciones y estado del contrato.


### ⚠️ Solución de problemas comunes

**Error:** `scarb: command not found` o *mismatch* de versión.

**Solución:**

```bash
asdf install scarb 2.12.0
asdf set scarb 2.12.0
# opcional: verificar versión
scarb --version
```

Luego, **reinicia** la terminal e intenta nuevamente `scarb build` y `scarb test`.

**Error:** `sncast/snforge: command not found` o *mismatch* de versión.

**Solución:**

```bash
asdf install starknet-foundry 0.49.0
asdf set starknet-foundry 0.49.0
# opcional: verificar versión
snforge --version
sncast --version
```

Luego, **reinicia** la terminal e intenta nuevamente `scarb build` y `scarb test`.

### Conexión con otras sesiones

Este playbook se apoya en el **taller de Fundamentos de Starknet** y sirve como puente hacia la siguiente clase, **Desarrollo Full-Stack en Starknet**. Aquí afianzarás los conceptos esenciales de **Cairo** y de **smart contracts** (estructura, `storage`, eventos y ciclo de transacciones) y el flujo de **construcción → pruebas → declaración → despliegue**, necesarios para integrar contratos en tus dApps.

## 📚 Recursos Extra

### Recursos para Cairo de 0 a 100
- https://www.cairo-lang.org/
- https://www.starknet.io/cairo-book/title-page.html
- https://starklings.app/
- https://docs.starknet.io/build/quickstart/environment-setup
- https://www.starknet.io/tutorials/
- https://github.com/starknet-foundation/teaching-cairo
- https://github.com/ByteBeasts/tamagotchi-contracts

### Herramientas Complementarias
- ASDF para Gestión de Herramientas: https://asdf-vm.com/
- Faucets: https://starknet-faucet.vercel.app/



