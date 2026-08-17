# Deployment Guide

## Docker Setup
```dockerfile
FROM python:3.11-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
EXPOSE 8000
CMD ["uvicorn", "api:app", "--host", "0.0.0.0", "--port", "8000"]
```

## API Endpoint
```python
from fastapi import FastAPI, UploadFile
app = FastAPI()

@app.post("/solve")
async def solve_sudoku(image: UploadFile):
    contents = await image.read()
    # Process image -> extract grid -> solve
    return {"solution": solved_grid, "confidence": 0.95}
```

## Quick Start
```bash
docker build -t sudoku-solver .
docker run -p 8000:8000 sudoku-solver
# Visit http://localhost:8000/docs for API docs
```

## Cloud Deployment
- **Railway**: One-click deploy with Dockerfile
- **Render**: Free tier with auto-deploy from GitHub
- **AWS Lambda**: Serverless with container image
