*Congratulations to Docling for climbing the charts to be *[*one of GitHub’s top repos*](https://github.com/trending?since=monthly&amp;spoken_language_code=)* of the month!*

Organizations have lots of data, from their intellectual property and knowledge to marketing, sales and customer data to operations policies and procedures and much more.  The challenge isn’t collecting the data or generating documents; it’s extracting meaningful insights from it. Actionable insights can lead to better customer service, faster time-to-customer value, smoother operations and so. Generative AI (gen AI) promises to bridge this gap, turning the mountain of organizational data into strategic insights.

The promises of gen AI cannot be realized, however, when the data is trapped in formats not directly consumable by a large language model (LLM). This could be when the data is in a pdf file or proprietary document format like docx, turning this challenge into a blocker for aligning the model to the organization’s needs. To solve those challenges, organizations need to preprocess existing documents into formats that can be consumed by fine-tuning pipelines or for the creation of retrieval-augmented generation (RAG).

This is not about a naive OCR or text extraction. An important part of this preprocessing stage is that the data needs to be extracted following context and element-aware techniques. For example, if a table spans multiple pages, it must be extracted as a single table, or if the document has a layout of multiple text columns per page or mixes elements like images and tables, each one of those elements must be extracted consistently and maintain the awareness of the context from where it is being extracted.

Throughout the years, many open source tools have tried to solve one or even a few aspects of this challenge, but none tackle the whole problem. This fragmented approach has forced organizations to use complex pipelines, interconnect disjointed tools and process the same documents multiple times using different tools. The results are inconsistent, computationally expensive and complex to maintain, and their output quality varies.

We faced these same challenges when creating document ingestion pipelines for processing documents to fine-tune a model with [InstructLab](https://github.com/instructlab). That is when we discovered and adopted [Docling](https://research.ibm.com/blog/docling-generative-AI), a project developed at IBM Research, which proved transformative for our workflow. Since IBM recently released Docling as an open source project in Fall 2024, this tool has become prominent in the NLP field, validating our early adoption. We are thrilled to witness its growing impact in the open source gen AI ecosystem.### Docling at a glance

[Docling](https://github.com/DS4SD/docling) is an upstream open source project and tool for parsing documents, from .pdf and .docx to .pptx and html and more, and converting them into formats like Markdown or JSON, making it easier to prepare content for gen AI applications. It supports advanced PDF processing optical character recognition (OCR) for scanned documents and integrates with tools like LlamaIndex and LangChain for RAG and question-answering tasks.
        [

](/rhdc/managed-files/docling_processing.png)
  

*Source: *[*https://github.com/DS4SD/docling?tab=readme-ov-file*](https://github.com/DS4SD/docling?tab=readme-ov-file)### Try out Docling for yourself

Simply install Docling from your package manager, e.g. pip:

`# pip install docling`

Once installed, you can do the document conversion programmatically in your Python module or use the Docling cli.```
from docling.document_converter import DocumentConverter

source = "https://arxiv.org/pdf/2408.09869"  # PDF path or URL
converter = DocumentConverter()
result = converter.convert(source)
print(result.document.export_to_markdown())  # output: "### Docling Technical Report[...]"

# docling https://arxiv.org/pdf/2206.01062
```

You can find other ways to configure this data conversion and details in the project repository [here](https://ds4sd.github.io/docling/usage/).### Docling in action today

Docling is already being used by the InstructLab community for users to submit public datasets to the Instructab taxonomy. Users can go to [https://ui.instructlab.ai/](https://ui.instructlab.ai/) and submit their datasets for inclusion in future versions of the open source InstructLab granite-lab community model. This granite-lab model is based on the open source [Granite-7b](https://huggingface.co/ibm-granite/granite-7b-base) base model, which has been customized with InstructLab to add new knowledge and skills submitted by community members. The upcoming granite-lab release uses the open source [Granite-3.0-8b](https://huggingface.co/ibm-granite/granite-3.0-8b-base) base model and is being customized with InstructLab. This service uses Docling to convert users' documents into the data format needed for the Instructlab taxonomy, simplifying the process of contributing new knowledge documents.  These same tools can also be used to customize a user’s private model instances. 
        [

](/rhdc/managed-files/InstructLab_Knowledge_Contribution.png)
  
### Red Hat and Docling

Red Hat [introduced](https://www.redhat.com/en/about/press-releases/red-hat-enterprise-linux-ai-now-generally-available-enterprise-ai-innovation-production) Red Hat Enterprise Linux AI ([RHEL AI](https://www.redhat.com/en/technologies/linux-platforms/enterprise-linux/ai)) and InstructLab earlier this year to bring these same capabilities to enterprise customers. RHEL AI is an enterprise-focused foundation model platform that integrates open source gen AI capabilities and is optimized for deployment across hybrid cloud environments. It combines IBM’s open source Granite LLMs with Red Hat’s InstructLab tools, enabling domain experts (not just data scientists) to fine-tune models with industry-specific knowledge, aligning them with unique organizational needs and data. Those models can then be deployed and managed across a hybrid cloud environment that spans from enterprise data centers, to public clouds and edge environments.

We embraced IBM Research’s decision to open source Docling, and their continued commitment to innovating in this field, making gen AI more accessible and achievable.  In upcoming RHEL AI releases, we intend to include Docling as a supported feature, giving customers a simpler way to ingest their own private enterprise data in various formats and presenting that to InstructLab synthetic data generation and phase training in RHEL AI to customize and tune their own model instances.

We are excited by the innovation and user benefits that Docling brings to the open-source community and look forward to bringing these capabilities to RHEL AI users. The speed at which open source projects are making gen AI more accessible is nothing short of amazing, and we’re pleased to both support these upstream communities and bring this innovation to our customers as enterprise-ready capabilities.## Watch this video to experience more