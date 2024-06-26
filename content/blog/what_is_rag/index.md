---
title: What Is Retrieval-Augmented Generation, aka RAG?
date: 2024-05-13T22:12:03.284Z
description: Retrieval-augmented generation (RAG) is a technique for enhancing the accuracy and reliability of generative AI models with facts fetched from external sources.
---

To understand the latest advance in [generative AI](https://www.nvidia.com/en-us/glossary/data-science/generative-ai/), imagine a courtroom.

Judges hear and decide cases based on their general understanding of the law. Sometimes a case — like a malpractice suit or a labor dispute — requires special expertise, so judges send court clerks to a law library, looking for precedents and specific cases they can cite.

Like a good judge, large language models ([LLMs](https://www.nvidia.com/en-us/glossary/data-science/large-language-models/)) can respond to a wide variety of human queries. But to deliver authoritative answers that cite sources, the model needs an assistant to do some research.

The court clerk of AI is a process called [retrieval-augmented generation](https://www.nvidia.com/en-us/glossary/retrieval-augmented-generation/), or RAG for short.

**How It Got Named ‘RAG’**
--------------------------

Patrick Lewis, lead author of the [2020 paper that coined the term](https://arxiv.org/pdf/2005.11401.pdf), apologized for the unflattering acronym that now describes a growing family of methods across hundreds of papers and dozens of commercial services he believes represent the future of generative AI.

[![Picture of Patrick Lewis, lead author of RAG paper](https://blogs.nvidia.com/wp-content/uploads/2023/11/Patrick-Lewis-RAG-lead-author-150x150.jpg)](https://blogs.nvidia.com/wp-content/uploads/2023/11/Patrick-Lewis-RAG-lead-author.jpg)

Patrick Lewis

“We definitely would have put more thought into the name had we known our work would become so widespread,” Lewis said in an interview from Singapore, where he was sharing his ideas with a regional conference of database developers.

“We always planned to have a nicer sounding name, but when it came time to write the paper, no one had a better idea,” said Lewis, who now leads a RAG team at AI startup Cohere.

**So, What Is Retrieval-Augmented Generation (RAG)?**
-----------------------------------------------------

Retrieval-augmented generation (RAG) is a technique for enhancing the accuracy and reliability of generative AI models with facts fetched from external sources.

In other words, it fills a gap in how LLMs work. Under the hood, LLMs are neural networks, typically measured by how many parameters they contain. An LLM’s parameters essentially represent the general patterns of how humans use words to form sentences.

That deep understanding, sometimes called parameterized knowledge, makes LLMs useful in responding to general prompts at light speed. However, it does not serve users who want a deeper dive into a current or more specific topic.

**Combining Internal, External Resources**
------------------------------------------

Lewis and colleagues developed retrieval-augmented generation to link generative AI services to external resources, especially ones rich in the latest technical details.

The paper, with coauthors from the former Facebook AI Research (now Meta AI), University College London and New York University, called RAG “a general-purpose fine-tuning recipe” because it can be used by nearly any LLM to connect with practically any external resource.

**Building User Trust**
-----------------------

Retrieval-augmented generation gives models sources they can cite, like footnotes in a research paper, so users can check any claims. That builds trust.

What’s more, the technique can help models clear up ambiguity in a user query. It also reduces the possibility a model will make a wrong guess, a phenomenon sometimes called hallucination.

Another great advantage of RAG is it’s relatively easy. A [blog](https://ai.meta.com/blog/retrieval-augmented-generation-streamlining-the-creation-of-intelligent-natural-language-processing-models/) by Lewis and three of the paper’s coauthors said developers can implement the process with as few as [five lines of code](https://huggingface.co/facebook/rag-token-nq).

That makes the method faster and less expensive than retraining a model with additional datasets. And it lets users hot-swap new sources on the fly.

**How People Are Using RAG**
----------------------------

With retrieval-augmented generation, users can essentially have conversations with data repositories, opening up new kinds of experiences. This means the applications for RAG could be multiple times the number of available datasets.

For example, a generative AI model supplemented with a medical index could be a great assistant for a doctor or nurse. Financial analysts would benefit from an assistant linked to market data.

In fact, almost any business can turn its technical or policy manuals, videos or logs into resources called knowledge bases that can enhance LLMs. These sources can enable use cases such as customer or field support, employee training and developer productivity.

The broad potential is why companies including [AWS](https://aws.amazon.com/blogs/machine-learning/simplify-access-to-internal-information-using-retrieval-augmented-generation-and-langchain-agents/), [IBM](https://research.ibm.com/blog/retrieval-augmented-generation-RAG), [Glean](https://www.glean.com/), Google, Microsoft, NVIDIA, [Oracle](https://www.oracle.com/artificial-intelligence/generative-ai/retrieval-augmented-generation-rag/) and [Pinecone](https://www.pinecone.io/learn/retrieval-augmented-generation/) are adopting RAG.

**Getting Started With Retrieval-Augmented Generation**
-------------------------------------------------------

To help users get started, NVIDIA developed an [AI workflow for retrieval-augmented generation](https://www.nvidia.com/en-us/ai-data-science/ai-workflows/generative-ai-chatbots/). It includes a sample chatbot and the elements users need to create their own applications with this new method.

The workflow uses [NVIDIA NeMo](https://www.nvidia.com/en-us/ai-data-science/generative-ai/nemo-framework/), a framework for developing and customizing generative AI models, as well as software like [NVIDIA Triton Inference Server](https://www.nvidia.com/en-us/ai-data-science/products/triton-inference-server/) and [NVIDIA TensorRT-LLM](https://developer.nvidia.com/blog/optimizing-inference-on-llms-with-tensorrt-llm-now-publicly-available/) for running generative AI models in production.

The software components are all part of [NVIDIA AI Enterprise](https://www.nvidia.com/en-us/data-center/products/ai-enterprise/), a software platform that accelerates development and deployment of production-ready AI with the security, support and stability businesses need.

Getting the best performance for RAG workflows requires massive amounts of memory and compute to move and process data. The [NVIDIA GH200 Grace Hopper Superchip](https://nvidianews.nvidia.com/news/gh200-grace-hopper-superchip-with-hbm3e-memory), with its 288GB of fast HBM3e memory and 8 petaflops of compute, is ideal — it can deliver a 150x speedup over using a CPU.

Once companies get familiar with RAG, they can combine a variety of off-the-shelf or custom LLMs with internal or external knowledge bases to create a wide range of assistants that help their employees and customers.

RAG doesn’t require a data center. LLMs are debuting on Windows PCs, thanks to NVIDIA software that enables all sorts of applications users can access even on their laptops.

[![Chart shows running RAG on a PC](https://blogs.nvidia.com/wp-content/uploads/2023/11/Using-RAG-on-PCs.jpg)](https://blogs.nvidia.com/wp-content/uploads/2023/11/Using-RAG-on-PCs.jpg)

An example application for RAG on a PC.

PCs equipped with NVIDIA RTX GPUs can now run some AI models locally. By using RAG on a PC, users can link to a private knowledge source – whether that be emails, notes or articles – to improve responses. The user can then feel confident that their data source, prompts and response all remain private and secure.

A [recent blog](https://nam11.safelinks.protection.outlook.com/?url=https%3A%2F%2Fblogs.nvidia.com%2Fblog%2F2023%2F10%2F17%2Ftensorrt-llm-windows-stable-diffusion-rtx%2F&data=05%7C01%7Crmerritt%40nvidia.com%7Cdfd2267cb8344597f73408dbd0e6fc36%7C43083d15727340c1b7db39efd9ccc17a%7C0%7C0%7C638333462716560839%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C3000%7C%7C%7C&sdata=V5FClNyBybzOnm3%2FKxiTT4i9aoT0GdLWzdLfnF8LBk0%3D&reserved=0) provides an example of RAG accelerated by TensorRT-LLM for Windows to get better results fast.

**The History of RAG**
----------------------

The roots of the technique go back at least to the early 1970s. That’s when researchers in information retrieval prototyped what they called question-answering systems, apps that use natural language processing ([NLP](https://www.nvidia.com/en-us/glossary/natural-language-processing/)) to access text, initially in narrow topics such as baseball.

The concepts behind this kind of text mining have remained fairly constant over the years. But the machine learning engines driving them have grown significantly, increasing their usefulness and popularity.

In the mid-1990s, the Ask Jeeves service, now Ask.com, popularized question answering with its mascot of a well-dressed valet. IBM’s Watson became a TV celebrity in 2011 when it handily beat two human champions on the _Jeopardy!_ game show.

[![Picture of Ask Jeeves, an early RAG-like web service](https://blogs.nvidia.com/wp-content/uploads/2023/11/Ask-Jeeves-2.jpg)](https://blogs.nvidia.com/wp-content/uploads/2023/11/Ask-Jeeves-2.jpg)

Today, LLMs are taking question-answering systems to a whole new level.

**Insights From a London Lab**
------------------------------

The seminal 2020 paper arrived as Lewis was pursuing a doctorate in NLP at University College London and working for Meta at a new London AI lab. The team was searching for ways to pack more knowledge into an LLM’s parameters and using a benchmark it developed to measure its progress.

Building on earlier methods and inspired by [a paper](https://arxiv.org/pdf/2002.08909.pdf) from Google researchers, the group “had this compelling vision of a trained system that had a retrieval index in the middle of it, so it could learn and generate any text output you wanted,” Lewis recalled.

[![Picture of IBM Watson winning on "Jeopardy" TV show, popularizing a RAG-like AI service](https://blogs.nvidia.com/wp-content/uploads/2023/11/IBM-Watson-wins-Jeopardy-YT.jpg)](https://blogs.nvidia.com/wp-content/uploads/2023/11/IBM-Watson-wins-Jeopardy-YT.jpg)

The IBM Watson question-answering system became a celebrity when it won big on the TV game show Jeopardy!

When Lewis plugged into the work in progress a promising retrieval system from another Meta team, the first results were unexpectedly impressive.

“I showed my supervisor and he said, ‘Whoa, take the win. This sort of thing doesn’t happen very often,’ because these workflows can be hard to set up correctly the first time,” he said.

Lewis also credits major contributions from team members Ethan Perez and Douwe Kiela, then of New York University and Facebook AI Research, respectively.

When complete, the work, which ran on a cluster of NVIDIA GPUs, showed how to make generative AI models more authoritative and [trustworthy](https://blogs.nvidia.com/blog/what-is-trustworthy-ai/). It’s since been cited by hundreds of papers that amplified and extended the concepts in what continues to be an active area of research.

**How Retrieval-Augmented Generation Works**
--------------------------------------------

At a high level, here’s how an [NVIDIA technical brief](https://docs.nvidia.com/ai-enterprise/workflows-generative-ai/0.1.0/technical-brief.html) describes the RAG process.

When users ask an LLM a question, the AI model sends the query to another model that converts it into a numeric format so machines can read it. The numeric version of the query is sometimes called an embedding or a vector.

[![NVIDIA diagram of how RAG works with LLMs](https://blogs.nvidia.com/wp-content/uploads/2023/11/NVIDIA-RAG-diagram-scaled.jpg)](https://blogs.nvidia.com/wp-content/uploads/2023/11/NVIDIA-RAG-diagram-scaled.jpg)

Retrieval-augmented generation combines LLMs with embedding models and vector databases.

The embedding model then compares these numeric values to vectors in a machine-readable index of an available knowledge base. When it finds a match or multiple matches, it retrieves the related data, converts it to human-readable words and passes it back to the LLM.

Finally, the LLM combines the retrieved words and its own response to the query into a final answer it presents to the user, potentially citing sources the embedding model found.

**Keeping Sources Current**
---------------------------

In the background, the embedding model continuously creates and updates machine-readable indices, sometimes called vector databases, for new and updated knowledge bases as they become available.

[![Chart of a RAG process described by LangChain](https://blogs.nvidia.com/wp-content/uploads/2023/11/LangChain-2-LLM-with-a-retriveal-process-672x268.jpg)](https://blogs.nvidia.com/wp-content/uploads/2023/11/LangChain-2-LLM-with-a-retriveal-process.jpg)

Retrieval-augmented generation combines LLMs with embedding models and vector databases.

Many developers find LangChain, an open-source library, can be particularly useful in chaining together LLMs, embedding models and knowledge bases. NVIDIA uses LangChain in its reference architecture for retrieval-augmented generation.

The LangChain community provides its own [description of a RAG process](https://blog.langchain.dev/tutorial-chatgpt-over-your-data/).

Looking forward, the future of generative AI lies in creatively chaining all sorts of LLMs and knowledge bases together to create new kinds of assistants that deliver authoritative results users can verify.

Get a hands on using retrieval-augmented generation with an AI chatbot in this [NVIDIA LaunchPad lab](https://www.nvidia.com/en-us/launchpad/ai/generative-ai-knowledge-base-chatbot/).

_Explore [generative AI](https://www.nvidia.com/gtc/sessions/generative-ai/?nvid=nv-int-txtad-141445 "Original URL: https://www.nvidia.com/gtc/sessions/generative-ai/?nvid=nv-int-txtad-141445 Click to follow link.") sessions and experiences at [NVIDIA GTC](https://www.nvidia.com/gtc/), the global conference on AI and accelerated computing, running March 18-21 in San Jose, Calif., and online._

Categories: [Deep Learning](https://blogs.nvidia.com/blog/category/enterprise/deep-learning/) | [Explainer](https://blogs.nvidia.com/blog/category/explainer/) | [Generative AI](https://blogs.nvidia.com/blog/category/generative-ai/)

Tags: [Artificial Intelligence](https://blogs.nvidia.com/blog/tag/artificial-intelligence/) | [Events](https://blogs.nvidia.com/blog/tag/events/) | [Inference](https://blogs.nvidia.com/blog/tag/inference/) | [Machine Learning](https://blogs.nvidia.com/blog/tag/machine-learning/) | [New GPU Uses](https://blogs.nvidia.com/blog/tag/new-gpu-uses/) | [TensorRT](https://blogs.nvidia.com/blog/tag/tensorrt/) | [Trustworthy AI](https://blogs.nvidia.com/blog/tag/trustworthy-ai/)

![Subscribe Widget](https://blogs.nvidia.com/gtc24-spring-best-of-gtc-nv-blog-406x350-2x/)[](https://www.nvidia.com/en-us/on-demand/?nvid=nv-int-bnr-685116)

### All NVIDIA News