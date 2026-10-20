# ATS12 — Integração Contínua com GitHub Actions

Pipeline de CI com GitHub Actions para uma API FastAPI: testa a soma e a multiplicação com pytest e confere, no runner, se a API sobe e responde.

O enunciado está em [assets/Exercício ATS12.pdf](assets/Exercício%20ATS12.pdf).

## Ambiente

Lembrando..

```bash
python -m venv .venv
```

No Linux/macOS:

```bash
source .venv/bin/activate
```

No Windows:

```bash
.venv\Scripts\activate
```

```bash
pip install -r requirements.txt
```

## Execução

Na raiz do projeto, com o ambiente ativo:

```bash
pytest test_main.py -v
```

Para subir a API na máquina local:

```bash
fastapi run main.py --port 8000
```

O workflow em `.github/workflows/ci.yml` roda no GitHub a cada push e a cada pull request. O job exigido na proteção da branch `main` é `verificar-api`.

## O que a atividade faz

1. Expõe `GET /`, `GET /somar/{a}/{b}` e `GET /multiplicar/{a}/{b}`.
2. A soma devolve `a + b` e a multiplicação devolve `a * b`, no campo `resultado`.
3. O job `verificar-api` roda o pytest em Python 3.10, 3.11 e 3.12.
4. Depois dos testes, sobe a API na porta 8000 e chama `/` e `/somar/10/20` com curl.

## Saída esperada

O pytest termina verde. `GET /somar/2/3` devolve `{"resultado": 5}` e `GET /multiplicar/2/2` devolve `{"resultado": 4}`.

No Actions, o job `verificar-api` fica verde nas três versões do Python. O curl de `/somar/10/20` recebe `{"resultado": 30}`.

## Autor

**Ryan Rodrigues Cordeiro**
