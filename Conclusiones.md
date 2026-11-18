# Conclusiones

**Proyecto:** Implementación de WAF para protección de aplicación web vulnerable
**Entorno:** SafeLine WAF 9.4.3 protegiendo DVWA en un laboratorio aislado

---

## 1. Resumen

Se desplegó SafeLine WAF delante de DVWA y se configuraron cuatro controles: limitación de tasa, autenticación de acceso, reglas Allow & Deny y análisis semántico por módulo de ataque. Cada control se probó y se documentó con evidencia visual. El WAF permitió proteger una aplicación vulnerable sin modificar su código, aunque su eficacia depende directamente de cómo se configure cada módulo.

---

## 2. Resultados por control

| Control | Configuración | Resultado |
|---|---|---|
| **Limitación de tasa** | 3 accesos en 10 segundos, bloqueo de 5 minutos | ✅ La IP fue bloqueada y el evento quedó registrado en el panel *Rate Limiting*. El cliente recibió la página *Access Forbidden* con el motivo del bloqueo. |
| **Autenticación (Auth)** | Condición: IP de origen igual a `192.168.100.153` | ✅ Se exige autenticación a las peticiones que cumplen la condición. |
| **Regla Deny por IP** | Regla `kali-deny`, posición *First*, sin modo monitor | ✅ La petición fue denegada y el WAF devolvió *Access Forbidden* con un identificador único de evento. |
| **Análisis semántico** | SQL Inj en *Disabled*; resto de módulos en *Balance Mode* | ⚠️ La inyección SQL no fue detectada mientras el módulo estuvo desactivado. |

---

## 3. Hallazgo principal

Con el módulo **SQL Inj** en *Disabled*, el payload de prueba llegó a la aplicación y DVWA devolvió los cinco usuarios de la tabla en lugar de uno solo. Esto confirma dos cosas:

- La aplicación es vulnerable a inyección SQL, como se esperaba de DVWA.
- Un WAF solo protege aquello que tiene activado. Un módulo desactivado deja la aplicación expuesta al ataque correspondiente, aunque el resto de controles esté bien configurado.

---

## 4. Lecciones aprendidas

- **El orden de las reglas importa.** Colocar una regla de denegación en la primera posición hace que se evalúe antes que las demás y tenga máxima prioridad.
- **Los controles se complementan.** La limitación de tasa frena el abuso de peticiones, las reglas Allow & Deny controlan el origen y el análisis semántico inspecciona el contenido. Ninguno reemplaza a los otros.
- **El modo de detección es una decisión de equilibrio.** *Audit* solo registra, *Balance* busca un punto medio con pocos falsos positivos y *Strict* detecta de forma más agresiva. Elegir el modo adecuado exige conocer la aplicación y su tráfico legítimo.
- **La evidencia es parte del trabajo.** Documentar cada configuración y cada prueba facilita reproducir el laboratorio y explicar los resultados.

---

## 5. Limitaciones

- El laboratorio se ejecutó en un entorno aislado, con una sola aplicación y tráfico generado manualmente.
- Las pruebas de ataque se limitaron a inyección SQL.
- No se midieron falsos positivos ni el impacto del WAF en el rendimiento.
