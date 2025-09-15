# Advanced Medical RAG System 🏥

A sophisticated medical document analysis chatbot built with Dify that intelligently processes and answers questions about medical documents using advanced RAG (Retrieval-Augmented Generation) techniques.

## 🎯 Features

- **Intelligent Question Classification**: Automatically categorizes questions into summarization or specific information extraction
- **Multi-format Document Support**: Processes PDF, TXT, DOC, DOCX, and image files
- **Advanced Document Structure Analysis**: Identifies sections, headings, tables, and figures in medical documents
- **Hybrid Retrieval System**: Combines keyword and vector search for optimal information retrieval
- **Medical-Aware Processing**: Enhanced relevance scoring for medical terms, dosages, and clinical information
- **Strict Instruction Following**: Respects exact word counts and format requirements

## 🚀 Quick Start

### Prerequisites
- Dify account (Cloud or Self-hosted)
- OpenAI API key
- Basic understanding of Dify workflows

### Installation

1. **Clone this repository:**
```bash
git clone https://github.com/yourusername/medical-rag-system.git
cd medical-rag-system
```

2. **Import to Dify:**
   - Log into your Dify workspace
   - Go to "Apps" → "Create App" → "Import"
   - Select the `medical-rag-workflow.yml` file
   - Configure your OpenAI API credentials

3. **Configure the Knowledge Base (Optional):**
   - Create a new knowledge base in Dify
   - Upload your medical documents
   - Connect it to the workflow

## 📋 How It Works

### Workflow Architecture

```
User Input → Question Classifier → Document Extractor → Advanced Processor → Hybrid Retrieval → GPT-4 → Answer
```

1. **Question Classifier**: Determines if the question requires summarization or specific information extraction
2. **Document Extractor**: Extracts text from uploaded files
3. **Advanced Processor**: 
   - Analyzes document structure (headings, sections, tables)
   - Creates intelligent chunks based on question type
   - Calculates medical relevance scores
4. **Hybrid Retrieval**: Combines keyword (30%) and vector (70%) search
5. **GPT-4 Processing**: Generates precise answers following user constraints

## 💡 Usage Examples

### Basic Usage
```
Upload a medical document and ask:
- "Summarize this document in 50 words"
- "What is the recommended dosage of epinephrine?"
- "List all mentioned side effects"
```

### Advanced Features
- **Strict Word Limits**: "Give me summary for Epinephrine in 3 words"
- **Table Analysis**: "What data is shown in the tables?"
- **Section-Specific**: "What does the conclusion section say?"

## 🛠️ Customization

### Adjusting Classification Categories
Edit the Question Classifier node to add more categories:
```yaml
classes:
  - id: summarization
    name: Summarization - Questions asking for summaries
  - id: answer_extraction
    name: Answer Extraction - Specific questions
  # Add your custom category here
```

### Modifying Chunk Sizes
In the Advanced Processor code:
```python
chunk_size = 900  # Adjust this value
overlap = 120     # Adjust overlap size
```

### Changing Retrieval Weights
In Hybrid Retrieval node:
```yaml
keyword_weight: 0.3  # Adjust keyword search weight
vector_weight: 0.7   # Adjust vector search weight
```

## 📊 Performance Specifications

- **Max file size**: 15MB per document
- **Supported formats**: PDF, TXT, DOC, DOCX, JPG, PNG
- **Max files per query**: 10
- **Chunk size**: 900 tokens with 120 token overlap
- **Retrieval top-k**: 6 most relevant chunks
- **Model**: GPT-4 with temperature 0.1 for consistency

## 🔧 Technical Stack

- **Platform**: Dify (v0.3.1)
- **LLM**: OpenAI GPT-4
- **Embeddings**: text-embedding-3-large
- **Processing**: Python 3 for document analysis
- **Retrieval**: Hybrid (Keyword + Vector) search

## 📝 Configuration Requirements

### Required API Keys:
- OpenAI API key with GPT-4 access

### Dify Settings:
- Advanced chat mode enabled
- File upload feature enabled
- Knowledge retrieval enabled

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## ⚠️ Important Notes

- **Medical Disclaimer**: This tool is for document analysis only and should not replace professional medical advice
- **Data Privacy**: Ensure compliance with HIPAA/GDPR when processing medical documents
- **API Costs**: Using GPT-4 will incur OpenAI API costs

## 🐛 Known Issues

- Classification may default to "answer_extraction" for ambiguous questions
- Large tables might be split across chunks
- Word count limits are enforced strictly, which may result in incomplete answers

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Built with [Dify](https://dify.ai)
- Powered by OpenAI GPT-4
- Medical terminology detection patterns adapted from various open-source medical NLP projects

## 📧 Support

For issues and questions:
- Open an issue on GitHub
- Check the [Dify documentation](https://docs.dify.ai)
- Contact: your.email@example.com

---

**Version**: 0.3.1  
**Last Updated**: December 2024  
**Status**: Active Development
