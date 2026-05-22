# LLM Service

## Responsabilidad
Todo lo relacionado con el LLM: RAG, memoria, Text-to-SQL, sentimiento y resumen diario.
No expone endpoints HTTP directos, el API Gateway actua de intermediario.

## Funcionalidades
- RAG con errores pasados: cuando was_correct=false en ml_signals, ese caso
  se embede con pgvector y se usa como contexto en futuras explicaciones
- Memoria de usuario: historial de conversaciones embebido en pgvector
- Text-to-SQL: el LLM traduce preguntas libres a SQL sobre nuestra DB
- Sentimiento: analiza noticias y posts de Reddit, devuelve score numerico
- Resumen diario: genera informe cada manana con lo que ha pasado en el mercado
- Cruce de noticias con senales: detecta contradicciones entre modelo y noticias

## LLM y embeddings
- LLM: Grok API via LangChain (gratuita)
- Embeddings: guardados en PostgreSQL con extension pgvector
- Fase 2: fine-tuning de Llama 3 con PEFT y LoRA

## Kafka
- Consumer: topic "signals" -> genera explicacion para cada senal nueva
- Consumer: topic "news" -> analiza sentimiento de cada noticia

## Base de datos - Tablas que gestiona
- llm_explanations
- rag_errors (embeddings pgvector de errores del modelo)
- user_memory (embeddings pgvector de conversaciones)

## Stack
- LangChain: framework principal para RAG y memoria
- Grok API: LLM gratuito
- pgvector: extension PostgreSQL para embeddings
- SQLAlchemy: ORM para PostgreSQL
- kafka-python: consumer de senales y noticias

## Estructura de carpetas esperada
llm-service/
  src/
    rag/
      error_memory.py
      user_memory.py
      retriever.py
    chains/
      signal_explainer.py
      sentiment_analyzer.py
      text_to_sql.py
      daily_summary.py
    kafka/
      consumer.py
    db/
      models.py
      session.py
  main.py
  requirements.txt
  Dockerfile
  .env.example

## Variables de entorno necesarias
- GROK_API_KEY
- DATABASE_URL
- KAFKA_BOOTSTRAP_SERVERS
- EMBEDDING_MODEL
