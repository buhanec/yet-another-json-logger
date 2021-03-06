# yet-another-json-logger [<img src="https://img.shields.io/gitlab/pipeline/alen/yet-another-json-logger/main?gitlab_url=https%3A%2F%2Fgitlab.home.alen.sh%2F&label=Gitlab%20CI&style=flat-square" align="right">](https://gitlab.home.alen.sh/alen/yet-another-json-logger) [<img src="https://img.shields.io/travis/buhanec/yet-another-json-logger/main.svg?label=Travis+CI&style=flat-square" align="right">](https://travis-ci.org/buhanec/yet-another-json-logger) [<img src="https://img.shields.io/azure-devops/build/buhanec/13746f63-b2e8-498b-a4f4-86a3207cfa78/5/main?label=Azure%20DevOps&style=flat-square" align="right">](https://dev.azure.com/buhanec/yet-another-json-logger/_build)

Yet another JSON logger.

Complete with opinionated decisions and hardcoded personal preferences.

## Installation

```json
pip install yet-another-json-logger
```

## Usage

```python
import logging

from yajl import JsonFormatter

json_handler = logging.FileHandler('log.json')
json_handler.setFormatter(JsonFormatter())

logger = logging.getLogger(__name__)
logger.addHandler(json_handler)
logger.setLevel(logging.INFO)

logger.info('Alice says %r', 'hi!')
try:
    1 / 0
except ZeroDivisionError:
    logger.exception('Bob divided by zero!')
```

Will result in `log.json` containing:

```json
{"hostname": "alen-dev-vm", "pwd": "/mnt/alen/dev/yet-another-json-logger", "user": "alen", "name": "__main__", "module": "test", "level": {"name": "INFO", "number": 20}, "file": {"path": "/mnt/alen/dev/yet-another-json-logger/test.py", "filename": "test.py", "line": 12, "func": "<module>"}, "timestamp": {"abs": 1618609778.928479, "rel": 839.9991989135742}, "proc": {"id": 36424, "name": "MainProcess"}, "thread": {"id": 24544, "name": "MainThread"}, "message": "Alice says 'hi!'"}
{"hostname": "alen-dev-vm", "pwd": "/mnt/alen/dev/yet-another-json-logger", "user": "alen", "name": "__main__", "module": "test", "level": {"name": "ERROR", "number": 40}, "file": {"path": "/mnt/alen/dev/yet-another-json-logger/test.py", "filename": "test.py", "line": 16, "func": "<module>"}, "timestamp": {"abs": 1618609778.928479, "rel": 839.9991989135742}, "proc": {"id": 36424, "name": "MainProcess"}, "thread": {"id": 24544, "name": "MainThread"}, "message": "Bob divided by zero!\nTraceback (most recent call last):\n  File \"/mnt/alen/dev/yet-another-json-logger/test.py\", line 14, in <module>\n    1 / 0\nZeroDivisionError: division by zero", "exception": {"type": "builtins.ZeroDivisionError", "str": "division by zero", "traceback": "  File \"/mnt/alen/dev/yet-another-json-logger/test.py\", line 14, in <module>\n    1 / 0\n"}}
```

or, if prettified:

```json
{
   "hostname": "alen-dev-vm",
   "pwd": "/mnt/alen/dev/yet-another-json-logger",
   "user": "alen",
   "name": "__main__",
   "module": "test",
   "level": {
      "name": "INFO",
      "number": 20
   },
   "file": {
      "path": "/mnt/alen/dev/yet-another-json-logger/test.py",
      "filename": "test.py",
      "line": 12,
      "func": "<module>"
   },
   "timestamp": {
      "abs": 1618609778.928479,
      "rel": 839.9991989135742
   },
   "proc": {
      "id": 36424,
      "name": "MainProcess"
   },
   "thread": {
      "id": 24544,
      "name": "MainThread"
   },
   "message": "Alice says 'hi!'"
}
```
```json
{
   "hostname": "alen-dev-vm",
   "pwd": "/mnt/alen/dev/yet-another-json-logger",
   "user": "alen",
   "name": "__main__",
   "module": "test",
   "level": {
      "name": "ERROR",
      "number": 40
   },
   "file": {
      "path": "/mnt/alen/dev/yet-another-json-logger/test.py",
      "filename": "test.py",
      "line": 16,
      "func": "<module>"
   },
   "timestamp": {
      "abs": 1618609778.928479,
      "rel": 839.9991989135742
   },
   "proc": {
      "id": 36424,
      "name": "MainProcess"
   },
   "thread": {
      "id": 24544,
      "name": "MainThread"
   },
   "message": "Bob divided by zero!\nTraceback (most recent call last):\n  File \"/mnt/alen/dev/yet-another-json-logger/test.py\", line 14, in <module>\n    1 / 0\nZeroDivisionError: division by zero",
   "exception": {
      "type": "builtins.ZeroDivisionError",
      "str": "division by zero",
      "traceback": "  File \"/mnt/alen/dev/yet-another-json-logger/test.py\", line 14, in <module>\n    1 / 0\n"
   }
}
```
