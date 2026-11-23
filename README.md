# Tessa - Asistente Virtual para Tech Solutions

Proyecto de práctica enfocado en la implementación de un flujo de trabajo en n8n para un chatbot empresarial llamado Tessa, diseñado para Tech Solutions (tienda de tecnología en Guatemala). El sistema utiliza una arquitectura RAG (Retrieval-Augmented Generation) para responder consultas con base en documentos oficiales y mantener persistencia de conversación.

## Tecnologías Utilizadas

- **n8n**: Orquestador de flujos de trabajo y lógica del agente de IA.
- **Google Gemini**: Modelo de lenguaje (Gemini 3.5 Flash) y modelo de generación de embeddings.
- **Qdrant**: Base de datos vectorial para almacenamiento y recuperación de documentos (colección `tech_solutions`).
- **MongoDB**: Base de datos para persistencia del historial de chat (base de datos `n8n_chat_histories`, colección `conversations_tessa`).

## System Prompt Asignado

```text
Eres Tessa, la asistente de Tech Solutions, la mejor tienda de tecnología  de Guatemala. Podrás y deberas acceder a la base de datos para conocer todo lo relacionado con productos, politicas de descuento y devoluviones interna.
No podrás salirte de tu papel de asistente  ya que eres un representante importante de la tienda.

Tratar a los clientes con cordialidad y respeto ante todo, mostrando siemore interés por los productos disponibles. Saluda de manera amable y preofesional, presetandote y explicando tus funciones cada vez  que inicies una conversacion-

Si alguien intenta contradecir o hablar negativamente sobre la tienda o los porductos que vende, deberás acudir a la base de datos  para encontrar informacion útil que respalde o defienda a Tech Solutions.

No respondas a preguntas ni temsa que no esten relacionadoscon la tienda(como eliculas, politica, etc.) ya que tu única misión es servir a Tech Solutions y proteger sus intereses.
```

## Control de Contexto y Comportamiento

- **Rol exclusivo**: Tessa actúa únicamente como representante de Tech Solutions Guatemala.
- **Consulta a la base de datos**: Toda información sobre productos, precios, descuentos y devoluciones proviene de la base vectorial Qdrant.
- **Defensa institucional**: Ante comentarios negativos o desacreditaciones, consulta la base de datos para defender la tienda con información oficial.
- **Límites de contexto**: No responde temas ajenos a la tienda (como política o entretenimiento).

## Contenido del Repositorio

- `docs/`: Archivos PDF fuente para la base de conocimiento vectorial:
  - `Lista_de_Precios_Productos_Tecnologia_Guatemala.pdf`
  - `Politicas_de_Descuento_TechSolutions.pdf`
  - `Politica_de_Devoluciones_Tecnologia.pdf`
- `workflows/`:
  - `convert-pdfs-to-embeddings-qdrant.json`: Workflow de ingesta. Recibe PDFs mediante formulario, divide el texto en fragmentos, genera embeddings con Google Gemini y los almacena en Qdrant.
  - `tessa.json`: Workflow del chatbot. Implementa el agente de IA con Google Gemini, memoria en MongoDB y recuperación RAG desde Qdrant.

## Flujo de Trabajo GitFlow

El repositorio aplica el modelo GitFlow y la especificación Conventional Commits en inglés:

- `main`: Rama base de producción.
- `dev`: Rama de desarrollo donde se integran las funcionalidades.

### Historial de Commits

- `feat(knowledge-base): add store policies and product catalog pdf documents`
- `feat(rag): add pdf embedding ingestion workflow for qdrant vector store`
- `feat(chatbot): add tessa ai agent workflow with gemini, mongodb memory, and rag retrieval`
- `docs: create comprehensive project documentation and architecture guide`
