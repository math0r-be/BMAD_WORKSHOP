# BMAD Method - BeCode Data Science Edition

## 🎯 What is BMAD Method?

**BMAD Method** (Breakthrough Method of Agile AI-driven Development) is a revolutionary framework that transforms how you approach software development and data science projects. It provides AI-powered agents that act as your virtual team members, each specialized in different aspects of development.

### 🚀 Why BMAD for Data Science?

This special BeCode edition includes **TonyFunkman 3.0**, your **Awesome AI Coach** **fully integrated and production-ready** that covers the entire data science curriculum from BeCode bootcamp to senior-level expertise:

- **Data Analysis & Visualization**
- **Machine Learning & Deep Learning**
- **Data Engineering & Pipelines**
- **MLOps & Model Deployment**
- **GenAI Applications**
- **Advanced SQL & Database Design**
- **Real-time Data Processing**

## 🏗️ Architecture Overview

BMAD Method works with **AI Agents** that you can summon in any AI chat interface (Claude, ChatGPT, Gemini, etc.):

```
@datadev *analyze-dataset     # Analyze your data
@datadev *build-ml-model      # Create ML models
@datadev *create-pipeline     # Build data pipelines
@architect *design-system     # System architecture
@dev *implement-feature       # Code implementation
```

## 🛠️ Installation Guide for BeCode Workshop

### Prerequisites

