## Implementación de reglas en el WAF y comprobación
En esta sección se nombrarán las reglas configuradas en en WAF junto con la comprobación de la aplicación de dichas reglass al ejecutar pruebas en la aplicación web vulnerable.

#### Protección de limitación de tasa
Se comenzará implementando un límite de peticiones para una misma IP de origen. La figura 1 muestra la regla implementada en el WAF para que una IP se bloquee por 5 minutos tras 3 peticiones en la páquina web en menos de 10 segundos. Para esto se debe ir a la sección de HTTP Flood -> Access Limiting del WAF.

<p align="center">
  <img src="images/edit_rules_resaltado.png" alt="Ventana Edit rules con los parámetros Duration, Access, Action y Block resaltados en rojo" width="700">
  <br>
  <em>Figura 1. Ventana "Edit rules" con los parámetros de la regla resaltados en rojo.</em>
</p>

Ahora, al implementar la regla, se puede entrar a la aplicación web configurada y probar seleccionar varios apartados de ella. Cuando se seleccionan 2 apartados aparece la siguiente advertencia.




