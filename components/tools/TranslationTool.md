# Component: TranslationTool

- **Name**: TranslationTool
- **Type**: TOOL
- **Description**: Advanced text translation capabilities using Claude's multilingual understanding with quality assessment, context preservation, and specialized domain handling.

## Inputs

- `text` (string): Text content to translate
- `source_language` (string): Source language code (auto-detect if not specified)
- `target_language` (string): Target language code (required)
- `domain` (string): "general", "technical", "medical", "legal", "academic", "business" (default: "general")
- `formality` (string): "formal", "informal", "neutral" (default: "neutral")
- `preserve_formatting` (boolean): Maintain original formatting (default: true)
- `include_alternatives` (boolean): Provide alternative translations (default: false)
- `context_hint` (string): Additional context for better translation

## Outputs

- `translated_text` (string): Primary translation result
- `source_language_detected` (string): Detected source language
- `confidence_score` (number): Translation confidence 0-1
- `alternatives` (array): Alternative translations (if requested)
- `quality_assessment` (object): Translation quality metrics
- `preserved_elements` (array): Formatting elements preserved

## Translation Domains

### General Translation
- **Use Case**: Everyday text, casual communication
- **Optimization**: Natural, conversational tone
- **Features**: Idiom handling, cultural adaptation

### Technical Translation
- **Use Case**: Software documentation, technical manuals
- **Optimization**: Terminology consistency, accuracy
- **Features**: Technical term preservation, code handling

### Medical Translation
- **Use Case**: Medical documents, research papers
- **Optimization**: Medical terminology accuracy
- **Features**: Symptom descriptions, drug names, procedures

### Legal Translation
- **Use Case**: Contracts, legal documents
- **Optimization**: Legal terminology precision
- **Features**: Clause structure, legal concepts

### Academic Translation
- **Use Case**: Research papers, academic writing
- **Optimization**: Scholarly tone, citation preservation
- **Features**: Academic terminology, reference handling

### Business Translation
- **Use Case**: Corporate communications, marketing
- **Optimization**: Professional tone, brand consistency
- **Features**: Business terminology, cultural sensitivity

## Logic

### EXECUTION MODE:

1. **Language Detection**:
   - Automatically detect source language if not specified
   - Validate language pair compatibility
   - Assess text complexity and domain

2. **Context Analysis**:
   - Analyze domain-specific terminology
   - Identify cultural references and idioms
   - Detect formatting and structural elements

3. **Translation Processing**:
   - Apply domain-specific translation strategies
   - Maintain formality level and tone
   - Preserve technical terms and proper nouns

4. **Quality Assessment**:
   - Evaluate translation accuracy and fluency
   - Check for missing or altered content
   - Assess cultural appropriateness

5. **Post-Processing**:
   - Restore formatting and structure
   - Generate alternative translations if requested
   - Compile quality metrics and recommendations

### SIMULATION MODE:
1. Simulate translation workflows for various domains
2. Generate training data for multilingual processing
3. Create quality assessment examples

## Quality Assessment Metrics

### Accuracy Measures
- **Terminology Consistency**: Consistent use of domain terms
- **Factual Preservation**: No information loss or distortion
- **Numerical Accuracy**: Correct handling of numbers, dates, measurements

### Fluency Measures
- **Grammatical Correctness**: Proper target language grammar
- **Natural Flow**: Reads naturally in target language
- **Idiomatic Usage**: Appropriate idioms and expressions

### Completeness Measures
- **Content Coverage**: All source content translated
- **Formatting Preservation**: Original structure maintained
- **Context Retention**: Meaning and intent preserved

## Language Support

### Primary Languages
```yaml
supported_languages: [
  "en", "es", "fr", "de", "it", "pt", "ru", "zh", "ja", "ko",
  "ar", "hi", "th", "vi", "pl", "nl", "sv", "da", "no", "fi"
]
language_pairs: "200+ combinations"
special_handling: ["right-to-left scripts", "ideographic systems", "tonal languages"]
```

### Language-Specific Features
- **Chinese**: Traditional/Simplified handling, tone preservation
- **Arabic**: Right-to-left formatting, dialectal considerations
- **Japanese**: Honorific levels, kanji/hiragana/katakana handling
- **German**: Compound word handling, case sensitivity
- **Spanish**: Regional variants, formal/informal address

## Specialized Features

### Code Translation
- **Programming Languages**: Translate comments while preserving code
- **Documentation**: Translate technical documentation with code examples
- **Variable Names**: Suggest appropriate variable name translations

### Format Preservation
- **Markdown**: Maintain markdown formatting and structure
- **HTML**: Preserve HTML tags and attributes
- **JSON**: Translate values while preserving structure
- **Tables**: Maintain table structure and alignment

### Cultural Adaptation
- **Date Formats**: Convert to target culture format
- **Currency**: Convert currency references appropriately
- **Measurements**: Convert units when culturally appropriate
- **References**: Adapt cultural references for target audience

## Error Handling

