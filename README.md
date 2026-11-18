# Implementación de WAF para protección de aplicación web vulnerable

Proyecto de laboratorio en el que se despliega y configura **SafeLine WAF** para proteger **DVWA** (Damn Vulnerable Web Application), una aplicación web intencionalmente vulnerable. Este documento es una introducción general; cada etapa se desarrolla en detalle por separado.

> ⚠️ Proyecto educativo ejecutado en un entorno de laboratorio aislado. No repliques estas pruebas en sistemas sin autorización expresa.

## 🎯 Objetivo

Proteger una aplicación web vulnerable con un WAF y evaluar la eficacia de sus controles frente a abuso de peticiones y ataques web.

## 🧪 Entorno

| Componente | Detalle |
|---|---|
| **WAF** | SafeLine WAF 9.4.3 |
| **Aplicación protegida** | DVWA |
| **Acceso** | `webserver.socialdork` por HTTPS (443) |

## 🛡️ Lo que se hizo

1. **Limitación de tasa:** bloqueo de 5 minutos a quien supere 3 accesos en 10 segundos.
2. **Autenticación (Auth):** módulo habilitado con usuario propio y condición por IP de origen.
3. **Reglas Allow & Deny:** regla de denegación por IP (`kali-deny`) con máxima prioridad.
4. **Análisis semántico:** configuración del modo de detección por módulo de ataque (SQL Inj, XSS, CMD Inj, entre otros).
5. **Pruebas sobre DVWA:** inyección SQL para validar el comportamiento del WAF.

## 📊 Resultados

| Control | Resultado |
|---|---|
| Limitación de tasa | ✅ Bloqueo efectivo de la IP |
| Regla Deny por IP | ✅ Petición denegada (*Access Forbidden*) |
| Módulo Auth | ✅ Autenticación exigida según condición |
| Análisis semántico de SQL | ⚠️ Con el módulo en *Disabled*, la inyección SQL no fue detectada |

## 👤 Autor

**Marcelo Cerda Muñoz**
