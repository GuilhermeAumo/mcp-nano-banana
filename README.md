# MCP Nano Banana

[![PyPI Version](https://img.shields.io/pypi/v/mcp-nano-banana.svg)](https://pypi.org/project/mcp-nano-banana/)

This project is an MCP (Model Context Protocol) server that generates images using the Google Gemini API.

## Description

This server implements the Model Context Protocol to expose a single tool, `generate_image`, to a compatible AI model. The tool accepts a text prompt, uses the Google Gemini API to generate an image, saves the image to the `public/` directory for auditing, and returns the raw image data as a base64-encoded string.

## To use the server with Claude Desktop or other applications

You need a Google Gemini API key and ImgBB API key to use this server.

Access https://api.imgbb.com/ to generate a IMGBB API Key. This is used to store and host the image online.

```json
{
  "mcpServers": {
    "mcp-nano-banana": {
        "command": "uvx",
        "args": [
            "mcp-nano-banana"
        ],
        "env": {
            "GEMINI_API_KEY": "YOUR_API_KEY_HERE",
            "IMGBB_API_KEY": "YOUR_API_KEY_HERE"
        }
    }
  }
}
```



## Dev Setup

### 1. Dependencies

This project uses Python and its dependencies are defined in `pyproject.toml`. You can install them using `pip`:

```bash
pip install .
# Or
uv sync
```

This will install `mcp`, `google-generativeai`, and other required packages.

### 2. API Key

You need a Google Gemini API key and ImgBB API key to use this server.

Access https://api.imgbb.com/ to generate a IMGBB API Key. This is used to store and host the image online.

1.  Create a file named `.env` in the root of the project.
2.  Add your API key to the `.env` file in the following format:

```
    GEMINI_API_KEY="YOUR_API_KEY_HERE"
    IMGBB_API_KEY="YOUR_API_KEY_HERE"
```

## Running the Server

This server is designed to be run as a subprocess by an MCP client or using the `mcp` command-line tool. The server listens for requests on `stdio`.

```bash
uvx --from git+https://github.com/GuilhermeAumo/mcp-nano-banana mcp-nano-banana
```


## Publishing new pipy version
To publish a new version of this package to PyPI:

1. **Update the version**  
   Edit the `version` field in `pyproject.toml` to the new version number.

2. **Build the package**  
   Run:
   ```bash
   uv build
   ```
   This will create `.tar.gz` and `.whl` files in the `dist/` directory.

3. **Upload to PyPI**  
   ```bash
   uv publish
   ```

4. **Tag the release (optional but recommended)**  
  Commit the changes to github first, then:
  
   ```bash
   git tag v<new-version>
   git push --tags
   ```

**Note:**  
- You need a PyPI account and must be listed as a maintainer of the project.

For more details, see the [Python Packaging User Guide](https://packaging.python.org/tutorials/packaging-projects/).
