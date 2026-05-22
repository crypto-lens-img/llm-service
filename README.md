# 🧠 LLM Service

Microservicio de inteligencia artificial para CryptoLens. Gestiona el RAG, memoria de usuario, análisis de sentimiento y generación de resúmenes diarios.

## Responsabilidad

Convierte datos crudos del mercado en explicaciones comprensibles. Aprende de los errores pasados del modelo ML para mejorar sus explicaciones con el tiempo.

## Funcionalidades

| Funcionalidad | Descripción |
|---|---|
| RAG con errores | Usa errores pasados del modelo como contexto para futuras explicaciones |
| Memoria de usuario | Recuerda preferencias e historial de conversaciones |
| Text-to-SQL | Traduce preguntas en lenguaje natural a consultas sobre la DB |
| Análisis de sentimiento | Puntúa noticias y posts de Reddit numéricamente |
| Resumen diario | Genera un informe automático cada mañana |
| Cruce de señales | Detecta contradicciones entre el modelo y las noticias |

## Stack

- `LangChain` — framework principal para RAG y memoria
- `Grok API` — LLM gratuito
- `pgvector` — embeddings en PostgreSQL
- `kafka-python` — consumer de señales y noticias

## Kafka

```
Consumer: signals → genera explicación por cada señal nueva
Consumer: news    → analiza sentimiento de cada noticia
```

## Fase 2 — LoRA Fine-tuning

Fine-tuning de Llama 3 con PEFT y LoRA usando datos acumulados de la plataforma para especializar el modelo en análisis crypto.

## Configuración

```bash
cp .env.example .env
docker compose up llm-service
```

## Parte de CryptoLens

[crypto-lens-img](https://github.com/crypto-lens-img) · [data-pipeline](https://github.com/crypto-lens-img/data-pipeline) · [ml-engine](https://github.com/crypto-lens-img/ml-engine) · [api-gateway](https://github.com/crypto-lens-img/api-gateway)
