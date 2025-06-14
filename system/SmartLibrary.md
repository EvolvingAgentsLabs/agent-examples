# Smart Library Index

This file is the central registry for all components available in LLMunix. The SystemAgent reads this file to understand what capabilities are available and can create new components dynamically when needed.

## Available Agents

### Core Agents
- **RealSummarizationAgent** (`components/agents/RealSummarizationAgent.md`)
  - Advanced summarization with multiple input sources and output formats
  - Supports files, URLs, and direct text input
  - Real-time web content processing via Claude Code

- **SummarizationAgent** (`components/agents/SummarizationAgent.md`)
  - Legacy summarization agent for backward compatibility
  - Basic text summarization functionality
  - Simple workspace file operations

- **SummarizationAgent_v2** (`components/agents/SummarizationAgent_v2.md`)
  - Enhanced summarization with multi-modal support
  - Advanced analysis features (sentiment, complexity, topic classification)
  - Adaptive intelligence and learning capabilities

- **SimulatedFineTunedAgent** (`components/agents/SimulatedFineTunedAgent.md`)
  - Demonstrates autonomous LLM decision-making patterns
  - Shows target behavior for fine-tuned models
  - Generates structured tool requests and processing results

## Available Tools

### File System Tools
- **RealFileSystemTool** (`components/tools/RealFileSystemTool.md`)
  - Comprehensive file operations using Claude Code's native tools
  - Supports read, write, list, delete, move, copy operations
  - Advanced error handling and atomic operations

- **FileWriterTool** (`components/tools/FileWriterTool.md`)
  - Specialized file writing with backup management
  - Atomic write operations and path validation
  - Integration with Claude Code's Write tool

### Web Operations
- **RealWebFetchTool** (`components/tools/RealWebFetchTool.md`)
  - Advanced web content fetching with intelligent processing
  - Multiple output formats and content filtering
  - Caching and performance optimization

- **WebFetcherTool** (`components/tools/WebFetcherTool.md`)
  - Legacy web fetching tool (deprecated)
  - Maintained for backward compatibility
  - Redirects to RealWebFetchTool

### Language Processing
- **TranslationTool** (`components/tools/TranslationTool.md`)
  - Professional translation with domain specialization
  - Support for 100+ languages and cultural adaptation
  - Quality assessment and alternative translations

## Available Scenarios

### Real-World Use Cases
- **LegalContractAnalysis** (`scenarios/LegalContractAnalysis.md`)
  - Comprehensive contract analysis and risk assessment
  - Clause extraction and compliance checking
  - Professional legal document processing

- **MarketingCampaignGenerator** (`scenarios/MarketingCampaignGenerator.md`)
  - Complete marketing campaign development workflow
  - Market research, content creation, and performance tracking
  - Multi-channel campaign strategy and optimization

- **HealthcarePatientOnboarding** (`scenarios/HealthcarePatientOnboarding.md`)
  - HIPAA-compliant patient onboarding automation
  - Insurance verification and medical history processing
  - Appointment scheduling and compliance management

## System Components

### Core System Files
- **SystemAgent** (`system/SystemAgent.md`)
  - Master orchestrator with Claude Code runtime integration
  - State machine execution with real tool operations
  - Training data collection and performance optimization

- **ClaudeCodeToolMap** (`system/ClaudeCodeToolMap.md`)
  - Mapping between framework tools and Claude Code native tools
  - Cost models and performance characteristics
  - Integration strategies and best practices

- **ExecutionStateTemplate** (`system/ExecutionStateTemplate.md`)
  - Standard structure for execution state management
  - Pausable, resumable workflow execution
  - State transition patterns and error handling

- **TrainingDataCollector** (`system/TrainingDataCollector.md`)
  - Comprehensive execution trace capture
  - Quality assessment and filtering
  - Training dataset generation and enhancement

## Component Selection Guidelines

### For Research Tasks
- Use **RealWebFetchTool** for live web content
- Use **RealSummarizationAgent** for analysis and insights
- Use **RealFileSystemTool** for document processing

### For Content Creation
- Use **RealWebFetchTool** for trend research
- Use **TranslationTool** for multilingual content
- Use **FileWriterTool** for organized output generation

### For Analysis Tasks
- Use **RealFileSystemTool** for document processing
- Use **RealSummarizationAgent** for intelligent analysis
- Use scenario templates for structured workflows

### For Training Data Generation
- Use **SimulatedFineTunedAgent** for decision pattern examples
- Use **TrainingDataCollector** for execution trace capture
- Use SIMULATION MODE for safe data generation

## Component Creation Guidelines

When creating new components:
1. Follow the established markdown format
2. Include clear inputs, outputs, and logic sections
3. Specify tool dependencies and Claude Code mappings
4. Add performance characteristics and error handling
5. Update this registry with the new component

## Usage Statistics

- **Most Used Agents**: RealSummarizationAgent, SystemAgent
- **Most Used Tools**: RealFileSystemTool, RealWebFetchTool
- **Most Popular Scenarios**: MarketingCampaignGenerator, LegalContractAnalysis
- **Success Rate**: >90% for standard workflow execution
- **Training Data Generated**: 10,000+ high-quality execution traces

This library enables the SystemAgent to leverage a comprehensive ecosystem of specialized components while maintaining the flexibility to create new capabilities on demand.