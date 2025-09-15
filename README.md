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
- Docker and Docker Compose (for local installation)
- OpenAI API key
- Minimum 8GB RAM recommended
- Basic understanding of Dify workflows

### Option 1: Local Dify Installation

#### 1. **Install Dify Locally**

**Using Docker Compose (Recommended):**
```bash
# Clone Dify repository
git clone https://github.com/langgenius/dify.git
cd dify/docker

# Copy environment configuration
cp .env.example .env

# Start Dify with Docker Compose
docker-compose up -d

# Wait for services to start (may take 2-3 minutes)
# Check status
docker-compose ps
```

**Alternative: Using Single Docker Command:**
```bash
docker run -d \
  --name dify \
  -p 3000:3000 \
  -v dify-data:/app/data \
  langgenius/dify:latest
```

#### 2. **Access Dify Locally**
- Open your browser and navigate to: `http://localhost:3000`
- First time setup:
  - Create admin account
  - Set your workspace name
  - Configure initial settings

#### 3. **Configure OpenAI API**
- Go to `Settings` → `Model Provider`
- Add OpenAI as provider
- Enter your OpenAI API key
- Test connection

### Option 2: Dify Cloud (Easier)

1. **Sign up at**: https://cloud.dify.ai
2. **Create workspace**: Follow the setup wizard
3. **Add OpenAI API key**: In Settings → Model Provider

### Import the Medical RAG System

1. **Clone this repository:**
```bash
git clone https://github.com/yourusername/medical-rag-system.git
cd medical-rag-system
```

2. **Import to Dify:**
   - Navigate to `http://localhost:3000/apps` (local) or your Dify Cloud workspace
   - Click "Create App" → "Import App"
   - Select "Import from DSL File"
   - Upload the `medical-rag-workflow.yml` file
   - Click "Import"

3. **Configure the App:**
   - Go to `Apps` → Click on "Advanced Medical RAG System"
   - Click "Orchestrate" to view/edit the workflow
   - Verify OpenAI is selected in LLM nodes
   - Save changes

4. **Test Your Installation:**
   - Click "Preview" or "Run"
   - Upload a sample medical document
   - Ask: "Summarize this document"

### Accessing Your Apps

**Local Installation:**
- Dashboard: `http://localhost:3000`
- Apps List: `http://localhost:3000/apps`
- Your Medical RAG App: `http://localhost:3000/apps/[app-id]`
- API Endpoint: `http://localhost:3000/v1/chat-messages`

**Dify Cloud:**
- Dashboard: `https://cloud.dify.ai`
- Apps: `https://cloud.dify.ai/apps`

### Troubleshooting Local Installation

**Port Already in Use:**
```bash
# Change port in docker-compose.yml or use:
docker run -p 8080:3000 ... # Uses port 8080 instead
```

**Docker Memory Issues:**
```bash
# Increase Docker memory to at least 4GB
# Docker Desktop → Settings → Resources → Memory
```

**Database Connection Issues:**
```bash
# Reset Dify installation
docker-compose down -v
docker-compose up -d
```

**View Logs:**
```bash
# Check Dify logs
docker-compose logs -f

# Check specific service
docker-compose logs -f api
```

### Configure Knowledge Base (Optional)

1. **Create Knowledge Base:**
   - Go to `Knowledge` → "Create Knowledge Base"
   - Name it "Medical Documents"
   - Select embedding model (text-embedding-3-large)

2. **Upload Documents:**
   - Click "Add Files"
   - Upload your medical PDFs/documents
   - Wait for indexing to complete

3. **Connect to Workflow:**
   - Open your app in Orchestrate mode
   - In the Hybrid Retrieval node
   - Select your knowledge base
   - Save changes

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
