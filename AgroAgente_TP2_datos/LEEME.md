# AgroAgente — datos del TP2

Carpeta de datos del agente de consultas fitosanitarias (maíz, soja, trigo y maní). La notebook
`AgroAgente_TP2_Colab.ipynb` la lee desde `Mi unidad/AgroAgente_TP2_datos`.

## Aclaración importante: no hay entrenamiento

El agente **no entrena ni ajusta (fine-tuning) ningún modelo**. Usa un LLM ya entrenado
(`Qwen/Qwen2.5-7B-Instruct`, vía Hugging Face Router, como en `17_Agentes` de la cátedra) y lo conecta
a herramientas. Los datos de esta carpeta son:

1. **Base de conocimiento (RAG)** que el agente consulta en cada pregunta (`corpus/`).
2. **Datos de evaluación** para medir la búsqueda y las respuestas del agente (`evaluacion/`).

Lo único que se "construye" a partir de los datos es un **índice de búsqueda BM25**, que la notebook arma
en segundos cada vez que corre.

## Contenido

| Ruta | Qué es | Origen |
|---|---|---|
| `corpus/sinavimo/*.md` (70) | Fichas oficiales de plagas, enfermedades y malezas: nombres, condición en Argentina, cultivos afectados, biología, síntomas, condiciones predisponentes y bibliografía | SINAVIMO – SENASA, https://www.sinavimo.gob.ar (descargadas el 2026-10-25) |
| `corpus/chicharrita/*.md` (10) | Texto de los informes N° 42 a 50 y 52 de la Red Nacional de Monitoreo de *Dalbulus maidis* (22/05/2026 a 20/10/2026) | MAIZAR / INTA, https://www.maizar.org.ar/vertodas_area.php?id=39 |
| `corpus/chicharrita/pdf/*.pdf` | Los PDF originales de esos informes | ídem |
| `plagas_objetivo.csv` | Las 70 plagas elegidas, con cultivo, grupo, prioridad y nombres usados en Argentina | Elaboración propia |
| `catalogo_plagas.csv` | Catálogo resumido de las 70 fichas (nombres vulgares, tipo, condición, URL) | Generado de las fichas |
| `evaluacion/preguntas_manual.jsonl` | 30 preguntas escritas a mano: síntomas sin nombrar la plaga, temporales y guardrails, con la ficha esperada | Elaboración propia |
| `evaluacion/preguntas_auto.jsonl` | 262 preguntas generadas desde las fichas, con la ficha y sección de referencia | Generado de las fichas |
| `evaluacion/juez_prompt.md` | Prompt de LLM-como-juez (fidelidad y tasa de respuesta) | Elaboración propia |
| `evaluacion/resultados_baseline_extractivo.jsonl` | Respuestas del baseline sin LLM (piso de comparación) | Generado |
| `resultados/` | La notebook guarda acá los resultados de cada evaluación que se corre | Generado por la notebook |

Datos que se consultan en vivo (no se guardan): pronóstico de Open-Meteo (CC BY 4.0) y tesauro AGROVOC (FAO).

## Formato de una ficha

Markdown con un encabezado YAML (`slug`, `titulo`, `nombres_vulgares`, `tipo_plaga`, `condicion`,
`cultivos_tp`, `url`, `fecha_descarga`) y una sección `## ...` por campo de la ficha original.

## Licencia y uso

Información oficial de acceso libre de SENASA y de la Red Nacional de Monitoreo, usada con fines académicos
y citando siempre la fuente original. Generado el 2026-10-27.
