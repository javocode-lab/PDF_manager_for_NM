# Organizador PDF por entidad, paciente y prefijo profesional — v0.6.0

Esta versión organiza PDFs de informes usando una tabla de pacientes y una tabla maestra de profesionales.

## Idea principal

- El PDF se usa para detectar el código de paciente y el profesional que firmó/cargó el informe.
- `Listado_Pacientes.xlsx` se usa como respaldo para obtener paciente y entidad.
- `Listado_profesionales.xlsx` es la fuente de verdad para el prefijo profesional final.
- La app NO intenta adivinar automáticamente si una kinesiología es motora, respiratoria o neurokinesiología cuando el PDF solo dice una especialidad genérica.

## Archivos necesarios

En la misma carpeta de la app colocá:

```txt
organizador_pdf_por_entidad_y_prefijo.py
requirements.txt
Archivos_PDF.zip
Listado_Pacientes.xlsx
Listado_profesionales.xlsx
```

## Instalación

```powershell
py -m pip install -r requirements.txt
```

Si `py` no funciona:

```powershell
python -m pip install -r requirements.txt
```

## Comando recomendado

```powershell
py organizador_pdf_por_entidad_y_prefijo.py --input-zip "Archivos_PDF.zip" --patients-file "Listado_Pacientes.xlsx" --professionals-file "Listado_profesionales.xlsx" --output-dir "salida_organizada"
```

## Compatibilidad con TXT

También acepta los argumentos anteriores:

```powershell
py organizador_pdf_por_entidad_y_prefijo.py --input-zip "Archivos_PDF.zip" --data-txt "datos.txt" --prof-txt "prof.txt" --output-dir "salida_organizada"
```

## Resultado

La salida queda así:

```txt
salida_organizada/
    ENTIDAD/
        APELLIDO, NOMBRE/
            PREFIJO - HC_Profesional_20265_Paciente_XXXXX_HC_Nro_YYYYYYY.pdf
```

Ejemplo:

```txt
salida_organizada/
    TCPRESALUD/
        BUSTOS GIRAUDO, AMADEO/
            MED - HC_Profesional_20265_Paciente_37176_HC_Nro_1186128.pdf
```

## Reportes generados

Dentro de `salida_organizada` se generan:

```txt
reporte_organizacion.txt
reporte_organizacion.csv
profesionales_detectados.csv
archivos_sin_prefijo.csv
debug_headers_sin_prefijo.txt
```

El archivo más importante para mejorar la tabla maestra es:

```txt
archivos_sin_prefijo.csv
```

Allí aparecen los PDFs donde la app no pudo encontrar el profesional en `Listado_profesionales.xlsx`.
