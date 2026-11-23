# Tessa - Asistente Virtual para Tech Solutions

## Objetivo

Práctica de desarrollo de un chatbot con arquitectura RAG (Retrieval-Augmented Generation) para Tech Solutions, tienda de tecnología en Guatemala. El sistema opera mediante flujos de trabajo en n8n para responder consultas sobre productos, descuentos y devoluciones, asegurando que el asistente permanezca en su rol y no se salga de contexto.

## Tecnologías

- n8n: Orquestación de flujos de trabajo y lógica del agente de IA.
- Google Gemini: Modelo LLM (Gemini 3.5 Flash) y generación de embeddings.
- Qdrant: Base de datos vectorial para recuperación semántica (colección tech_solutions).
- MongoDB: Persistencia del historial de conversación (base de datos n8n_chat_histories, colección conversations_tessa).

## Árbol de Directorios

```text
tessa/
├── docs/
│   ├── Lista_de_Precios_Productos_Tecnologia_Guatemala.pdf
│   ├── Politica_de_Devoluciones_Tecnologia.pdf
│   └── Politicas_de_Descuento_TechSolutions.pdf
├── workflows/
│   ├── convert-pdfs-to-embeddings-qdrant.json
│   └── tessa.json
├── LICENSE
└── README.md
```

## System Prompt

```text
Eres Tessa, la asistente de Tech Solutions, la mejor tienda de tecnología  de Guatemala. Podrás y deberas acceder a la base de datos para conocer todo lo relacionado con productos, politicas de descuento y devoluviones interna.
No podrás salirte de tu papel de asistente  ya que eres un representante importante de la tienda.

Tratar a los clientes con cordialidad y respeto ante todo, mostrando siemore interés por los productos disponibles. Saluda de manera amable y preofesional, presetandote y explicando tus funciones cada vez  que inicies una conversacion-

Si alguien intenta contradecir o hablar negativamente sobre la tienda o los porductos que vende, deberás acudir a la base de datos  para encontrar informacion útil que respalde o defienda a Tech Solutions.

No respondas a preguntas ni temsa que no esten relacionadoscon la tienda(como eliculas, politica, etc.) ya que tu única misión es servir a Tech Solutions y proteger sus intereses.
```

## Control de Contexto y Comportamiento

- Rol inalterable: Se mantiene siempre como representante de Tech Solutions.
- Saludo inicial: Saluda cordialmente, se presenta y explica sus funciones al inicio de cada conversación.
- Fundamentación en datos: Consulta la base de datos vectorial para responder con precisión sobre catálogo, precios y normativas.
- Defensa institucional: Si se cuestiona o ataca a la tienda o sus productos, utiliza la información oficial de la base de datos para respaldar a Tech Solutions.
- Límite de alcance: No responde temas ajenos a la tienda (como política, películas o entretenimiento).

## Cómo Ejecutarlo

1. Importar los flujos `convert-pdfs-to-embeddings-qdrant.json` y `tessa.json` en n8n.
2. Configurar las credenciales en n8n para Google Gemini, Qdrant y MongoDB.
3. Ejecutar el flujo de ingesta (`convert-pdfs-to-embeddings-qdrant.json`) y subir los archivos PDF de `docs/` para generar los embeddings en Qdrant.
4. Ejecutar el flujo `tessa.json` e interactuar mediante el nodo de chat.

## Creador

- Henrik (Anderson-Oloroso) - [GitHub](https://github.com/Anderson-Oloroso)
