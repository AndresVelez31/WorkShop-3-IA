<div align="center">
 
  <h1>📄 Workshop 3 - Inteligencia Artificial</h1>
  <h3>Asistente de Documentos con Gemini y Gradio</h3>

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)
![Gradio](https://img.shields.io/badge/Gradio-UI-ff4b4b.svg)
![Gemini](https://img.shields.io/badge/Gemini-API-4285F4.svg)

</div>

---

## 👥 Información del Equipo

| Nombre | Código |
|--------|--------|
| **Andres Felipe Velez Alvarez** | 1021923619 |
| **Nathalia Valentina Cardoza Azuaje** | 4992531 |
| **Sebastian Salazar Henao** | 1022003377 |

**Universidad:** Universidad EAFIT  
**Curso:** Inteligencia Artificial  
**Semestre:** 5to Semestre  
**Fecha:** Abril 24, 2026

---

## 📋 Descripción del Proyecto

Este repositorio implementa un asistente conversacional que responde preguntas basadas únicamente en un PDF (Attention is All You Need), usando:

- Extracción de texto con `pypdf`
- Generación con Gemini (`google-genai`)
- Interfaz web con `gradio`

El proyecto demuestra el patrón base de inyección de contexto y su evolución hacia una aproximación tipo RAG.

---

## 🎯 Objetivos del Workshop

-  Extraer texto de un documento PDF en Python
-  Construir prompts con contexto documental
-  Restringir respuestas al contenido del documento
-  Implementar una interfaz de chat en Gradio
-  Identificar limitaciones de escalabilidad del enfoque
-  Aplicar mejoras: subida dinámica de PDF, conteo de tokens y citas

---

## 📂 Estructura del Proyecto

```text
WorkShop-3-IA/
│
├── 05_ejercicio.ipynb              # Notebook principal del ejercicio
├── attention_is_all_you_need.pdf   # Documento base (entrada)
├── .env                            # Variables de entorno (API key)
└── README.md                       # Este archivo
```

---

## 🧠 Arquitectura de la Solución

### Flujo base
1. Cargar PDF
2. Extraer texto completo
3. Construir `system prompt` con reglas
4. Enviar historial + pregunta a Gemini
5. Mostrar respuesta en streaming con Gradio

---

## 🧪 Funcionalidades Implementadas

###  Versión inicial (pasos 1–5)
- Lectura del PDF local `attention_is_all_you_need.pdf`
- Chat restringido al documento
- Interfaz `gr.ChatInterface`
- Preguntas de prueba (incluyendo pregunta trampa: “¿Qué es GPT-4?”)

###  Mejoras (Paso 6)
- A) Indicador de tokens del prompt
- B) Subida dinámica de PDF con `gr.File(type="filepath")`
- C) Citas obligatorias del documento en cada respuesta

---

## 🛠️ Tecnologías Utilizadas

| Tecnología | Uso |
|------------|-----|
| Python | Lenguaje principal |
| Jupyter Notebook | Desarrollo interactivo |
| pypdf | Extracción de texto PDF |
| google-genai | Llamadas al modelo Gemini |
| gradio | Interfaz web conversacional |
| python-dotenv | Carga segura de API keys |

---

## 📦 Dependencias

```bash
pip install pypdf gradio google-genai python-dotenv
```

---

## 🚀 Instalación y Ejecución (macOS / VS Code)

### 1) Crear y activar entorno virtual
```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 2) Instalar librerías
```bash
pip install -U pip
pip install pypdf gradio google-genai python-dotenv
```

### 3) Configurar credenciales
Crear `.env` en la raíz del proyecto:
```env
GEMINI_API_KEY="tu_api_key_aqui"
```

### 4) Abrir notebook
```bash
jupyter notebook 05_ejercicio.ipynb
```
o ejecutarlo desde VS Code.

### 5) Lanzar interfaz
El notebook lanza Gradio en:
- `http://0.0.0.0:8080`
- Usar `http://localhost:8080` en navegador local

---

## 📌 Modelo utilizado

En el notebook se define:
- `MODELO = "gemini-2.5-flash-lite"`

---

## ⚠️ Limitaciones del Enfoque

- Alto costo y latencia al inyectar documentos grandes
- Límite de contexto del modelo
- Mayor ruido al incluir “todo” el texto
- Riesgo de respuestas desde conocimiento paramétrico si no se audita evidencia

Esto justifica migrar a una arquitectura RAG para producción.

---

## 🎓 Aprendizajes Clave

- Separar búsqueda de información y generación mejora escalabilidad
- Exigir evidencia/citas aumenta trazabilidad
- Preguntas de control validan fidelidad al documento
- Subida dinámica de documentos mejora usabilidad real del asistente
