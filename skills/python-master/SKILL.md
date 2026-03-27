---
name: python-master
description: Expert Python development guidance for scripting, automation, data processing, web development, and software engineering. Use for Python best practices, debugging, optimization, and code review.
license: Complete terms in LICENSE.txt
---

# Python Master Guide

You are a Python expert providing guidance on best practices, debugging, optimization, and code quality.

## Core Capabilities

### 1. Code Development
- Clean, Pythonic code
- Type hints and annotations
- Error handling
- Testing strategies

### 2. Performance Optimization
- Profiling and benchmarking
- Memory optimization
- Async programming
- C extensions

### 3. Web Development
- FastAPI, Flask, Django
- API design
- Database integration
- Authentication

### 4. Data Processing
- pandas, numpy
- Data pipelines
- ETL processes
- Visualization

---

## Python Best Practices

### Code Style (PEP 8)

```python
# ✅ Good
def calculate_total(items, tax_rate):
    """Calculate total with tax.
    
    Args:
        items: List of item prices
        tax_rate: Tax rate as decimal
    
    Returns:
        Total amount including tax
    """
    subtotal = sum(items)
    return subtotal * (1 + tax_rate)

# ❌ Bad
def calc(l,r):
    s=sum(l)
    return s*(1+r)
```

### Type Hints

```python
from typing import List, Dict, Optional, Union, Callable

def process_users(
    users: List[Dict[str, str]],
    filter_func: Optional[Callable[[Dict], bool]] = None
) -> Dict[str, List[Dict]]:
    """Process users with optional filter."""
    
    if filter_func:
        filtered = [u for u in users if filter_func(u)]
    else:
        filtered = users
    
    return {"processed": filtered}
```

### Error Handling

```python
# ✅ Good: Specific exceptions
def read_config(path: str) -> dict:
    try:
        with open(path, 'r') as f:
            return json.load(f)
    except FileNotFoundError:
        logger.error(f"Config not found: {path}")
        return {}
    except json.JSONDecodeError as e:
        logger.error(f"Invalid JSON: {e}")
        raise ConfigError(f"Invalid config file: {e}")

# ❌ Bad: Catch all
def read_config(path):
    try:
        with open(path) as f:
            return json.load(f)
    except:
        return {}
```

### Context Managers

```python
from contextlib import contextmanager

@contextmanager
def database_connection(conn_string):
    conn = create_connection(conn_string)
    try:
        yield conn
        conn.commit()
    except Exception:
        conn.rollback()
        raise
    finally:
        conn.close()

# Usage
with database_connection(conn_string) as conn:
    cursor = conn.cursor()
    cursor.execute(query)
```

---

## Performance Optimization

### Profiling

```python
import cProfile
import pstats
from pstats import SortKey

def profile_function(func, *args):
    profiler = cProfile.Profile()
    profiler.enable()
    
    result = func(*args)
    
    profiler.disable()
    stats = pstats.Stats(profiler).sort_stats(SortKey.TIME)
    stats.print_stats(10)
    
    return result
```

### Memory Optimization

```python
# ✅ Good: Generator for large datasets
def process_large_file(path):
    with open(path) as f:
        for line in f:
            yield process_line(line)

# ❌ Bad: Load all into memory
def process_large_file(path):
    with open(path) as f:
        lines = f.readlines()
    return [process_line(l) for l in lines]

# Use __slots__ for many instances
class Point:
    __slots__ = ['x', 'y']
    def __init__(self, x, y):
        self.x = x
        self.y = y
```

### Async Programming

```python
import asyncio
import aiohttp

async def fetch_all(urls):
    async with aiohttp.ClientSession() as session:
        tasks = [fetch(session, url) for url in urls]
        return await asyncio.gather(*tasks)

async def fetch(session, url):
    async with session.get(url) as response:
        return await response.text()

# Run
results = asyncio.run(fetch_all(urls))
```

---

## Common Patterns

### Singleton Pattern

```python
class Singleton:
    _instance = None
    
    def __new__(cls):
        if cls._instance is None:
            cls._instance = super().__new__(cls)
        return cls._instance
```

### Factory Pattern

```python
from enum import Enum

class DatabaseType(Enum):
    POSTGRES = "postgres"
    MYSQL = "mysql"
    SQLITE = "sqlite"

class DatabaseFactory:
    @staticmethod
    def create(db_type: DatabaseType, **kwargs):
        if db_type == DatabaseType.POSTGRES:
            return PostgresDB(**kwargs)
        elif db_type == DatabaseType.MYSQL:
            return MySQLDB(**kwargs)
        elif db_type == DatabaseType.SQLITE:
            return SQLiteDatabase(**kwargs)
        raise ValueError(f"Unknown database type: {db_type}")
```

### Decorator Pattern

```python
from functools import wraps
import time

def timing(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f"{func.__name__} took {end - start:.2f}s")
        return result
    return wrapper

@timing
def slow_function():
    time.sleep(1)
```

---

## Testing

### pytest Examples

```python
import pytest

def test_addition():
    assert 1 + 1 == 2

@pytest.fixture
def sample_data():
    return {"key": "value"}

def test_with_fixture(sample_data):
    assert sample_data["key"] == "value"

@pytest.mark.parametrize("input,expected", [
    (1, 2),
    (2, 4),
    (3, 6),
])
def test_multiply(input, expected):
    assert input * 2 == expected
```

### Mocking

```python
from unittest.mock import patch, MagicMock

@patch('module.external_api')
def test_with_mock(mock_api):
    mock_api.get.return_value = {"status": "success"}
    
    result = module.call_api()
    
    assert result == {"status": "success"}
    mock_api.get.assert_called_once()
```

---

## Usage Examples

```
"Use python-master skill to review this code for best practices"
"Use python-master skill to optimize this slow function"
"Use python-master skill to add type hints to this module"
"Use python-master skill to create pytest tests"
"Use python-master skill to debug this memory leak"
```
