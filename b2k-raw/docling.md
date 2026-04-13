[
    
  ](https://github.com/docling-project/docling)

  [](https://trendshift.io/repositories/12132)

[](https://arxiv.org/abs/2408.09869)
[](https://docling-project.github.io/docling/)
[](https://pypi.org/project/docling/)
[](https://pypi.org/project/docling/)
[](https://github.com/astral-sh/uv)
[](https://github.com/astral-sh/ruff)
[](https://pydantic.dev)
[](https://github.com/pre-commit/pre-commit)
[](https://opensource.org/licenses/MIT)
[](https://pepy.tech/projects/docling)
[](https://apify.com/vancura/docling)
[](https://app.dosu.dev/097760a8-135e-4789-8234-90c8837d7f1c/ask?utm_source=github)
[](https://docling.ai/discord)
[](https://www.bestpractices.dev/projects/10101)
[](https://lfaidata.foundation/projects/)

Docling simplifies document processing, parsing diverse formats — including advanced PDF understanding — and providing seamless integrations with the gen AI ecosystem.

- 🗂️ Parsing of [multiple document formats](https://docling-project.github.io/docling/usage/supported_formats/) incl. PDF, DOCX, PPTX, XLSX, HTML, WAV, MP3, WebVTT, images (PNG, TIFF, JPEG, ...), LaTeX, plain text, and more

- 📑 Advanced PDF understanding incl. page layout, reading order, table structure, code, formulas, image classification, and more

- 🧬 Unified, expressive [DoclingDocument](https://docling-project.github.io/docling/concepts/docling_document/) representation format

- ↪️ Various [export formats](https://docling-project.github.io/docling/usage/supported_formats/) and options, including Markdown, HTML, WebVTT, [DocTags](https://arxiv.org/abs/2503.11576) and lossless JSON

- 📜 Support of several application-specifc XML schemas incl. [USPTO](https://www.uspto.gov/patents) patents, [JATS](https://jats.nlm.nih.gov/) articles, and [XBRL](https://www.xbrl.org/) financial reports.

- 🔒 Local execution capabilities for sensitive data and air-gapped environments

- 🤖 Plug-and-play [integrations](https://docling-project.github.io/docling/integrations/) incl. LangChain, LlamaIndex, Crew AI &amp; Haystack for agentic AI

- 🔍 Extensive OCR support for scanned PDFs and images

- 👓 Support of several Visual Language Models ([GraniteDocling](https://huggingface.co/ibm-granite/granite-docling-258M))

- 🎙️ Audio support with Automatic Speech Recognition (ASR) models

- 🔌 Connect to any agent using the [MCP server](https://docling-project.github.io/docling/usage/mcp/)

- 💻 Simple and convenient CLI

- 📤 Structured [information extraction](https://docling-project.github.io/docling/examples/extraction/) [🧪 beta]

- 📑 New layout model (**Heron**) by default, for faster PDF parsing

- 🔌 [MCP server](https://docling-project.github.io/docling/usage/mcp/) for agentic applications

- 💼 Parsing of XBRL (eXtensible Business Reporting Language) documents for financial reports

- 💬 Parsing of WebVTT (Web Video Text Tracks) files and export to WebVTT format

- 💬 Parsing of LaTeX files

- 📝 Parsing of plain-text files (`.txt`, `.text`) and Markdown supersets (`.qmd`, `.Rmd`)

- 📝 Chart understanding (Barchart, Piechart, LinePlot): converting them into tables, code or adding detailed descriptions

- 📝 Metadata extraction, including title, authors, references &amp; language

- 📝 Complex chemistry understanding (Molecular structures)

To use Docling, simply install `docling` from your package manager, e.g. pip:

**Note:** Python 3.9 support was dropped in docling version 2.70.0. Please use Python 3.10 or higher.

Works on macOS, Linux and Windows environments. Both x86_64 and arm64 architectures.

More [detailed installation instructions](https://docling-project.github.io/docling/installation/) are available in the docs.

To convert individual documents with python, use `convert()`, for example:

from docling.document_converter import DocumentConverter

source = "https://arxiv.org/pdf/2408.09869"  # document per local path or URL
converter = DocumentConverter()
result = converter.convert(source)
print(result.document.export_to_markdown())  # output: "## Docling Technical Report[...]"

More [advanced usage options](https://docling-project.github.io/docling/usage/advanced_options/) are available in
the docs.

Docling has a built-in CLI to run conversions.

docling https://arxiv.org/pdf/2206.01062

You can also use 🥚[GraniteDocling](https://huggingface.co/ibm-granite/granite-docling-258M) and other VLMs via Docling CLI:

docling --pipeline vlm --vlm-model granite_docling https://arxiv.org/pdf/2206.01062

This will use MLX acceleration on supported Apple Silicon hardware.

Read more [here](https://docling-project.github.io/docling/usage/)

Check out Docling's [documentation](https://docling-project.github.io/docling/), for details on
installation, usage, concepts, recipes, extensions, and more.

Go hands-on with our [examples](https://docling-project.github.io/docling/examples/),
demonstrating how to address different application use cases with Docling.

To further accelerate your AI application development, check out Docling's native
[integrations](https://docling-project.github.io/docling/integrations/) with popular frameworks
and tools.

Please feel free to connect with us using the [discussion section](https://github.com/docling-project/docling/discussions).

For more details on Docling's inner workings, check out the [Docling Technical Report](https://arxiv.org/abs/2408.09869).

Please read [Contributing to Docling](https://github.com/docling-project/docling/blob/main/CONTRIBUTING.md) for details.

If you use Docling in your projects, please consider citing the following:

@techreport{Docling,
  author = {Deep Search Team},
  month = {8},
  title = {Docling Technical Report},
  url = {https://arxiv.org/abs/2408.09869},
  eprint = {2408.09869},
  doi = {10.48550/arXiv.2408.09869},
  version = {1.0.0},
  year = {2024}
}

The Docling codebase is under MIT license.
For individual model usage, please refer to the model licenses found in the original packages.

Docling is hosted as a project in the [LF AI &amp; Data Foundation](https://lfaidata.foundation/projects/).

The project was started by the AI for knowledge team at IBM Research Zurich.