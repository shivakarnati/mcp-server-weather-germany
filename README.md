# Weather MCP Tool

## Overview

The **Weather** project is a lightweight [MCP](https://github.com/hackthebox/mcp)‑based service that exposes weather data for the United States and will be extended to support Germany.  It communicates over **stdin/stdout** using simple JSON messages and can be used from the command line, scripts, or as an RPC service inside a larger system.

| Feature                     | Description |
|-----------------------------|-------------|
| `get_alerts(state)`         | Retrieve active NOAA Weather Alerts for a US state (e.g. `CA`). |
| `get_forecast(lat,long)` | Get a 5‑period weather forecast for a geographic coordinate. |
| Future                       | A dedicated `/weather/germany` endpoint backed by the German Meteorological Service (DWD). |

The code follows the OpenSpec workflow – design, tasks, and specs are stored under `openspec/changes/`.  When a new feature is finished a change is **archived** and the main specs are updated.

## Prerequisites

* Python 3.14 or newer (the project requires the `typing` `Literal` and `defint` syntax which was stabilized in 3.14).
* `uv` – Python build tool.  Install via:
  ```bash
  pip install uv
  ```

## Installation

```bash
# Clone the repository
git clone https://github.com/your-org/weather.git
cd weather

# Create a transient environment with uv
uv sync

# Install the tool globally (optional)
uv pip install --editable .
```

After installation you can invoke the command line wrapper using `weather`.

## Usage

The MCP server can be started with:

```bash
uv run weather
```

The server is ready to accept JSON requests on `stdin` and writes the result to `stdout`.  The following examples show how to call the two built‑in tools.

### 1. Get alerts for California

```bash
printf '{"tool": "get_alerts", "args": ["CA"]}' | uv run weather
```

The output will be plain text that lists all active alerts for the state.

### 2. Get forecast for a coordinate

```bash
printf '{"tool": "get_forecast", "args": [37.7749, -122.4194]}' | uv run weather
```

You can also run the server as a daemon and communicate with it over a socket.  Refer to the [MCP documentation](https://github.com/hackthebox/mcp) for a full description of transports and protocol.

## Development

### Running Tests

The project currently ships with no tests, but you can easily add `pytest` or similar tools.  Example:

```bash
uv run pytest
```

### Contributing

All changes are managed through the OpenSpec change‑driven workflow.  When you create a new feature:

1. Create a change directory under `openspec/changes/` (e.g. `add-germany-weather`).
2. Follow the conventions for design, tasks, and specs.
3. Use the OpenSpec CLI tools (`openspec apply`, `openspec archive`, etc.) to move the change and publish the artifacts.

The `proposal.md`, `design.md`, `tasks.md`, and `spec.md` files inside a change directory should be as complete as possible to keep reviewers on the same page.

### Packaging

Build a distributable wheel with:

```bash
uv wheel . --wheel-dir dist
```

To install from a wheel:

```bash
pip install dist/weather-0.1.0-py3-none-any.whl
```

## License

This project is released under the MIT License.

---

**Note:** This README was generated as part of the repository scaffolding.  Feel free to adapt it further to match your project's conventions or add more details about the upcoming Germany endpoint map.