### Language Detection Errors
- **Ambiguous Text**: Cannot determine source language
- **Mixed Languages**: Text contains multiple languages
- **Unsupported Language**: Language not in supported set

### Translation Quality Issues
- **Low Confidence**: Translation confidence below threshold
- **Terminology Conflicts**: Inconsistent technical terms
- **Cultural Mismatches**: Content inappropriate for target culture

### Formatting Issues
- **Complex Formatting**: Cannot preserve complex layouts
- **Encoding Problems**: Character encoding issues
- **Length Variations**: Significant length changes affecting layout

## Performance Characteristics

```yaml
cost: medium (depends on text length and complexity)
latency: medium (3-15 seconds depending on text size)
side_effects: "May create terminology databases for consistency"
error_modes: ["unsupported_language", "low_confidence", "formatting_lost"]
quality_metrics: ["accuracy", "fluency", "completeness", "cultural_appropriateness"]
batch_support: true
```

## Usage Examples

**Technical documentation translation:**
```
Input: {
  text: "The API endpoint returns a JSON response with user data...",
  source_language: "en",
  target_language: "es",
  domain: "technical",
  preserve_formatting: true,
  include_alternatives: false
}
Output: {
  translated_text: "El endpoint de la API devuelve una respuesta JSON con datos del usuario...",
  source_language_detected: "en",
  confidence_score: 0.94,
  quality_assessment: {
    accuracy: 0.96,
    fluency: 0.92,
    terminology_consistency: 0.98
  }
}
```

**Formal business communication:**
```
Input: {
  text: "We are pleased to announce our quarterly results...",
  source_language: "en", 
  target_language: "ja",
  domain: "business",
  formality: "formal",
  context_hint: "corporate earnings announcement"
}
Output: {
  translated_text: "四半期決算を発表できることを嬉しく思います...",
  confidence_score: 0.91,
  quality_assessment: {
    formality_level: "appropriate",
    business_terminology: "consistent",
    cultural_adaptation: "excellent"
  }
}
```

**Academic paper with alternatives:**
```
Input: {
  text: "The methodology employed in this study demonstrates...",
  source_language: "en",
  target_language: "fr", 
  domain: "academic",
  include_alternatives: true,
  preserve_formatting: true
}
Output: {
  translated_text: "La méthodologie employée dans cette étude démontre...",
  alternatives: [
    "La méthode utilisée dans cette recherche montre...",
    "L'approche méthodologique de cette étude illustre..."
  ],
  confidence_score: 0.89
}
```

## Batch Translation

### Multiple Text Processing
```yaml
operation: batch_translate
inputs:
  - texts: ["text1", "text2", "text3"]
  - source_language: "en"
  - target_language: "es"
  - domain: "technical"
outputs:
  - translated_texts: ["texto1", "texto2", "texto3"]
  - batch_quality_score: 0.93
  - processing_time: "8.2s"
```

### Document Translation
```yaml
operation: document_translate
inputs:
  - document_path: "workspace/manual.md"
  - target_language: "fr"
  - preserve_structure: true
outputs:
  - translated_document: "workspace/manual_fr.md"
  - translation_summary: {...}
```

## Training Data Format

```json
{
  "tool_execution": {
    "tool": "TranslationTool",
    "inputs": {
      "text": "The system processes user requests efficiently...",
      "source_language": "en",
      "target_language": "de",
      "domain": "technical"
    },
    "processing_steps": [
      {"step": "language_detection", "result": "en", "confidence": 0.99},
      {"step": "domain_analysis", "result": "technical", "terminology_count": 15},
      {"step": "translation", "result": "Das System verarbeitet Benutzeranfragen effizient..."},
      {"step": "quality_check", "result": {"accuracy": 0.95, "fluency": 0.92}}
    ],
    "outputs": {
      "translated_text": "Das System verarbeitet Benutzeranfragen effizient...",
      "confidence_score": 0.94,
      "quality_assessment": {...}
    },
    "performance": {
      "processing_time": "4.1s",
      "character_count": 156,
      "terminology_lookups": 8
    }
  }
}
```

## Integration Capabilities

### Terminology Management
- **Custom Dictionaries**: Domain-specific term databases
- **Consistency Checking**: Ensure consistent term usage
- **Term Evolution**: Learn new terminology from usage
- **Glossary Generation**: Auto-generate translation glossaries

### Workflow Integration
- **Document Pipelines**: Integrate with document processing workflows
- **Real-time Translation**: Support for live translation needs
- **Review Workflows**: Integration with human review processes
- **Quality Assurance**: Automated quality checking and validation

### Memory Systems
- **Translation Memory**: Reuse previous translations for consistency
- **Domain Learning**: Improve domain-specific translations over time
- **User Preferences**: Remember user translation preferences
- **Quality Tracking**: Monitor and improve translation quality metrics

This tool provides comprehensive translation capabilities that go beyond simple text conversion to include cultural adaptation, domain expertise, and quality assurance for professional translation needs.