- **Node.js 20+** (Download from [nodejs.org](https://nodejs.org/))
- **Git** (Download from [git-scm.com](https://git-scm.com/))
- **AI Chat Interface** (Claude, ChatGPT, Gemini CLI, etc.)

### Step 1: Clone the BeCode Edition

```bash
# Clone this specific BeCode version
git clone https://github.com/math0r/BMAD-METHOD.git
cd BMAD-METHOD
```

### Step 2: Install Dependencies

```bash
# Install all required packages
npm install
```

### Step 3: Build the Agents

```bash
# Build all agent bundles with data science capabilities
npm run build
```

### Step 4: Install BMAD in Your Project Directory

#### For All Platforms:

```bash
# Option A: Use the npm script (Recommended)
npm run install:bmad

# Option B: Direct installation with options
node tools/installer/bin/bmad.js install -i gemini -d my-data-project
```

#### Platform-Specific Scripts:

**Windows Users:**

```bash
# Use the batch script
./install-local.bat

# Or with options
./install-local.bat -i gemini -d my-data-project
```

**Mac/Linux Users:**

```bash
# Make the script executable (first time only)
chmod +x install-local.sh

# Run the installation
./install-local.sh

# Or with options
./install-local.sh -i gemini -d my-data-project
```

### Step 5: Choose Your Installation Options

The installer will ask you:

1. **IDE Integration**: Choose your preferred AI interface
   - `gemini` - **Google Gemini CLI (RECOMMENDED FOR STUDENTS - FREE!)** 🆓
   - `cursor` - Cursor IDE (available for Mac)
   - `claude-code` - Claude in VS Code
   - `windsurf` - Windsurf IDE (Mac compatible)
   - `other` - Any other AI chat interface

   **🎓 For BeCode Students - We Recommend Gemini CLI**: It's completely free, powerful, and works perfectly with BMAD Method!

2. **Installation Type**:
   - **Full Installation** - Complete BMAD with all agents
   - **Data Science Focus** - Optimized for data science projects

3. **Team Configuration**:
   - `team-data-complete` - Full data science team
   - `team-data-science` - Specialized data science team
   - `team-fullstack` - Full-stack development team

## 🆓 Gemini CLI Setup (Recommended for Students)

### Why Gemini CLI for BeCode Students?

- **100% FREE** - No subscription required
- **Powerful AI** - Google's latest Gemini Pro model
- **Perfect for BMAD** - Designed to work seamlessly with our agents
- **Cross-platform** - Works on Windows, Mac, and Linux
- **No rate limits** - Use as much as you need for learning

### Windows Installation Guide

#### Step 1: Install Gemini CLI

```cmd
# Install Gemini CLI globally
npm install -g @google/generative-ai-cli

# Verify installation
gemini --version
```

#### Step 2: Get Your Free API Key

1. Go to [Google AI Studio](https://aistudio.google.com/app/apikey)
2. Sign in with your Google account
3. Click "Create API Key"
4. Copy your API key

#### Step 3: Configure Gemini CLI

```cmd
# Set up your API key (run this once)
gemini config set apiKey YOUR_API_KEY_HERE

# Test the connection
gemini chat "Hello, can you help me with data science?"
```

#### Step 4: Using BMAD with Gemini CLI

```cmd
# Navigate to your project directory
cd your-bmad-project

# Start a chat session
gemini chat

# In the chat, paste your agent (e.g., from .bmad-core/agents/datadev.txt)
# Then start using BMAD commands:
# *help
# *analyze-data
# *build-model
```

### Alternative: Using Gemini CLI with File Input

```cmd
# Copy agent content to a file
copy .bmad-core\agents\datadev.txt agent.txt

# Start Gemini with the agent loaded
gemini chat --file agent.txt

# Now you can directly use BMAD commands
```

### Gemini CLI Pro Tips for Students

1. **Save Sessions**: Use `--save-session` to continue conversations
2. **File Input**: Use `--file` to load agent definitions
3. **Output to File**: Use `--output` to save results
4. **Multiple Models**: Switch between different Gemini models

```cmd
# Advanced usage examples
gemini chat --model gemini-pro --save-session my-project
gemini chat --file .bmad-core/agents/datadev.txt --output analysis.md
```

## 🎮 Quick Start Guide

### 1. Navigate to Your Installed Project

**All Platforms:**

```bash
cd your-project-directory
```

**Mac Users - Additional Options:**

```bash
# Open project in Finder
open your-project-directory

# Open project in VS Code
code your-project-directory

# Open project in Cursor
cursor your-project-directory
```

### 2. Start with TonyFunkman 3.0 (Your Awesome AI Coach)

#### Using Gemini CLI (Recommended):

```cmd
# Method 1: Direct file loading
gemini chat --file .bmad-core/agents/datadev.txt

# Method 2: Copy and paste
gemini chat
# Then paste the content from .bmad-core/agents/datadev.txt
```

#### Using Other AI Interfaces:

Copy the content from `.bmad-core/agents/datadev.txt` and paste it into your AI chat interface, then:

```
*help
```

**Note**: With Gemini CLI, you don't need the `@datadev` prefix - just use the commands directly like `*help`, `*analyze-data`, etc.

**New in 3.0**: TonyFunkman now has **contextual modes** for specialized focus:

```
*mode-engineering    # Focus on data pipelines and infrastructure
*mode-analysis       # Focus on data analysis and business intelligence
*mode-science        # Focus on machine learning and AI
*mode-production     # Focus on deployment and MLOps
*mode-auto          # Auto-detect best mode (default)
```

### 3. Common Data Science Workflows

**TonyFunkman 3.0** includes **9 consolidated core tasks**:

```bash
# Data Analysis & Exploration
*analyze-data          # Comprehensive dataset analysis
*analyze-ecommerce     # E-commerce specific analysis with RFM

# Machine Learning & AI
*build-model          # Complete ML pipeline with optimization
*deploy-model         # Production deployment with monitoring

# Business Intelligence
*create-dashboard     # Interactive dashboards with Streamlit/Plotly
*measure-impact       # Business ROI and value measurement

# Advanced Operations (Production-Ready)
*adaptive-processing  # Smart processing (pandas/Dask/Spark)
*integrate-legacy     # Legacy systems integration
*optimize-costs       # Automatic cost and performance optimization
```

### 4. Team Collaboration

```bash
# Get system architecture advice
@architect *design-system

# Implement features
@dev *implement-feature

# Quality assurance
@qa *test-feature

# Project management
@pm *plan-sprint

# Agile story management
@sm *draft
```

## 📚 Available Agents

### Core Agents

- **@datadev** (TonyFunkman) - Awesome AI Coach for complete data science
- **@architect** - System architecture and design
- **@dev** - Software development and implementation
- **@analyst** - Business analysis and requirements
- **@qa** - Quality assurance and testing
- **@pm** - Project management
- **@sm** (Bob) - Scrum Master for agile project management
- **@ux-expert** - User experience design

### Specialized Teams

- **team-data-complete** - Full data-driven development team
- **team-data-science** - Specialized data science team
- **team-fullstack** - Complete full-stack development team

## 🔧 TonyFunkman 3.0 Capabilities

Our **production-ready** data science agent covers the complete BeCode curriculum plus enterprise-level features:

### 📊 Data Analysis & Visualization

- Exploratory Data Analysis (EDA)
- Statistical analysis and hypothesis testing
- Interactive dashboards with Plotly/Streamlit
- Data storytelling and reporting

### 🤖 Machine Learning

- Supervised/Unsupervised learning
- Deep learning with TensorFlow/PyTorch
- Model evaluation and optimization
- Feature engineering and selection

### 🏗️ Data Engineering

- ETL/ELT pipeline design
- Database design and optimization
- Real-time data processing
- Cloud data architecture

### 🚀 MLOps & Deployment

- Model versioning and tracking
- CI/CD for ML projects
- Model monitoring and maintenance
- Production deployment strategies

### 🧠 Advanced Topics

- Generative AI applications
- Advanced SQL and database design
- A/B testing frameworks
- Feature stores and ML platforms

### 🏭 Production-Ready Features (New in 3.0)

- **Error handling** with comprehensive logging and fallbacks
- **Legacy system integration** (Oracle, DB2, Mainframe, AS/400)
- **Adaptive processing** automatically chooses pandas/Dask/Spark based on data size
- **Cost optimization** with automatic resource management and monitoring
- **Business impact measurement** with ROI tracking and statistical significance testing

### 🏃 Agile Data Science with Scrum Master

- **Story breakdown** for complex data science tasks
- **Sprint planning** adapted to data science workflows
- **Epic management** for large-scale data projects
- **Retrospectives** to improve data science processes

## 💡 Workshop Examples

### Example 1: Analyze a Dataset (Enhanced in 3.0)

```
@datadev *analyze-data

# TonyFunkman 3.0 will guide you through:
# 1. Intelligent data loading with error handling
# 2. Comprehensive missing value analysis with alerts
# 3. Statistical summaries with outlier detection
# 4. Interactive visualization recommendations
# 5. Data quality assessment with actionable insights
# 6. Memory usage optimization for large datasets
```

### Example 2: Build a Production-Ready ML Model (Enhanced in 3.0)

```
@datadev *build-model

# TonyFunkman 3.0 will help you:
# 1. Define the problem type with business context
# 2. Prepare data with robust preprocessing
# 3. Select algorithms with hyperparameter optimization
# 4. Train models with cross-validation and statistical testing
# 5. Evaluate with comprehensive metrics and feature importance
# 6. Prepare for production deployment with monitoring
```

### Example 3: Create a Data Pipeline

```
@datadev *create-pipeline

# TonyFunkman will design:
# 1. Data ingestion strategy
# 2. Processing and transformation steps
# 3. Quality checks and validation
# 4. Storage and output formats
# 5. Monitoring and alerting
```

### Example 4: Organize Data Science Project with Scrum

```
@sm *draft

# Bob (Scrum Master) will help you:
# 1. Break down complex data science epics into manageable stories
# 2. Define clear acceptance criteria for data science tasks
# 3. Plan sprints adapted to data science workflows
# 4. Manage dependencies between data, model, and deployment tasks
# 5. Facilitate retrospectives to improve team processes
```

### Example 5: Measure Business Impact (New in 3.0)

```
@datadev *measure-impact

# TonyFunkman 3.0 will help you:
# 1. Calculate ROI and payback period for data science projects
# 2. Track KPI improvements with statistical significance
# 3. Measure business value and cost-benefit analysis
# 4. Set up monitoring dashboards for ongoing impact tracking
# 5. Generate executive reports with actionable insights
```

## 🆕 What's New in TonyFunkman 3.0

### **Contextual Intelligence**
TonyFunkman now adapts to your specific needs with **5 specialized modes**:
- `*mode-engineering` - Focus on data pipelines and infrastructure
- `*mode-analysis` - Focus on business intelligence and reporting  
- `*mode-science` - Focus on machine learning and AI
- `*mode-production` - Focus on deployment and MLOps
- `*mode-auto` - Automatically detects the best mode for your task

### **Production-Ready Features**
- **Robust error handling** with comprehensive logging
- **Adaptive data processing** automatically chooses the best strategy (pandas/Dask/Spark)
- **Legacy system integration** for Oracle, DB2, Mainframe systems
- **Cost optimization** with automatic resource monitoring
- **Business impact measurement** with ROI calculations

### **Consolidated Task System**
All data science capabilities are now organized in **9 core tasks** instead of 16+ separate files:
- Easier navigation and learning
- Consistent experience across all tasks
- Faster loading and better performance

## 🎯 Best Practices for BeCode Students

### 🆓 Complete Gemini CLI Workflow for Students

#### Daily Workflow Example:

```cmd
# 1. Start your data science session
cd my-data-project
gemini chat --file .bmad-core/agents/datadev.txt --save-session today-analysis

# 2. Set your focus mode
*mode-analysis

# 3. Start with data exploration
*analyze-data

# 4. Build models based on findings
*build-model

# 5. Create visualizations
*create-dashboard

# 6. Save your session for later
# (Gemini CLI automatically saves with --save-session)
```

#### Project Organization with Gemini CLI:

```cmd
# Create project structure
mkdir my-data-project
cd my-data-project

# Install BMAD
node path/to/BMAD-METHOD/tools/installer/bin/bmad.js install -i gemini -d .

# Start working with different agents
gemini chat --file .bmad-core/agents/datadev.txt    # For data science
gemini chat --file .bmad-core/agents/architect.txt  # For system design
gemini chat --file .bmad-core/agents/pm.txt         # For project planning
```

### 1. Start with Clear Objectives

Always begin by explaining your project goals to the agent:

**With Gemini CLI:**
```
# After loading the datadev agent
I need to analyze customer churn data to predict which customers are likely to leave our service.
```

**With other interfaces:**
```
@datadev I need to analyze customer churn data to predict which customers are likely to leave our service.
```

### 2. Iterate and Refine

Use the agents iteratively:

**With Gemini CLI:**
```
*analyze-data
# Review results, then:
Based on the analysis, let's build a classification model
*build-model
```

**With other interfaces:**
```
@datadev *analyze-dataset
# Review results, then:
@datadev Based on the analysis, let's build a classification model
```

### 3. Combine Multiple Agents

Use different agents for different aspects:

```
@architect *design-system  # For overall architecture
@datadev *build-ml-model   # For ML implementation
@qa *test-feature          # For testing strategy
@sm *draft                 # For story breakdown and sprint planning
```

### 4. Agile Data Science Workflow

Data science projects benefit from agile methodology:

```
@sm *draft                 # Break down data science epics into stories
@datadev *analyze-dataset  # Execute data analysis stories
@datadev *build-ml-model   # Implement ML model stories
@sm *correct-course        # Adjust course based on findings
```

### 4. Document Everything

Ask agents to help with documentation:

```
@datadev Create comprehensive documentation for this data pipeline
```

## 🍎 Mac-Specific Instructions

### Prerequisites for Mac Users

1. **Install Homebrew** (if not already installed):

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

2. **Install Node.js via Homebrew**:

```bash
brew install node
```

3. **Verify installation**:

```bash
node --version  # Should show v20+
npm --version   # Should show npm version
```

### Mac Installation Steps

```bash
# 1. Clone the repository
git clone https://github.com/math0r/BMAD-METHOD.git
cd BMAD-METHOD

# 2. Install dependencies
npm install

# 3. Build the agents
npm run build

# 4. Make installation script executable
chmod +x install-local.sh

# 5. Run installation
./install-local.sh
```

### Mac-Specific Notes

- **Terminal**: Use Terminal.app or iTerm2 for best experience
- **File Permissions**: The `chmod +x` command is required to make scripts executable
- **Path Issues**: If you get "command not found" errors, ensure `/usr/local/bin` is in your PATH
- **Gemini CLI**: Install with `npm install -g @google/generative-ai-cli` if using Gemini

### Recommended AI Interfaces for Mac

1. **Cursor IDE** - Native Mac app with excellent AI integration
2. **Windsurf** - Modern AI-powered IDE with Mac support
3. **VS Code with Claude** - Free option with Claude extension
4. **Gemini CLI** - Terminal-based interface for Google Gemini
5. **ChatGPT/Claude Web** - Browser-based interfaces work perfectly

### Mac Terminal Tips

```bash
# Use these commands in Terminal.app or iTerm2
cd ~/Desktop/my-project          # Navigate to project
open .                          # Open current directory in Finder
code .                          # Open current directory in VS Code
cursor .                        # Open current directory in Cursor
```

## 🔍 Troubleshooting

### Gemini CLI Specific Issues

**Issue**: "gemini: command not found"
**Solution**: 
```cmd
# Reinstall Gemini CLI globally
npm install -g @google/generative-ai-cli

# Check if npm global bin is in PATH
npm config get prefix
# Add the bin folder to your PATH if needed
```

**Issue**: "API key not working"
**Solution**:
```cmd
# Reset your API key
gemini config set apiKey YOUR_NEW_API_KEY

# Test the connection
gemini chat "test"
```

**Issue**: "Rate limit exceeded"
**Solution**: Gemini CLI is free but has reasonable usage limits. Wait a few minutes and try again.

**Issue**: "Agent commands not working"
**Solution**: Make sure you loaded the agent file correctly:
```cmd
# Correct way to load agent
gemini chat --file .bmad-core/agents/datadev.txt

# Then use commands without @ prefix
*help
*analyze-data
```

### Common Issues

**Issue**: "Agent not responding correctly"
**Solution**: Make sure you copied the complete agent content and started with the activation command

**Issue**: "Missing dependencies"
**Solution**: Run `npm install` in the BMAD-METHOD directory

**Issue**: "Build fails"
**Solution**: Ensure Node.js 20+ is installed and run `npm run build` again

### Mac-Specific Issues

**Issue**: "Permission denied" when running scripts
**Solution**: Run `chmod +x install-local.sh` to make the script executable

**Issue**: "command not found: node"
**Solution**: Install Node.js via Homebrew: `brew install node`

**Issue**: "EACCES: permission denied" during npm install
**Solution**: Use `sudo npm install` or fix npm permissions with `npm config set prefix ~/.npm-global`

### Platform Command Differences

| Task                       | Windows               | Mac/Linux                   |
| -------------------------- | --------------------- | --------------------------- |
| **Run installer script**   | `./install-local.bat` | `./install-local.sh`        |
| **Make script executable** | Not needed            | `chmod +x install-local.sh` |
| **Open directory**         | `explorer .`          | `open .`                    |
| **Clear terminal**         | `cls`                 | `clear`                     |
| **List files**             | `dir`                 | `ls -la`                    |
| **Copy files**             | `copy`                | `cp`                        |
| **Environment variables**  | `%PATH%`              | `$PATH`                     |

### Getting Help

1. **Check the agent help**: `*help` (with Gemini CLI) or `@datadev *help` (other interfaces)
2. **Review task documentation**: Look in the `tasks/` directory
3. **Ask the agent directly**: Agents can explain their capabilities
4. **Workshop support**: Ask your instructor during the session

### 🔗 Useful Links for Students

- **Gemini CLI Documentation**: [https://github.com/google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli)
- **Get Free API Key**: [https://aistudio.google.com/app/apikey](https://aistudio.google.com/app/apikey)
- **Google AI Studio**: [https://aistudio.google.com/](https://aistudio.google.com/)
- **BMAD Method Repository**: [https://github.com/math0r/BMAD-METHOD](https://github.com/math0r/BMAD-METHOD)

### 💡 Gemini CLI Pro Tips for BeCode Students

1. **Save Your Work**: Always use `--save-session project-name` to continue later
2. **File Management**: Use `--output filename.md` to save important results
3. **Multiple Projects**: Create different sessions for different projects
4. **Collaboration**: Share your session files with classmates
5. **Learning**: Ask the agent to explain concepts you don't understand

```cmd
# Example of a complete student workflow
gemini chat --file .bmad-core/agents/datadev.txt --save-session churn-analysis --output results.md

# In the chat:
*mode-analysis
*analyze-data
Can you explain the statistical concepts you just used?
*build-model
What are the pros and cons of each algorithm you suggested?
```

## 🤔 Choosing Your AI Interface: Student Guide

### 🆓 Free Options (Perfect for Students)

| Interface | Cost | Pros | Cons | Best For |
|-----------|------|------|------|----------|
| **Gemini CLI** | FREE | • No subscription<br>• Powerful AI<br>• File integration<br>• Session saving | • Command line only<br>• Requires setup | **Recommended for all students** |
| **ChatGPT Free** | FREE | • Web interface<br>• Easy to use | • Limited usage<br>• No file integration | Beginners who prefer web |
| **Claude Free** | FREE | • Good reasoning<br>• Web interface | • Limited usage<br>• Regional restrictions | Quick experiments |

### 💰 Paid Options (If Budget Allows)

| Interface | Cost | Pros | Cons | Best For |
|-----------|------|------|------|----------|
| **ChatGPT Plus** | $20/month | • Unlimited usage<br>• Latest models | • Subscription cost | Heavy users |
| **Claude Pro** | $20/month | • Excellent reasoning<br>• Large context | • Subscription cost | Complex projects |
| **Cursor IDE** | $20/month | • IDE integration<br>• Code assistance | • Subscription cost | Professional development |

### 🎓 Our Recommendation for BeCode Students

**Start with Gemini CLI** because:
- ✅ Completely free with no usage limits
- ✅ Works perfectly with BMAD Method
- ✅ Teaches you command-line skills
- ✅ Professional workflow preparation
- ✅ Can save and share sessions
- ✅ File integration for easy agent loading

**Upgrade later** if you need:
- Web interface (ChatGPT/Claude)
- IDE integration (Cursor)
- Specialized features

## 🌟 Advanced Features

### Custom Workflows

Create custom workflows by combining multiple tasks:

```
@datadev *analyze-dataset
@datadev *build-ml-model
@datadev *deploy-ml-model
```

### Knowledge Base Integration

Access the comprehensive data science knowledge base:

```
@datadev *kb-mode-interaction
```

### Team Collaboration

Use team bundles for complex projects:

```
# Load team-data-complete.txt for full data science team
@bmad-orchestrator coordinate the team for this data science project
```

## 📈 Learning Path for BeCode Students

### Beginner Level (Start Here)

1. **Data Exploration**: `@datadev *analyze-data` - Learn data profiling and EDA
2. **Visualization**: `@datadev *create-dashboard` - Build interactive dashboards  
3. **Business Context**: `@datadev *analyze-ecommerce` - Understand domain-specific analysis

### Intermediate Level (Build Skills)

1. **Machine Learning**: `@datadev *build-model` - Complete ML pipeline development
2. **Business Value**: `@datadev *measure-impact` - Learn ROI and business metrics
3. **Production Basics**: `@datadev *deploy-model` - Deploy models to production

### Advanced Level (Production Ready)

1. **Smart Processing**: `@datadev *adaptive-processing` - Handle large-scale data efficiently
2. **System Integration**: `@datadev *integrate-legacy` - Work with existing enterprise systems
3. **Cost Optimization**: `@datadev *optimize-costs` - Manage resources and performance

### Pro Tips for Each Level

- **Beginners**: Use `*mode-analysis` for easier business-focused guidance
- **Intermediate**: Switch between `*mode-science` and `*mode-analysis` as needed  
- **Advanced**: Use `*mode-production` for enterprise-grade implementations

## 🏃 Why Scrum Master is Essential for Data Science

Data science projects are inherently **experimental and iterative**. The Scrum Master (Bob) helps you:

### 🎯 **Project Organization**

- **Break down complex data science epics** into manageable stories
- **Define clear acceptance criteria** for data analysis and ML tasks
- **Manage dependencies** between data collection, analysis, modeling, and deployment

### 📋 **Sprint Planning for Data Science**

- **Adapt agile methodology** to data science workflows
- **Plan sprints** that account for data exploration uncertainty
- **Balance research tasks** with deliverable outcomes

### 🔄 **Iterative Improvement**

- **Facilitate retrospectives** to improve data science processes
- **Adjust course** when data reveals unexpected insights
- **Coordinate team efforts** across different data science disciplines

### 💡 **Practical Example**

```
# Start a data science project with proper organization
@sm *draft
# "I need to build a customer churn prediction model"

# Bob will help you create stories like:
# Story 1: "As a data scientist, I want to explore the customer dataset to understand churn patterns"
# Story 2: "As a data scientist, I want to engineer features that predict customer churn"
# Story 3: "As a data scientist, I want to train and evaluate multiple ML models for churn prediction"
# Story 4: "As a data scientist, I want to deploy the best model to production"

# Then execute each story with TonyFunkman:
@datadev *analyze-dataset    # Execute Story 1
@datadev *build-ml-model     # Execute Story 3
@datadev *deploy-ml-model    # Execute Story 4
```

## 🎉 Ready to Start!

You now have access to a complete AI-powered data science team with proper agile management. Start with simple tasks and gradually work your way up to complex projects. Remember, these agents are here to guide you, teach you, and help you build amazing data science solutions!

**Use the Scrum Master to organize your work, and TonyFunkman 3.0 to execute it with production-ready intelligence! Happy coding with BMAD Method! 🚀**

---

## 🎉 TonyFunkman 3.0 - Production Enterprise Ready!

### **What Makes 3.0 Special**

- **🧠 Contextual Intelligence** - 5 specialized modes for different focus areas
- **🏭 Production Features** - Error handling, legacy integration, cost optimization  
- **📊 Business Focus** - ROI measurement and business impact tracking
- **⚡ Smart Processing** - Automatic strategy selection based on data size
- **🎯 Consolidated Experience** - 9 core tasks instead of 16+ scattered files

### **Perfect for BeCode Workshop**

TonyFunkman 3.0 bridges the gap between **learning** and **real-world application**:
- Start with beginner-friendly analysis tasks
- Progress to intermediate ML development
- Master advanced production deployment
- Always with business context and real-world constraints

**From BeCode bootcamp to enterprise data scientist - TonyFunkman 3.0 guides you all the way! 💪**

---

_This BeCode edition was specially crafted to support your data science learning journey. For questions during the workshop, don't hesitate to ask your instructor or experiment with the agents directly._