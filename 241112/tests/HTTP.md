import requests
import pytest

def test_real_request():
    response = requests.get('https://example.com/api')
    assert response.status_code == 200
    assert 'expected_key' in response.json()
