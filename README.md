# Calculadora de recuento celular en cámara de Neubauer

**Herramienta de apoyo al Procedimiento Técnico Metodológico PT-LA-01**
Servicio de Laboratorio Clínico · Hospital General Reynosa "Dr. José María Cantú Garza"
Servicios de Salud IMSS-Bienestar · Reynosa, Tamaulipas, México

---

## Ficha técnica

| Campo | Contenido |
|---|---|
| **Nombre de la herramienta** | Calculadora de recuento celular en cámara de Neubauer |
| **Clave propuesta** | HA-LA-01 (pendiente de asignación por el Departamento de Calidad) |
| **Versión** | 1.0 |
| **Fecha de liberación** | Agosto de 2026 |
| **Documento del que deriva** | PT-LA-01 · Procedimiento Técnico Metodológico para el Estudio Citoquímico de Líquidos Corporales, numerales 9.2 y 14 |
| **Área responsable** | Servicio de Laboratorio Clínico |
| **Autor** | Q.F.B. Protacio Serna Ramírez |
| **Tipo de recurso** | Aplicación web local, archivo HTML único, sin dependencias externas |
| **Requiere internet** | No. Funciona sin conexión una vez descargada |
| **Requiere instalación** | No |
| **Almacena datos** | No. No guarda, transmite ni registra información de pacientes |

---

## Propósito

Estandarizar el cálculo del recuento celular en líquidos corporales, reduciendo el error en la determinación del área contada y del factor de dilución, que son las dos fuentes de error aritmético más frecuentes en el procedimiento.

La herramienta surge del análisis de causa raíz documentado en el reporte de no conformidad RNC-LC-01, que evidenció variabilidad en la unidad de reporte y en el método de recuento entre turnos.

---

## Alcance

**Aplica a:** cálculo de la concentración de leucocitos y eritrocitos en líquido cefalorraquídeo, líquidos serosos, líquido sinovial y líquido de diálisis peritoneal, a partir del conteo en cámara de Neubauer mejorada.

**No aplica a:** conteo diferencial, identificación morfológica, determinaciones químicas, ni ninguna otra fase del estudio citoquímico.

---

## Fundamento del cálculo

```
células/µL = (células contadas × factor de dilución) ÷ (área contada en mm² × 0.1 mm)
```

Donde 0.1 mm corresponde a la profundidad de la cámara de Neubauer mejorada.

| Selección | Área | Divisor |
|---|---|---|
| 9 cuadros grandes | 9 mm² | 0.9 |
| 4 cuadros grandes angulares | 4 mm² | 0.4 |
| 1 cuadro grande | 1 mm² | 0.1 |
| Retícula central completa (25 medianos) | 1 mm² | 0.1 |
| 5 cuadros medianos centrales | 0.2 mm² | 0.02 |

Cada cuadro mediano de la retícula central equivale a 0.04 mm². La aplicación calcula el área a partir de los cuadros que el usuario marca en la representación gráfica de la cámara.

### Casos de verificación

| Entrada | Resultado esperado | Verificado |
|---|---|---|
| 36 células, sin diluir, 4 cuadros angulares | 90 células/µL | Sí |
| 20 células, sin diluir, 9 cuadros grandes | 22.22 células/µL | Sí |
| 50 células, dilución 1:20, 4 cuadros angulares | 2 500 células/µL | Sí |
| 100 células, sin diluir, 5 medianos centrales | 5 000 células/µL | Sí |
| 12 células, sin diluir, 1 cuadro grande | 120 células/µL | Sí |

---

## Avisos automáticos

La herramienta emite señalamientos cuando detecta condiciones que comprometen la confiabilidad del conteo:

- **Conteo superior a 200 células** en el área marcada: recomienda diluir y repetir.
- **Celularidad baja con área reducida**: recomienda ampliar a los 9 cuadros grandes sin diluir.
- **Resultado superior a 5 leucocitos/µL**: señala que excede el rango de referencia del LCR y que requiere diferencial y correlación.
- **Presencia de eritrocitos**: señala la posibilidad de punción traumática o hemorragia.

