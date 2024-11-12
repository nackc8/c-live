### Exempel 1: Använda `pytest` Utan Mocking
Detta exempel testar en enkel funktion som adderar två tal.

**Funktion att testa (`math_utils.py`)**
```python
def add_numbers(a, b):
    return a + b
```

**Testfil (`test_math_utils.py`)**
```python
import pytest
from math_utils import add_numbers

def test_add_numbers():
    result = add_numbers(3, 5)
    assert result == 8  # Förväntat resultat
```

**Så kör du testet**
```bash
pytest test_math_utils.py
```

### Exempel 2: Använda `pytest` Med Mocking
Detta exempel testar en funktion som hämtar data från ett externt API. Vi använder `unittest.mock` för att mocka beteendet hos biblioteket `requests`.

**Funktion att testa (`data_fetcher.py`)**
```python
import requests

def fetch_data(url):
    response = requests.get(url)
    if response.status_code == 200:
        return response.json()
    else:
        return None
```

**Testfil (`test_data_fetcher.py`)**
```python
import pytest
from unittest.mock import patch
from data_fetcher import fetch_data

@patch('data_fetcher.requests.get')
def test_fetch_data_success(mock_get):
    # Mocka svaret från requests.get
    mock_get.return_value.status_code = 200
    mock_get.return_value.json.return_value = {'key': 'value'}

    result = fetch_data('http://example.com/api')
    assert result == {'key': 'value'}

@patch('data_fetcher.requests.get')
def test_fetch_data_failure(mock_get):
    # Mocka svaret från requests.get för att simulera ett fel
    mock_get.return_value.status_code = 404

    result = fetch_data('http://example.com/api')
    assert result is None
```

**Förklaring**
- `@patch('data_fetcher.requests.get')`: Denna dekoratör ersätter `requests.get` i modulen `data_fetcher` med ett mock-objekt under testets gång.
- `mock_get.return_value.status_code = 200`: Anger returvärdet för `status_code`.
- `mock_get.return_value.json.return_value = {'key': 'value'}`: Anger returvärdet för `response.json()` när det anropas.

**Så kör du testet**
```bash
pytest test_data_fetcher.py
```