Estos avisos son orientativos y no constituyen interpretación diagnóstica.

---

## Limitaciones

1. **No sustituye la validación técnica ni clínica** del químico responsable del turno.
2. **No corrige errores de técnica.** Un conteo mal ejecutado —cámara sobrellenada, sin reposo previo, con criterio de límite inconsistente o con reactivo inadecuado— produce un resultado erróneo que la herramienta calculará con exactitud. La capacitación supervisada al microscopio sigue siendo indispensable.
3. **No realiza el conteo.** El número de células lo aporta el usuario.
4. **No incorpora la corrección por punción traumática.** Esa corrección se aplica conforme al Anexo D del PT-LA-01.
5. Los umbrales de referencia incorporados corresponden a los definidos en el PT-LA-01 y deben revisarse cuando dicho procedimiento se actualice.

---

## Uso

1. Descargar el archivo `index.html`, o abrir el enlace publicado.
2. Marcar en la cámara los cuadros efectivamente contados.
3. Capturar el número total de células contadas, la dilución empleada y el tipo de célula.
4. Verificar el resultado y la fórmula desarrollada que se muestra debajo.
5. Consignar el resultado en el sistema conforme al PT-LC-01, en células/µL.

El archivo funciona sin conexión a internet. Puede copiarse a una memoria USB o al escritorio de las computadoras del laboratorio.

---

## Control de versiones

| Versión | Fecha | Cambios |
|---|---|---|
| 1.0 | Agosto de 2026 | Versión inicial. Cámara interactiva, cálculo de área automático, avisos de conteo y de rango. |

El historial completo de modificaciones, con fecha y autor de cada cambio, se conserva en el registro de commits de este repositorio y constituye la evidencia de control documental de la herramienta.

---

## Correspondencia con MOCEBPASS

| Estándar | Aportación de la herramienta |
|---|---|
| Eje 5 · Componente A · Estándar 22/25 *(Indispensable)* | Estandariza el cálculo analítico y reduce la variabilidad entre operadores y turnos |
| Eje 3 · Componente B · Estándar 20/38 | Apoya la ejecución técnica homogénea por personal de competencia variable |
| Eje 4 · Componente B · Estándar 3/8 | Incorpora los rangos de referencia definidos institucionalmente |
| Eje 3 · Componente A · Estándar 12/31 *(Indispensable)* | Señala resultados que requieren escalamiento al químico responsable |

---

## Validación y autorización

Esta herramienta requiere revisión y autorización formal antes de su uso rutinario:

- [ ] Verificación del fundamento de cálculo por el Responsable del Servicio de Laboratorio Clínico
- [ ] Verificación de los umbrales de referencia contra el PT-LA-01 vigente
- [ ] Asignación de clave documental por el Departamento de Calidad y Seguridad del Paciente
- [ ] Autorización de uso por la Subdirección Médica
- [ ] Capacitación documentada del personal de los tres turnos
- [ ] Incorporación al listado maestro de documentos y herramientas controladas

---

## Aviso legal

© 2026 Q.F.B. Protacio Serna Ramírez. Todos los derechos reservados.

Herramienta desarrollada para uso interno del Departamento de Laboratorio Clínico del Hospital General Reynosa "Dr. José María Cantú Garza", Servicios de Salud IMSS-Bienestar.

No se autoriza su reproducción, modificación ni distribución sin consentimiento expreso del autor y de la institución.

El logotipo institucional del Hospital General Reynosa "Dr. José María Cantú Garza" y la identidad gráfica de Servicios de Salud IMSS-Bienestar son propiedad de sus respectivos titulares y se emplean con fines de identificación institucional.

Esta herramienta no constituye dispositivo médico ni software de diagnóstico. Es un auxiliar de cálculo aritmético cuyo resultado debe ser validado por profesional competente conforme a la NOM-007-SSA3-2011.

---

## Contacto

Departamento de Laboratorio Clínico · Hospital General Reynosa "Dr. José María Cantú Garza"
Boulevard Álvaro Obregón #425, Col. Presa la Laguna, C.P. 88758, Reynosa, Tamaulipas
